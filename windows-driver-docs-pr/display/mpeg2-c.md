---
title: MPEG2_C
description: MPEG2_C
ms.assetid: 610ca80d-b29a-4c30-98df-8df8fe825157
keywords:
- MPEG2_C restricted profile WDK DirectX VA
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# MPEG2\_C


## <span id="ddk_mpeg2_c_gg"></span><span id="DDK_MPEG2_C_GG"></span>


The MPEG2\_C restricted profile contains a set of features required for support of MPEG-2 video Main Profile. Support of this profile is required for video accelerator drivers that provide hardware video acceleration capabilities.

Because the MPEG2\_C restricted profile is defined by a relaxation of the accelerator requirements of the [MPEG2\_A](mpeg2-a.md) profile (by allowing an accelerator to not support any of the members of the minimal interoperability set for MPEG2\_A), all accelerators that support the MPEG2\_A profile must support the MPEG2\_C profile. Similarly, all accelerators that support the [MPEG2\_D](mpeg2-d.md) profile must support the MPEG2\_C profile.

The restrictions for MPEC2\_C are defined by the restrictions listed for MPEG2\_A, except for the following additional restrictions.

### <span id="Restrictions_on_DXVA_ConnectMode"></span><span id="restrictions_on_dxva_connectmode"></span><span id="RESTRICTIONS_ON_DXVA_CONNECTMODE"></span>Restrictions on DXVA\_ConnectMode

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Structure Member</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>wRestrictedMode</strong></p></td>
<td align="left"><p>DXVA_RESTRICTED_MODE_MPEG2_C</p></td>
</tr>
</tbody>
</table>

 

### <span id="Restrictions_on_DXVA_ConfigPictureDecode"></span><span id="restrictions_on_dxva_configpicturedecode"></span><span id="RESTRICTIONS_ON_DXVA_CONFIGPICTUREDECODE"></span>Restrictions on DXVA\_ConfigPictureDecode

This profile adds an additional configuration to the [minimal interoperability set](minimal-interoperability-configuration-sets.md) for picture decoding. This additional configuration is defined by the following DXVA\_ConfigPictureDecode members.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Structure Member</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>bConfigResidDiffHost</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfigResidDiffAccelerator</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[display\display]:%20MPEG2_C%20%20%20RELEASE:%20%282/10/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




