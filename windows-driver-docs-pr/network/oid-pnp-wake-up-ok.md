---
title: OID\_PNP\_WAKE\_UP\_OK
author: windows-driver-content
description: OID\_PNP\_WAKE\_UP\_OK
ms.assetid: 93389bfe-11b9-4433-8eca-4446f05d01c0
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -OID_PNP_WAKE_UP_OK Network Drivers Starting with Windows Vista
---

# OID\_PNP\_WAKE\_UP\_OK


## <a href="" id="ddk-oid-pnp-wake-up-ok-nr"></a>


The optional OID\_PNP\_WAKE\_UP\_OK OID indicates the number of valid wake-ups that are signaled by the miniport driver's NIC. A valid wake-up occurs when the NIC wakes up the system in response to a valid pattern match or magic packet.

The data type for this OID is a ULONG value.

An intermediate driver in which the upper edge receives this OID request must always propagate the request to the underlying miniport driver by calling Ndis(Co)Request.

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
<td><p>Supported for NDIS 5.1, and NDIS 6.0 and later.</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20OID_PNP_WAKE_UP_OK%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


