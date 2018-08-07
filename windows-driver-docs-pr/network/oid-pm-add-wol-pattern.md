---
title: OID\_PM\_ADD\_WOL\_PATTERN
author: windows-driver-content
description: As a set, NDIS protocol drivers use the OID\_PM\_ADD\_WOL\_PATTERN OID to add a power management wake-on-LAN pattern to a network adapter. The InformationBuffer member of the NDIS\_OID\_REQUEST structure contains a pointer to an NDIS\_PM\_WOL\_PATTERN structure.
ms.assetid: 1005cebb-8ead-4d16-b3ea-5a74da0b054f
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -OID_PM_ADD_WOL_PATTERN Network Drivers Starting with Windows Vista
---

# OID\_PM\_ADD\_WOL\_PATTERN


As a set, NDIS protocol drivers use the OID\_PM\_ADD\_WOL\_PATTERN OID to add a power management wake-on-LAN pattern to a network adapter. The **InformationBuffer** member of the [**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710) structure contains a pointer to an [**NDIS\_PM\_WOL\_PATTERN**](https://msdn.microsoft.com/library/windows/hardware/ff566768) structure.

Remarks
-------

NDIS 6.20 and later protocol drivers use OID\_PM\_ADD\_WOL\_PATTERN to add a Wake on LAN (WOL) pattern to a network adapter. The OID request contains criterion that the network adapter must compare to incoming packets when it is in a low power state. The network adapter must generate a wake up event when it receives a packet that matches the pattern criteria.

A protocol driver can add WOL patterns after it successfully binds to an underlying network adapter and as soon as it has the necessary data (such as the IP address of the interface) to set up the WOL pattern. The protocol driver can also add a WOL pattern in response to some other power management event notifications such as the rejection of a previously added WOL pattern or an offloaded protocol.

To avoid race conditions in NDIS and other protocol drivers that are bound to the same miniport adapter, after NDIS starts to set a network adapter to a low power state, it will fail any attempt to add a new wake up pattern to that network adapter. For example, if an NDIS protocol driver tries to add a new WOL pattern in the context of processing a **NetEventSetPower** event notification for that network adapter, NDIS will fail the request.

Before NDIS sends this OID request down to the underlying NDIS drivers or completes the request to the overlying driver, it sets the ULONG **PatternId** member of the [**NDIS\_PM\_WOL\_PATTERN**](https://msdn.microsoft.com/library/windows/hardware/ff566768) structure to a unique value. Protocol drivers and NDIS use this pattern identifier with the [OID\_PM\_REMOVE\_WOL\_PATTERN](oid-pm-remove-wol-pattern.md) OID request to remove the WOL pattern from the underlying network adapter.

**Note**  The pattern identifier is a unique value for each of the patterns that are set on a network adapter. However, the pattern identifier is not globally unique across all miniport adapters.

 

If NDIS or an underlying network adapter removes a WOL pattern, it generates an [**NDIS\_STATUS\_PM\_WOL\_PATTERN\_REJECTED**](https://msdn.microsoft.com/library/windows/hardware/ff567414) status indication. The **StatusBuffer** member of the [**NDIS\_STATUS\_INDICATION**](https://msdn.microsoft.com/library/windows/hardware/ff567373) structure contains the ULONG WOL pattern identifier of the rejected WOL pattern.

The miniport driver returns one of the following status codes for the request:

<a href="" id="ndis-status-success"></a>NDIS\_STATUS\_SUCCESS  
The requested pattern was added successfully. The **PatternId** member of the NDIS\_PM\_WOL\_PATTERN structure contains a pattern identifier.

<a href="" id="ndis-status-pending"></a>NDIS\_STATUS\_PENDING  
The request is pending completion. NDIS will pass the final status code and results to the OID request completion handler of the caller after the request is complete.

<a href="" id="ndis-status-pm-wol-pattern-list-full"></a>NDIS\_STATUS\_PM\_WOL\_PATTERN\_LIST\_FULL  
The request failed because the pattern list is full and the network adapter cannot add another pattern.

<a href="" id="ndis-status-resources"></a>NDIS\_STATUS\_RESOURCES  
NDIS or underlying network adapter could not add the new pattern due to lack of resources.

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_STATUS\_INVALID\_PARAMETER  
One or more parameters in the NDIS\_PM\_WOL\_PATTERN structure were invalid.

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_STATUS\_BUFFER\_TOO\_SHORT  
The information buffer was too short. NDIS set the **DATA.SET\_INFORMATION.BytesNeeded** member in the NDIS\_OID\_REQUEST structure to the minimum buffer size that is required.

<a href="" id="ndis-status-not-supported"></a>NDIS\_STATUS\_NOT\_SUPPORTED  
The network adapter does not support the requested WOL pattern.

<a href="" id="ndis-status-failure"></a>NDIS\_STATUS\_FAILURE  
The request failed for reasons other than the preceding reasons.

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
<td><p>Supported in NDIS 6.20 and later. Mandatory for miniport drivers.</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## See also


[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_PM\_WOL\_PATTERN**](https://msdn.microsoft.com/library/windows/hardware/ff566768)

[**NDIS\_STATUS\_INDICATION**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_STATUS\_PM\_WOL\_PATTERN\_REJECTED**](https://msdn.microsoft.com/library/windows/hardware/ff567414)

[OID\_PM\_REMOVE\_WOL\_PATTERN](oid-pm-remove-wol-pattern.md)

[OID\_PNP\_ADD\_WAKE\_UP\_PATTERN](oid-pnp-add-wake-up-pattern.md)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20OID_PM_ADD_WOL_PATTERN%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


