---
title: OID\_GEN\_BYTES\_RCV
author: windows-driver-content
description: As a query, NDIS and overlying drivers use the OID\_GEN\_BYTES\_RCV OID to determine the total number of bytes that a miniport adapter received.
ms.assetid: e613e155-e4ff-48e4-8087-20ecad3c4644
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -OID_GEN_BYTES_RCV Network Drivers Starting with Windows Vista
---

# OID\_GEN\_BYTES\_RCV


As a query, NDIS and overlying drivers use the OID\_GEN\_BYTES\_RCV OID to determine the total number of bytes that a miniport adapter received.

**Version Information**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista and later versions of Windows  
Supported.

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 and later miniport drivers  
Not requested. (see Remarks section)

Remarks
-------

NDIS handles this OID for miniport drivers. See the [OID\_GEN\_STATISTICS](oid-gen-statistics.md) OID for more information about statistics.

The total byte count is the sum of the receive-directed byte count, receive-multicast byte count and receive-broadcast byte count. This value is the same as the sum of the values that are returned by the [OID\_GEN\_DIRECTED\_BYTES\_RCV](oid-gen-directed-bytes-rcv.md), [OID\_GEN\_MULTICAST\_BYTES\_RCV](oid-gen-multicast-bytes-rcv.md), and [OID\_GEN\_BROADCAST\_BYTES\_RCV](oid-gen-broadcast-bytes-rcv.md) OIDs.

Requirements
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## See also


[OID\_GEN\_BROADCAST\_BYTES\_RCV](oid-gen-broadcast-bytes-rcv.md)

[OID\_GEN\_DIRECTED\_BYTES\_RCV](oid-gen-directed-bytes-rcv.md)

[OID\_GEN\_MULTICAST\_BYTES\_RCV](oid-gen-multicast-bytes-rcv.md)

[OID\_GEN\_STATISTICS](oid-gen-statistics.md)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20OID_GEN_BYTES_RCV%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


