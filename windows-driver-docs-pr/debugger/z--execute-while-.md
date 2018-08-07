---
title: z (Execute While)
description: The z command executes a command while a given condition is true.
ms.assetid: 075dc012-68c2-4172-9d37-57bc8358297c
keywords: ["z (Execute While) Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- z (Execute While)
api_type:
- NA
---

# z (Execute While)


The **z** command executes a command while a given condition is true.

User-Mode

```
Command ; z( Expression ) 
```

Kernel-Mode

```
Command ; [Processor] z( Expression )
```

## <span id="ddk_cmd_execute_while_dbg"></span><span id="DDK_CMD_EXECUTE_WHILE_DBG"></span>Parameters


<span id="_______Command______"></span><span id="_______command______"></span><span id="_______COMMAND______"></span> *Command*   
Specifies the command to execute while the *Expression* condition evaluates to a nonzero value. This command is always executed at least once.

<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *Processor*   
Specifies the processor that applies to the test. For more information about the syntax, see [Multiprocessor Syntax](multiprocessor-syntax.md). You can specify processors only in kernel mode.

<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *Expression*   
Specifies the condition to test. If this condition evaluates to a nonzero value, the *Command* command is executed again and then *Expression* is tested again. For more information about the syntax, see [Numerical Expression Syntax](numerical-expression-syntax.md).

### <span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Modes</strong></p></td>
<td align="left"><p>User mode, kernel mode</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Targets</strong></p></td>
<td align="left"><p>Live, crash dump</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Platforms</strong></p></td>
<td align="left"><p>All</p></td>
</tr>
</tbody>
</table>

 

Remarks
-------

In many debugger commands, the semicolon is used to separate unrelated commands. However, in the **z** command, a semicolon separates the "z" from the *Command* parameter.

The *Command* command is always executed at least once, and then *Expression* is tested. If the condition is a nonzero value, the command is again executed, and then *Expression* is tested again. (This behavior is similar to a C-language **do - while** loop, not a simple **while** loop.)

If there are several semicolons to the left of the "z", all commands to the left of the "z" repeat as long as the *Expression* condition is true. Such commands can be any debugger commands that permit a terminal semicolon.

If you add another semicolon and additional commands after the **z** command, these additional commands are executed after the loop is complete. We do not typically recommend a line that begins with "z" because it generates uninteresting output forever unless the condition becomes false because of some other action. Note that you can nest **z** commands.

To break a loop that is continuing for too long, use [**CTRL+C**](ctrl-c--break-.md) in CDB or KD, or use [Debug | Break](debug---break.md) or CTRL+BREAK in WinDbg.

The following code example shows an unnecessarily complex way to zero the **eax** register.

```
0:000> reax = eax - 1 ; z(eax)
```

The following example increments the **eax** and **ebx** registers until one of them is at least 8 and then it increments the **ecx** register once.

```
0:000> reax=eax+1; rebx=ebx+1; z((eax<8)|(ebx<8)); recx=ecx+1
```

The following example uses C++ expression syntax and uses the pseudo-register **$t0** as a loop variable.

```
0:000> .expr /s c++
Current expression evaluator: C++ - C++ source expressions

0:000> db pindexcreate[@$t0].szKey; r$t0=@t0+1; z( @$t0 < cIndexCreate )
```

## <span id="see_also"></span>See also


[**j (Execute If-Else)**](j--execute-if---else-.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20z%20%28Execute%20While%29%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





