---
title: OID\_SRIOV\_PROBED\_BARS
author: windows-driver-content
description: NDIS issues an object identifier (OID) query request of OID\_SRIOV\_PROBED\_BARS to obtain the values of a network adapter's PCI Express (PCIe) Base Address Registers (BARs).
ms.assetid: 81C3A5B5-58D5-41F4-A000-79F3F4E00DAD
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -OID_SRIOV_PROBED_BARS Network Drivers Starting with Windows Vista
---

# OID\_SRIOV\_PROBED\_BARS


NDIS issues an object identifier (OID) query request of OID\_SRIOV\_PROBED\_BARS to obtain the values of a network adapter's PCI Express (PCIe) Base Address Registers (BARs). This function returns the BAR values that were reported by the network adapter following a query performed by the PCI bus driver. This query determines the memory or I/O address space that is required by the network adapter.

NDIS issues OID query requests of OID\_SRIOV\_PROBED\_BARS to the miniport driver for the network adapter's PCIe Physical Function (PF). This OID query request is required for PF miniport drivers that support the single root I/O virtualization (SR-IOV) interface.

The **InformationBuffer** member of the [**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710) structure contains a pointer to a buffer. This buffer is formatted to contain the following:

-   An [**NDIS\_SRIOV\_PROBED\_BARS\_INFO**](https://msdn.microsoft.com/library/windows/hardware/hh451679) structure that contains the parameters for a read operation on the PCI BARs of a network adapter.

-   An array of ULONG values for each BAR of the PCIe network adapter. The maximum number of elements within this array is PCI\_TYPE0\_ADDRESSES.

Remarks
-------

The PCI bus driver, which runs in the management operating system of the Hyper-V parent partition, queries the memory or I/O address space requirements of each PCI Base Address Register (BAR) of the network adapter. The PCI bus driver performs this query when it first detects the adapter on the bus.

Through this PCI BAR query, the PCI bus driver determines the following:

-   Whether a PCI BAR is supported by the network adapter.

-   If a BAR is supported, how much memory or I/O address space is required for the BAR.

The virtual PCI (VPCI) bus driver runs in the guest operating system of a Hyper-V child partition. When a PCI Express (PCIe) Virtual Function (VF) is attached to the child partition, the VPCI bus driver will expose a virtual network adapter for the VF (*VF network adapter*). Before it does this, the VPCI bus driver must perform a PCI BAR query to determine the required memory or address space that is required by the VF network adapter.

Because access to the PCI configuration space is a privileged operation, it can only be performed by components that run in the management operating system of a Hyper-V parent partition. When the VPCI bus driver queries the PCI BARs, NDIS issues an OID query request of OID\_SRIOV\_PROBED\_BARS to the PF miniport driver. The results returned by this OID query request are forwarded to the VPCI bus driver so that it can determine how much memory address space would be needed by the VF network adapter.

**Note**  OID requests of OID\_SRIOV\_PROBED\_BARS can only be issued by NDIS. The OID request must not be issued by overlying drivers, such as protocol of filter drivers.

 

The OID\_SRIOV\_PROBED\_BARS query request contains an [**NDIS\_SRIOV\_PROBED\_BARS\_INFO**](https://msdn.microsoft.com/library/windows/hardware/hh451679) structure. When the PF miniport driver handles this OID, the driver must return the PCI BAR values within the array referenced by the **BaseRegisterValuesOffset** member of the **NDIS\_SRIOV\_PROBED\_BARS\_INFO** structure. For each offset within the array, the PF miniport driver must set the array element to the ULONG value of the BAR at the same offset within the physical adapter's PCI configuration space.

Each BAR value returned by the driver must be the same value that would follow a PCI BAR query as performed by the PCI driver that runs in the management operating system. The PF miniport driver can call [**NdisMQueryProbedBars**](https://msdn.microsoft.com/library/windows/hardware/hh451520) to determine this information.

For more information about the BARs of a PCI device, see the *PCI Local Bus Specification*.

For more information on how to query PCI BAR registers for a VF, see the [Querying the PCI Base Address Registers of a Virtual Function](https://msdn.microsoft.com/library/windows/hardware/hh440182).

### Return Status Codes

The PF miniport driver returns one of the following status codes for the query request of OID\_SRIOV\_PROBED\_BARS:

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
<td><p>The PF miniport driver either does not support the single root I/O virtualization (SR-IOV) interface or is not enabled to use the interface.</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>One or more of the members of the [<strong>NDIS_SRIOV_PROBED_BARS_INFO</strong>](https://msdn.microsoft.com/library/windows/hardware/hh451679) structure have invalid values.</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>The information buffer is less than (sizeof([<strong>NDIS_SRIOV_PROBED_BARS_INFO</strong>](https://msdn.microsoft.com/library/windows/hardware/hh451679)) + PCI_TYPE0_ADDRESSES). The PF miniport driver must set the <strong>DATA.QUERY_INFORMATION.BytesNeeded</strong> member in the [<strong>NDIS_OID_REQUEST</strong>](https://msdn.microsoft.com/library/windows/hardware/ff566710) structure to the minimum buffer size that is required.</p></td>
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

[**NDIS\_SRIOV\_PROBED\_BARS\_INFO**](https://msdn.microsoft.com/library/windows/hardware/hh451679)

[**NdisMQueryProbedBars**](https://msdn.microsoft.com/library/windows/hardware/hh451520)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20OID_SRIOV_PROBED_BARS%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


