---
title: OID\_NIC\_SWITCH\_VF\_PARAMETERS
author: windows-driver-content
description: An overlying driver or user-mode application issues an object identifier (OID) method request of OID\_NIC\_SWITCH\_VF\_PARAMETERS to obtain the current configuration parameters of a PCI Express (PCIe) Virtual Function (VF) on a network adapter.
ms.assetid: DF08B0BA-6D86-4C4F-AC38-8A401F097925
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -OID_NIC_SWITCH_VF_PARAMETERS Network Drivers Starting with Windows Vista
---

# OID\_NIC\_SWITCH\_VF\_PARAMETERS


An overlying driver or user-mode application issues an object identifier (OID) method request of OID\_NIC\_SWITCH\_VF\_PARAMETERS to obtain the current configuration parameters of a PCI Express (PCIe) Virtual Function (VF) on a network adapter. Only VFs that have resources allocated through an OID method request of [OID\_NIC\_SWITCH\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md) can be queried through an OID method request of OID\_NIC\_SWITCH\_VF\_PARAMETERS.

NDIS handles the OID method request of OID\_NIC\_SWITCH\_VF\_PARAMETERS for miniport drivers.

When the OID method request is made, the **InformationBuffer** member of the [**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710) structure contains a pointer to an [**NDIS\_NIC\_SWITCH\_VF\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451593) structure.

Remarks
-------

The overlying driver or user-mode application specifies the VF to query by setting the **VFId** member of the [**NDIS\_NIC\_SWITCH\_VF\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451593) structure to the identifier of the VF. The overlying driver or application obtains the VF identifier through one of the following ways:

-   By issuing an OID method request of [OID\_NIC\_SWITCH\_ENUM\_VFS](oid-nic-switch-enum-vfs.md).

    If this OID request is completed successfully, the overlying driver or user-mode application receives a list of all VFs allocated on the network adapter. Each element within the list is an [**NDIS\_NIC\_SWITCH\_VF\_INFO**](https://msdn.microsoft.com/library/windows/hardware/hh451591) structure, with the VF identifier specified by the **VFId** member.

-   By issuing an OID method request of [OID\_NIC\_SWITCH\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md).

    If this OID request is completed successfully, the overlying driver receives the identifier of the newly created VF in the **VFId** member of the returned [**NDIS\_NIC\_SWITCH\_VF\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451593) structure.

    **Note**  Only overlying drivers can obtain the VF identifier in this manner.

     

After a successful return from the OID method request, the **InformationBuffer** member of the [**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710) structure contains a pointer to an [**NDIS\_NIC\_SWITCH\_VF\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451593) structure. This structure contains the configuration parameters for the specified VF.

### Return Status Codes

NDIS handles the OID method request of OID\_NIC\_SWITCH\_VF\_PARAMETERS for miniport drivers, and returns the following status code for OID method requests of OID\_NIC\_SWITCH\_VF\_PARAMETERS.

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
<td><p>The request completed successfully. The <strong>InformationBuffer</strong> member points to an [<strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong>](https://msdn.microsoft.com/library/windows/hardware/hh451593) structure.</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>The miniport driver either does not support the single root I/O virtualization (SR-IOV) interface or is not enabled to use the interface.</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>One or more of the members of the [<strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong>](https://msdn.microsoft.com/library/windows/hardware/hh451593) structure have invalid values.</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>The length of the information buffer is less than sizeof([<strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong>](https://msdn.microsoft.com/library/windows/hardware/hh451593)). NDIS sets the <strong>DATA.METHOD_INFORMATION.BytesNeeded</strong> member in the [<strong>NDIS_OID_REQUEST</strong>](https://msdn.microsoft.com/library/windows/hardware/ff566710) structure to the minimum buffer size that is required.</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>The information buffer was too short. NDIS sets the <strong>DATA.METHOD_INFORMATION.BytesNeeded</strong> member in the [<strong>NDIS_OID_REQUEST</strong>](https://msdn.microsoft.com/library/windows/hardware/ff566710) structure to the minimum buffer size that is required.</p></td>
</tr>
<tr class="even">
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
[**NDIS\_NIC\_SWITCH\_VF\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451593)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[OID\_NIC\_SWITCH\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_SWITCH\_ENUM\_VFS](oid-nic-switch-enum-vfs.md)

[**NDIS\_NIC\_SWITCH\_VF\_INFO**](https://msdn.microsoft.com/library/windows/hardware/hh451591)

[OID\_NIC\_SWITCH\_VF\_PARAMETERS](oid-nic-switch-vf-parameters.md)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20OID_NIC_SWITCH_VF_PARAMETERS%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


