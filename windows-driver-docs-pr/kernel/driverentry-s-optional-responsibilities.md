---
title: DriverEntry's Optional Responsibilities
author: windows-driver-content
description: DriverEntry's Optional Responsibilities
ms.assetid: 859282f7-6b40-47a8-b845-cdb7c26585dd
keywords: ["DriverEntry WDK kernel , optional responsibilities", "claiming hardware resources", "executive worker threads WDK kernel", "worker threads WDK kernel", "system-space memory allocations WDK kernel", "system resource storage WDK kernel", "storing system resources", "hardware resource claiming WDK kernel", "resource claiming WDK kernel"]
ms.author: windowsdriverdev
ms.date: 06/16/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# DriverEntry's Optional Responsibilities


## <a href="" id="ddk-driverentry-s-optional-responsibilities-kg"></a>


Depending on the position of a particular driver in a chain of layered drivers, the nature of the underlying device, and the design of the driver, a [**DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff544113) routine also can be responsible for the following:

-   Calling [**IoAllocateDriverObjectExtension**](https://msdn.microsoft.com/library/windows/hardware/ff548233) to create and initialize a driver object extension, if the driver requires storage for data on a driver-wide basis. The driver object extension is a driver-specific data structure. For example, a driver might use its driver object extension to store a registry path or other global information.

-   Calling [**PsCreateSystemThread**](https://msdn.microsoft.com/library/windows/hardware/ff559932) to create executive worker threads, if the driver is a highest-level driver (such as a file system driver) that uses such threads. In this case, the driver must also have a callback routine of type WORKER\_THREAD\_ROUTINE, which takes a single input PVOID *Parameter*.

-   Registering a [*Reinitialize*](https://msdn.microsoft.com/library/windows/hardware/ff561022) routine. (See [Writing a Reinitialize Routine](writing-a-reinitialize-routine.md).)

-   Handling class-specific initialization requirements that differ from those discussed here, such as those that a device-specific miniport or miniclass driver working in tandem with a port or class driver might have. See the device-type specific documentation in the Windows Driver Kit (WDK) for details.

### Providing Storage for System Resources

Per-device objects should be allocated in the [*AddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff540521) routine or in the Dispatch routine that handles the PnP [**IRP\_MN\_START\_DEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff551749) request, not in **DriverEntry**.

However, a driver might need to allocate additional system-space memory for other driver-wide uses. If so, the **DriverEntry** routine can call one (or more) of the following routines:

-   **IoAllocateDriverObjectExtension**, to create a context area associated with the driver object

-   [**ExAllocatePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544520) for paged or nonpaged system-space memory

-   [**MmAllocateNonCachedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554479) or [**MmAllocateContiguousMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554460) for cache-aligned nonpaged system-space memory (used for I/O buffers)

Every **DriverEntry** routine is run in the context of a system thread at IRQL = PASSIVE\_LEVEL. Therefore, any memory allocated with **ExAllocatePoolWithTag** for use exclusively during initialization can be from paged pool, as long as the driver does not control the device that holds the system page file. The allocated memory must be released with [**ExFreePool**](https://msdn.microsoft.com/library/windows/hardware/ff544590) before **DriverEntry** returns control. However, a driver that sets a *Reinitialize* routine can pass a pointer to this memory when it calls [**IoRegisterDriverReinitialization**](https://msdn.microsoft.com/library/windows/hardware/ff549511), thus making the driver's *Reinitialize* routine responsible for freeing the memory allocation.

### <a href="" id="claiming-hardware-resources-"></a>Claiming Hardware Resources

Older, non-PnP drivers claimed resources from the registry. PnP drivers, on the other hand, neither claim device resources from nor directly write resource requirements to the registry. Instead, these drivers report requirements in response to certain PnP IRPs, as part of the PnP manager's enumeration process. A PnP driver receives its allocated resources in a PnP **IRP\_MN\_START\_DEVICE** request.

Drivers that do not interact directly with the PnP manager, such as certain miniport drivers, might have different reporting requirements imposed by a class or port driver that does interact with the PnP manager. Such requirements are specific to the device class. For device-specific and class-specific details, see the documentation for the relevant device class in the Windows Driver Kit (WDK).

### Using the Registry

A **DriverEntry** routine might use the registry to get some of the information it needs to initialize the driver, or it might set information in the registry for other drivers or protected subsystems to use. The nature of the information depends on the type of device. Drivers can access the registry using **Zw*Xxx*** and **Rtl*Xxx*** routines. The **DriverEntry** routine's *RegistryPath* parameter points to a counted Unicode string that specifies a path to the driver's registry key, **\\Registry\\Machine\\System\\CurrentControlSet\\Services\\*DriverName***. The routine should save a copy of the string, not the pointer itself, since the pointer is no longer valid after **DriverEntry** returns.

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bkernel\kernel%5D:%20DriverEntry's%20Optional%20Responsibilities%20%20RELEASE:%20%286/14/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


