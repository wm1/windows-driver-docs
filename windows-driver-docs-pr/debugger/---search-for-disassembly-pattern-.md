---
title: # (Search for Disassembly Pattern)
description: The number sign (#) command searches for the specified pattern in the disassembly code.
ms.assetid: 834dd432-94b8-4bf6-9318-09a118eab5ab
keywords: ["(Search for Disassembly Pattern) Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- (Search for Disassembly Pattern)
api_type:
- NA
---

# \# (Search for Disassembly Pattern)


The number sign (**\#**) command searches for the specified pattern in the disassembly code.

```
# [Pattern] [Address [ L Size ]] 
```

## <span id="ddk_cmd_search_for_disassembly_pattern_dbg"></span><span id="DDK_CMD_SEARCH_FOR_DISASSEMBLY_PATTERN_DBG"></span>Parameters


<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span> *Pattern*   
Specifies the pattern to search for in the disassembly code. *Pattern* can contain a variety of wildcard characters and specifiers. For more information about the syntax, see [String Wildcard Syntax](string-wildcard-syntax.md). If you want to include spaces in *Pattern*, you must enclose the pattern in quotation marks. The pattern is not case sensitive. If you have previously used the **\#** command and you omit *Pattern*, the command reuses the most recently used pattern.

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
Specifies the address where the search begins. For more information about the syntax, see [Address and Address Range Syntax](address-and-address-range-syntax.md).

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span> *Size*   
Specifies the number of instructions to search. If you omit *Size*, the search continues until the first match occurs.

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

 

### <span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>Additional Information

For more information about assembly debugging and related commands, see [Debugging in Assembly Mode](debugging-in-assembly-mode.md).

Remarks
-------

If you previously used the **\#** command and you omit *Address*, the search begins where the previous search ended.

This command works by searching the disassembled text for the specified pattern. You can use this command to find register names, constants, or any other string that appears in the disassembly output. You can repeat the command without the *Address* parameter to find successive occurrences of the pattern.

You can view disassembly instructions by using the [**u (Unassemble)**](u--unassemble-.md) command or by using the [Disassembly window](disassembly-window.md) in WinDbg. The disassembly display contains up to four parts: Address offset, Binary code, Assembly language mnemonic, and Assembly language details. The following example shows a possible display.

```
0040116b    45          inc         ebp            
0040116c    fc          cld                        
0040116d    8945b0      mov         eax,[ebp-0x1c] 
```

The **\#** command can search for text within any single part of the disassembly display. For example, you could use **\# eax 0040116b** to find the **mov eax,\[ebp-0x1c\]** instruction at address 0040116d. The following commands also find this instruction.

```
#  [ebp?0x  0040116b 
#  mov  0040116b 
#  8945*  0040116b 
#  116d  0040116b 
```

However, you cannot search for **mov eax\*** as a single unit, because **mov** and **eax** appear in different parts of the display. Instead, use **mov\*eax**.

As an additional example, you could issue the following command to search for the first reference to the **strlen** function after the entry point **main**.

```
# strlen main
```

Similarly, you could issue the following two commands to find the first **jnz** instruction after address 0x779F9FBA and then find the next **jnz** instruction after that.

```
# jnz 779f9fba# 
```

When you omit *Pattern* or *Address*, their values are based on the previous use of the **\#** command. If you omit either parameter the first time that you issue the **\#** command, no search is performed. However, the values of *Pattern* and *Address* are initialized even in this situation.

If you include *Pattern* or *Address*, its value is set to the entered value. If you omit *Address*, it is initialized to the current value of the program counter. If you omit *Pattern*, it is initialized to an empty pattern.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20#%20%28Search%20for%20Disassembly%20Pattern%29%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




