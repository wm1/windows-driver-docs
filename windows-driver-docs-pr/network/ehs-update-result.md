---
title: eHS\_UPDATE\_RESULT enumeration
author: windows-driver-content
description: The eHS\_UPDATE\_RESULT enumeration indicates the result of a “check for updates” request.
ms.assetid: 7b9b8ddc-3101-466a-9640-b936f6d14de4
keywords: 
- eHS_UPDATE_RESULT enumeration Network Drivers Starting with Windows Vista
ms.author: windowsdriverdev
ms.date: 07/31/2017 
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# eHS\_UPDATE\_RESULT enumeration


The **eHS\_UPDATE\_RESULT** enumeration indicates the result of a “check for updates” request.

Syntax
------

```ManagedCPlusPlus
typedef enum _eHS_UPDATE_RESULT { 
  HS_UPDATE_RESULT_SUCCESS,
  HS_UPDATE_RESULT_ACTION_RECONNECT,
  HS_UPDATE_RESULT_ACTION_RELOAD,
  HS_UPDATE_RESULT_MAX
} eHS_UPDATE_RESULT;
```

Constants
---------

<a href="" id="hs-update-result-success"></a>**HS\_UPDATE\_RESULT\_SUCCESS**  
Indicates the update was successful.

<a href="" id="hs-update-result-action-reconnect"></a>**HS\_UPDATE\_RESULT\_ACTION\_RECONNECT**  
The result of the update request requires the service to disconnect and reconnect.

<a href="" id="hs-update-result-action-reload"></a>**HS\_UPDATE\_RESULT\_ACTION\_RELOAD**  
The result of the update request requires the service to unload and reload the plugin.

<a href="" id="hs-update-result-max"></a>**HS\_UPDATE\_RESULT\_MAX**  
Indicates an out-of-range value.

Remarks
-------

The plugin passes this enumeration value to the hotspot plugin host through the [**HS\_HOST\_UPDATE\_CONFIGURATION\_COMPLETION**](hs-host-update-configuration-completion.md) function, which is used to inform the hotspot plugin host of the results of a call to [**HS\_PLUGIN\_CHECK\_FOR\_UPDATES**](hs-plugin-check-for-updates.md).

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
<td><p>Windows 10 Mobile</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin.h (include Hotspotoffloadplugin.h)</td>
</tr>
</tbody>
</table>

## See also


[**HS\_HOST\_UPDATE\_CONFIGURATION\_COMPLETION**](hs-host-update-configuration-completion.md)

[**HS\_PLUGIN\_CHECK\_FOR\_UPDATES**](hs-plugin-check-for-updates.md)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20eHS_UPDATE_RESULT%20enumeration%20%20RELEASE:%20%287/31/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


