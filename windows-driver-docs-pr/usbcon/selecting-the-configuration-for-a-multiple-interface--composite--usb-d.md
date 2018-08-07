---
Description: This topic provides information about registry settings that configure the way Usbccgp.sys selects a USB configuration.
title: Configuring Usbccgp.sys to Select a Non-Default USB Configuration
author: windows-driver-content
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Configuring Usbccgp.sys to Select a Non-Default USB Configuration


This topic provides information about registry settings that configure the way Usbccgp.sys selects a USB configuration. The topic also describes how Usbccgp.sys handles select-configuration requests sent by a client driver that controls one of functions of a composite device.

## <a href="" id="ddk-selecting-the-configuration-for-a-multiple-interface-composite-usb"></a>


A USB composite device consists of multiple functions (functional devices) within a single USB device. If Windows loads Microsoft-provided [USB Generic Parent Driver](usb-common-class-generic-parent-driver.md) (Usbccgp.sys) for a composite device, from that point forward, Usbccgp.sys is responsible for selecting the configuration of the device. Each interface or interface collection of a composite device is, in many respects, like a separate device that has its own physical device object (PDO). Resetting the configuration of the device changes the configuration for all of the device's interfaces, not just the one that the client driver controls. The operating system does not allow this. Therefore, a client driver that controls a set of interfaces or an interface collection of the composite device cannot change the configuration that is initially set by Usbccgp.sys.

However, in Windows Vista and later versions of Windows, you can add the following registry values to specify the configuration to select:

| Registry Key               | Type       | Value                                                                                                          | Default Value |
|----------------------------|------------|----------------------------------------------------------------------------------------------------------------|---------------|
| OriginalConfigurationValue | REG\_DWORD | USB configuration index. Usbccgp.sys uses OriginalConfigurationValue first for a select-configuration request. | 0             |
| AltConfigurationValue      | REG\_DWORD | The configuration index to use if the select-configuration request with OriginalConfigurationValue fails.      | 0             |

 

**Note**  The preceding registry settings are not present, by default. They must be added under this node:
HKLM\\SYSTEM\\CurrentControlSet\\Enum\\USB\\*&lt;device\_identifier&gt;*\\*&lt;instance\_identifier&gt;*\\DeviceParameters

 

The registry setting allows the CCGP driver to select an alternate configuration.

Registry values described in the preceding table correspond to the USB-defined configuration index, indicated by the **bConfigurationValue** member of the configuration descriptor ([**USB\_CONFIGURATION\_DESCRIPTOR**](https://msdn.microsoft.com/library/windows/hardware/ff539241)) and *not* by the **bConfigurationNum** values reported in the device's configuration descriptor. First, Usbccgp.sys sends a select-configuration request to the parent USB bus driver (Usbhub.sys) by using the USB configuration index specified by OriginalConfigurationValue. If that request fails, Usbccgp.sys attempts to use the value specified in AlternateConfigurationValue. Usbccgp.sys uses default values if AlternateConfigurationValue or OriginalConfigurationValue are invalid.

A select-configuration request can fail for many reasons. The most common failure occurs when the device does not respond properly to the request or when the **bMaxPower** value (power required by the requested configuration) exceeds the power value supported by the hub port. For example, **bMaxPower** for a particular configuration (specified by OriginalConfigurationValue) is 100 milliamperes but the hub port is only able to provide 50 milliamperes. When Usbccgp.sys sends a select-configuration request for that configuration, the USB driver stack (specifically, the USB port driver) fails the request. Usbccgp.sys then sends another select-configuration request by specifying the configuration indicated by AltConfigurationValue. If the alternate configuration requires 50 milliamperes or less and no other problems occur, the select-configuration request completes successfully.

### <a href="" id="compatibility-feature"></a> Compatibility Feature

Even though a client driver for a function in the composite device is not able to select the configuration of a composite device, the client driver can still send a select-configuration request to Usbccgp.sys. For information about how to build that request, see [How to Select a Configuration for a USB Device](how-to-select-a-configuration-for-a-usb-device.md). Usbccgp.sys performs the following tasks after receiving a select-configuration request from a client driver:

1.  Validates the received request by using the same criteria used by the USB port driver to validate any select-configuration requests.
2.  If the request specifies interface or pipe settings that are different from the current settings, Usbccgp.sys issues a select-interface request by sending an URB of the type URB\_FUNCTION\_SELECT\_INTERFACE to change the existing settings to the new interface and pipe settings.
3.  Copies the cached contents of the [**USBD\_INTERFACE\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff539068) and [**USBD\_PIPE\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff539114) structures into the URB.
4.  Completes the URB.

## Related topics
[How to Select a Configuration for a USB Device](how-to-select-a-configuration-for-a-usb-device.md)  
[USB device configuration](configuring-usb-devices.md)  

--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Busbcon\buses%5D:%20Configuring%20Usbccgp.sys%20to%20Select%20a%20Non-Default%20USB%20Configuration%20%20RELEASE:%20%281/26/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


