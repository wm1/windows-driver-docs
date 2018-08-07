---
title: Other Symbol Servers
description: Other Symbol Servers
ms.assetid: 69d88a60-88b6-4118-9f8b-0d7b80bad1ab
keywords: ["symbol servers, writing your own symbol server"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Other Symbol Servers


## <span id="ddk_using_other_symbol_servers_dbg"></span><span id="DDK_USING_OTHER_SYMBOL_SERVERS_DBG"></span>


If you wish to use a different method for your symbol search, you can provide your own symbol server DLL rather than using SymSrv.

### <span id="setting_the_symbol_path"></span><span id="SETTING_THE_SYMBOL_PATH"></span>Setting the Symbol Path

When implementing a symbol server other than SymSrv, the debugger's symbol path is set in the same way as with SymSrv. See [SymSrv](symsrv.md) for an explanation of the symbol path syntax. The only change you need to make is to replace the string **symsrv.dll** with the name of your own symbol server DLL.

If you wish, you are free to use a different syntax within the parameters to indicate the use of different technologies such as UNC paths, SQL database identifiers, or Internet specifications.

### <span id="implementing_your_own_symbol_server"></span><span id="IMPLEMENTING_YOUR_OWN_SYMBOL_SERVER"></span>Implementing Your Own Symbol Server

The central portion of the server is the code that communicates with DbgHelp to find the symbols. Every time DbgHelp requires symbols for a newly loaded module, it calls the symbol server to locate the appropriate symbol files. The symbol server locates each file according to unique parameters such as the time stamp or image size. The server returns a validated path to the requested file. To implement this, the server must export the **SymbolServer** function.

The server should also support the **SymbolServerSetOptions** and **SymbolServerGetOptions** functions. And DbgHelp will call the **SymbolServerClose** function, if it is exported by the server. See [Symbol Server API](symbol-server-api.md) for information about where these routines are documented.

You must not change the actual symbol file name returned by your symbol server. DbgHelp stores the name of a symbol file in multiple locations. Therefore, the server must return a file of the same name as that specified when the symbol was requested. This restriction is needed to assure that the symbol names displayed during symbol loading are the ones that the programmer will recognize.

### <span id="restrictions_on_multiple_symbol_servers"></span><span id="RESTRICTIONS_ON_MULTIPLE_SYMBOL_SERVERS"></span>Restrictions on Multiple Symbol Servers

DbgHelp supports the use of only one symbol server at a time. Your symbol path can contain multiple instances of the same symbol server DLL, but not two different symbol server DLLs. This is not much of a restriction, since you are still free to include multiple instances of a symbol server in your symbol path, each pointing to a different symbol store. But if you want to switch between two different symbol server DLLs, you will have to change the symbol path each time.

### <span id="installing_your_symbol_server"></span><span id="INSTALLING_YOUR_SYMBOL_SERVER"></span>Installing Your Symbol Server

The details of your symbol server installation will depend on your situation. You might wish to set up an installation process that copies your symbol server DLL and sets the \_NT\_SYMBOL\_PATH environment variable automatically.

Depending on the technology used in your server, you may also need to install or access the symbol data itself.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Other%20Symbol%20Servers%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




