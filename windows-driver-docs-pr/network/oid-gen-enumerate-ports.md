---
title: OID\_GEN\_ENUMERATE\_PORTS
author: windows-driver-content
description: As a query, NDIS and overlying drivers use the OID\_GEN\_ENUMERATE\_PORTS OID to determine the characteristics of the active NDIS ports that are associated with an underlying miniport adapter.
ms.assetid: 42a12a05-e360-4493-b037-d3a63906a132
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -OID_GEN_ENUMERATE_PORTS Network Drivers Starting with Windows Vista
---

# OID\_GEN\_ENUMERATE\_PORTS


As a query, NDIS and overlying drivers use the OID\_GEN\_ENUMERATE\_PORTS OID to determine the characteristics of the active NDIS ports that are associated with an underlying miniport adapter.

**Version Information**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista and later versions of Windows  
Supported.

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 and later miniport drivers  
Not requested. (see Remarks section)

Remarks
-------

NDIS handles this OID and miniport drivers do not receive this OID query.

If the query succeeds, NDIS returns NDIS\_STATUS\_SUCCESS and provides the results of the query in an [**NDIS\_PORT\_ARRAY**](https://msdn.microsoft.com/library/windows/hardware/ff566786) structure. The **NumberOfPorts** member of NDIS\_PORT\_ARRAY contains the number of active ports that are associated with the miniport adapter. The **Ports** member of NDIS\_PORT\_ARRAY contains a list of pointers to [**NDIS\_PORT\_CHARACTERISTICS**](https://msdn.microsoft.com/library/windows/hardware/ff566791) structures. Each NDIS\_PORT\_CHARACTERISTICS structure defines the characteristics of a single NDIDS port.

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


[**NDIS\_PORT\_ARRAY**](https://msdn.microsoft.com/library/windows/hardware/ff566786)

[**NDIS\_PORT\_CHARACTERISTICS**](https://msdn.microsoft.com/library/windows/hardware/ff566791)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20OID_GEN_ENUMERATE_PORTS%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


