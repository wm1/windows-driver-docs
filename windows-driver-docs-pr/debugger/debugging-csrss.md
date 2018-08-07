---
title: Debugging CSRSS
description: Debugging CSRSS
ms.assetid: 9c3a8498-d9e4-4070-aee8-c038fa1666a4
keywords: ["CSRSS debugging", "NTSD, debugging CSRSS", "controlling the user-mode debugger from the kernel debugger, debugging CSRSS"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Debugging CSRSS


## <span id="ddk_debugging_csrss_with_ntsd_dbg"></span><span id="DDK_DEBUGGING_CSRSS_WITH_NTSD_DBG"></span>


The Client Server Run-Time Subsystem (CSRSS) is the user-mode process that controls the underlying layer for the Windows environment. There are a number of problems that make it necessary to debug CSRSS itself.

Debugging CSRSS is also useful when the Windows subsystem terminates unexpectedly with a [**Bug Check 0xC000021A**](bug-check-0xc000021a--status-system-process-terminated.md) (STATUS\_SYSTEM\_PROCESS\_TERMINATED). In this case, debugging CSRSS will catch the failure before it gets to an "unexpected" point.

### <span id="controlling_ntsd_from_the_kernel_debugger"></span><span id="CONTROLLING_NTSD_FROM_THE_KERNEL_DEBUGGER"></span>Controlling NTSD from the Kernel Debugger

The easiest way to debug CSRSS is to use NTSD and [control it from the kernel debugger](controlling-the-user-mode-debugger-from-the-kernel-debugger.md).

### <span id="enabling_csrss_debugging"></span><span id="ENABLING_CSRSS_DEBUGGING"></span>Enabling CSRSS Debugging

CSRSS debugging must be enabled before you can proceed. If the target computer is running a [*checked build*](https://msdn.microsoft.com/library/windows/hardware/ff556274#wdkgloss-checked-build) of Windows, CSRSS debugging is always enabled. If the target computer is running a [*free build*](https://msdn.microsoft.com/library/windows/hardware/ff556280#wdkgloss-free-build) of Windows, you will have to enable CSRSS debugging through the Global Flags Utility (GFlags).

To do this, start the GFlags utility, select the **System Registry** radio button, and select **Enable debugging of Win32 subsystem**.

Alternatively, you can use the following GFlags command-line:

```
gflags /r +20000 
```

Or, if you prefer, you can edit the registry key manually instead of using GFlags. Open the following registry key:

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager 
```

Edit the **GlobalFlag** value entry (of type REG\_DWORD) and set the bit 0x00020000.

After using GFlags or manually editing the registry, you must reboot for the changes to take effect.

### <span id="starting_ntsd"></span><span id="STARTING_NTSD"></span>Starting NTSD

Because you will be controlling the user-mode debugger from the kernel debugger, you will need to set up a kernel debugging connection. See [Getting Set Up for Debugging](getting-set-up-for-debugging.md) for details.

After the registry has been properly configured, it is a simple matter of starting NTSD as follows:

**ntsd --**

See [Controlling the User-Mode Debugger from the Kernel Debugger](controlling-the-user-mode-debugger-from-the-kernel-debugger.md) for an explanation of how to proceed.

You will have to set your symbol path to a location on your host computer or to some other location on your network. When CSRSS is being debugged, network authentication on the target computer will not work properly.

Note that you may see an "in page io error" message. This is another manifestation of a hardware failure.

In Windows XP and later versions of Windows, when the debugging session ends, the debugger will detach from CSRSS while the CSRSS process is still running. This avoids termination of the CSRSS process itself.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Debugging%20CSRSS%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




