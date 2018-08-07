---
title: for_each_function
description: The for_each_function extension executes a debugger command for each function, in a specified module, whose name matches a specified pattern.
ms.assetid: D51C3562-3D49-4528-A208-71A8756EBC8E
keywords: ["for_each_function Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- for_each_function
api_type:
- NA
---

# !for\_each\_function


The **!for\_each\_function** extension executes a debugger command for each function, in a specified module, whose name matches a specified pattern.

```
!for_each_function -m:ModuleName -p:Pattern -c:CommandString
!for_each_function -?
```

## <span id="ddk__vad_dbg"></span><span id="DDK__VAD_DBG"></span>Parameters


<span id="_______-m_ModuleName______"></span><span id="_______-m_modulename______"></span><span id="_______-M_MODULENAME______"></span> -m:*ModuleName*   
Specifies the module name. This name is typically the file name without the file name extension. In some cases, the module name differs significantly from the file name.

<span id="-p_Pattern______"></span><span id="-p_pattern______"></span><span id="-P_PATTERN______"></span>-p:*Pattern*   
Specifies the pattern to be matched.

<span id="_______-c_CommandString______"></span><span id="_______-c_commandstring______"></span><span id="_______-C_COMMANDSTRING______"></span> -c:*CommandString*   
Specifies the debugger command to execute for each function, in the specified module, that matches the pattern.

You can use the following aliases in *CommandString*.

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Alias</th>
<th align="left">Data type</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>@#SymbolName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>The symbol name.</p></td>
</tr>
<tr class="even">
<td align="left"><p>@#SymbolAddress</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>The symbol address.</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@#ModName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>The module name.</p></td>
</tr>
<tr class="even">
<td align="left"><p>@#FunctionName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>The function name.</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-_______"></span> -?   
Displays help for this extension.

### <span id="DLL"></span><span id="dll"></span>DLL

Ext.dll

Remarks
-------

The following example shows how to list all function names, in the PCI module, that match the pattern \*read\*.

```
1: kd> !for_each_function -m:pci -p:*read* -c:.echo @#FunctionName

PciReadDeviceConfig
PciReadDeviceSpace
PciReadSlotIdData
PciExternalReadDeviceConfig
PiRegStateReadStackCreationSettingsFromKey
VmProxyReadDevicePathsFromRegistry
PpRegStateReadCreateClassCreationSettings
ExpressRootPortReadConfigSpace
PciReadRomImage
PciDevice_ReadConfig
PciReadDeviceConfigEx
PciReadSlotConfig
```

If an alias is not preceded and followed by a blank space, you must put the alias inside the [**${} Alias Interpreter**](-------alias-interpreter-.md) token.

The following example shows how to list all symbols, in all modules, whose function names match the pattern \*CreateFile\*. The alias @\#ModuleName is not preceded by a blank space. Therefore, it is put inside the [**${} Alias Interpreter**](-------alias-interpreter-.md) token.

**Note**  Do not confuse the @\#ModuleName alias with the @\#ModName alias. The @\#ModuleName alias belongs to the [**!for\_each\_module**](-for-each-module.md) extension, and the @\#ModName alias belongs to the **!for\_each\_function** extension.

 

```
1: kd> !for_each_module !for_each_function -m:${@#ModuleName} -p:*CreateFile* -c:.echo @#SymbolName
nt!BiCreateFileDeviceElement
nt!NtCreateFile
...
Wdf01000!FxFileObject::_CreateFileObject
fltmgr!FltCreateFileEx2$fin$0
fltmgr!FltCreateFileEx2
...
Ntfs!TxfIoCreateFile
Ntfs!NtfsCreateFileLock
...
MpFilter!MpTxfpCreateFileEntryUnsafe
mrxsmb10!MRxSmbFinishLongNameCreateFile
...
srv!SrvIoCreateFile
```

You can put a sequence of commands in a command file, and use [**$$&gt;&lt; (Run Script File)**](-----------------------a---run-script-file-.md) to execute those commands for each function that matches the pattern. Suppose that a file named Commands.txt contains the following commands:

```
.echo
.echo @#FunctionName
u @#SymbolAddress L1
```

In the following example, the commands in the Commands.text file are executed for each function, in the PCI module, that matches the pattern \*read\*.

```
1: kd> !for_each_function -m:pci -p:*read* -c:$$><Commands.txt

PciReadDeviceConfig
pci!PciReadDeviceConfig [d:\wmm1\drivers\busdrv\pci\config.c @ 349]:
fffff880`00f7b798 48895c2408      mov     qword ptr [rsp+8],rbx

PciReadDeviceSpace
pci!PciReadDeviceSpace [d:\wmm1\drivers\busdrv\pci\config.c @ 1621]:
fffff880`00f7c044 48895c2408      mov     qword ptr [rsp+8],rbx

...
```

## <span id="see_also"></span>See also


[**!for\_each\_module**](-for-each-module.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20!for_each_function%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





