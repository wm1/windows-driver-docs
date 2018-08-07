---
title: OID\_NIC\_SWITCH\_CREATE\_SWITCH
author: windows-driver-content
description: NDIS issues an object identifier (OID) method request of OID\_NIC\_SWITCH\_CREATE\_SWITCH to create a NIC switch on a network adapter.
ms.assetid: 16FFC6A4-11A6-45A1-ABCF-8C1EBE3FD953
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -OID_NIC_SWITCH_CREATE_SWITCH Network Drivers Starting with Windows Vista
---

# OID\_NIC\_SWITCH\_CREATE\_SWITCH


NDIS issues an object identifier (OID) method request of OID\_NIC\_SWITCH\_CREATE\_SWITCH to create a NIC switch on a network adapter. When it handles this OID request, the miniport driver allocates the resources for the NIC switch on the adapter.

NDIS issues this OID method request to the miniport driver of the network adapter's PCI Express (PCIe) Physical Function (PF). This OID method request is required for PF miniport drivers that support the single root I/O virtualization (SR-IOV) interface.

**Note**  Overlying drivers, such as protocol or filter drivers, cannot issue OID method requests of OID\_NIC\_SWITCH\_CREATE\_SWITCH to the PF miniport driver.

 

The **InformationBuffer** member of the [**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710) structure contains a pointer to an [**NDIS\_NIC\_SWITCH\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451587) structure.

Remarks
-------

When it receives the OID method request of OID\_NIC\_SWITCH\_CREATE\_SWITCH, the PF miniport driver must do the following:

1.  If the PF miniport driver supports static switch creation and configuration, it creates the NIC switch when NDIS calls [*MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389). When the driver handles this OID request, it must verify the configuration parameters in the [**NDIS\_NIC\_SWITCH\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451587) structure. The parameters must be the same as those used by the driver to create the switch during the call to *MiniportInitializeEx*. If this is not true, the driver must fail the OID request.

    For more information, see [Static Creation of a NIC Switch](https://msdn.microsoft.com/library/windows/hardware/hh440256).

2.  If the PF miniport driver supports dynamic switch creation and configuration, the driver must validate the configuration values of the [**NDIS\_NIC\_SWITCH\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451587) structure and create the NIC switch based on these values.

    For more information, see [Dynamic Creation of a NIC Switch](https://msdn.microsoft.com/library/windows/hardware/hh406694).

3.  The PF miniport driver must allocate the necessary hardware and software resources for the default VPort on the NIC switch.

    **Note**  The default VPort is always created through an OID request of OID\_NIC\_SWITCH\_CREATE\_SWITCH and deleted through an OID request of [OID\_NIC\_SWITCH\_DELETE\_SWITCH](oid-nic-switch-delete-switch.md). OID requests of [OID\_NIC\_SWITCH\_CREATE\_VPORT](oid-nic-switch-create-vport.md) and [OID\_NIC\_SWITCH\_DELETE\_VPORT](oid-nic-switch-delete-vport.md) are used for the creation and deletion of nondefault VPorts on the NIC switch.

     

4.  The PF miniport driver that supports dynamic switch creation and configuration must enable SR-IOV virtualization on the switch by calling [**NdisMEnableVirtualization**](https://msdn.microsoft.com/library/windows/hardware/hh451481). This call configures the **NumVFs** member and the **VF Enable** bit in the SR-IOV Extended Capability structure of the adapter's PCI Express (PCIe) configuration space.

    For more information about the SR-IOV configuration space, see the PCI-SIG [Single Root I/O Virtualization and Sharing 1.1](http://go.microsoft.com/fwlink/p/?linkid=221742) specification.

    **Note**  If the PF miniport driver supports static switch creation, it enables SR-IOV virtualization after it creates the switch when [*MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389) is called.

     

If the PF miniport driver successfully completes the OID method request of OID\_NIC\_SWITCH\_CREATE\_SWITCH, it allows the following to occur:

-   VFs can be allocated on the NIC switch through OID method requests of [OID\_NIC\_SWITCH\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md).

-   Nondefault VPorts can be created on the NIC switch through OID method requests of [OID\_NIC\_SWITCH\_CREATE\_VPORT](oid-nic-switch-create-vport.md).

For more information on how to handle this OID request, see [Handling the OID\_NIC\_SWITCH\_CREATE\_SWITCH Request](https://msdn.microsoft.com/library/windows/hardware/hh451370).

### Return Status Codes

The PF miniport driver returns one of the following status codes for the OID method request of OID\_NIC\_SWITCH\_CREATE\_SWITCH.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Status Code</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>The OID request completed successfully.</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>The PF miniport driver either does not support the SR-IOV interface or is not enabled to use the interface.</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>One or more of the members of the [<strong>NDIS_NIC_SWITCH_PARAMETERS</strong>](https://msdn.microsoft.com/library/windows/hardware/hh451587) structure have invalid values.</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>The length of the information buffer is less than sizeof([<strong>NDIS_NIC_SWITCH_PARAMETERS</strong>](https://msdn.microsoft.com/library/windows/hardware/hh451587)). The PF miniport driver must set the <strong>DATA.METHOD_INFORMATION.BytesNeeded</strong> member in the [<strong>NDIS_OID_REQUEST</strong>](https://msdn.microsoft.com/library/windows/hardware/ff566710) structure to the minimum buffer size that is required.</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>The request failed for other reasons.</p></td>
</tr>
</tbody>
</table>

 

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
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## See also


****
[*MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_NIC\_SWITCH\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451587)

[**NdisMEnableVirtualization**](https://msdn.microsoft.com/library/windows/hardware/hh451481)

[OID\_NIC\_SWITCH\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_SWITCH\_CREATE\_VPORT](oid-nic-switch-create-vport.md)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20OID_NIC_SWITCH_CREATE_SWITCH%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


