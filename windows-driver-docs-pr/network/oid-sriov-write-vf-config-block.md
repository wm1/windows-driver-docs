---
title: OID\_SRIOV\_WRITE\_VF\_CONFIG\_BLOCK
author: windows-driver-content
description: An overlying driver issues an object identifier (OID) set request of OID\_SRIOV\_WRITE\_VF\_CONFIG\_BLOCK to write data to a PCI Express (PCIe) Virtual Function (VF) configuration block.
ms.assetid: 60527938-5627-482D-B94D-522DA8E32540
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -OID_SRIOV_WRITE_VF_CONFIG_BLOCK Network Drivers Starting with Windows Vista
---

# OID\_SRIOV\_WRITE\_VF\_CONFIG\_BLOCK


An overlying driver issues an object identifier (OID) set request of OID\_SRIOV\_WRITE\_VF\_CONFIG\_BLOCK to write data to a PCI Express (PCIe) Virtual Function (VF) configuration block.

Overlying drivers issue this OID set request to the miniport driver for the network adapter's PCIe Physical Function (PF). This OID method request is required for PF miniport drivers that support the single root I/O virtualization (SR-IOV) interface.

The **InformationBuffer** member of the [**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710) structure contains a pointer to a caller-allocated buffer. This buffer is formatted to contain the following:

-   An [**NDIS\_SRIOV\_WRITE\_VF\_CONFIG\_BLOCK\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451687) structure that contains the offset, in units of bytes, from the beginning of this structure to a location within the buffer that contains the data that is written to the VF configuration block.

-   Additional buffer space for the data to be written to the specified VF configuration block.

Remarks
-------

A VF configuration block is used for backchannel communication between the PF and VF miniport drivers. The IHV can define one or more VF configuration blocks for the miniport drivers. Each VF configuration block has an IHV-defined format, length, and block ID.

**Note**  Data from each VF configuration block is used only by the PF and VF miniport drivers.

 

Before it issues the OID set request of OID\_SRIOV\_WRITE\_VF\_CONFIG\_BLOCK, the overlying driver must set the members of [**NDIS\_SRIOV\_WRITE\_VF\_CONFIG\_BLOCK\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451687) structure in the following way:

-   Set the **VFId** member to the identifier of the VF for which the information is to be written.

-   Set the **BlockId** member to the identifier of the configuration block from which the information is to be written.

-   Set the **Length** member to the number of bytes to write to the VF configuration block.

-   Set the **BufferOffset** member to the offset within the buffer (referenced by **InformationBuffer** member) that contains the data that is to be written from the specified VF configuration block. This offset is specified in units of bytes from the beginning of the [**NDIS\_SRIOV\_WRITE\_VF\_CONFIG\_BLOCK\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451687) structure.

When it handles the OID set request of OID\_SRIOV\_WRITE\_VF\_CONFIG\_BLOCK, the PF miniport driver must follow these guidelines:

-   The PF miniport driver must verify that the VF, specified by the **VFId** member of the [**NDIS\_SRIOV\_WRITE\_VF\_CONFIG\_BLOCK\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451687) structure, has resources that have been previously allocated. The PF miniport driver allocates resources for a VF during an OID method request of [OID\_NIC\_SWITCH\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md). If resources for the specified VF have not been allocated, the driver must fail the OID request.

-   The PF miniport driver must verify that the **BlockId** member of the [**NDIS\_SRIOV\_WRITE\_VF\_CONFIG\_BLOCK\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451687) structure specifies a valid VF configuration block. If not, the driver must fail the OID request.

For more information about backchannel communication within the single root I/O virtualization (SR-IOV) interface, see [SR-IOV PF/VF Backchannel Communication](https://msdn.microsoft.com/library/windows/hardware/hh440251).

### Return Status Codes

The miniport driver returns one of the following status codes for the OID set request of OID\_SRIOV\_WRITE\_VF\_CONFIG\_BLOCK:

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
<td><p>The miniport driver either does not support the single root I/O virtualization (SR-IOV) interface or is not enabled to use the interface.</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>One or more of the members of the [<strong>NDIS_SRIOV_WRITE_VF_CONFIG_BLOCK_PARAMETERS</strong>](https://msdn.microsoft.com/library/windows/hardware/hh451687) structure have invalid values.</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>The information buffer was too short. NDIS sets the <strong>DATA.SET_INFORMATION.BytesNeeded</strong> member in the [<strong>NDIS_OID_REQUEST</strong>](https://msdn.microsoft.com/library/windows/hardware/ff566710) structure to the minimum buffer size that is required.</p></td>
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
[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SRIOV\_WRITE\_VF\_CONFIG\_BLOCK\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451687)

[OID\_NIC\_SWITCH\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[OID\_SRIOV\_READ\_VF\_CONFIG\_SPACE](oid-sriov-read-vf-config-space.md)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20OID_SRIOV_WRITE_VF_CONFIG_BLOCK%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


