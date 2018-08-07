---
title: Using the CONNECT_MESSAGE_BASED Version of IoConnectInterruptEx
author: windows-driver-content
description: Using the CONNECT_MESSAGE_BASED Version of IoConnectInterruptEx
ms.assetid: 8e06c6aa-85de-4ed2-ac0d-0179201d1272
keywords: ["IoConnectInterruptEx", "CONNECT_MESSAGE_BASED", "message-signaled interrupts WDK kernel", "automatic interrupt detections WDK kernel"]
ms.author: windowsdriverdev
ms.date: 06/16/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Using the CONNECT\_MESSAGE\_BASED Version of IoConnectInterruptEx


For Windows Vista and later operating systems, a driver can use the CONNECT\_MESSAGE\_BASED version of [**IoConnectInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff548378) to register an ISR for the driver's message-signaled interrupts. The driver specifies a value of CONNECT\_MESSAGE\_BASED for *Parameters*-&gt;**Version**, and uses the members of *Parameters*-&gt;**MessageBased** to specify the other parameters of the operation.

-   *Parameters***-&gt;MessageBased.PhysicalDeviceObject** specifies the PDO for the device that the ISR services. The system uses the device object to automatically identify the device's message-signaled interrupts.

-   *Parameters***-&gt;MessageBased.MessageServiceRoutine** points to the [*InterruptMessageService*](https://msdn.microsoft.com/library/windows/hardware/ff547940) routine, while *Parameters***-&gt;MessageBased.ServiceContext** specifies the value that the system passes as the *ServiceContext* parameter to *InterruptMessageService*. The driver can use this to pass context information. For more information about passing context information, see [Providing ISR Context Information](providing-isr-context-information.md).

-   The driver can also specify a fallback *InterruptMessageService* routine in *Parameters***-&gt;MessageBased.FallBackServiceRoutine**. If the device has line-based interrupts, but no message-signaled interrupts, the system will instead register the *InterruptMessageService* routine to service the line-based interrupts. In this case, the system passes *Parameters***-&gt;MessageBased.ServiceContext** as the *ServiceContext* parameter to [*InterruptService*](https://msdn.microsoft.com/library/windows/hardware/ff547958). **IoConnectInterruptEx** updates *Parameters***-&gt;Version** to CONNECT\_LINE\_BASED if it registered the fallback routine.

-   *Parameters***-&gt;MessageBased.ConnectionContext** points to a variable that receives a pointer to either a [**IO\_INTERRUPT\_MESSAGE\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff550576) (for *InterruptMessageService*) structure or a [**KINTERRUPT**](https://msdn.microsoft.com/library/windows/hardware/ff554237) structure (for *InterruptService*). The driver can use the received pointer to remove the ISR. For more information, see [Removing an ISR](removing-an-isr.md).

-   Drivers can optionally specify a spin lock in *Parameters***-&gt;MessageBased.SpinLock** for the system to use when synchronizing with the ISR. Most drivers can just specify **NULL** to enable the system to allocate a spin lock on behalf of the driver. For more information about synchronizing with an ISR, see [Synchronizing Access to Device Data](synchronizing-access-to-device-data.md).

The following code example demonstrates how to register an *InterruptMessageService* routine by using CONNECT\_MESSAGE\_BASED.

```
IO_CONNECT_INTERRUPT_PARAMETERS params;

// deviceExtension is a pointer to the driver&#39;s device extension. 
//     deviceExtension->IntInfo is a PVOID.
//     deviceExtension->IntType is a ULONG.
// deviceInterruptService is a pointer to the driver&#39;s InterruptService routine.
// deviceInterruptMessageService is a pointer to the driver&#39;s InterruptMessageService routine.
// PhysicalDeviceObject is a pointer to the device&#39;s PDO. 
// ServiceContext is a pointer to driver-specified context for the ISR.

RtlZeroMemory( &params, sizeof(IO_CONNECT_INTERRUPT_PARAMETERS) );
params.Version = CONNECT_MESSAGE_BASED;
params.MessageBased.PhysicalDeviceObject = PhysicalDeviceObject;
params.MessageBased.MessageServiceRoutine = deviceInterruptMessageService;
params.MessageBased.ServiceContext = ServiceContext;
params.MessageBased.SpinLock = NULL;
params.MessageBased.SynchronizeIrql = 0;
params.MessageBased.FloatingSave = FALSE;
params.MessageBased.FallBackServiceRoutine = deviceInterruptService;

status = IoConnectInterruptEx(&params);

if (NT_SUCCESS(status)) {
    // We record the type of ISR registered.
    devExt->IsrType = params.Version;
} else {
    // Operation failed. Handle error.
    ...
}
```

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bkernel\kernel%5D:%20Using%20the%20CONNECT_MESSAGE_BASED%20Version%20of%20IoConnectInterruptEx%20%20RELEASE:%20%286/14/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


