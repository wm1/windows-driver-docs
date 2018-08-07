---
title: NDIS_STATUS_RECEIVE_FILTER_CURRENT_CAPABILITIES
author: windows-driver-content
description: The miniport driver issues an NDIS_STATUS_RECEIVE_FILTER_CURRENT_CAPABILITIES status indication when its currently enabled receive filtering capabilities change.
ms.assetid: 6A1141A3-6E46-4A97-B482-CBE69E3D5075
ms.author: windowsdriverdev 
ms.date: 07/18/2017 
ms.topic: article 
ms.prod: windows-hardware 
ms.technology: windows-devices 
keywords:
 - NDIS_STATUS_RECEIVE_FILTER_CURRENT_CAPABILITIES Network Drivers Starting with Windows Vista
---

# NDIS\_STATUS\_RECEIVE\_FILTER\_CURRENT\_CAPABILITIES


The miniport driver issues an **NDIS\_STATUS\_RECEIVE\_FILTER\_CURRENT\_CAPABILITIES** status indication when its currently enabled receive filtering capabilities change.

**Note**  This status indication should only be made by miniport drivers that support NDIS receive filters.

 

When the miniport driver makes this status indication, it sets the **StatusBuffer** member of the [**NDIS\_STATUS\_INDICATION**](https://msdn.microsoft.com/library/windows/hardware/ff567373) structure to a pointer to an [**NDIS\_RECEIVE\_FILTER\_CAPABILITIES**](https://msdn.microsoft.com/library/windows/hardware/ff566864) structure. The driver initializes this structure with its currently enabled receive filter capabilities.

Remarks
-------

NDIS receive filters are used in the following NDIS interfaces:

-   [NDIS Packet Coalescing](https://msdn.microsoft.com/library/windows/hardware/hh451601). For more information about how to use receive filters in this interface, see [Managing Packet Coalescing Receive Filters](https://msdn.microsoft.com/library/windows/hardware/hh464026).

-   [Single Root I/O Virtualization (SR-IOV)](https://msdn.microsoft.com/library/windows/hardware/hh440235). For more information about how to use receive filters in this interface, see [Setting a Receive Filter on a Virtual Port](https://msdn.microsoft.com/library/windows/hardware/hh440224).

-   [Virtual Machine Queue (VMQ)](https://msdn.microsoft.com/library/windows/hardware/ff571035). For more information about how to use receive filters in this interface, see [Setting and Clearing VMQ Filters](https://msdn.microsoft.com/library/windows/hardware/ff570780).

The miniport driver issues the **NDIS\_STATUS\_RECEIVE\_FILTER\_CURRENT\_CAPABILITIES** status indication when one of the following conditions is true:

-   The currently enabled receive filter capabilities change on a single network adapter. For example, receive filters can be enabled or disabled through a management application developed by the independent hardware vendor (IHV).

-   The currently enabled receive filter capabilities change for one or more network adapters that belong to a load balancing failover (LBFO) team managed by a MUX intermediate driver. For more information, see [NDIS MUX Intermediate Drivers](https://msdn.microsoft.com/library/windows/hardware/ff566498).

The miniport driver follows these steps when it issues the **NDIS\_STATUS\_RECEIVE\_FILTER\_CURRENT\_CAPABILITIES** status indication:

1.  The miniport initializes the [**NDIS\_RECEIVE\_FILTER\_CAPABILITIES**](https://msdn.microsoft.com/library/windows/hardware/ff566864) structure with the receive filter capabilities that are currently enabled on the network adapter.

    When the miniport driver initializes the **Header** member, it sets the **Type** member of **Header** to NDIS\_OBJECT\_TYPE\_DEFAULT. The miniport driver sets the **Revision** member of **Header** to NDIS\_RECEIVE\_FILTER\_CAPABILITIES\_REVISION\_2 and the **Size** member to NDIS\_SIZEOF\_RECEIVE\_FILTER\_CAPABILITIES\_REVISION\_2.

2.  The miniport driver initializes an [**NDIS\_STATUS\_INDICATION**](https://msdn.microsoft.com/library/windows/hardware/ff567373) structure for the status indication in the following way:

    -   The **StatusCode** member must be set to **NDIS\_STATUS\_RECEIVE\_FILTER\_CURRENT\_CAPABILITIES**.

    -   The **StatusBuffer** member must be set to the address of the [**NDIS\_RECEIVE\_FILTER\_CAPABILITIES**](https://msdn.microsoft.com/library/windows/hardware/ff566864) structure.

    -   The **StatusBufferSize** member must be set to `sizeof(NDIS_RECEIVE_FILTER_CAPABILITIES)`.

3.  The miniport driver issues the status indication by calling [**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600). The driver must pass a pointer to the [**NDIS\_STATUS\_INDICATION**](https://msdn.microsoft.com/library/windows/hardware/ff567373) structure to the *StatusIndication* parameter.

**Note**  Overlying drivers can use the **NDIS\_STATUS\_RECEIVE\_FILTER\_CURRENT\_CAPABILITIES** status indication to determine the currently enabled receive filter capabilities of the network adapter. Alternatively, these drivers can also issue OID query requests of [OID\_RECEIVE\_FILTER\_CURRENT\_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff569786) to obtain the currently enabled receive filter capabilities at any time.

 

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
<td><p>Supported in NDIS 6.30 and later.</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## See also


****
[**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)

[**NDIS\_STATUS\_INDICATION**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_RECEIVE\_FILTER\_CAPABILITIES**](https://msdn.microsoft.com/library/windows/hardware/ff566864)

[OID\_RECEIVE\_FILTER\_CURRENT\_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff569786)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20NDIS_STATUS_RECEIVE_FILTER_CURRENT_CAPABILITIES%20%20RELEASE:%20%287/5/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


