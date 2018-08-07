---
title: WdbgExts Threads and Processes
description: WdbgExts Threads and Processes
ms.assetid: fa513435-ea91-4dc5-9488-85087d585f96
keywords: ["WdbgExts extensions, threads", "WdbgExts extensions, processes"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# WdbgExts Threads and Processes


This topic provides a brief overview of how threads and processes can be manipulated using the WdbgExts API. For an overview of threads and processes in the [debugger engine](introduction.md#debugger-engine), see [Threads and Processes](threads-and-processes.md) in the [Debugger Engine Overview](debugger-engine-overview.md) section of this documentation.

### <span id="threads"></span><span id="THREADS"></span>Threads

To get the address of the thread environment block (TEB) that describes the current thread, use the method [**GetTebAddress**](https://msdn.microsoft.com/library/windows/hardware/ff549267). In kernel-mode debugging, the KTHREAD structure is also available to describe a thread. This structure is returned by [**GetCurrentThreadAddr**](https://msdn.microsoft.com/library/windows/hardware/ff545889) (in user-mode debugging, **GetCurrentThreadAddr** returns the address of the TEB).

The [thread context](scopes-and-symbol-groups.md#thread-context) is the state preserved by Windows when switching threads; it is represented by the CONTEXT structure. This structure varies with the operating system and platform and care should be taken when using the CONTEXT structure. The thread context is returned by the [**GetContext**](https://msdn.microsoft.com/library/windows/hardware/ff545736) function and can be set using the [**SetContext**](https://msdn.microsoft.com/library/windows/hardware/ff556644) function.

To examine the stack trace for the current thread, use the [**StackTrace**](https://msdn.microsoft.com/library/windows/hardware/ff558794) function. To temporarily change the thread used for examining the stack trace, use the [**SetThreadForOperation**](https://msdn.microsoft.com/library/windows/hardware/ff556830) or [**SetThreadForOperation64**](https://msdn.microsoft.com/library/windows/hardware/ff556832) functions. See [Examining the Stack Trace](examining-the-stack-trace.md) in the [Using the Debugger Engine API](using-the-debugger-engine-api.md) section of this documentation for additional methods for examining the stack.

To get information about an operating system thread in the target, use the [**Ioctl**](https://msdn.microsoft.com/library/windows/hardware/ff551084) operation [**IG\_GET\_THREAD\_OS\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff550924).

### <span id="processes"></span><span id="PROCESSES"></span>Processes

To get the address of the process environment block (PEB) that describes the current process use the method [**GetPebAddress**](https://msdn.microsoft.com/library/windows/hardware/ff548122). In kernel-mode debugging, the KPROCESS structure is also available to describe a process. This structure is returned by [**GetCurrentProcessAddr**](https://msdn.microsoft.com/library/windows/hardware/ff545779) (in user-mode debugging, **GetCurrentProcessAddr** returns the address of the PEB).

The method [**GetCurrentProcessHandle**](https://msdn.microsoft.com/library/windows/hardware/ff545816) returns the system handle for the current process.

### <span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>Additional Information

For a more powerful thread manipulation and process manipulation API, see [Controlling Threads and Processes](controlling-threads-and-processes.md) in the [Using the Debugger Engine API](using-the-debugger-engine-api.md) section of this documentation.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20WdbgExts%20Threads%20and%20Processes%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




