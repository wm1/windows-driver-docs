---
title: WDI_TLV_INTERFACE_ATTRIBUTES
author: windows-driver-content
description: WDI_TLV_INTERFACE_ATTRIBUTES is a TLV that contains the attributes of an interface.
ms.assetid: A36AC0A7-6F5B-4461-841D-3B4C19BD49EB
ms.author: windowsdriverdev 
ms.date: 07/18/2017 
ms.topic: article 
ms.prod: windows-hardware 
ms.technology: windows-devices 
keywords:
 - WDI_TLV_INTERFACE_ATTRIBUTES Network Drivers Starting with Windows Vista
---

# WDI\_TLV\_INTERFACE\_ATTRIBUTES


WDI\_TLV\_INTERFACE\_ATTRIBUTES is a TLV that contains the attributes of an interface.

## TLV Type


0x21

## Length


The sum (in bytes) of the sizes of all contained TLVs.

## Values


| Type                                                                         | Multiple TLV instances allowed | Optional | Description                                                                                                                                                                                     |
|------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_INTERFACE\_CAPABILITIES**](wdi-tlv-interface-capabilities.md)  |                                |          | The capabilities of the interface.                                                                                                                                                              |
| [**WDI\_TLV\_FIRMWARE\_VERSION**](wdi-tlv-firmware-version.md)              |                                |          | An ASCII string that specifies the firmware version.                                                                                                                                            |
| [**WDI\_TLV\_IHV\_NON\_WDI\_OIDS\_LIST**](wdi-tlv-ihv-non-wdi-oids-list.md) |                                | X        | List of non-WDI OIDs that the adapter wants to advertise to the operating system. The adapter should not assume that the operating system has already filtered non-WDI OIDs to match this list. |

 

Requirements
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Minimum supported client</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>Minimum supported server</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20WDI_TLV_INTERFACE_ATTRIBUTES%20%20RELEASE:%20%287/10/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


