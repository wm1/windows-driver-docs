---
title: .ocommand (Expect Commands from Target)
description: The .ocommand command enables the target application to send commands to the debugger.
ms.assetid: a4363395-111f-48eb-b1da-c17c0ad9f067
keywords: ["Expect Commands from Target (.ocommand) command", ".ocommand (Expect Commands from Target) Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- .ocommand (Expect Commands from Target)
api_type:
- NA
---

# .ocommand (Expect Commands from Target)


The **.ocommand** command enables the target application to send commands to the debugger.

```
.ocommand  String 
.ocommand -d 
.ocommand 
```

## <span id="ddk_meta_expect_commands_from_target_dbg"></span><span id="DDK_META_EXPECT_COMMANDS_FROM_TARGET_DBG"></span>Parameters


<span id="_______String______"></span><span id="_______string______"></span><span id="_______STRING______"></span> *String*   
Specifies the command prefix string. *String* can include spaces, but you cannot use C-style control characters such as **\\"** and **\\n**. You can also enclose *String* in quotation marks. However, if *String* includes a semicolon, leading spaces, or trailing spaces, you must enclose *String* in quotation marks.

<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
Deletes the command prefix string.

### <span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Modes</strong></p></td>
<td align="left"><p>User mode only</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Targets</strong></p></td>
<td align="left"><p>Live debugging only</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Platforms</strong></p></td>
<td align="left"><p>All</p></td>
</tr>
</tbody>
</table>

 

### <span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>Additional Information

For more information about [**OutputDebugString**](https://msdn.microsoft.com/library/windows/desktop/aa363362) and other user-mode functions that communicate with a debugger, see the Microsoft Windows SDK documentation.

Remarks
-------

If you use the **.ocommand** command without parameters, the debugger displays the current command prefix string. To clear the existing string, use **.ocommand -d**.

When you have set a command prefix string, any target output (such as the contents of an [**OutputDebugString**](https://msdn.microsoft.com/library/windows/desktop/aa363362) command) is scanned. If this output begins with the command prefix string, the text of the output that follows the prefix string is treated as a debugger command string and is run. When this text is executed, the command string is not displayed.

The target can include an [**.echo (Echo Comment)**](-echo--echo-comment-.md) command in the output string if you want additional messages. Target output that does not begin with the prefix string is displayed in the typical manner.

After the commands within the command string have been executed, the target remains broken into the debugger, unless the final command is [**g (Go)**](g--go-.md).

The comparison between the command prefix string and the target output is not case sensitive. (However, subsequent uses of **.ocommand** display the string that you entered with the case preserved).

For this example, assume that you enter the following command in the debugger.

```
0:000> .ocommand magiccommand
```

Then, the target application executes the following line.

```
OutputDebugString("MagicCommand kb;g");
```

The debugger recognizes the command string prefix and executes **kb;g** immediately.

However, the following line does not cause any commands to be executed.

```
OutputDebugString("Command on next line.\nmagiccommand kb;g");
```

There are no commands executed from the preceding example because the command string prefix is not at the beginning of the output, even though it does begin a new line.

**Note**   You should choose a command string prefix that will not likely appear in any target output other than your own commands.

 

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20.ocommand%20%28Expect%20Commands%20from%20Target%29%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




