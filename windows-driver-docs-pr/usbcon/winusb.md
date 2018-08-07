---
Description: This section describes the generic WinUSB driver (Winusb.sys) and its user-mode component (Winusb.dll) provided by Microsoft for all USB devices.
title: WinUSB (Winusb.sys)
author: windows-driver-content
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# WinUSB (Winusb.sys)


This section describes the generic WinUSB driver (Winusb.sys) and its user-mode component (Winusb.dll) provided by Microsoft for all USB devices.

In versions of Windows earlier than Windows XP with Service Pack 2 (SP2), all USB device drivers were required to operate in kernel mode. If you created a USB device for which the operating system did not have a native class driver, you had to write a kernel-mode device driver for your device.

Windows USB (WinUSB) is a generic driver for USB devices that was developed concurrently with the Windows Driver Frameworks (WDF) for Windows XP with SP2. The WinUSB architecture consists of a kernel-mode driver (Winusb.sys) and a user-mode dynamic link library (Winusb.dll) that exposes [WinUSB functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb). By using these functions, you can manage USB devices with user-mode software.

Winusb.sys is also a key part of the link between a UMDF function driver and the associated device. Winusb.sys is installed in the device's kernel-mode stack as an upper filter driver. An application communicates with the device's UMDF function driver to issue read, write, or device I/O control requests. The driver interacts with the framework, which passes the request to Winusb.sys. Winusb.sys then processes the request and passes it to the protocol drivers and ultimately to the device. Any response returns by the reverse path. Winusb.sys also serves as the device stack's Plug and Play and power owner.

**Note**  WinUSB functions require Windows XP or later. You can use these functions in your C/C++ application to communicate with your USB device. Microsoft does not provide a managed API for WinUSB.

This section describes how to use WinUSB to communicate with your USB devices. The topics in this section provide guidelines about choosing the correct driver for your device, information about installing Winusb.sys as a USB device's function driver, and a detailed walkthrough with code examples that show how applications and USB devices communicate with each other.

This section includes the following topics:

-   [WinUSB Architecture and Modules](winusb-architecture.md)
-   [WinUSB (Winusb.sys) Installation](winusb-installation.md)
-   [WinUSB Device](automatic-installation-of-winusb.md)
-   [How to Access a USB Device by Using WinUSB Functions](using-winusb-api-to-communicate-with-a-usb-device.md)
-   [WinUSB Functions for Pipe Policy Modification](winusb-functions-for-pipe-policy-modification.md)
-   [WinUSB Power Management](winusb-power-management.md)

## Windows Support for WinUSB


The following table summarizes WinUSB support in different versions of Windows.

| Windows Version      | WinUSB support |
|----------------------|----------------|
| Windows 10 and later | Yes²           |
| Windows 7            | Yes¹           |
| Windows Server 2008  | Yes²           |
| Windows Vista        | Yes²           |
| Windows Server 2003  | No             |
| Windows XP           | Yes³           |
| Windows 2000         | No             |

 

**Note**  
Yes¹: All SKUs of this version of Windows support WinUSB on x86-based, x64-based, and Itanium-based systems.

Yes²: All SKUs of this version of Windows support WinUSB on x86-based and x64-based systems.

Yes³: All client SKUs of Windows XP with SP2 service packs support WinUSB. WinUSB is not native to Windows XP; it must be installed with the WinUSB co-installer.

No: WinUSB is not supported in this version of Windows.

 

## USB Features Supported by WinUSB


The following table shows the high-level USB features that are supported by WinUSB in different versions of Windows.

| Feature                                | Windows 8.1 and later | Windows 7/Vista/XP |
|----------------------------------------|-----------------------|--------------------|
| Device I/O control requests            | Supported             | Supported          |
| Isochronous transfers                  | Supported             | Not Supported      |
| Bulk, control, and interrupt transfers | Supported             | Supported          |
| Selective suspend                      | Supported             | Supported          |
| Remote wake                            | Supported             | Supported          |

 

## Related topics
[Microsoft-provided USB drivers](system-supplied-usb-drivers.md)  

--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Busbcon\buses%5D:%20WinUSB%20%28Winusb.sys%29%20%20RELEASE:%20%281/26/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


