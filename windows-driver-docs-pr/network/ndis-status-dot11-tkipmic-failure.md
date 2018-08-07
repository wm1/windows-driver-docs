---
title: NDIS\_STATUS\_DOT11\_TKIPMIC\_FAILURE
author: windows-driver-content
description: A miniport driver uses the NDIS\_STATUS\_DOT11\_TKIPMIC\_FAILURE indication whenever a received packet, successfully decrypted by the TKIP cipher algorithm, fails the message integrity code (MIC) verification.
ms.assetid: bd1b010f-e5d0-4d51-917f-3a6065c932f6
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -NDIS_STATUS_DOT11_TKIPMIC_FAILURE Network Drivers Starting with Windows Vista
---

# NDIS\_STATUS\_DOT11\_TKIPMIC\_FAILURE


**Important**  The [Native 802.11 Wireless LAN](https://msdn.microsoft.com/library/windows/hardware/ff560690) interface is deprecated in Windows 10 and later. Please use the WLAN Device Driver Interface (WDI) instead. For more information about WDI, see [WLAN Universal Windows driver model](https://msdn.microsoft.com/library/windows/hardware/dn897672).

 

A miniport driver uses the NDIS\_STATUS\_DOT11\_TKIPMIC\_FAILURE indication whenever a received packet, successfully decrypted by the TKIP cipher algorithm, fails the message integrity code (MIC) verification.

The data type for this indication is the DOT11\_TKIPMIC\_FAILURE\_PARAMETERS structure:

```ManagedCPlusPlus
    typedef struct DOT11_TKIPMIC_FAILURE_PARAMETERS {
         NDIS_OBJECT_HEADER Header;
         BOOLEAN bDefaultKeyFailure;
         ULONG uKeyIndex;
         DOT11_MAC_ADDRESS PeerMac;
    } DOT11_TKIPMIC_FAILURE_PARAMETERS,   *PDOT11_TKIPMIC_FAILURE_PARAMETERS;
  
```

The DOT11\_TKIPMIC\_FAILURE\_PARAMETERS structure contains the following members:

<a href="" id="header"></a>**Header**  
The type, revision, and size of the DOT11\_TKIPMIC\_FAILURE\_PARAMETERS structure. This member is formatted as an [**NDIS\_OBJECT\_HEADER**](https://msdn.microsoft.com/library/windows/hardware/ff566588) structure.

The miniport driver must set the members of **Header** to the following values:

<a href="" id="type"></a>**Type**  
This member must be set to NDIS\_OBJECT\_TYPE\_DEFAULT.

<a href="" id="revision"></a>**Revision**  
This member must be set to DOT11\_TKIPMIC\_FAILURE\_PARAMETERS\_REVISION\_1.

<a href="" id="size"></a>**Size**  
This member must be set to sizeof(DOT11\_TKIPMIC\_FAILURE\_PARAMETERS).

For more information about these members, see [**NDIS\_OBJECT\_HEADER**](https://msdn.microsoft.com/library/windows/hardware/ff566588).

<a href="" id="bdefaultkeyfailure"></a>**bDefaultKeyFailure**  
A Boolean value that indicates which cipher key type detected the TKIP-MIC failure occurred. If **TRUE**, the TKIP-MIC failure was detected through a default cipher key. For more information about default cipher keys, see [OID\_DOT11\_CIPHER\_DEFAULT\_KEY](oid-dot11-cipher-default-key.md).

If **FALSE**, the TKIP-MIC failure was detected through a key mapping cipher key. For more information about key mapping cipher keys, see [OID\_DOT11\_CIPHER\_KEY\_MAPPING\_KEY](oid-dot11-cipher-key-mapping-key.md).

<a href="" id="ukeyindex"></a>**uKeyIndex**  
The index of the cipher key in the default key array. The value of **uKeyIndex** must be from 0 through 3.

The **uKeyIndex** member is valid only if the **bDefaultKeyFailure** member is **TRUE**. The miniport driver must set **uKeyIndex** to zero if **bDefaultKeyFailure** is **FALSE**.

<a href="" id="peermac"></a>**PeerMac**  
The media access control (MAC) address of the access point (AP) (for infrastructure BSS networks) or peer station (for independent BSS (IBSS) networks) that transmitted the packet that failed MIC verification. If the NIC is in Extensible Access Point (ExtAP) mode, this member contains the MAC address of the associated peer station that transmitted the packet that failed MIC verification.

The miniport driver calls [**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600) to make an NDIS\_STATUS\_DOT11\_TKIPMIC\_FAILURE indication, and must pass a pointer to an [**NDIS\_STATUS\_INDICATION**](https://msdn.microsoft.com/library/windows/hardware/ff567373) structure through the *StatusIndication* parameter. When making this indication, the driver must set the following members of the NDIS\_STATUS\_INDICATION structure:

-   **StatusCode** must be set to NDIS\_STATUS\_DOT11\_TKIPMIC\_FAILURE.

-   **StatusBuffer** must be set to the address of a DOT11\_TKIPMIC\_FAILURE\_PARAMETERS structure.

-   **StatusBufferSize** must be set to sizeof(DOT11\_TKIPMIC\_FAILURE\_PARAMETERS).

The operating system will consume this indication and determine whether and how TKIP countermeasures are invoked.

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
<td><p>Available in Windows Vista and later versions of the Windows operating systemss.</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Windot11.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20NDIS_STATUS_DOT11_TKIPMIC_FAILURE%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


