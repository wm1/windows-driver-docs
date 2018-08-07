---
title: OID\_WWAN\_PACKET\_SERVICE
author: windows-driver-content
description: OID\_WWAN\_PACKET\_SERVICE is used to instruct miniport drivers to perform packet service attach/detach actions on the current registered provider’s network for both GSM-based and CDMA-based MB devices.
ms.assetid: 97bb9324-8052-437c-baa5-fb9a8176c779
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -OID_WWAN_PACKET_SERVICE Network Drivers Starting with Windows Vista
---

# OID\_WWAN\_PACKET\_SERVICE


OID\_WWAN\_PACKET\_SERVICE is used to instruct miniport drivers to perform packet service attach/detach actions on the current registered provider’s network for both GSM-based and CDMA-based MB devices. In addition to the packet service attach/detach status, this OID is used to determine data class availability and the currently used data class information.

Miniport drivers must process set and query requests asynchronously, initially returning NDIS\_STATUS\_INDICATION\_REQUIRED to the original request, and later sending an [**NDIS\_STATUS\_WWAN\_PACKET\_SERVICE**](ndis-status-wwan-packet-service.md) status notification containing an [**NDIS\_WWAN\_PACKET\_SERVICE\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff567910) structure to provide information about the current packet service state regardless of completing set or query requests.

Callers requesting to set the current packet service state provide an [**NDIS\_WWAN\_SET\_PACKET\_SERVICE**](https://msdn.microsoft.com/library/windows/hardware/ff567921) structure to the miniport driver with the appropriate information.

Remarks
-------

See [WWAN Packet Service Attach Operations](https://msdn.microsoft.com/library/windows/hardware/ff559092) for more information about using this OID.

Miniport drivers can access the provider network when processing query or set operations, but should not access the Subscriber Identity Module (SIM card).

CDMA-based devices should use this as an opportunity to release the network resource allocation if possible.

Some SIM cards enable the MB device to register only on the packet domain and not the circuit-switched domain. Once a data call ends, the VAN UI sends an OID\_WWAN\_PACKET\_SERVICE set request to detach packet service. This causes the MB device to detach from the packet domain. The MB device unregisters from the network and goes into a power save mode. Consequently, the device disappears from the VAN UI as a result of being unregistered, and can only be recovered by rebooting. In this scenario, miniport drivers should spoof the packet attach/detach operations by returning positive data without setting the MB device into such a mode.

For technologies that do not support packet-attach, miniport drivers should spoof an attach state to let the MB Service know that it can proceed with context activation. Miniport drivers should also spoof the set OID\_WWAN\_PACKET\_SERVICE requests in the miniport driver. Miniport drivers should send [**NDIS\_STATUS\_WWAN\_PACKET\_SERVICE**](ndis-status-wwan-packet-service.md) notifications for query operations and for unsolicited events. Miniport drivers should fail PDP activation if the device packet service state is not set to *WwanPacketServiceStateAttached*.

The MB Service shall not proceed with context activation until the packet service state has reached *WwanPacketServiceStateAttached*.

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
<td><p>Available in Windows 7 and later versions of Windows.</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## See also


[**NDIS\_WWAN\_SET\_PACKET\_SERVICE**](https://msdn.microsoft.com/library/windows/hardware/ff567921)

[**NDIS\_STATUS\_WWAN\_PACKET\_SERVICE**](ndis-status-wwan-packet-service.md)

[WWAN Packet Service Attach Operations](https://msdn.microsoft.com/library/windows/hardware/ff559092)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20OID_WWAN_PACKET_SERVICE%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


