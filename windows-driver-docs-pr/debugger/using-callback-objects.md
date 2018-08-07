---
title: Using Callback Objects
description: Using Callback Objects
ms.assetid: 9090a465-b6ab-4e99-8155-b0abdb729468
keywords: ["Debugger Engine API, callback objects", "callback objects", "callback objects, event callbacks", "event callbacks", "callback objects, input callbacks", "input callbacks", "callback objects, output callbacks", "output callbacks"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Using Callback Objects


There are three callback COM like interfaces that are used by the engine: [IDebugEventCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550550) for notifying [debugger extensions](debugger-extensions.md) and applications of changes to the engine or target, [IDebugInputCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550785) for requesting input, and [IDebugOutputCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550801) for sending output.

Callback objects are registered with clients. At most, one instance of each of the three callback interfaces can be registered with each client (the Unicode and ASCII versions of a interface count as the same interface).

When a client is created, the engine remembers the thread in which it was created. The engine uses this same thread whenever it makes a call to a callback instance registered with the client. If the thread is in use, the engine will queue the calls it needs to make. To allow the engine to make these calls, the method [*DispatchCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff541970) should be called whenever a client's thread is idle. The method [**ExitDispatch**](https://msdn.microsoft.com/library/windows/hardware/ff543265) will cause *DispatchCallbacks* to return. If the thread is the same thread that was used to start the debugger session, then the engine can make the callback calls during the [**WaitForEvent**](https://msdn.microsoft.com/library/windows/hardware/ff561229) method, and *DispatchCallbacks* does not need to be called.

The method [**FlushCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff545475) tells the engine to send all buffered output to the output callbacks.

### <span id="event_callbacks"></span><span id="EVENT_CALLBACKS"></span>Event Callback Objects

The [IDebugEventCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550550) interface is used by the engine to notify the debugger extensions and applications of [events](events.md#events) and changes to the engine and target. An implementation of **IDebugEventCallbacks** can be registered with a client using [*SetEventCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff556671). The current implementation registered with a client can be found using [*GetEventCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff546601). The number of event callbacks registered across all clients can be found using [*GetNumberEventCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff547896).

For details on how the engine manages events, see [Monitoring Events](monitoring-events.md).

### <span id="input_callbacks"></span><span id="INPUT_CALLBACKS"></span>Input Callback Objects

The [IDebugInputCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550785) interface is used by the engine to request input from debugger extensions and applications. An implementation of **IDebugInputCallbacks** can be registered with a client using [*SetInputCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff556721). The current implementation registered with a client can be found using [*GetInputCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff546892). The number of input callbacks registered across all clients can be found using [*GetNumberInputCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff547923).

For details on how the engine manages input, see [Input and Output](using-input-and-output.md).

### <span id="output_callbacks"></span><span id="OUTPUT_CALLBACKS"></span>Output Callback Objects

The **IDebugOutputCallbacks** interface is used by the engine to send output to the debugger extensions and applications. An implementation of **IDebugOutputCallbacks** can be registered with a client using [*SetOutputCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff556751). The current implementation registered with a client can be found using [*GetOutputCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff548071). The number of output callbacks registered across all clients can be found using [*GetNumberOutputCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff547931).

For details on how the engine manages output, see [Input and Output](using-input-and-output.md).

**Note**   As is typical for COM objects, the engine will call **IUnknown::AddRef** on a callback COM object when it is registered with a client, and **IUnknown::Release** when the object is replaced or the client is deleted.

 

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Using%20Callback%20Objects%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




