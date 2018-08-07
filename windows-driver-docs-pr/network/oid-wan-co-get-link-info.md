---
title: OID\_WAN\_CO\_GET\_LINK\_INFO
author: windows-driver-content
description: The OID\_WAN\_CO\_GET\_LINK\_INFO OID requests the miniport driver to return PPP framing information about the current state of a virtual connection (VC). This information is returned in an NDIS\_WAN\_CO\_GET\_LINK\_INFO structure, defined as follows.
ms.assetid: 26582bc4-c32f-4243-a208-9230c62f4d16
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -OID_WAN_CO_GET_LINK_INFO Network Drivers Starting with Windows Vista
---

# OID\_WAN\_CO\_GET\_LINK\_INFO


The OID\_WAN\_CO\_GET\_LINK\_INFO OID requests the miniport driver to return PPP framing information about the current state of a virtual connection (VC). This information is returned in an NDIS\_WAN\_CO\_GET\_LINK\_INFO structure, defined as follows.

```ManagedCPlusPlus
    typedef struct _NDIS_WAN_CO_GET_LINK_INFO {
         OUT ULONG MaxSendFrameSize;
         OUT ULONG MaxRecvFrameSize;
         OUT ULONG SendFramingBits;
         OUT ULONG RecvFramingBits;
         OUT ULONG SendCompressionBits;
         OUT ULONG RecvCompressionBits;
         OUT ULONG SendACCM;
         OUT ULONG RecvACCM;
    } NDIS_WAN_CO_GET_LINK_INFO,   *PNDIS_WAN_CO_GET_LINK_INFO;
  
```

## <a href="" id="ddk-oid-wan-co-get-link-info-nr"></a>


The members of this structure contain the following information:

<a href="" id="maxsendframesize"></a>**MaxSendFrameSize**  
Specifies the maximum buffer size, in bytes, that the miniport driver can accept for transmission on this VC. The miniport driver's *MiniportCoSendPackets* function can reject any incoming send packet that is larger than this size.

<a href="" id="maxrecvframesize"></a>**MaxRecvFrameSize**  
Specifies the largest packet that will be received from the network. The miniport driver can drop any packets that are larger.

<a href="" id="sendframingbits"></a>**SendFramingBits**  
Specifies send-framing bits indicating the type of framing that should be sent. If the miniport driver detects incompatibilities between **SendFramingBits** and **RecvFramingBits**, it returns NDIS\_STATUS\_INVALID\_DATA.

The proper NLPID and framing format should be used based on the framing bits wherever applicable.

<a href="" id="recvframingbits"></a>**RecvFramingBits**  
Specifies receive-framing bits indicating the type of framing that should be received.

<a href="" id="sendcompressionbits"></a>**SendCompressionBits**  
Reserved.

<a href="" id="recvcompressionbits"></a>**RecvCompressionBits**  
Reserved.

<a href="" id="sendaccm"></a>**SendACCM**  
For asynchronous media types, logical bits 0-31 indicate the respective byte to be byte stuffed. That is, if bit 0 is set to 1, then ASCII character 0x00 should be byte stuffed, and so forth.

<a href="" id="recvaccm"></a>**RecvACCM**  
As described for **SendACCM**.

Remarks
-------

Possible values for **SendFramingBits** and **RecvFramingBits** include any the driver returned in response to the OID\_WAN\_CO\_GET\_LINK\_INFO query.

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
<td><p>Supported for NDIS 6.0 and NDIS 5.1 drivers in Windows Vista. Supported for NDIS 5.1 drivers in Windows XP.</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## See also


[OID\_WAN\_CO\_GET\_LINK\_INFO](oid-wan-co-get-link-info.md)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20OID_WAN_CO_GET_LINK_INFO%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


