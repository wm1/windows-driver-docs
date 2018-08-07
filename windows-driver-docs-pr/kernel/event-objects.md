---
title: Event Objects
author: windows-driver-content
description: Event Objects
ms.assetid: da9df4a2-26cf-4861-80ca-1790ca059e45
keywords: ["kernel dispatcher objects WDK , event objects", "dispatcher objects WDK kernel , event objects", "event objects WDK kernel"]
ms.author: windowsdriverdev
ms.date: 06/16/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Event Objects


## <a href="" id="ddk-event-objects-kg"></a>


A driver can use an event object to wait while the next-lower driver processes an IRP set up by the waiting driver. Drivers that have driver-created threads or driver dispatch routines that wait for the completion of a synchronous I/O request also can use an event object to synchronize operations between their threads and/or other driver routines.

This section contains the following topics:

[Defining and Using an Event Object](defining-and-using-an-event-object.md)

[Standard Event Objects](standard-event-objects.md)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bkernel\kernel%5D:%20Event%20Objects%20%20RELEASE:%20%286/14/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


