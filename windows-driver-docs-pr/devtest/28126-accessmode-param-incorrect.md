---
title: C28126
description: Warning C28126 The AccessMode parameter to ObReferenceObject* should be IRP->RequestorMode.
ms.assetid: be8f909e-2d4a-4e22-b457-81a048d90df8
keywords:
- warnings listed WDK PREfast for Drivers
- errors listed WDK PREfast for Drivers
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# C28126


warning C28126: The AccessMode parameter to ObReferenceObject\* should be IRP-&gt;RequestorMode

In a call to [**ObReferenceObjectByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff558679) or [**ObReferenceObjectByPointer**](https://msdn.microsoft.com/library/windows/hardware/ff558686), the driver is passing **UserMode** or **KernelMode** for the *AccessMode* parameter, instead of using **Irp-&gt;RequestorMode**.

The driver should use **Irp-&gt;RequestorMode**, rather than specifying **UserMode** or **KernelMode**. This allows the senders of kernel-mode IRP to supply kernel-mode handles safely.

This warning is intended for the top-level driver in the driver stack. You can ignore or suppress this warning for all other drivers.

The top-level driver in the driver stack should use **Irp-&gt;RequestorMode**, rather than specifying **UserMode** or **KernelMode**. This allows the senders of kernel-mode IRP to supply kernel-mode handles safely. All other drivers in the stack should specify **KernelMode**, which skips the access check and leaves responsibility for the access check to the top-level driver.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[devtest\devtest]:%20C28126%20%20RELEASE:%20%2811/17/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




