---
title: CTRL+C (Break)
description: The CTRL+C key breaks into the debugger, stopping the target application or target computer, and cancels debugger commands.
ms.assetid: ee9df6d7-4a40-4006-90df-478e06899e3a
keywords: ["CTRL+C (Break) Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- CTRL+C (Break)
api_type:
- NA
---

# CTRL+C (Break)


The CTRL+C key breaks into the debugger, stopping the target application or target computer, and cancels debugger commands.

CDB Syntax

```
CTRL+C 
```

KD Syntax

```
CTRL+C 
```

Target Computer Syntax

```
SYSRQ 
ALT+SYSRQ 
F12 
```

## <span id="ddk_meta_ctrl_c_dbg"></span><span id="DDK_META_CTRL_C_DBG"></span>


### <span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Debuggers</strong></p></td>
<td align="left"><p>CDB and KD only</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Modes</strong></p></td>
<td align="left"><p>user mode, kernel mode</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Targets</strong></p></td>
<td align="left"><p>live, crash dump</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Platforms</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>Additional Information

For other methods of issuing this command and an overview of related commands, see [Controlling the Target](controlling-the-target.md).

Remarks
-------

**When Using CDB:**

In user mode, the CTRL+C key causes the target application to break into the debugger. The target application freezes, the debugger becomes active, and debugger commands can be entered.

If the debugger is already active, CTRL+C does not affect the target application. It can be, however, used to terminate a debugger command. For instance, if you have requested a long display and no longer want to see it, CTRL+C will end the display and return you to the debugger command prompt.

When performing remote debugging with CDB, CTRL+C can be pressed on the host computer's keyboard. If you want to issue a break from the target computer's keyboard, use CTRL+C on an x86 machine.

The F12 key can be used to get a command prompt when the application being debugged is busy. Set the focus on one of the target application's windows and press the F12 key on the target computer.

**When Using KD:**

In kernel mode, the CTRL+C key causes the target computer to break into the debugger. This locks the target computer and wakes up the debugger.

When debugging a system that is still running, CTRL+C must be pressed on the host keyboard to get the initial command prompt.

If the debugger is already active, CTRL+C does not affect the target computer. It can be used, however, to terminate a debugger command. For instance, if you have requested a long display and no longer want to see it, CTRL+C will end the display and return you to the debugger command prompt.

CTRL+C can also be used to get a command prompt when a debugger command is generating a long display or when the target computer is busy. When debugging an x86 machine, it can be pressed on either the host or target keyboard.

SYSRQ (or ALT+SYSRQ on an enhanced keyboard) is similar. It works from the host or target keyboard on any processor. However, it only works if the prompt has been acquired by pressing CTRL+C at least once before.

The SYSRQ key can be disabled by editing the registry. In the registry key

```
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\i8042prt\Parameters
```

create a value named **BreakOnSysRq**, and set it equal to DWORD 0x0. Then reboot. After this is done, pressing the SYSRQ key on the target computer's keyboard will not break into the kernel debugger.

**When Debugging KD with CDB:**

If you are debugging KD with CDB, then CTRL+C will be intercepted by the host debugger (CDB). To break into the target debugger (KD), you should use [**CTRL+F**](ctrl-f--break-to-kd-.md) instead.

**Note**   Note that in WinDbg, CTRL+C is a [shortcut key](keyboard-shortcuts.md) that is used to copy text from a window. To issue a break command in WinDbg, use [CTRL+BREAK](debug---break.md) or select Debug | Break from the menu.

 

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20CTRL+C%20%28Break%29%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




