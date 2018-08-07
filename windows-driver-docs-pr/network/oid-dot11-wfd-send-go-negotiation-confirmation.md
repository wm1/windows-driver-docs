---
title: OID\_DOT11\_WFD\_SEND\_GO\_NEGOTIATION\_CONFIRMATION
author: windows-driver-content
description: When set, the OID\_DOT11\_WFD\_SEND\_GO\_NEGOTIATION\_CONFIRMATION object identifier (OID) provides the miniport driver with the parameters for a Group Owner (GO) negotiation confirmation.
ms.assetid: 4D836BED-F3F0-4224-9438-C39B8122EE03
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -OID_DOT11_WFD_SEND_GO_NEGOTIATION_CONFIRMATION Network Drivers Starting with Windows Vista
---

# OID\_DOT11\_WFD\_SEND\_GO\_NEGOTIATION\_CONFIRMATION


**Important**  The [Native 802.11 Wireless LAN](https://msdn.microsoft.com/library/windows/hardware/ff560690) interface is deprecated in Windows 10 and later. Please use the WLAN Device Driver Interface (WDI) instead. For more information about WDI, see [WLAN Universal Windows driver model](https://msdn.microsoft.com/library/windows/hardware/dn897672).

 

When set, the OID\_DOT11\_WFD\_SEND\_GO\_NEGOTIATION\_CONFIRMATION object identifier (OID) provides the miniport driver with the parameters for a Group Owner (GO) negotiation confirmation. The OID\_DOT11\_WFD\_SEND\_GO\_NEGOTIATION\_CONFIRMATION request is sent after the miniport inidicates a [**NDIS\_STATUS\_DOT11\_WFD\_RECEIVED\_GO\_NEGOTIATION\_RESPONSE**](https://msdn.microsoft.com/library/windows/hardware/hh439791) indication.

The data type for OID\_DOT11\_WFD\_SEND\_GO\_NEGOTIATION\_CONFIRMATION is the [**DOT11\_SEND\_GO\_NEGOTIATION\_COMFIRMATION\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh406537) structure.

This is a direct OID called in the context of a [**NDIS\_STATUS\_DOT11\_WFD\_RECEIVED\_GO\_NEGOTIATION\_RESPONSE**](https://msdn.microsoft.com/library/windows/hardware/hh439791) indication.

After receiving this OID, the miniport must create and populate all the required Peer-to-Peer (P2P) attributes in the P2P Information Element (IE) before it sends the GO negotiation confirmation packet.

**Note**  Miniports must handle this OID synchronously. They must not process requests as pending.

 

The completion of the attempt to send the GO negotiation response attempt must be indicated to the system with a [**NDIS\_STATUS\_DOT11\_WFD\_GO\_NEGOTIATION\_CONFIRMATION\_SEND\_COMPLETE**](https://msdn.microsoft.com/library/windows/hardware/hh451706) indication. The miniport driver must send the **NDIS\_STATUS\_DOT11\_WFD\_GO\_NEGOTIATION\_CONFIRMATION\_SEND\_COMPLETE** indication after it has stopped the attempt to send the GO negotiation response. This must occur in either case of success or failure.
Requirements
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>Supported starting with Windows 8.</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Windot11.h (include Windot11.h)</td>
</tr>
</tbody>
</table>

## See also


[**DOT11\_SEND\_GO\_NEGOTIATION\_COMFIRMATION\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh406537)

[**NDIS\_STATUS\_DOT11\_WFD\_RECEIVED\_GO\_NEGOTIATION\_RESPONSE**](https://msdn.microsoft.com/library/windows/hardware/hh439791)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20OID_DOT11_WFD_SEND_GO_NEGOTIATION_CONFIRMATION%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


