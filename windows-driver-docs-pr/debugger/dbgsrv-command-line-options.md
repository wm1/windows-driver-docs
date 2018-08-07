---
title: DbgSrv Command-Line Options
description: The DbgSrv command line uses the following syntax.
ms.assetid: 817f7ede-bdaf-4d4e-a1bd-579c67ea1ab9
keywords: ["DbgSrv Command-Line Options Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- DbgSrv Command-Line Options
api_type:
- NA
---

# DbgSrv Command-Line Options


The DbgSrv command line uses the following syntax.

```
dbgsrv -t ServerTransport [-sifeo image.ext] -c[s] AppCmdLine [-x | -pc] 

dbgsrv -? 
```

All options are case-sensitive.

## <span id="ddk_dbgsrv_command_line_options_dbg"></span><span id="DDK_DBGSRV_COMMAND_LINE_OPTIONS_DBG"></span>Parameters


<span id="_______-t_______ServerTransport______"></span><span id="_______-t_______servertransport______"></span><span id="_______-T_______SERVERTRANSPORT______"></span> **-t** *ServerTransport*   
Specifies the transport protocol. For a list of the possible protocols and the syntax for *ServerTransport* in each case, see [**Activating a Process Server**](activating-a-process-server.md).

<span id="_______-sifeo_______Executable______"></span><span id="_______-sifeo_______executable______"></span><span id="_______-SIFEO_______EXECUTABLE______"></span> **-sifeo** *Executable*   
Suspends the Image File Execution Option (IFEO) value for the given image. *Executable* should include the file name of the executable image, including the file name extensions. The -sifeo option allows DbgSrv to be set as the IFEO debugger for an image created by the -c option, without causing recursive invocation due to the IFEO setting. This option can be used only if -c is used.

<span id="_______-c______"></span><span id="_______-C______"></span> **-c**   
Causes DbgSrv to create a new process. You can use this to create a process that you intend to debug. This is similar to spawning a new process from the debugger, except that this process will *not* be debugged when it is created. To debug this process, determine its PID and use the **-p** option when starting the smart client to debug this process.

<span id="_______s______"></span><span id="_______S______"></span> **s**   
Causes the newly-created process to be immediately suspended. If you are using this option, it is recommended that you use CDB as your smart client, and that you start the smart client with the -pb command-line option, in conjunction with -p PID. If you include the -pb option on the command line, the process will resume when the debugger attaches to it; otherwise you can resume the process with the [**~\*m**](-m--resume-thread-.md) command.

<span id="_______AppCmdLine______"></span><span id="_______appcmdline______"></span><span id="_______APPCMDLINE______"></span> *AppCmdLine*   
Specifies the full command line of the process to be created. *AppCmdLine* can be either a Unicode or ASCII string, and can include any printable character. All text that appears after the **-c**\[**s**\] parameter will be taken to form the string *AppCmdLine*.

<span id="_______-x______"></span><span id="_______-X______"></span> **-x**   
Causes the remainder of the command line to be ignored. This option is useful if you are launching DbgSrv from an application that may append unwanted text to its command line.

<span id="_______-pc______"></span><span id="_______-PC______"></span> **-pc**   
Causes the remainder of the command line to be ignored. This option is useful if you are launching DbgSrv from an application that may append unwanted text to its command line. A syntax error results if -pc is the final element on the DbgSrv command line. Aside from this restriction, -pc is identical to -x.

<span id="_______-_______"></span> **-?**   
Displays a message box with help text for the DbgSrv command line.

For information about using DbgSrv, see [Process Servers (User Mode)](process-servers--user-mode-.md).

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20DbgSrv%20Command-Line%20Options%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




