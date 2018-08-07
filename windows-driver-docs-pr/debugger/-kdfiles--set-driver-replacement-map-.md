---
title: .kdfiles (Set Driver Replacement Map)
description: The .kdfiles command reads a file and uses its contents as the driver replacement map.
ms.assetid: 3b0ac8c1-f0bd-4878-9303-23d6999650ee
keywords: ["Set Driver Replacement Map (.kdfiles) command", "driver replacement map, Set Driver Replacement Map (.kdfiles) command", ".kdfiles (Set Driver Replacement Map) Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- .kdfiles (Set Driver Replacement Map)
api_type:
- NA
---

# .kdfiles (Set Driver Replacement Map)


The **.kdfiles** command reads a file and uses its contents as the driver replacement map.

```
.kdfiles MapFile 
.kdfiles -m OldDriver NewDriver
.kdfiles -s SaveFile 
.kdfiles -c 
.kdfiles 
```

## <span id="ddk_meta_set_driver_replacement_map_dbg"></span><span id="DDK_META_SET_DRIVER_REPLACEMENT_MAP_DBG"></span>Parameters


<span id="_______MapFile______"></span><span id="_______mapfile______"></span><span id="_______MAPFILE______"></span> *MapFile*   
Specifies the driver replacement map file to read.

<span id="_______-m______"></span><span id="_______-M______"></span> **-m**   
Adds a driver replacement association to the current association list.

<span id="_______OldDriver______"></span><span id="_______olddriver______"></span><span id="_______OLDDRIVER______"></span> *OldDriver*   
Specifies the path and file name of the previous driver on the target computer. The syntax for *OldDriver* is the same as that of the first line after **map** in a driver replacement file. For more information about this syntax, see [Mapping Driver Files](mapping-driver-files.md).

<span id="_______NewDriver______"></span><span id="_______newdriver______"></span><span id="_______NEWDRIVER______"></span> *NewDriver*   
Specifies the path and file name of the new driver. This driver can be on the host computer or at some other network location. The syntax for *NewDriver* is the same as that of the second line after **map** in a driver replacement file. For more information about this syntax, see [Mapping Driver Files](mapping-driver-files.md).

<span id="_______-s______"></span><span id="_______-S______"></span> **-s**   
Creates a file and writes the current driver replacement associations to that file.

<span id="_______SaveFile______"></span><span id="_______savefile______"></span><span id="_______SAVEFILE______"></span> *SaveFile*   
Specifies the name of the file to create.

<span id="_______-c______"></span><span id="_______-C______"></span> **-c**   
Deletes the existing driver replacement map. (This option does not alter the map file itself. Instead, this option clears the debugger's current map settings.)

### <span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

You can use the **.kdfiles** command in Microsoft Windows XP and later versions of Windows. If you use this command in earlier versions of Windows, the command has no effect and does not generate an error.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Modes</strong></p></td>
<td align="left"><p>Kernel mode only</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Targets</strong></p></td>
<td align="left"><p>Live debugging only</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Platforms</strong></p></td>
<td align="left"><p>x86-based and Itanium-based processors only</p></td>
</tr>
</tbody>
</table>

 

### <span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>Additional Information

For more information about and examples of driver replacement and the replacement of other kernel-mode modules, a description of the format for driver replacement map files, and restrictions for using this feature, see [Mapping Driver Files](mapping-driver-files.md).

Remarks
-------

If you use the **.kdfiles** command without parameters, the debugger displays the path and name of the current driver replacement map file and the current set of replacement associations.

When you run this command, the specified *MapFile*file is read. If the file is not found or if it does not contain text in the proper format, the debugger displays a message that states, "Unable to load file associations".

If the specified file is in the correct driver replacement map file format, the debugger loads the file's contents and uses them as the driver replacement map. This map remains until you exit the debugger, or until you issue another **.kdfiles** command.

After the file has been read, the driver replacement map is not affected by subsequent changes to the file (unless these changes are followed by another **.kdfiles** command).

Requirements
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>Supported in Windows XP and later versions of the Windows operating system.</p></td>
</tr>
</tbody>
</table>

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20.kdfiles%20%28Set%20Driver%20Replacement%20Map%29%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




