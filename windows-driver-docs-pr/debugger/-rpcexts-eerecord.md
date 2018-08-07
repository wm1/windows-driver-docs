---
title: rpcexts.eerecord
description: The rpcexts.eerecord extension displays the contents of an extended error information record.
ms.assetid: 3c861842-d3ac-4c7d-88e3-d00233189b74
keywords: ["rpcexts.eerecord Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- rpcexts.eerecord
api_type:
- NA
---

# !rpcexts.eerecord


The **!rpcexts.eerecord** extension displays the contents of an extended error information record.

```
!rpcexts.eerecord EERecordAddress
```

## <span id="ddk__rpcexts_eerecord_dbg"></span><span id="DDK__RPCEXTS_EERECORD_DBG"></span>Parameters


<span id="_______EERecordAddress______"></span><span id="_______eerecordaddress______"></span><span id="_______EERECORDADDRESS______"></span> *EERecordAddress*   
Specifies the address of the extended error record.

### <span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Unavailable</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP and later</strong></p></td>
<td align="left"><p>Rpcexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>Additional Information

For more information about debugging Microsoft Remote Procedure Call (RPC), see [RPC Debugging](rpc-debugging.md).

Remarks
-------

This extension displays the contents of one extended error information record in the debugger. In most cases, it is easier to use [**!rpcexts.eeinfo**](-rpcexts-eeinfo.md), which displays the whole chain. If the chain is very long and you wish to see only one record, use **!eerecord** instead.

Here is an example:

```
0:001> !rpcexts.eerecord 0xb015f0
Computer Name: (null)
ProcessID: 708 (0x2C4)
System Time is: 3/21/2000 4:3:0:264
Generating component: 8
Status: 14
Detection Location: 311
Flags:
Parameter 0:(Long value) : -30976 (0xFFFF8700)
Parameter 1:(Long value) : 16777343 (0x100007F)
```

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20!rpcexts.eerecord%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




