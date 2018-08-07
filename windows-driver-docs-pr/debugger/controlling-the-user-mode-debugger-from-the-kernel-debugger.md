---
title: Controlling the User-Mode Debugger from the Kernel Debugger
description: Controlling the User-Mode Debugger from the Kernel Debugger
ms.assetid: 8fba2187-cf22-41ad-9b06-228a5b082822
keywords: ["KD, controlling CDB or NTSD", "WinDbg, controlling CDB or NTSD", "CDB, redirecting control to the kernel debugger", "NTSD, redirecting control to the kernel debugger", "redirecting user-mode output to the kernel debugger", "controlling the user-mode debugger from the kernel debugger", "controlling the user-mode debugger from the kernel debugger, overview", "controlling the user-mode debugger from the kernel debugger, sleep mode", "sleep mode"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Controlling the User-Mode Debugger from the Kernel Debugger


## <span id="ddk_controlling_the_user_mode_debugger_from_the_kernel_debugger_dbg"></span><span id="DDK_CONTROLLING_THE_USER_MODE_DEBUGGER_FROM_THE_KERNEL_DEBUGGER_DBG"></span>


You can redirect the input and output from a user-mode debugger to a kernel debugger. This redirection enables the kernel debugger to control a specific user-mode debugging session that is occurring on the target computer.

You can use either KD or WinDbg as the kernel debugger. Note that many of the familiar features of WinDbg are not available in this scenario. For example, you cannot use the Locals window, the Disassembly window, or the Call Stack window, and you cannot step through source code. This is because WinDbg is only acting as a viewer for the debugger (NTSD or CDB) running on the target computer.

You can use either CDB or NTSD as the user-mode debugger. NTSD is the better choice, because it requires minimal resources from the processor and operating system of the computer whose application is being debugged. In fact, when NTSD is started under the control of the kernel debugger, no NTSD window is created. With NTSD, you can perform user-mode debugging through the serial port early in the boot phase and late into shutdown.

**Note**  The [**.shell**](-shell--command-shell-.md) command is not supported when the output of a user-mode debugger is redirected to the kernel debugger.

 

This section includes the following:

-   [Starting the Debugging Session](starting-the-debugging-session.md) describes how to begin a session where the user-mode debugger is controlled from the kernel debugger.

-   [Switching Modes](switching-modes.md) describes the four different modes that are involved, and how to alternate between them.

-   [When to Use This Technique](when-to-use-this-technique.md) describes scenarios where this technique is particularly useful.

-   [Combining This Method with Remote Debugging](combining-this-method-with-remote-debugging.md) describes how to control the user-mode debugger from a kernel debugger, and use it as a debugging server at the same time. This combination can be useful if your user-mode symbols are located on a symbol server.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Controlling%20the%20User-Mode%20Debugger%20from%20the%20Kernel%20Debugger%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




