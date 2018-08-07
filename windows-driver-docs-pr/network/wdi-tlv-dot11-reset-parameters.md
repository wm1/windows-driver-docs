---
title: WDI_TLV_DOT11_RESET_PARAMETERS
author: windows-driver-content
description: WDI_TLV_DOT11_RESET_PARAMETERS is a TLV that contains parameters for OID_WDI_TASK_DOT11_RESET.
ms.assetid: 14F3DECD-E875-44BB-969B-705B075E4636
ms.author: windowsdriverdev 
ms.date: 07/18/2017 
ms.topic: article 
ms.prod: windows-hardware 
ms.technology: windows-devices 
keywords:
 - WDI_TLV_DOT11_RESET_PARAMETERS Network Drivers Starting with Windows Vista
---

# WDI\_TLV\_DOT11\_RESET\_PARAMETERS


WDI\_TLV\_DOT11\_RESET\_PARAMETERS is a TLV that contains parameters for [OID\_WDI\_TASK\_DOT11\_RESET](https://msdn.microsoft.com/library/windows/hardware/dn925952).

## TLV Type


0xA2

## Length


The size (in bytes) of a UINT8.

## Values


| Type  | Description                                                                                                     |
|-------|-----------------------------------------------------------------------------------------------------------------|
| UINT8 | If (and only if) this is set to 1, all MIB attributes for the port being reset are set to their default values. |

 

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
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20WDI_TLV_DOT11_RESET_PARAMETERS%20%20RELEASE:%20%287/10/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


