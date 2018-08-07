---
title: Debugging Environments
description: Starting with Windows Driver Kit (WDK) 8.0, the driver development environment and the Windows debugger are integrated into Microsoft Visual Studio.
ms.assetid: 13F9D82A-4C04-425A-A063-B349DB5C8E08
keywords: ["WinDbg", "KD", "CDB", "NTSD"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Debugging Environments


Starting with Windows Driver Kit (WDK) 8.0, the driver development environment and the Windows debugger are integrated into Microsoft Visual Studio.

After you install Visual Studio and the WDK, you have six available debugging environments:

-   Visual Studio with integrated Windows debugger
-   Microsoft Windows Debugger (WinDbg)
-   Microsoft Kernel Debugger (KD)
-   NTKD
-   Microsoft Console Debugger (CDB)
-   Microsoft NT Symbolic Debugger (NTSD)

The following sections describe the debugging environments.

### <span id="Visual_Studio_with_integrated_Windows_debugger"></span><span id="visual_studio_with_integrated_windows_debugger"></span><span id="VISUAL_STUDIO_WITH_INTEGRATED_WINDOWS_DEBUGGER"></span>Visual Studio with integrated Windows debugger

Starting with WDK 8.0, the driver development environment and the Windows debugger are integrated into Visual Studio. In this integrated environment, most of the tools you need for coding, building, packaging, testing, debugging, and deploying a driver are available in the Visual Studio user interface.

Typically kernel-mode debugging requires two computers. The debugger runs on the *host computer* and the code being debugged runs on the *target computer*. With the the Windows debugger integrated into Visual Studio, you can perform a wide variety of debugging tasks, including those shown in the following list, from the host computer.

-   Configure a set of target computers for debugging.
-   Configure the debugging connections to a set of target computers.
-   Launch a kernel-mode debugging session between the host computer and a target computer.
-   Debug a user-mode process on the host computer.
-   Debug a user-mode process on a target computer.
-   Connect to remote debugging sessions.
-   View assembly code and source code.
-   View and manipulate local variables, parameters, and other symbols.
-   View and manipulate memory.
-   Navigate call stacks.
-   Set breakpoints.
-   Execute debugger commands.

You can also build drivers, deploy drivers, and run driver tests from within the Visual Studio user interface. If you make use of the Visual Studio integration provided by both the WDK and Debugging Tools for Windows, you can perform almost all of the driver development, packaging, deployment, testing, and debugging tasks from within Visual Studio on the host computer. Here are some of the WDK capabilities that have been integrated into Visual Studio.

-   Configure a set of target computers for driver testing.
-   Create and sign a driver package.
-   Deploy a driver package to a target computer.
-   Install and load a driver on a target computer.
-   Test a driver on a target computer.

### <span id="WinDbg"></span><span id="windbg"></span><span id="WINDBG"></span>WinDbg

Microsoft Windows Debugger (WinDbg) is a powerful Windows-based debugger that is capable of both user-mode and kernel-mode debugging. WinDbg provides debugging for the Windows kernel, kernel-mode drivers, and system services, as well as user-mode applications and drivers.

WinDbg uses the Visual Studio debug symbol formats for source-level debugging. It can access any symbol or variable from a module that has PDB symbol files, and can access any public function's name that is exposed by modules that were compiled with COFF symbol files (such as Windows .dbg files).

WinDbg can view source code, set breakpoints, view variables (including C++ objects), stack traces, and memory. Its Debugger Command window allows the user to issue a wide variety of commands.

For kernel-mode debugging, WinDbg typically requires two computers (the host computer and the target computer). WinDbg also supports various remote debugging options for both user-mode and kernel-mode targets.

WinDbg is a graphical-interface counterpart to CDB/NTSD and to KD/NTKD.

### <span id="KD"></span><span id="kd"></span>KD

Microsoft Kernel Debugger (KD) is a character-based console program that enables in-depth analysis of kernel-mode activity on all NT-based operating systems. You can use KD can to debug kernel-mode components and drivers, or to monitor the behavior of the operating system itself. KD also supports multiprocessor debugging.

Typically, KD does not run on the computer being debugged. You need two computers (the *host computer* and the *target computer*) for kernel-mode debugging.

### <span id="NTKD"></span><span id="ntkd"></span>NTKD

There is a variation of the KD debugger named NTKD. It is identical to KD in every way, except that it spawns a new text window when it is started, whereas KD inherits the Command Prompt window from which it was invoked.

### <span id="CDB"></span><span id="cdb"></span>CDB

Microsoft Console Debugger (CDB) is a character-based console program that enables low-level analysis of Windows user-mode memory and constructs. CDB is extremely powerful for debugging a program that is currently running or has recently crashed (live analysis), yet simple to set up. It can be used to investigate the behavior of a working application. In the case of a failing application, CDB can be used to obtain a stack trace or to look at the guilty parameters. It works well across a network (using a remote access server), as it is character-based.

With CDB, you can display and execute program code, set breakpoints, and examine and change values in memory. CDB can analyze binary code by disassembling it and displaying assembly instructions. It can also analyze source code directly.

Because CDB can access memory locations through addresses or global symbols, you can refer to data and instructions by name rather than by address, making it easy to locate and debug specific sections of code. CDB supports debugging multiple threads and processes. It is extensible, and can read and write both paged and non-paged memory.

If the target application is itself a console application, the target will share the console window with CDB. To spawn a separate console window for a target console application, use the *-2* command-line option.

### <span id="NTSD"></span><span id="ntsd"></span>NTSD

There is a variation of the CDB debugger named Microsoft NT Symbolic Debugger (NTSD). It is identical to CDB in every way, except that it spawns a new text window when it is started, whereas CDB inherits the Command Prompt window from which it was invoked.

Like CDB, NTSD is fully capable of debugging both console applications and graphical Windows programs. (The name *Console Debugger* is used to indicate the fact that CDB is classified as a console application; it does not imply that the target application must be a console application.)

Since the **start** command can also be used to spawn a new console window, the following two constructions will give the same results:

```
start cdb parameters 
ntsd parameters
```

It is possible to redirect the input and output from NTSD (or CDB) so that it can be controlled from a kernel debugger (either Visual Studio, WinDbg, or KD). If this technique is used with NTSD, no console window will appear at all. Controlling NTSD from the kernel debugger is therefore especially useful, since it results in an extremely light-weight debugger that places almost no burden on the computer containing the target application. This combination can be used to debug system processes, shutdown, and the later stages of boot up. See [Controlling the User-Mode Debugger from the Kernel Debugger](controlling-the-user-mode-debugger-from-the-kernel-debugger.md) for details.

## <span id="related_topics"></span>Related topics


[Windows Debugging](index.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Debugging%20Environments%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





