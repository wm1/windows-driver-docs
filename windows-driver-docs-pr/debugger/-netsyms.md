---
title: .netsyms (Disable Network Symbol Loading)
description: .netsyms (Disable Network Symbol Loading)
ms.assetid: 09347909-47C8-4a4d-8246-C32A1791F46B
---

# .netsyms (Disable Network Symbol Loading)


## <span id="ddk_apc_meta_netsyms_dbg"></span><span id="DDK_APC_META_NETSYMS_DBG"></span>


Use the .netsyms command to allow or disallow loading symbols from a network path.

### <span id="kd_syntax"></span><span id="KD_SYNTAX"></span>Syntax

**.netsyms** *{yes|no}*

### <span id="parameters"></span><span id="PARAMETERS"></span>Parameters

<span id="yes"></span><span id="YES"></span>*yes*  
Enables network symbol loading. This is the default.

<span id="no"></span><span id="NO"></span>*no*  
Disables network symbol loading.

### <span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Modes</strong></p></td>
<td align="left"><p>user mode, kernel mode</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Targets</strong></p></td>
<td align="left"><p>live, crash dump</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Platforms</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <span id="remarks"></span><span id="REMARKS"></span>Remarks

Use .netsyms with no argument to display the current state of this setting.

Use [**!sym noisy**](-sym.md) or the *-n* [**WinDbg Command-Line Option**](windbg-command-line-options.md) to display additional detail as symbols are loaded.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20.netsyms%20%28Disable%20Network%20Symbol%20Loading%29%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




