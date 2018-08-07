---
title: How To Implement Extended Camera Control Properties
author: windows-driver-content
description: Implementing extended camera control properties for a camera driver.
ms.assetid: BF5B2F1F-AC1D-4ED1-B1FC-64E8FA1218DA
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# How To Implement Extended Camera Control Properties


The camera driver should implement [extended camera control properties](extended-camera-control-properties.md) as individual property sets—that is, each property should be implemented as a single property set. The following example code can be used as a starting point for implementing these properties.

**Note**  Because an extended property’s data size can be of arbitrary length, query the user-mode stack for the size of the data by passing a null buffer. A two-step process is needed: first the driver returns the required length, as shown in the example code, then the user-mode stack requests a proper buffer for the property data.

 

## Driver implementation


```ManagedCPlusPlus
DEFINE_KSPROPERTY_TABLE(SocSimFilterFocusPropertyItems)
{       
    DEFINE_KSPROPERTY_ITEM(
        0,
        CCaptureFilter::FocusRectHandler,
        sizeof(KSPROPERTY),
        0,
        CCaptureFilter::FocusRectHandler,
        NULL, 0, NULL, NULL, 0
        )
};

DEFINE_KSPROPERTY_TABLE(SocSimFilterVideoStabPropertyItems)
{       
    DEFINE_KSPROPERTY_ITEM(
        0,
        CCaptureFilter::VideoStabilizationModeHandler,
        sizeof(KSPROPERTY),
        0,
        CCaptureFilter::VideoStabilizationModeHandler,
        NULL, 0, NULL, NULL, 0
        )
};

DEFINE_KSPROPERTY_TABLE(SocSimFilterFlashPropertyItems)
{       
    DEFINE_KSPROPERTY_ITEM(
        0,
        CCaptureFilter::FlashHandler,
        sizeof(KSPROPERTY),
        0,
        CCaptureFilter::FlashHandler,
        NULL, 0, NULL, NULL, 0
        )
};

DEFINE_KSPROPERTY_SET_TABLE(SocSimFilterPropertySets)
{
    DEFINE_KSPROPERTY_SET(
        &PROPSETID_VIDCAP_CAMERACONTROL_REGION_OF_INTEREST,
        SIZEOF_ARRAY(SocSimFilterFocusPropertyItems),
        SocSimFilterFocusPropertyItems,
        0,
        NULL),

    DEFINE_KSPROPERTY_SET(
        &PROPSETID_VIDCAP_CAMERACONTROL_FLASH,
        SIZEOF_ARRAY(SocSimFilterFlashPropertyItems),
        SocSimFilterFlashPropertyItems,
        0,
        NULL),

    DEFINE_KSPROPERTY_SET(
        &PROPSETID_VIDCAP_CAMERACONTROL_VIDEO_STABILIZATION,
        SIZEOF_ARRAY(SocSimFilterVideoStabPropertyItems),
        SocSimFilterVideoStabPropertyItems,
        0,
        NULL)

};

NTSTATUS
CCaptureFilter::FlashHandler(
    __in    PIRP Irp,
    __in    PKSPROPERTY Property,
    __inout PVOID pData
    )
{
    PAGED_CODE();
    NTSTATUS Status = STATUS_SUCCESS;
    NT_ASSERT(Irp);
    NT_ASSERT(Property);

    CCaptureFilter* pFilter = reinterpret_cast <CCaptureFilter*>(KsGetFilterFromIrp(Irp)->Context);

    PIO_STACK_LOCATION pIrpStack = IoGetCurrentIrpStackLocation(Irp);
    ULONG ulOutputBufferLength = pIrpStack->Parameters.DeviceIoControl.OutputBufferLength;
    ULONG InputBufferLength = pIrpStack->Parameters.DeviceIoControl.InputBufferLength;

    if (Property->Flags & KSPROPERTY_TYPE_SET)
    {
        if (ulOutputBufferLength == 0)
        {
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S);
            Status = STATUS_BUFFER_OVERFLOW;
        }
        else if (ulOutputBufferLength < sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S))
        {
            Status = STATUS_BUFFER_TOO_SMALL;
        }
        else if (pData && ulOutputBufferLength >= sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S))
        {
            PKSPROPERTY_CAMERACONTROL_FLASH_S pFlash = (PKSPROPERTY_CAMERACONTROL_FLASH_S)pData;
            pFilter->m_Flash = pFlash->Flash;
            pFilter->m_FlashCapabilites = pFlash->Capabilities;
            Status = STATUS_SUCCESS;
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S);
        }
        else 
        {
            Status = STATUS_INVALID_PARAMETER;
        }
    }
    else if (Property->Flags & KSPROPERTY_TYPE_GET)
    {
        if (ulOutputBufferLength == 0)
        {
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S);
            Status = STATUS_BUFFER_OVERFLOW;
        }
        else if (ulOutputBufferLength < sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S))
        {
            Status = STATUS_BUFFER_TOO_SMALL;
        }
        else if (pData && ulOutputBufferLength >= sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S))
        {
            PKSPROPERTY_CAMERACONTROL_FLASH_S pFlash = (PKSPROPERTY_CAMERACONTROL_FLASH_S)pData;
            pFlash->Flash = pFilter->m_Flash;
            pFlash->Capabilities = pFilter->m_FlashCapabilites;
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S);
            Status = STATUS_SUCCESS;
        }
        else
        {
            Status = STATUS_INVALID_PARAMETER;
        }
    }

    return Status;
}

NTSTATUS
CCaptureFilter::VideoStabilizationModeHandler(
    __in    PIRP Irp,
    __in    PKSPROPERTY Property,
    __inout PVOID pData
    )
{
    PAGED_CODE();
    NTSTATUS Status = STATUS_SUCCESS;
    NT_ASSERT(Irp);
    NT_ASSERT(Property);

    CCaptureFilter* pFilter = reinterpret_cast <CCaptureFilter*>(KsGetFilterFromIrp(Irp)->Context);

    PIO_STACK_LOCATION pIrpStack = IoGetCurrentIrpStackLocation(Irp);
    ULONG ulOutputBufferLength = pIrpStack->Parameters.DeviceIoControl.OutputBufferLength;
    ULONG InputBufferLength = pIrpStack->Parameters.DeviceIoControl.InputBufferLength;

    if (Property->Flags & KSPROPERTY_TYPE_SET)
    {
        if (ulOutputBufferLength == 0)
        {
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S);
            Status = STATUS_BUFFER_OVERFLOW;
        }
        else if (ulOutputBufferLength < sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S))
        {
            Status = STATUS_BUFFER_TOO_SMALL;
        }
        else if (pData && ulOutputBufferLength >= sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S))
        {
            PKSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S pVideoStab = (PKSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S)pData;
            pFilter->m_VideoStabMode = pVideoStab->VideoStabilizationMode;
            pFilter->m_VideoStabCapabilites = pVideoStab->Capabilities;
            Status = STATUS_SUCCESS;
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S);
        }
        else 
        {
            Status = STATUS_INVALID_PARAMETER;
        }
    }
    else if (Property->Flags & KSPROPERTY_TYPE_GET)
    {
        if (ulOutputBufferLength == 0)
        {
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S);
            Status = STATUS_BUFFER_OVERFLOW;
        }
        else if (ulOutputBufferLength < sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S))
        {
            Status = STATUS_BUFFER_TOO_SMALL;
        }
        else if (pData && ulOutputBufferLength >= sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S))
        {
            PKSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S pVideoStab = (PKSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S)pData;
            pVideoStab->VideoStabilizationMode = pFilter->m_VideoStabMode;
            pVideoStab->Capabilities = pFilter->m_VideoStabCapabilites;
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S);
            Status = STATUS_SUCCESS;
        }
        else
        {
            Status = STATUS_INVALID_PARAMETER;
        }
    }

    return Status;
}

NTSTATUS
CCaptureFilter::FocusRectHandler(
    __in    PIRP Irp,
    __in    PKSPROPERTY Property,
    __inout PVOID pData
    )
{
    PAGED_CODE();
    NTSTATUS Status = STATUS_SUCCESS;
    NT_ASSERT(Irp);
    NT_ASSERT(Property);

    CCaptureFilter* pFilter = reinterpret_cast <CCaptureFilter*>(KsGetFilterFromIrp(Irp)->Context);

    PIO_STACK_LOCATION pIrpStack = IoGetCurrentIrpStackLocation(Irp);
    ULONG ulOutputBufferLength = pIrpStack->Parameters.DeviceIoControl.OutputBufferLength;
    ULONG InputBufferLength = pIrpStack->Parameters.DeviceIoControl.InputBufferLength;

    if (Property->Flags & KSPROPERTY_TYPE_SET)
    {
        if (ulOutputBufferLength == 0)
        {
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S);
            Status = STATUS_BUFFER_OVERFLOW;
        }
        else if (ulOutputBufferLength < sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S))
        {
            Status = STATUS_BUFFER_TOO_SMALL;
        }
        else if (pData && ulOutputBufferLength >= sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S))
        {
            PKSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S pFocusRect = (PKSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S)pData;
            pFilter->m_FocusRect.left = pFocusRect->FocusRect.left;
            pFilter->m_FocusRect.top = pFocusRect->FocusRect.top;
            pFilter->m_FocusRect.right = pFocusRect->FocusRect.right;
            pFilter->m_FocusRect.bottom = pFocusRect->FocusRect.bottom;
            pFilter->m_AutoFocusLock = pFocusRect->AutoFocusLock;
            pFilter->m_AutoExposureLock = pFocusRect->AutoExposureLock;
            pFilter->m_AutoWhitebalanceLock = pFocusRect->AutoWhitebalanceLock;
            Status = STATUS_SUCCESS;
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S);
        }
        else 
        {
            Status = STATUS_INVALID_PARAMETER;
        }
    }
    else if (Property->Flags & KSPROPERTY_TYPE_GET)
    {
        if (ulOutputBufferLength == 0)
        {
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S);
            Status = STATUS_BUFFER_OVERFLOW;
        }
        else if (ulOutputBufferLength < sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S))
        {
            Status = STATUS_BUFFER_TOO_SMALL;
        }
        else if (pData && ulOutputBufferLength >= sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S))
        {
            PKSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S pFocusRect = (PKSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S)pData;
            pFocusRect->FocusRect.left = pFilter->m_FocusRect.left;
            pFocusRect->FocusRect.top = pFilter->m_FocusRect.top;
            pFocusRect->FocusRect.right = pFilter->m_FocusRect.right;
            pFocusRect->FocusRect.bottom = pFilter->m_FocusRect.bottom;
            pFocusRect->AutoFocusLock = pFilter->m_AutoFocusLock;
            pFocusRect->AutoExposureLock = pFilter->m_AutoExposureLock;
            pFocusRect->AutoWhitebalanceLock = pFilter->m_AutoWhitebalanceLock;
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S);
            Status = STATUS_SUCCESS;
        }
        else
        {
            Status = STATUS_INVALID_PARAMETER;
        }
    }

    return Status;
}
```

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bstream\stream%5D:%20How%20To%20Implement%20Extended%20Camera%20Control%20Properties%20%20RELEASE:%20%288/23/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


