---
title: Remote Targets
description: Remote Targets
ms.assetid: ed7ea3dc-07d1-481c-90e0-7f0b0e77ad42
keywords: ["Debugger Engine API, targets, remote", "Debugger Engine API, debugging servers", "Debugger Engine API, process servers", "Debugger Engine API, kernel connection servers", "Debugger Engine API, smart clients"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Remote Targets


## <span id="ddk_remote_debugging_dbx"></span><span id="DDK_REMOTE_DEBUGGING_DBX"></span>


There are two different forms of remote debugging, depending on which computer (remote client or server) is the host computer. The *host computer* is the computer on which the [debugger engine](introduction.md#debugger-engine) is active. On the other computer, the debugger engine is merely acting as a proxy relaying commands and data to the host engine.

All debugger operations -- such as executing commands and [extensions](introduction.md#extensions), and symbol loading -- are performed by the host engine. A debugger session is also relative to the host engine.

To list the debugging servers and process servers currently running on a computer, use [**OutputServers**](https://msdn.microsoft.com/library/windows/hardware/ff553247).

### <span id="debugging_server_and_debugging_client"></span><span id="DEBUGGING_SERVER_AND_DEBUGGING_CLIENT"></span>Debugging Servers and Debugging Clients

A *debugging server* is an instance of the debugger engine acting as a host and listening for connections from debugging clients. The method [**StartServer**](https://msdn.microsoft.com/library/windows/hardware/ff558813) will tell the debugger engine to start listening for connections from debugging clients.

A *debugging client* is an instance of the debugger engine acting as a proxy, sending debugger commands and I/O to the debugging server. The function [**DebugConnect**](https://msdn.microsoft.com/library/windows/hardware/ff540465) can be used to connect to the debugging server.

The client object returned by **DebugConnect** is not automatically joined to the debugger session on the debugging server. The method [**ConnectSession**](https://msdn.microsoft.com/library/windows/hardware/ff539245) can be used to join the session, synchronizing input and output.

The communication between a debugging server and a debugging client mostly consists of debugger commands and RPC calls sent to the server, and command output sent back to the client.

### <span id="process_server_and_smart_client"></span><span id="PROCESS_SERVER_AND_SMART_CLIENT"></span>Process Servers, Kernel Connection Servers, and Smart Clients

*Process servers* and *kernel connection servers* are both instances of the debugger engine acting as proxies, listening for connections from smart clients, and performing memory, processor, or operating system operations as requested by these remote clients. A *process server* facilitates the debugging of processes that are running on the same computer. A *kernel connection server* facilitates the debugging of a Windows kernel debugging target that is connected to the computer that is running the connection server. A process server can be started using the method [**StartProcessServer**](https://msdn.microsoft.com/library/windows/hardware/ff558810) or the program [DbgSrv](process-servers--user-mode-.md). The method [**WaitForProcessServerEnd**](https://msdn.microsoft.com/library/windows/hardware/ff561230) will wait for a process server started with **StartProcessServer** to end. A kernel connection server can be activated using the program [**KdSrv**](activating-a-kd-connection-server.md).

A *smart client* is an instance of the debugger engine acting as a host engine and connected to a process server. The method [**ConnectProcessServer**](https://msdn.microsoft.com/library/windows/hardware/ff539237) will connect to a process server. Once connected, the methods described in [Live User-Mode Targets](live-user-mode-targets.md) can be used.

When the remote client is finished with the process server, it can disconnect using [**DisconnectProcessServer**](https://msdn.microsoft.com/library/windows/hardware/ff541969), or it can use [**EndProcessServer**](https://msdn.microsoft.com/library/windows/hardware/ff542993) to request that the process server shut down. To shut down the process server from the computer that it is running on, use Task Manager to end the process. If the instance of the debugger engine that used **StartProcessServer** is still running, it can use [**Execute**](https://msdn.microsoft.com/library/windows/hardware/ff543208) to issue the debugger command [**.endsrv 0**](-endsrv--end-debugging-server-.md), which will end the process server (this is an exception to the usual behavior of **.endsrv**, which generally does not affect process servers).

The communication between a process server and a smart client typically consists of low-level memory, processor, and operating system operations and requests that are sent from the remote client to the server. Their results are then sent back to the client.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Remote%20Targets%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




