---
title: Supporting 32-Bit I/O in Your 64-Bit Driver
author: windows-driver-content
description: Supporting 32-Bit I/O in Your 64-Bit Driver
ms.assetid: c024c74e-0b83-4f86-8370-8269cbf69c9a
keywords: ["32-bit I/O support WDK 64-bit", "64-bit WDK kernel , 32-bit I/O support", "thunking WDK", "WOW64 thunking layer WDK", "converting parameters to fixed-precision types", "32-bit I/O support WDK 64-bit , about 32-bit I/O support in 64-bit", "control codes WDK 64-bit", "I/O control codes WDK kernel , 32-bit I/O in 64-bit drivers", "IOCTLs WDK kernel , 32-bit I/O in 64-bit drivers", "file system control codes WDK 64-bit", "FSCTL WDK 64-bit", "buffer pointers WDK 64-bit"]
ms.author: windowsdriverdev
ms.date: 06/16/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Supporting 32-Bit I/O in Your 64-Bit Driver


## <a href="" id="ddk-supporting-32-bit-i-o-in-your-64-bit-driver-kg"></a>


Windows on Windows (WOW64) enables Microsoft Win32 user-mode applications to run on 64-bit Windows. It does this by intercepting Win32 function calls and converting parameters from pointer-precision types to fixed-precision types as appropriate before making the transition to the 64-bit kernel. This conversion, which is called *thunking*, is done automatically for all Win32 functions, with one important exception: the data buffers passed to [**DeviceIoControl**](https://msdn.microsoft.com/library/windows/desktop/aa363216). The contents of these buffers, which are pointed to by the *InputBuffer* and *OutputBuffer* parameters, are not thunked, because their structure is driver-specific.

**Note**   Although the buffer *contents* are not thunked, the buffer *pointers* are converted into 64-bit pointers.

 

User-mode applications call [**DeviceIoControl**](https://msdn.microsoft.com/library/windows/desktop/aa363216) to send an I/O request directly to a specified kernel-mode driver. This request contains an I/O control code (IOCTL) or file system control code (FSCTL) and pointers to input and output data buffers. The format of these data buffers is specific to the IOCTL or FSCTL, which in turn is defined by the kernel-mode driver. Because the buffer format is arbitrary, and because it is known to the driver and not WOW64, the task of thunking the data is left to the driver.

Your 64-bit driver must support 32-bit I/O if all of the following are true:

-   The driver exposes an IOCTL (or FSCTL) to user-mode applications.

-   At least one of the I/O buffers used by the IOCTL contains pointer-precision data types.

-   Your IOCTL code cannot easily be rewritten to eliminate the use of pointer-precision buffer data types.

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bkernel\kernel%5D:%20Supporting%2032-Bit%20I/O%20in%20Your%2064-Bit%20Driver%20%20RELEASE:%20%286/14/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


