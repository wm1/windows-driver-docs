---
title: Introduction to Threaded DPCs
author: windows-driver-content
description: Introduction to Threaded DPCs
ms.assetid: 891a8a52-83ff-400a-9477-8edca1b9a83c
keywords: ["threaded DPCs WDK kernel", "real-time threads WDK kernel", "preempted DPCs WDK kernel"]
ms.author: windowsdriverdev
ms.date: 06/16/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Introduction to Threaded DPCs


## <a href="" id="ddk-introduction-to-threaded-dpcs-kg"></a>


Threaded DPCs are available in Windows Vista and later versions of Windows.

A *threaded DPC* is a DPC that the system executes at IRQL = PASSIVE\_LEVEL. Threaded DPCs are enabled by default, but you can disable them by setting the **HKLM\\System\\CCS\\Control\\SessionManager\\Kernel\\ThreadDpcEnable** registry key to zero. When threaded DPCs are disabled, they execute as ordinary DPCs.

An ordinary DPC preempts the execution of all threads, and cannot be preempted by a thread or by another DPC. If the system has a large number of ordinary DPCs queued, or if one of those DPCs runs for a long time, every thread will remain paused for an arbitrarily long time. Thus, each ordinary DPC increases system latency, which can hurt the performance of time-sensitive applications, such as audio or video playback.

Conversely, a threaded DPC can be preempted by an ordinary DPC, but not by other threads. Therefore, you should use threaded DPCs rather than ordinary DPCs—unless a particular DPC must not be preempted, not even by another DPC.

The system represents threaded DPCs (and ordinary DPCs) as [**KDPC**](https://msdn.microsoft.com/library/windows/hardware/ff551882) structures. To initialize a **KDPC** structure for a threaded DPC, call the [**KeInitializeThreadedDpc**](https://msdn.microsoft.com/library/windows/hardware/ff552166) routine, and pass it a [*CustomThreadedDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542976) routine that performs the action of the DPC.

Because a *CustomThreadedDpc* routine can execute at either PASSIVE\_LEVEL or DISPATCH\_LEVEL, you must ensure that your *CustomThreadedDpc* routine correctly synchronizes at both IRQLs. For more information about how to do so, see [Synchronization and Threaded DPCs](synchronization-and-threaded-dpcs.md).

In addition, you must ensure that your *CustomThreadedDpc* routine obeys all the restrictions for DISPATCH\_LEVEL code. If threaded DPCs are enabled, they run at IRQL = PASSIVE\_LEVEL but are still subject to the same restrictions as ordinary DPCs. All of the code that executes in a threaded DPC—including all functions that are called by the *CustomThreadedDpc* routine—must conform to the restrictions of the DPC environment. For example, code must not block on passive-level synchronization objects, such as [KEVENT objects](defining-and-using-an-event-object.md). Most existing device stacks, such as networking, storage, and USB, do not support threaded DPC processing, and they might try to block if they detect that they are called at PASSIVE\_LEVEL. For similar reasons, the [Kernel-Mode Driver Framework](https://msdn.microsoft.com/library/windows/hardware/ff544296) (KMDF) does not support threaded DPC processing, and KMDF drivers should not try to use threaded DPCs. For more information about the DPC environment, see [Writing DPC Routines](writing-dpc-routines.md).

To add a threaded DPC to the DPC queue, call [**KeInsertQueueDpc**](https://msdn.microsoft.com/library/windows/hardware/ff552185). To remove a threaded DPC from the queue before it executes, call [**KeRemoveQueueDpc**](https://msdn.microsoft.com/library/windows/hardware/ff553169).

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bkernel\kernel%5D:%20Introduction%20to%20Threaded%20DPCs%20%20RELEASE:%20%286/14/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


