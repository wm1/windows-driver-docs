---
title: OID\_DOT11\_HOPPING\_PATTERN
author: windows-driver-content
description: When queried, the OID\_DOT11\_HOPPING\_PATTERN object identifier (OID) requests that the miniport driver return the list of hopping patterns currently used by the current PHY type on the 802.11 station.
ms.assetid: 6bf0c5e9-f2d6-48ab-9f2e-a4fd742f20f7
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -OID_DOT11_HOPPING_PATTERN Network Drivers Starting with Windows Vista
---

# OID\_DOT11\_HOPPING\_PATTERN


**Important**  The [Native 802.11 Wireless LAN](https://msdn.microsoft.com/library/windows/hardware/ff560690) interface is deprecated in Windows 10 and later. Please use the WLAN Device Driver Interface (WDI) instead. For more information about WDI, see [WLAN Universal Windows driver model](https://msdn.microsoft.com/library/windows/hardware/dn897672).

 

When queried, the OID\_DOT11\_HOPPING\_PATTERN object identifier (OID) requests that the miniport driver return the list of hopping patterns currently used by the current PHY type on the 802.11 station.

**Note**  Support for OID\_DOT11\_HOPPING\_PATTERN is mandatory if the NIC supports the **dot11\_phy\_type\_fhss** PHY type and more than one regulatory domain. For more information about how the miniport driver specifies its list of supported PHY types, see [OID\_DOT11\_SUPPORTED\_PHY\_TYPES](oid-dot11-supported-phy-types.md).

 

The data type for OID\_DOT11\_HOPPING\_PATTERN is the DOT11\_HOPPING\_PATTERN\_ENTRY\_LIST structure.

```ManagedCPlusPlus
    typedef struct _DOT11_HOPPING_PATTERN_ENTRY_LIST {
         ULONG uNumOfEntries;
         ULONG uTotalNumOfEntries;
         DOT11_HOPPING_PATTERN_ENTRY dot11HoppingPatternEntry[1];
    } DOT11_HOPPING_PATTERN_ENTRY_LIST, *PDOT11_HOPPING_PATTERN_ENTRY_LIST;
  
```

This structure includes the following members:

<a href="" id="unumofentries"></a>**uNumOfEntries**  
Number of entries in the **dot11HoppingPatternEntry** array. A zero value for this member indicates an empty list of hopping patterns.

<a href="" id="utotalnumofentries"></a>**uTotalNumOfEntries**  
Maximum number of entries that the **dot11HoppingPatternEntry** array requires.

<a href="" id="dot11hoppingpatternentry"></a>**dot11HoppingPatternEntry**  
The list of hopping patterns.

Each element of the **dot11HoppingPatternEntry** array is formatted as a DOT11\_HOPPING\_PATTERN\_ENTRY structure, which is based on the IEEE 802.11d **dot11HoppingPatternEntry** MIB object:

``` syntax
typedef struct _DOT11_HOPPING_PATTERN_ENTRY {         ULONG uHoppingPatternIndex;
 ULONG
 uRandomTableFieldNumber; } DOT11_HOPPING_PATTERN_ENTRY, *PDOT11_HOPPING_PATTERN_ENTRY;
```

This structure includes the following members:

<a href="" id="uhoppingpatternindex"></a>**uHoppingPatternIndex**  
Identifies this entry in the miniport driver's hopping pattern table.

<a href="" id="urandomtablefieldnumber"></a>**uRandomTableFieldNumber**  
The starting channel number in the subband for the domain that is identified by the IEEE 802.11 **dot11CountryString** management information base (MIB) object. For more information about this MIB object, see [OID\_DOT11\_COUNTRY\_STRING](oid-dot11-country-string.md).

The **dot11HoppingPatternEntry** MIB object is valid for the frequency-hopping spread spectrum (FHSS) PHY type only. If the current PHY type is not set to **dot11\_phy\_type\_fhss**, the miniport driver must fail the query request by returning NDIS\_STATUS\_INVALID\_DATA from its [*MiniportOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559416) function.

When OID\_DOT11\_HOPPING\_PATTERN is queried, the miniport driver must verify that the **InformationBuffer** member of the [*MiniportOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559416) function's *OidRequest* parameter is large enough to return the entire DOT11\_HOPPING\_PATTERN\_ENTRY\_LIST structure, including all entries in the **dot11HoppingPatternEntry** array. The value of the **InformationBufferLength** member of the *OidRequest* parameter determines what the miniport driver must do, for example:

-   If the value of the **InformationBufferLength** member is less than the length, in bytes, of the entire DOT11\_HOPPING\_PATTERN\_ENTRY\_LIST structure, the miniport driver must do the following:

    -   For the *OidRequest* parameter, set the **BytesWritten** member to zero and the **BytesNeeded** member to the length, in bytes, of the entire DOT11\_HOPPING\_PATTERN\_ENTRY\_LIST structure.

    -   Fail the query request by returning NDIS\_STATUS\_BUFFER\_OVERFLOW from its [*MiniportOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559416) function.

-   If the value of the **InformationBufferLength** member is greater than or equal to the length, in bytes, of the entire DOT11\_HOPPING\_PATTERN\_ENTRY\_LIST structure, the miniport driver must do the following to complete a successful query request:

    -   For the DOT11\_HOPPING\_PATTERN\_ENTRY\_LIST structure, set the **uNumOfEntries** and **uTotalNumOfEntries** members to the total number of entries in the **dot11HoppingPatternEntry** array.

    -   For the *OidRequest* parameter, set the **BytesNeeded** member to zero and the **BytesWritten** member to the length, in bytes, of the entire DOT11\_HOPPING\_PATTERN\_ENTRY\_LIST structure. The miniport driver must also copy the entire DOT11\_RECV\_SENSITIVITY\_LIST structure to the **InformationBuffer** member and the entire DOT11\_HOPPING\_PATTERN\_ENTRY\_LIST structure to the **InformationBuffer** member.

    -   Return NDIS\_STATUS\_SUCCESS from its [*MiniportOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559416) function.

If the miniport driver is operating in Extensible Station (ExtSTA) mode, the current PHY type is determined through the ExtSTA **msDot11CurrentPhyID** MIB object. This MIB object specifies the index of the current PHY type within the 802.11 station's list of supported PHY types. For more information about **msDot11CurrentPhyID**, see [OID\_DOT11\_CURRENT\_PHY\_ID](oid-dot11-current-phy-id.md).

**Note**  A Native 802.11 miniport driver that is designed to run on the Windows Vista or Windows Server 2008 operating systems must always reset this 802.11 MIB OID to its default value. This is the case regardless of the value of the **bSetDefaultMIB** member of the DOT11\_RESET\_REQUEST structure. This requirement applies to a miniport driver that, in a call to the **NdisMSetMiniportAttributes** function, sets **MiniportAttributes** -&gt; **Native\_802\_11\_Attributes** -&gt; **Header** -&gt; **Revision** to NDIS\_MINIPORT\_ADAPTER\_802\_11\_ATTRIBUTES\_REVISION\_1.

 

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
<td><p>Available in Windows Vista and later versions of the Windows operating systems.</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Windot11.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## See also


[Native 802.11 MIB OIDs](https://msdn.microsoft.com/library/windows/hardware/ff560645)

[Native 802.11 Wireless LAN OIDs](https://msdn.microsoft.com/library/windows/hardware/ff560691)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20OID_DOT11_HOPPING_PATTERN%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


