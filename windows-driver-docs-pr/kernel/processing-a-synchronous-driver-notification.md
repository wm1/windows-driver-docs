---
title: Processing a Synchronous Driver Notification
author: windows-driver-content
description: Processing a Synchronous Driver Notification
ms.assetid: 84e4e05f-1383-4f5f-8fc0-20cd508afa3c
keywords: ["driver notification WDK dynamic hardware partitioning , processing", "synchronous driver notification WDK dynamic hardware partitioning , processing", "registering for driver notification WDK dynamic hardware partitioning , synchronous"]
ms.author: windowsdriverdev
ms.date: 06/16/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Processing a Synchronous Driver Notification


When the operating system calls a registered callback function, it passes a pointer to a [**KE\_PROCESSOR\_CHANGE\_NOTIFY\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff554229) structure in the *ChangeContext* parameter and a pointer to a variable that contains an NTSTATUS code in the *OperationStatus* parameter. The **KE\_PROCESSOR\_CHANGE\_NOTIFY\_CONTEXT** structure contains the state of the processor add operation, the processor number of the new processor that is being added, and an NTSTATUS code that is associated with the indicated state.

When a new processor is added to the hardware partition, the operating system calls the registered callback function two times. The operating system first calls the callback function with the **KeProcessorAddStartNotify** state before it starts the new processor. If the operating system successfully adds the new processor, it calls the callback function a second time with the **KeProcessorAddCompleteNotify** state. Otherwise, it calls the callback function a second time with the **KeProcessorAddFailureNotify** state.

If the KE\_PROCESSOR\_CHANGE\_ADD\_EXISTING flag was specified when the device driver registered the callback function, the callback function is also called immediately for each active processor that currently exists in the hardware partition. Typically, the callback function will not have to distinguish between when it is called for an existing processor and when it is called for a new processor. For more information about when the operating system calls a registered callback function, see the description of the [**KeRegisterProcessorChangeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff553120) function.

The following code example shows an implementation of a callback function that processes synchronous driver notifications:

```
// Synchronous notification callback function
VOID
  SyncProcessorCallback(
    IN PVOID CallbackContext,
    IN PKE_PROCESSOR_CHANGE_NOTIFICATION_CONTEXT ChangeContext,
    IN PNTSTATUS OperationStatus
    )
{
  PNTSTATUS CallbackStatus;
  ULONG ProcessorNumber;
  ULONG ProcessorCount;
  KAFFINITY ActiveProcessors;

  // The CallbackContext contains a pointer to a
  // variable that contains an NTSTATUS code. This
  // is used to pass back any error status to the
  // caller of KeRegisterProcessorChangeCallback.
  CallbackStatus =
    (PNTSTATUS)
      CallbackContext;

  // Get the processor number of the new processor
  ProcessorNumber =
    ChangeContext->NtNumber;

  // Switch on the state of the add operation
  switch (ChangeContext->State)
  {
    // Before the operating system has added the new processor
    case KeProcessorAddStartNotify:

      // Allocate any per-processor data
      // structures for the new processor.
      ...

      // Assign any other per-processor resources
      // to the new processor.
      ...

      // Perform any other necessary preparation
      // for execution of the driver code
      // on the new processor.
      ...

      // If an error occurs such that continuing
      // to add the processor would be fatal
      // (for example, an allocation failure of a
      // per-processor data structure), set the
      // status to an appropriate NTSTATUS code.
      if (...)
      {
        // This returns the status to the operating system.
        *OperationStatus = STATUS_INSUFFICIENT_RESOURCES;

        // This returns the status to the caller of the
        // KeRegisterProcessorChangeCallback function.
        *CallbackStatus = STATUS_INSUFFICIENT_RESOURCES;
      }

      break;

    // The operating system has successfully added the new processor
    case KeProcessorAddCompleteNotify:

      //
      // The following can be performed either here or
      // in an asynchronous notification callback function.
      //

      // Get the current processor count and affinity
      ProcessorCount =
        KeQueryActiveProcessorCount(
          &ActiveProcessors
          );

      // Adjust any resource allocations that are based
      // on the number of processors.
      ...

      // Adjust the assignment of resources that are
      // assigned to specific processors.
      ...

      // Begin scheduling any per-processor threads
      // on the new processor.
      ...

      // Adjust the scheduling of DPCs and other threads
      ...

      // Adjust any load balancing algorithms
      ...

      break;

    // The operating system has failed to add the new processor
    case KeProcessorAddFailureNotify:

      // Clean up and free any per-processor
      // resources that were allocated for the
      // specified processor during the
      // KeProcessorAddStartNotify state.
      ...

      break;
  }
}
```

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bkernel\kernel%5D:%20Processing%20a%20Synchronous%20Driver%20Notification%20%20RELEASE:%20%286/14/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


