---
title: OID\_SWITCH\_PORT\_PROPERTY\_ENUM
author: windows-driver-content
description: The Hyper-V extensible switch extension issues an object identifier (OID) method request of OID\_SWITCH\_PORT\_PROPERTY\_ENUM to obtain an array.
ms.assetid: 5C391B82-FCA6-4A95-992F-EDB5DF6183C7
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -OID_SWITCH_PORT_PROPERTY_ENUM Network Drivers Starting with Windows Vista
---

# OID\_SWITCH\_PORT\_PROPERTY\_ENUM


The Hyper-V extensible switch extension issues an object identifier (OID) method request of OID\_SWITCH\_PORT\_PROPERTY\_ENUM to obtain an array. This array contains the provisioned port policies that match the specified criteria. Each element in the array specifies the properties of a policy for a specified extensible switch port.

The **InformationBuffer** member of the [**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710) structure contains a pointer to a buffer. This buffer contains the following data:

-   An [**NDIS\_SWITCH\_PORT\_PROPERTY\_ENUM\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh598236) structure that specifies the parameters for the policy enumeration of a specified port.

-   An array of [**NDIS\_SWITCH\_PORT\_PROPERTY\_ENUM\_INFO**](https://msdn.microsoft.com/library/windows/hardware/hh598233) structures. Each of these structures contains information about the properties of an extensible switch port policy.

    **Note**  If the **NumProperties** member of the [**NDIS\_SWITCH\_PORT\_PROPERTY\_ENUM\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh598236) structure is set to zero, no [**NDIS\_SWITCH\_PORT\_PROPERTY\_ENUM\_INFO**](https://msdn.microsoft.com/library/windows/hardware/hh598233) structures are returned.

     

Remarks
-------

Before it issues an OID method request of OID\_SWITCH\_PORT\_PROPERTY\_ENUM, the extensible switch extension must follow these guidelines:

-   The extension can only issue the OID\_SWITCH\_PORT\_PROPERTY\_ENUM request after the protocol edge of the extensible switch issues an [OID\_SWITCH\_PORT\_CREATE](oid-switch-port-create.md) request and before it issues an [OID\_SWITCH\_PORT\_TEARDOWN](oid-switch-port-teardown.md) request.

-   The extension must call [*ReferenceSwitchPort*](https://msdn.microsoft.com/library/windows/hardware/hh598295) before it calls [**NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830) to issue the OID\_SWITCH\_PORT\_PROPERTY\_ENUM request. This ensures that the specified port will not be deleted until after the OID request is completed.

    After the OID request is completed, the extension must call [*DereferenceSwitchPort*](https://msdn.microsoft.com/library/windows/hardware/hh598142). The extension must call this function regardless of whether the OID request was completed with NDIS\_STATUS\_SUCCESS.

The OID\_SWITCH\_PORT\_PROPERTY\_ENUM OID must only be issued when the Hyper-V extensible switch has completed activation. Please see [Querying the Hyper-V Extensible Switch Configuration](https://msdn.microsoft.com/library/windows/hardware/hh598293) for more details.

**Note**  If the extension receives the OID method request of OID\_SWITCH\_PORT\_PROPERTY\_ENUM, it must not complete the OID request. Instead, it must call [**NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830) to forward the OID request down the extensible switch driver stack.

 

### Return Status Codes

The underlying miniport edge of the extensible switch completes the OID query request of OID\_SWITCH\_PORT\_PROPERTY\_ENUM and returns the following status code.

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
[*DereferenceSwitchPort*](https://msdn.microsoft.com/library/windows/hardware/hh598142)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SWITCH\_PORT\_PROPERTY\_ENUM\_INFO**](https://msdn.microsoft.com/library/windows/hardware/hh598233)

[**NDIS\_SWITCH\_PORT\_PROPERTY\_ENUM\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh598236)

[**NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)

[Querying the Hyper-V Extensible Switch Configuration](https://msdn.microsoft.com/library/windows/hardware/hh598293)

[*ReferenceSwitchPort*](https://msdn.microsoft.com/library/windows/hardware/hh598295)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20OID_SWITCH_PORT_PROPERTY_ENUM%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


