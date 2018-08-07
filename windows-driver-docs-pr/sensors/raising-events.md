---
title: Raising sensor events
author: windows-driver-content
description: Raising sensor events
ms.assetid: a6e428f8-1613-4e8d-813d-5a54824dab82
keywords:
- sensor events
- event handler
- data update event
- sensor data update event
- state change event
- sensor state change event
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Raising sensor events


For more information about how sensor events work, see [About Sensor Driver Events](about-sensor-driver-events.md).

The following code example demonstrates a class that raises data-updated and state-changed events. The class is named **CSensorManager**.

### Member Variables

This class defines the following member variables.

```
// Smart pointer to the sensor class extension object.
CComPtr<ISensorClassExtension> m_spSensorCXT;

// Pointer to the callback class that the class extension calls.
CSensorDdi* m_pDdi;

// The event thread handle
HANDLE m_hEventThread;

// Handle to an event used to signal the thread to close.
HANDLE m_hCloseThread;

// The current report interval.
DWORD m_dwInterval;
```

### Global Variables

The driver would define the following global variables used by this class.

```
// Sensor ID
static const LPWSTR g_wszSensorID = L"My Sensor ID";

// Default event interval
static const DWORD g_dwDefaultInterval = 1000; // one second
```

### Lifetime Management

The callback class, named CSensorDdi, which implements [ISensorDriver](https://msdn.microsoft.com/library/windows/hardware/ff545566), creates an instance of the CSampleEvents event class when the first client subscribes to events. The callback class destroys the CSampleEvents instance when clients are no longer subscribed to events.

CSampleEvents calls back to CSensorDdi to retrieve the newest data by using the same methods that the class extension uses, such as [**ISensorDriver::OnGetDataFields**](https://msdn.microsoft.com/library/windows/hardware/ff545607).

The following code example contains the method implementations for the CSampleEvents event class.

```
CSampleEvents::CSampleEvents()
{
    // Initialize member variables.
    m_hEventThread = NULL;
    m_hCloseThread = NULL;
    m_dwInterval = g_dwDefaultInterval; 
};

CSampleEvents::~CSampleEvents()
{    
};

// Initialize
// Sets the pointers to the class extension and the callback class.
HRESULT CSampleEvents::Initialize(ISensorClassExtension *pSensorCXT, CSensorDdi* pDdi)
{
    HRESULT hr = S_OK;

    if(NULL == pSensorCXT || NULL == pDdi)
    {
        return E_POINTER;
    }

    // Cache the pointers to the class extension and DDI callback class.
    m_spSensorCXT = pSensorCXT;
    m_pDdi = pDdi;

    // Create the event used to close the thread.
    m_hCloseThread = ::CreateEvent(NULL, FALSE, FALSE, TEXT("CloseThreadEvent"));

    if(NULL == m_hCloseThread)
    {
        hr = E_UNEXPECTED;
    }

    if(SUCCEEDED(hr))
    {
        m_hEventThread = ::CreateThread(NULL,   // Cannot be inherited by child process
                     0,                                       // Default stack size
                     &CSampleEvents::_EventThreadProc,     // Thread proc
                     (LPVOID)this,                            // Thread proc argument
                     0,                                       // Starting state = running
                     NULL);                                   // No thread identifier
 
        if(NULL == m_hEventThread)
        {
            hr = E_UNEXPECTED;
        }
    }

    return hr;
};

// Uninitializes the event class.
HRESULT CSampleEvents::Uninitialize()
{
    HRESULT hr = S_OK;

    // Stop the event thread.
    ::SetEvent(m_hCloseThread);

    // Wait for the thread to end.
    ::WaitForSingleObject(m_hEventThread, INFINITE);

    if (NULL != m_hEventThread)
    {
        CloseHandle(m_hEventThread);
        m_hEventThread = NULL;
    }

    if(NULL != m_hCloseThread)
    {
        CloseHandle(m_hCloseThread);
        m_hCloseThread = NULL;
    }

    // After Uninitialize, clients must call Initialize to set new pointers.
    m_pDdi = NULL;
    m_spSensorCXT.Release();

    return hr;
};

// Post a state change event
HRESULT CSampleEvents::PostStateEvent()
{
    HRESULT hr = (NULL == m_spSensorCXT) ? E_UNEXPECTED : S_OK ;

    if (SUCCEEDED(hr))
    {
        SensorState st;  
        hr = m_pDdi->GetSensorState(&st);

        if (SUCCEEDED(hr))
        {
            // Post the state change event.
            hr = m_spSensorCXT->PostStateChange(g_wszSensorID, st);
        }
    }

    return hr;
}

// Post a data updated event
HRESULT CSampleEvents::PostDataEvent(IPortableDeviceValues* pValues)
{
    HRESULT hr = (NULL == m_spSensorCXT) ? E_UNEXPECTED : S_OK ;

    if (SUCCEEDED(hr))
    {
        CComPtr<IPortableDeviceValuesCollection> spValuesCollection;
        hr = spValuesCollection.CoCreateInstance(CLSID_PortableDeviceValuesCollection);

        if (SUCCEEDED(hr))
        {
            hr = spValuesCollection->Add(pValues);

            if (SUCCEEDED(hr))
            {
                hr = m_spSensorCXT->PostEvent(g_wszSensorID, spValuesCollection);
            }
        }
    }

    return hr;
}
```

### Thread Procedure

The following example code shows a thread procedure that uses the CSampleEvents class to raise data-updated events.

```
DWORD WINAPI CSampleEvents::_EventThreadProc(__in LPVOID pvData)
{
// Cast the argument to the correct type.
 CSampleEvents* pThis = static_cast<CSampleEvents*>(pvData);

// New threads must always CoInitialize...
    HRESULT hr = CoInitializeEx(NULL, COINIT_MULTITHREADED);

    if (SUCCEEDED(hr))
    {
        // Wait loop timed to use current report interval.
        while (WAIT_TIMEOUT == WaitForSingleObject(pThis->m_hCloseThread, pThis->m_dwInterval))
        {
            if(NULL == pThis->m_pDdi ||
               NULL == pThis->m_spSensorCXT.p)
            {
                Trace(TRACE_LEVEL_ERROR, "%!FUNC!: NULL pointer in helper function.");
                hr = E_POINTER;
            }
 
            CComPtr<IPortableDeviceValues> spEventParams;
            CComPtr<IPortableDeviceKeyCollection> spKeys;
 
            if(SUCCEEDED(hr))
            {            
                // Use the Ddi class to create the key collection.
                hr = pThis->m_pDdi->OnGetSupportedDataFields(g_wszSensorID, &spKeys);
            }

            if(SUCCEEDED(hr))
            {
                CComPtr<IWDFFile> spTemp;

                // Get the data fields.
                // Note that we&#39;re using a DDI call as a helper function, here.
                // Setting the first parameter to NULL will be problematic if you
                // choose to track or use IWDFFile pointers in OnGetDataFields.
                // This sample does not do so, therefore this is a safe thing to do
                // in this code.
                hr = pThis->m_pDdi->OnGetDataFields(spTemp, g_wszSensorID, spKeys, 
                                                              &spEventParams);
            }

            if(SUCCEEDED(hr))
            {
                // Add the data event property key.
                hr = spEventParams->SetGuidValue(SENSOR_EVENT_PARAMETER_EVENT_ID,
                                                                SENSOR_EVENT_DATA_UPDATED);
 
                if(SUCCEEDED(hr))
                {
                    // Post the event.
                    hr = pThis->PostDataEvent(spEventParams);                
                }
            }
        }
    }

 CoUninitialize();

    return SUCCEEDED(hr) ? 0 : 1;
};
```

## Related topics
[The Sensors Geolocation Driver Sample](https://msdn.microsoft.com/library/windows/hardware/hh768273)  

--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bsensors\sensors%5D:%20Raising%20sensor%20events%20%20RELEASE:%20%281/12/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


