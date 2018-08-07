---
title: Setting Breakpoints
description: Setting Breakpoints
ms.assetid: 9715c35a-0c8c-4e89-be28-2899f21ec964
keywords: ["Debugger Engine API, setting breakpoints"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Setting Breakpoints


## <span id="ddk_using_breakpoints_dbx"></span><span id="DDK_USING_BREAKPOINTS_DBX"></span>


Breakpoints are created with the [**AddBreakpoint**](https://msdn.microsoft.com/library/windows/hardware/ff537856) method. This method creates an [IDebugBreakpoint](https://msdn.microsoft.com/library/windows/hardware/ff549812) object that represents the breakpoint. It also set the *breakpoint type* (software breakpoint or processor breakpoint). Once a breakpoint has been created, its type cannot be changed.

Breakpoints are deleted with the [**RemoveBreakpoint**](https://msdn.microsoft.com/library/windows/hardware/ff554487) method. This also deletes the **IDebugBreakpoint** object; this object may not be used again.

**Note**   Although **IDebugBreakpoint** implements the **IUnknown** interface, the methods **IUnknown::AddRef** and **IUnknown::Release** are not used to control the lifetime of the breakpoint. These methods have no effect on the lifetime of the breakpoint. Instead, an **IDebugBreakpoint** object is deleted after the method [**RemoveBreakpoint**](https://msdn.microsoft.com/library/windows/hardware/ff554487) is called.

 

When the breakpoint is created, it is given a unique *breakpoint ID*. This identifier will not change. However, after the breakpoint has been deleted, its ID may be used for another breakpoint. For details on how to receive notification of the removal of a breakpoint, see [Monitoring Events](monitoring-events.md).

When a breakpoint is created, it is initially disabled; this means that it will not cause the target to stop executing. This breakpoint may be enabled by using the method [**AddFlags**](https://msdn.microsoft.com/library/windows/hardware/ff537903) to add the DEBUG\_BREAKPOINT\_ENABLED flag.

When a breakpoint is first created, it has the memory location 0x00000000 associated with it. The location can be changed by using [**SetOffset**](https://msdn.microsoft.com/library/windows/hardware/ff556741) with an address, or by using [**SetOffsetExpression**](https://msdn.microsoft.com/library/windows/hardware/ff556745) with a symbolic expression. The breakpoint's location should be changed from its initial value before it is used.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Setting%20Breakpoints%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




