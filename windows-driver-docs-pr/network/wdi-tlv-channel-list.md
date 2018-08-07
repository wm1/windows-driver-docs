---
title: WDI_TLV_CHANNEL_LIST
author: windows-driver-content
description: WDI_TLV_CHANNEL_LIST is a TLV that contains one or more channel numbers.
ms.assetid: DBBA28C2-D80F-409B-BEE6-81B6FEDF7484
ms.author: windowsdriverdev 
ms.date: 07/18/2017 
ms.topic: article 
ms.prod: windows-hardware 
ms.technology: windows-devices 
keywords:
 - WDI_TLV_CHANNEL_LIST Network Drivers Starting with Windows Vista
---

# WDI\_TLV\_CHANNEL\_LIST


WDI\_TLV\_CHANNEL\_LIST is a TLV that contains one or more channel numbers.

## TLV Type


0x4

## Length


The size (in bytes) of the array of [**WDI\_CHANNEL\_MAPPING\_ENTRY**](https://msdn.microsoft.com/library/windows/hardware/dn897799) structures. The array must contain 1 or more structures.

## Values


| Type                                                                       | Description                          |
|----------------------------------------------------------------------------|--------------------------------------|
| [**WDI\_CHANNEL\_MAPPING\_ENTRY**](https://msdn.microsoft.com/library/windows/hardware/dn897799)\[\] | An array of channel mapping entries. |

 

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
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20WDI_TLV_CHANNEL_LIST%20%20RELEASE:%20%287/10/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


