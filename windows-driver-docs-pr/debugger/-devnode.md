---
title: devnode
description: The devnode extension displays information about a node in the device tree.
ms.assetid: 0c8cb743-f756-461e-b92b-352b550706c1
keywords: ["device node", "device tree", "devnode Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- devnode
api_type:
- NA
---

# !devnode


The **!devnode** extension displays information about a node in the device tree.

```
!devnode Address [Flags] [Service]  
!devnode 1 
!devnode 2
```

## <span id="ddk__devnode_dbg"></span><span id="DDK__DEVNODE_DBG"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
Specifies the hexadecimal address of the device extension whose node is to be displayed. If this is zero, the root of the main device tree is displayed.

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *Flags*   
Specifies the level of output to be displayed. This can be any combination of the following bits:

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>Bit 0 (0x1)  
Causes the display to include all children of the device node.

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>Bit 1 (0x2)  
Causes the display to include resources used (CM\_RESOURCE\_LIST). These include the boot configuration reported by IRP\_MN\_QUERY\_RESOURCES, as well as the resources allocated to the device in the *AllocatedResources* parameter of IRP\_MN\_START\_DEVICE.

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>Bit 2 (0x4)  
Causes the display to include resources required (IO\_RESOURCE\_REQUIREMENTS\_LIST) as reported by IRP\_MN\_FILTER\_RESOURCE\_REQUIREMENTS.

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>Bit 3 (0x8)  
Causes the display to include a list of translated resources as allocated to the device in the *AllocatedResourcesTranslated* parameter of IRP\_MN\_START\_DEVICE.

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>Bit 4 (0x10)  
Specifies that only device nodes that are not started should be displayed.

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>Bit 5 (0x20)  
Specifies that only device nodes with problems should be displayed. (These are nodes that contain the flag bits DNF\_HAS\_PROBLEM or DNF\_HAS\_PRIVATE\_PROBLEM.)

<span id="_______Service______"></span><span id="_______service______"></span><span id="_______SERVICE______"></span> *Service*   
Specifies the name of a service. If this is included, only those device nodes driven by this service will be displayed. (If *Flags* includes bit 0x1, device nodes driven by this service and all their children will be displayed.)

### <span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP and later</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>Additional Information

See [Plug and Play Debugging](plug-and-play-debugging.md) for applications of this extension command. For information about device trees, see the Windows Driver Kit (WDK) documentation and *Microsoft Windows Internals* by Mark Russinovich and David Solomon. (These resources may not be available in some languages and countries.)

Remarks
-------

The **!devnode 1** command lists all pending removals of device objects.

The **!devnode 2** command lists all pending ejects of device objects.

You can use **!devnode 0 1** to see the entire device tree.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20!devnode%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




