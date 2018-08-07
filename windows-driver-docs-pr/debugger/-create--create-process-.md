---
title: .create (Create Process)
description: The .create command creates a new target application.
ms.assetid: 9e34eadf-1f68-4eec-ad6b-d70163d5d876
keywords: [".create (Create Process) Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- .create (Create Process)
api_type:
- NA
---

# .create (Create Process)


The **.create** command creates a new target application.

```
.create [-premote RemoteOptions] [-f] CommandLine 
```

## <span id="ddk_meta_create_process_dbg"></span><span id="DDK_META_CREATE_PROCESS_DBG"></span>Parameters


<span id="_______RemoteOptions______"></span><span id="_______remoteoptions______"></span><span id="_______REMOTEOPTIONS______"></span> *RemoteOptions*   
Specifies a process server to which to attach. The options are the same as those for the command line **-premote** option. See [**Activating a Smart Client**](activating-a-smart-client.md) for syntax details.

<span id="_______-f______"></span><span id="_______-F______"></span> **-f**   
Freezes all threads in all target applications, except in the new target being created. These threads will remain frozen until an exception occurs in the newly-created process. Note that an initial breakpoint qualifies as an exception. Individual threads can be unfrozen by using the [**~u (Unfreeze Thread)**](-u--unfreeze-thread-.md) command.

<span id="_______CommandLine______"></span><span id="_______commandline______"></span><span id="_______COMMANDLINE______"></span> *CommandLine*   
Specifies the complete command line for the new process. *CommandLine* may contain spaces, and must not be surrounded with quotes. All text after the **.create** command is taken as part of *CommandLine*; this command cannot be followed with a semicolon and additional debugger commands.

### <span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Modes</strong></p></td>
<td align="left"><p>user mode only</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Targets</strong></p></td>
<td align="left"><p>live debugging only</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Platforms</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

Remarks
-------

This command can be used when CDB is dormant, or if it is already debugging one or more processes. It cannot be used when WinDbg is dormant.

If this command is successful, the debugger will create the specified process the next time the debugger issues an execution command. If this command is used several times in a row, execution will have to be requested as many times as this command was used.

Multiple target processes will always be executed together, unless some of their threads are frozen or suspended.

If you wish to create a new process and freeze all your existing targets, use the -f option.

If the **-premote** option is used, the new process will be part of a new system. For details, see [Debugging Multiple Targets](debugging-multiple-targets.md).

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20.create%20%28Create%20Process%29%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




