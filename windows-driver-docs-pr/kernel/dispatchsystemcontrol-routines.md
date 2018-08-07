---
title: DispatchSystemControl Routines
author: windows-driver-content
description: DispatchSystemControl Routines
ms.assetid: b885a4a3-a9b6-423c-83bb-ee502724b0d0
keywords: ["dispatch routines WDK kernel , DispatchSystemControl routine", "system control dispatch routines WDK kernel", "IRP_MJ_SYSTEM_CONTROL I/O function code", "DispatchSystemControl routine"]
ms.author: windowsdriverdev
ms.date: 06/16/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# DispatchSystemControl Routines


## <a href="" id="ddk-dispatchsystemcontrol-routines-kg"></a>


A driver's [*DispatchSystemControl*](https://msdn.microsoft.com/library/windows/hardware/ff543412) routine handles IRPs for the [**IRP\_MJ\_SYSTEM\_CONTROL**](https://msdn.microsoft.com/library/windows/hardware/ff550813) I/O function code.

All drivers must provide a *DispatchSystemControl* routine. The purpose of this routine is to provide support for Windows Management Instrumentation (WMI). Regardless of whether a driver supports WMI, this routine must pass the IRP to the next-lower driver.

To learn how to implement a *DispatchSystemControl* routine, and how to support WMI in general, see [Windows Management Instrumentation](implementing-wmi.md).

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bkernel\kernel%5D:%20DispatchSystemControl%20Routines%20%20RELEASE:%20%286/14/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


