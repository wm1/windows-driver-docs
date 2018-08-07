---
title: I (Windows Debugger Glossary)
description: Glossary page - H
Robots: noindex, nofollow
ms.assetid: 4415522d-6ea3-42f6-9acc-0e3ceaa36dc7
---

# I


<span id="i_o_request_packet__irp_"></span><span id="I_O_REQUEST_PACKET__IRP_"></span>**I/O Request Packet (IRP)**  
A data structure used to represent an I/O request and control its processing. An IRP structure consists of a header and one or more stack locations.

<span id="image"></span><span id="IMAGE"></span>**image**  
An executable, DLL, or driver that Windows has loaded as part of a user-mode process or the Windows kernel.

See also image file.

<span id="image_file"></span><span id="IMAGE_FILE"></span>**image file**  
The file from which an image was loaded.

<span id="implicit_process"></span><span id="IMPLICIT_PROCESS"></span>**implicit process**  
In kernel-mode debugging, the process used to determine which virtual address space to use when performing virtual to physical address translation. When an event occurs, the implicit process is set to the event process.

See also implicit thread.

For more information, see [Threads and Processes](threads-and-processes.md).

<span id="implicit_thread"></span><span id="IMPLICIT_THREAD"></span>**implicit thread**  
In kernel-mode debugging, the thread used to determine some of the target's registers, including frame offset and instruction offset. When an event occurs, the implicit thread is set to the event thread.

<span id="inaccessible"></span><span id="INACCESSIBLE"></span>**inaccessible**  
A debugging session is *inaccessible* when all the targets are executing.

<span id="initial_breakpoint"></span><span id="INITIAL_BREAKPOINT"></span>**initial breakpoint**  
A breakpoint that automatically occurs near the beginning of a debugging session, after a reboot, or after a target application is restarted.

For more information, see [Using Breakpoints](using-breakpoints.md).

<span id="input_callback_objects"></span><span id="INPUT_CALLBACK_OBJECTS"></span>**input callback objects**  
Instances of the [IDebugInputCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550785) interface which have been registered with a client. Whenever the debugger engine requires input it asks the input callbacks to provide it.

See also output callbacks.

For more information, see [Using AMLI Debugger Commands](using-amli-debugger-commands.md).

<span id="input_callbacks"></span><span id="INPUT_CALLBACKS"></span>**input callbacks**  
See input callback objects.

<span id="interrupt"></span><span id="INTERRUPT"></span>**interrupt**  
A condition that disrupts normal command execution and transfers control to an interrupt handler. I/O devices requiring service from the processor usually initiate interrupts.

<span id="interrupt_request_level__irql_"></span><span id="INTERRUPT_REQUEST_LEVEL__IRQL_"></span>**Interrupt Request Level (IRQL)**  
The priority ranking of an interrupt. Each processor has an IRQL setting that threads can raise or lower. Interrupts that occur at or below the processor's IRQL setting are masked and will not interfere with the current operation. Interrupts that occur above the processor's IRQL setting take precedence over the current operation.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20I%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




