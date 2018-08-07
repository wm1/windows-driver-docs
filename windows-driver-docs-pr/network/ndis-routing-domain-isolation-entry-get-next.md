---
title: NDIS\_ROUTING\_DOMAIN\_ISOLATION\_ENTRY\_GET\_NEXT macro
author: windows-driver-content
description: Hyper-V extensible switch extensions use the NDIS\_ROUTING\_DOMAIN\_ISOLATION\_ENTRY\_GET\_NEXT macro to access the next NDIS\_ROUTING\_DOMAIN\_ISOLATION\_ENTRY element that follows an NDIS\_ROUTING\_DOMAIN\_ISOLATION\_ENTRY structure in the array that is specified by an NDIS\_SWITCH\_PORT\_PROPERTY\_ROUTING\_DOMAIN structure.
ms.assetid: DFBBD989-08E5-48A3-9D03-C6F914753131
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -NDIS_ROUTING_DOMAIN_ISOLATION_ENTRY_GET_NEXT macro Network Drivers Starting with Windows Vista
---

# NDIS\_ROUTING\_DOMAIN\_ISOLATION\_ENTRY\_GET\_NEXT macro


Hyper-V extensible switch extensions use the **NDIS\_ROUTING\_DOMAIN\_ISOLATION\_ENTRY\_GET\_NEXT** macro to access the next [**NDIS\_ROUTING\_DOMAIN\_ISOLATION\_ENTRY**](https://msdn.microsoft.com/library/windows/hardware/dn383684) element that follows an **NDIS\_ROUTING\_DOMAIN\_ISOLATION\_ENTRY** structure in the array that is specified by an [**NDIS\_SWITCH\_PORT\_PROPERTY\_ROUTING\_DOMAIN**](https://msdn.microsoft.com/library/windows/hardware/dn383688) structure.

Syntax
------

```ManagedCPlusPlus
PNDIS_ROUTING_DOMAIN_ISOLATION_ENTRY NDIS_ROUTING_DOMAIN_ISOLATION_ENTRY_GET_NEXT(
   PNDIS_ROUTING_DOMAIN_ISOLATION_ENTRY _IsolationInfoEntry_
);
```

Parameters
----------

*\_IsolationInfoEntry\_*   
A pointer to an [**NDIS\_ROUTING\_DOMAIN\_ISOLATION\_ENTRY**](https://msdn.microsoft.com/library/windows/hardware/dn383684) structure.

Return value
------------

The **NDIS\_ROUTING\_DOMAIN\_ISOLATION\_ENTRY\_GET\_NEXT** macro returns a pointer to the next [**NDIS\_ROUTING\_DOMAIN\_ISOLATION\_ENTRY**](https://msdn.microsoft.com/library/windows/hardware/dn383684) element in the array. If the *\_IsolationInfoEntry\_* parameter already points to the last element in the array, the macro returns **NULL**.

Requirements
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Target platform</p></td>
<td>Desktop</td>
</tr>
<tr class="even">
<td><p>Version</p></td>
<td><p>Supported in NDIS 6.40 and later.</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## See also


[**NDIS\_ROUTING\_DOMAIN\_ISOLATION\_ENTRY**](https://msdn.microsoft.com/library/windows/hardware/dn383684)

[**NDIS\_SWITCH\_PORT\_PROPERTY\_ROUTING\_DOMAIN**](https://msdn.microsoft.com/library/windows/hardware/dn383688)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20NDIS_ROUTING_DOMAIN_ISOLATION_ENTRY_GET_NEXT%20macro%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


