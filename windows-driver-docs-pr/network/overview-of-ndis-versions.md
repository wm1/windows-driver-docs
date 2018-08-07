---
title: Overview of NDIS versions
description: Overview of NDIS versions
ms.assetid: 6ecd4040-2831-4238-8080-97edc6a7c3ba
keywords:
- network drivers WDK , NDIS versions
- NDIS WDK , versions in network drivers
- backward compatibility WDK networking
- compatibility WDK networking
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Overview of NDIS versions


## <a href="" id="ddk-ndis-versions-ng"></a>


If you are writing an NDIS driver for more than one version of Microsoft Windows, be sure the features that you are using are supported on each Windows version. New features have been added to NDIS with each release. Other features became obsolete and were removed from later NDIS versions.

This set of design guide documentation is targeted at Windows Vista and later operating systems and NDIS 6.0 and later drivers. Documentation for earlier Windows and NDIS versions is contained in prior releases of the documentation. For the Windows XP and NDIS 5.1 documentation, see [Windows 2000 and Windows XP Networking Design Guide](https://msdn.microsoft.com/library/windows/hardware/ff565849).

> [!NOTE]
> A driver can query the NDIS version by calling the [**NdisReadConfiguration**](https://msdn.microsoft.com/library/windows/hardware/ff564511) function with the *Keyword* parameter set to **NdisVersion**. 

Windows operating system, Microsoft Windows Driver Kit (WDK), and Driver Development Kit (DDK) version support for NDIS versions, as well as support for major NDIS features across NDIS versions, are described in the following table.

| Operating system | Development Kit | Supported NDIS version | CoNDIS | Deserialized driver | Intermediate driver |
| --- | --- | --- | --- | --- | --- |
| Windows 95 | Windows NT 4.0 DDK or Windows 95 DDK | 3.1 |  |  |  |
|  |  | Added support for miniport drivers and Plug and Play. |
| Windows 95 OSR2 | Windows NT 4.0 DDK or Windows 95 DDK | 4.0 |  |  |  |
|  |  | Protocol driver is a vxd-type driver. |
| Windows 98 | Windows NT 4.0 DDK or Windows 98 DDK | 4.1 | X | X | X |
|  |  | Protocol driver is a vxd-type driver. |
| Windows 98 SE | Windows NT 4.0 DDK or Windows 98 DDK | 5.0 | X | X | X |
|  |  | Added support for Power Management and WMI. |
| Windows Me | Windows NT 4.0 DDK or Windows 98 DDK for Vxds | 5.0 | X | X | X |
| Windows NT 3.5 | Windows NT 3.5 DDK | 3.0 |  |  |  |
| Windows NT 4.0 | Windows NT 4.0 DDK | 4.0 |  |  |  |
|  |  | Added these features: <ul><li>[**MiniportSendPackets**](https://msdn.microsoft.com/library/windows/hardware/ff550524)</li><li>[**ProtocolReceivePacket**](https://msdn.microsoft.com/library/windows/hardware/ff563251)</li><li>[**MiniportAllocateComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549352)</li></ul> |
| Windows NT 4.0 SP3 | Windows NT DDK with updated NDIS header and library | 4.1 | X | X | X |
| Windows 2000 | Windows 2000 DDK | 5.0 | X | X | X |
|  |  | Added support for: <ul><li>New INF file format compatible with Windows 95/98/Me</li><li>Plug and Play and Power Management</li><li>WMI</li><li>LBFO</li><li>Scatter/gather DMA support for deserialized miniport drivers</li></ul> |
| Windows XP | See [Download kits for Windows hardware development](http://go.microsoft.com/fwlink/p/?linkid=239721) | 5.1 | X | X | X |
|  |  | Added support for: <ul><li>[**MiniportCancelSendPackets**](https://msdn.microsoft.com/library/windows/hardware/ff549359)</li><li>[**MiniportPnPEventNotify**](https://msdn.microsoft.com/library/windows/hardware/ff550487)</li><li>[**MiniportShutdown**](https://msdn.microsoft.com/library/windows/hardware/ff550533)</li><li>[**NdisCancelSendPackets**](https://msdn.microsoft.com/library/windows/hardware/ff550821)</li><li>[**NdisCopyFromPacketToPacketSafe**](https://msdn.microsoft.com/library/windows/hardware/ff551071)</li><li>[**NdisGeneratePartialCancelId**](https://msdn.microsoft.com/library/windows/hardware/ff562623)</li><li>[**NdisGetFirstBufferFromPacketSafe**](https://msdn.microsoft.com/library/windows/hardware/ff552066)</li><li>[**NdisGetPoolFromPacket**](https://msdn.microsoft.com/library/windows/hardware/ff552090)</li><li>[**NdisGetSharedDataAlignment**](https://msdn.microsoft.com/library/windows/hardware/ff562671)</li><li>[**NdisIMGetCurrentPacketStack**](https://msdn.microsoft.com/library/windows/hardware/ff552155)</li><li>[**NdisIMNotifyPnPEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552203)</li><li>[**NdisQueryPendingIOCount**](https://msdn.microsoft.com/library/windows/hardware/ff554456)</li><li>[**NDIS\_GET\_PACKET\_CANCEL\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff556988)</li><li>[**NDIS\_SET\_PACKET\_CANCEL\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff557195)</li><li>[OID\_GEN\_MACHINE\_NAME](https://msdn.microsoft.com/library/windows/hardware/ff569596)</li><li>New miniport driver attribute flags</li><li>64-bit statistical counters</li><li>Remote NDIS</li><li>Scatter/gather support for both serialized and deserialized miniport drivers</li><li>Packet stacking for intermediate drivers</li><li>VLAN tagging</li><li>Offloading the Processing of UDP-Encapsulated ESP Packets (Windows Server 2003 only)</li><li>Wi-Fi Protected Access (WPA) in Windows XP SP1</li></ul> |
|  |  | Dropped support for: <ul><li>Full Mac drivers</li><li>NDIS 3.0 protocols</li><li>**NdisQueryMapRegisterCount**</li><li>EISA bus</li></ul> |
| Windows Vista | See [Download kits for Windows hardware development](http://go.microsoft.com/fwlink/p/?linkid=239721) | 6.0 | X | X | X |
|  |  | Major improvements in the following provide significant performance gains for both clients and servers: <ul><li>Network data packaging</li><li>Send and receive paths</li><li>Run-time reconfiguration capabilities</li><li>Scatter/gather DMA</li><li>Filter drivers</li><li>Multiprocessor scaling of received data handling</li><li>Offloading TCP tasks to NICs</li></ul> |
|  |  | The following improvements simplify driver development: <ul><li>Streamlined driver initialization</li><li>Versioning support for NDIS interfaces</li><li>Simplified reset handling</li><li>A standard interface for obtaining management information</li><li>A filter driver model to replace filter intermediate drivers</li></ul> |
|  |  | For more information about NDIS 6.0 features, see [Introduction to NDIS 6.0](introduction-to-ndis-6-0.md). |
|  |  | For information about backward compatibility and obsolete features that are not supported in NDIS 6.0 drivers, see [NDIS 6.0 Backward Compatibility](ndis-6-0-backward-compatibility.md). |
| Windows Vista with Service Pack 1 (SP1) and Windows Server 2008 | See [Download kits for Windows hardware development](http://go.microsoft.com/fwlink/p/?linkid=239721). | 6.1 | X | X | X |
|  |  | For information about NDIS 6.1 features, see [Introduction to NDIS 6.1](introduction-to-ndis-6-1.md). |
| Windows 7 and Windows Server 2008 R2 | See [Download kits for Windows hardware development](http://go.microsoft.com/fwlink/p/?linkid=239721). | 6.20 | X | X | X |
|  |  | For information about NDIS 6.20 features, see [Introduction to NDIS 6.20](introduction-to-ndis-6-20.md). |
|  |  | For information about backward compatibility and obsolete features that are not supported in NDIS 6.20 drivers, see [NDIS 6.20 Backward Compatibility](ndis-6-20-backward-compatibility.md). |
| Windows 8 and Windows Server 2012 | See [Download kits for Windows hardware development](http://go.microsoft.com/fwlink/p/?linkid=239721). | 6.30 | X | X | X |
|  |  | For information about NDIS 6.30 features, see [Introduction to NDIS 6.30](introduction-to-ndis-6-30.md). |
| Windows 8.1 and Windows Server 2012 R2 | See [Download kits for Windows hardware development](http://go.microsoft.com/fwlink/p/?linkid=239721). | 6.40 | X | X | X |
|  |  | For information about NDIS 6.40 features, see [Introduction to NDIS 6.40](introduction-to-ndis-6-40.md). |
| Windows 10, version 1507 | See [Download kits for Windows hardware development](http://go.microsoft.com/fwlink/p/?linkid=239721). | 6.50 | X | X | X |
|   |   | For more information about NDIS 6.50 features, see [Introduction to NDIS 6.50](introduction-to-ndis-6-50.md). | 
| Windows 10, version 1511 | See [Download kits for Windows hardware development](http://go.microsoft.com/fwlink/p/?linkid=239721). | 6.51 | X | X | X |
| Windows 10, version 1607 and Windows Server 2016 | See [Download kits for Windows hardware development](http://go.microsoft.com/fwlink/p/?linkid=239721). | 6.60 | X | X | X |
|   |   | For more information about NDIS 6.60 features, see [Introduction to NDIS 6.60](introduction-to-ndis-6-60.md). | 
| Windows 10, version 1703 | See [Download kits for Windows hardware development](http://go.microsoft.com/fwlink/p/?linkid=239721). | 6.70 | X | X | X |
|   |   | NDIS 6.70 coincided with a preview release of the Network Adapter WDF Class Extension, a.k.a. [NetAdapterCx](../netcx/index.md).<p>For more information about NDIS 6.70 features, see [Introduction to NDIS 6.70](introduction-to-ndis-6-70.md).</p> | 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bp_mb\p_mb%5D:%20Planning%20your%20APN%20database%20submission%20%20RELEASE:%20%281/18/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")

