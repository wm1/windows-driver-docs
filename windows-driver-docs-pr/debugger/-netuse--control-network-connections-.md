---
title: .netuse (Control Network Connections)
description: The .netuse command adds a connection to a network share.
ms.assetid: f27e5ae5-1beb-4d2b-987e-5e91d0742e2d
keywords: [".netuse (Control Network Connections) Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- .netuse (Control Network Connections)
api_type:
- NA
---

# .netuse (Control Network Connections)


The **.netuse** command adds a connection to a network share.

```
.netuse /a "[Local]" "Remote" "[User]" "[Password]" 
```

## <span id="ddk_meta_control_network_connections_dbg"></span><span id="DDK_META_CONTROL_NETWORK_CONNECTIONS_DBG"></span>Parameters


<span id="________a______"></span><span id="________A______"></span> **/a**   
Adds a new connection. You must always use the **/a** switch.

<span id="_______Local______"></span><span id="_______local______"></span><span id="_______LOCAL______"></span> *Local*   
Specifies the drive letter to use for the connection. You must enclose *Local* in quotation marks. If you omit this parameter, you must include an empty pair of quotation marks as the parameter.

<span id="_______Remote______"></span><span id="_______remote______"></span><span id="_______REMOTE______"></span> *Remote*   
Specifies the UNC path of the share that is being connected. You must enclose *Remote* in quotation marks.

<span id="_______User______"></span><span id="_______user______"></span><span id="_______USER______"></span> *User*   
Specifies the user name of an account that is authorized to establish the connection. You must enclose *User* in quotation marks. If you omit this parameter, you must include an empty pair of quotation marks as the parameter.

<span id="_______Password______"></span><span id="_______password______"></span><span id="_______PASSWORD______"></span> *Password*   
Specifies the password that is associated with the *User* account. You must enclose *Password* in quotation marks. If you omit this parameter, you must include an empty pair of quotation marks as the parameter.

### <span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Modes</strong></p></td>
<td align="left"><p>User mode, kernel mode</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Targets</strong></p></td>
<td align="left"><p>Live, crash dump</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Platforms</strong></p></td>
<td align="left"><p>All</p></td>
</tr>
</tbody>
</table>

 

Remarks
-------

The **.netuse** command behaves like the **net use** Microsoft MS-DOS command.

If you use **.netuse** during a remote debugging session, this command affects the debugging server, not the debugging client.

The following example shows this command.

```
0:000> .netuse "m:" "\\myserver\myshare" "" "" 
```

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20.netuse%20%28Control%20Network%20Connections%29%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




