---
title: WDI_TLV_BAND_INFO
author: windows-driver-content
description: WDI_TLV_BAND_INFO is a TLV that contains band information.
ms.assetid: 37F1CE39-5471-489A-8DA2-F058B631B31F
ms.author: windowsdriverdev 
ms.date: 07/18/2017 
ms.topic: article 
ms.prod: windows-hardware 
ms.technology: windows-devices 
keywords:
 - WDI_TLV_BAND_INFO Network Drivers Starting with Windows Vista
---

# WDI\_TLV\_BAND\_INFO


WDI\_TLV\_BAND\_INFO is a TLV that contains band information.

## TLV Type


0x27

## Length


The sum (in bytes) of the sizes of all contained TLVs.

## Values


| Type                                                                 | Multiple TLV instances allowed | Optional | Description                                   |
|----------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------|
| [**WDI\_TLV\_BAND\_CAPABILITIES**](wdi-tlv-band-capabilities.md)    |                                |          | The capabilities of the band.                 |
| [**WDI\_TLV\_PHY\_TYPE\_LIST**](wdi-tlv-phy-type-list.md)           |                                |          | A list of valid PHY types in this band.       |
| [**WDI\_TLV\_CHANNEL\_LIST**](wdi-tlv-channel-list.md)              |                                |          | A list of valid channel numbers in this band. |
| [**WDI\_TLV\_CHANNEL\_WIDTH\_LIST**](wdi-tlv-channel-width-list.md) |                                |          | A list of channel widths in MHz               |

 

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
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20WDI_TLV_BAND_INFO%20%20RELEASE:%20%287/10/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


