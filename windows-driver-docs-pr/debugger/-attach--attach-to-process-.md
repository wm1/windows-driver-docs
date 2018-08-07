---
title: .attach (Attach to Process)
description: The .attach command attaches to a new target application.
ms.assetid: e637c7eb-9c3c-4501-b972-a9293a6da52a
keywords: ["Attach to Process (.attach) command", "process, Attach to Process (.attach) command", ".attach (Attach to Process) Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- .attach (Attach to Process)
api_type:
- NA
---

# .attach (Attach to Process)


The **.attach** command attaches to a new target application.

```
.attach [-premote RemoteOptions] AttachOptions PID
```

## <span id="ddk_meta_attach_to_process_dbg"></span><span id="DDK_META_ATTACH_TO_PROCESS_DBG"></span>Parameters


<span id="_______RemoteOptions______"></span><span id="_______remoteoptions______"></span><span id="_______REMOTEOPTIONS______"></span> *RemoteOptions*   
Specifies a process server to attach to. The options are the same as those for the command line **-premote** option. See [**Activating a Smart Client**](activating-a-smart-client.md) for syntax details.

<span id="_______AttachOptions______"></span><span id="_______attachoptions______"></span><span id="_______ATTACHOPTIONS______"></span> *AttachOptions*   
Specifies how the attach is to be done. This can include any of the following options:

<span id="-b"></span><span id="-B"></span>**-b**  
(Windows XP and later) Prevents the debugger from requesting an initial break-in when attaching to a target process. This can be useful if the application is already suspended, or if you want to avoid creating a break-in thread in the target.

<span id="-e"></span><span id="-E"></span>**-e**  
(Windows XP and later) Allows the debugger to attach to a process that is already being debugged. See [Re-attaching to the Target Application](reattaching-to-the-target-application.md) for details.

<span id="-k"></span><span id="-K"></span>**-k**  
(Windows XP and later) Begins a local kernel debugging session. See [Performing Local Kernel Debugging](performing-local-kernel-debugging.md) for details.

<span id="-f"></span><span id="-F"></span>**-f**  
Freezes all threads in all target applications, except in the new target being attached to. These threads will remain frozen until an exception occurs in the newly-attached process. Note that an initial breakpoint qualifies as an exception. Individual threads can be unfrozen by using the [**~u (Unfreeze Thread)**](-u--unfreeze-thread-.md) command.

<span id="-r"></span><span id="-R"></span>**-r**  
(Windows XP and later)

Causes the debugger to start the target process running when it attaches to it. This can be useful if the application is already suspended and you want it to resume execution.

<span id="-v"></span><span id="-V"></span>**-v**  
Causes the specified process to be debugged noninvasively.

<span id="_______PID______"></span><span id="_______pid______"></span> *PID*   
Specifies the process ID of the new target application.

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

If this command is successful, the debugger will attach to the specified process the next time the debugger issues an execution command. If this command is used several times in a row, execution will have to be requested as many times as this command was used.

Because execution is not permitted during noninvasive debugging, the debugger is not able to noninvasively debug more than one process at a time. This also means that using the **.attach -v** command may render an already-existing invasive debugging session less useful.

Multiple target processes will always be executed together, unless some of their threads are frozen or suspended.

If you wish to attach to a new process and freeze all your existing targets, use the **-f** option. For example, you might be debugging a crash in a client application and want to attach to the server process without letting the client application continue running.

If the **-premote** option is used, the new process will be part of a new system. For details, see [Debugging Multiple Targets](debugging-multiple-targets.md).

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20.attach%20%28Attach%20to%20Process%29%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




