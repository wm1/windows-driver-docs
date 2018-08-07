---
title: WDI_TLV_IPV4_CHECKSUM_OFFLOAD
author: windows-driver-content
description: WDI_TLV_IPV4_CHECKSUM_OFFLOAD is a TLV that contains checksum offload capabilities for IPv4.
ms.assetid: FCC5880E-4323-4A24-98C6-CE7C84D03C16
ms.author: windowsdriverdev 
ms.date: 07/18/2017 
ms.topic: article 
ms.prod: windows-hardware 
ms.technology: windows-devices 
keywords:
 - WDI_TLV_IPV4_CHECKSUM_OFFLOAD Network Drivers Starting with Windows Vista
---

# WDI\_TLV\_IPV4\_CHECKSUM\_OFFLOAD


WDI\_TLV\_IPV4\_CHECKSUM\_OFFLOAD is a TLV that contains checksum offload capabilities for IPv4.

## TLV Type


0xCF

## Length


The sum (in bytes) of the sizes of all contained TLVs.

## Values


| Type                                                                                                 | Multiple TLV instances allowed | Optional | Description                                  |
|------------------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------|
| [**WDI\_TLV\_CHECKSUM\_OFFLOAD\_V4\_TX\_PARAMETERS**](wdi-tlv-checksum-offload-v4-tx-parameters.md) |                                |          | Parameters for Tx checksum offload for IPv4. |
| [**WDI\_TLV\_CHECKSUM\_OFFLOAD\_V4\_RX\_PARAMETERS**](wdi-tlv-checksum-offload-v4-rx-parameters.md) |                                |          | Parameters for Rx checksum offload for IPv4. |

 

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
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20WDI_TLV_IPV4_CHECKSUM_OFFLOAD%20%20RELEASE:%20%287/10/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


