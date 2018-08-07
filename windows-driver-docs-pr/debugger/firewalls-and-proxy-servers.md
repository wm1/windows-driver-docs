---
title: Firewalls and Proxy Servers
description: Firewalls and Proxy Servers
ms.assetid: 6b438602-299e-4cc5-ac75-ac9ee3cb50bb
keywords: ["SymSrv, firewalls and proxy servers", "firewalls and SymSrv", "internet firewalls and SymSrv", "proxy servers and SymSrv"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Firewalls and Proxy Servers


## <span id="ddk_firewalls_and_proxy_servers_dbg"></span><span id="DDK_FIREWALLS_AND_PROXY_SERVERS_DBG"></span>


If you are using SymSrv to access symbols, and your computer is on a network that uses a proxy server or the symbol store is outside your firewall, authentication may be required for data transmission to take place.

When SymSrv receives authentication requests, the debugger can either display the authentication request or automatically refuse the request, depending on how it has been configured.

SymSrv has integrated support for a proxy server. It can either use the default proxy server, [SymProxy](symproxy.md), or it can use another proxy server of your choice.

### <span id="authentication_requests"></span><span id="AUTHENTICATION_REQUESTS"></span>Authentication Requests

The debugger can be configured to allow authentication requests. When a firewall or proxy server requests authorization, a dialog box will appear. You will have to enter some sort of information (usually a user name and password) before the debugger can download symbols. If you enter incorrect information, the dialog box will be redisplayed. If you select the **Cancel** button, the dialog box will vanish and no symbol information will be transferred.

If the debugger is configured to refuse all authentication requests, no dialog box will appear, and no symbols will be transferred if authentication is required.

If you refuse an authentication request, or if the debugger automatically refuses an authentication request, SymSrv will make no further attempts to contact the symbol store. If you wish to renew contact, you must either restart the debugging session or use [**!symsrv close**](-symsrv.md).

**Note**   If you are using KD or CDB, the authentication dialog box may appear behind an open window. If this occurs, you may have to move or minimize some windows in order to find this dialog box.

 

In WinDbg, authentication requests are allowed by default. In KD and CDB, authentication requests are automatically refused by default.

To allow authentication requests, use either [**!sym prompts**](-sym.md) or [**.symopt-0x80000**](-symopt--set-symbol-options-.md). To refuse all requests, use either **!sym prompts off** or **.symopt+0x80000**. To display the current setting, use **!sym**.

You must use [**.reload (Reload Module)**](-reload--reload-module-.md) after making any changes to the authentication permission status.

### <span id="choosing_a_proxy_server"></span><span id="CHOOSING_A_PROXY_SERVER"></span>Choosing a Proxy Server

To select a default proxy server for Windows, open **Internet Options** in Control Panel, select the **Connections** tab, and then select the **LAN Settings** button. You can then enter the proxy server name and port number, or select **Advanced** to configure multiple proxy servers. For more details, see Internet Explorer's help file.

To select a specific proxy server for symsrv to use, set the \_NT\_SYMBOL\_PROXY environment variable equal to the name or IP of the proxy server, followed by a colon and then the port number. For example:

```
set _NT_SYMBOL_PROXY=myproxyserver:80
```

When a proxy server is chosen in this way, it will be used by any Windows debugger that is using SymSrv to access a symbol server. It will also be used by any other debugging tool that uses DbgHelp as its symbol handler. No other programs will be affected by this setting.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Firewalls%20and%20Proxy%20Servers%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




