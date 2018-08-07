---
title: NDIS_STATUS_WDI_INDICATION_SEND_AP_ASSOCIATION_RESPONSE_COMPLETE
author: windows-driver-content
description: Miniport drivers use NDIS_STATUS_WDI_INDICATION_SEND_AP_ASSOCIATION_RESPONSE_COMPLETE to indicate information about the AP association response sent by OID_WDI_TASK_SEND_AP_ASSOCIATION_RESPONSE.
ms.assetid: c8bfa3b3-5d22-4831-9355-94c62fed7fd4
ms.author: windowsdriverdev 
ms.date: 07/18/2017 
ms.topic: article 
ms.prod: windows-hardware 
ms.technology: windows-devices 
keywords:
 - NDIS_STATUS_WDI_INDICATION_SEND_AP_ASSOCIATION_RESPONSE_COMPLETE Network Drivers Starting with Windows Vista
---

# NDIS\_STATUS\_WDI\_INDICATION\_SEND\_AP\_ASSOCIATION\_RESPONSE\_COMPLETE


Miniport drivers use NDIS\_STATUS\_WDI\_INDICATION\_SEND\_AP\_ASSOCIATION\_RESPONSE\_COMPLETE to indicate information about the AP association response sent by [OID\_WDI\_TASK\_SEND\_AP\_ASSOCIATION\_RESPONSE](oid-wdi-task-send-ap-association-response.md).

| Object |
|--------|
| Port   |

 

## Payload data


Type
Multiple TLV instances allowed
Optional
Description
[**WDI\_TLV\_ASSOCIATION\_RESPONSE\_RESULT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/dn926138)
The association response parameters.
[**WDI\_TLV\_ASSOCIATION\_RESPONSE\_FRAME**](https://msdn.microsoft.com/library/windows/hardware/dn926135)
The received association response. This does not include the 802.11 MAC header.
[**WDI\_TLV\_BEACON\_IES**](https://msdn.microsoft.com/library/windows/hardware/dn926148)
The beacon IEs from the association.
[**WDI\_TLV\_PHY\_TYPE\_LIST**](https://msdn.microsoft.com/library/windows/hardware/dn898029)
X
The list of PHY types.
 

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20NDIS_STATUS_WDI_INDICATION_SEND_AP_ASSOCIATION_RESPONSE_COMPLETE%20%20RELEASE:%20%286/30/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


