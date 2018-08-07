---
Description: Describes a typical hardware design of a USB Type-C system and the Microsoft-provided drivers that support the hardware components.
title: Architecture of USB Type-C design for a Windows system
author: windows-driver-content
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Architecture: USB Type-C design for a Windows system


**Applies to OEMs developing systems with USB Type-C connectors**

-   USB dual-role capabilities by using USB Type-C
-   Faster charging by using USB Type-C current levels and Power Delivery 2.0
-   Display-Out capabilities by using alternate modes and wired docking experiences.

**Last Updated**

-   December 2016

**Windows version**

-   Windows 10 for desktop editions (Home, Pro, Enterprise, and Education)
-   Windows 10 Mobile

Describes a typical hardware design of a USB Type-C system and the Microsoft-provided drivers that support the hardware components.

## <a href="" id="drivers"></a>Drivers for supporting USB Type-C components


![usb type-c software components](images/type-c-arch.png)

In the preceding image,

-   **USB device-side drivers**

    The [USB device-side drivers](usb-device-side-drivers-in-windows.md) service the function/device/peripheral. The USB function controller class extension supports MTP (Media Transfer Protocol) and charging using BC 1.2 chargers. Microsoft provides in-box client drivers for Synopsys USB 3.0 and ChipIdea USB 2.0 controllers. You can write a custom client driver for your function controller by using [USB function controller client driver programming interfaces](https://msdn.microsoft.com/library/windows/hardware/mt188010). For more information, see [Developing Windows drivers for USB function controllers](developing-windows-drivers-for-usb-function-controllers.md).

    The SoC vendor might provide you with the USB function lower filter driver for legacy proprietary charger detection. You can implement your own filter driver if the function controller is Synopsys USB 3.0 or ChipIdea USB 2.0 controllers

-   **USB host-side drivers**

    The USB host-side drivers are a set of drivers that work with EHCI or XHCI compliant USB host controllers. The drivers are loaded if the role-switch driver enumerates the host role. If your host controller is not specification-compliant, then you can write a custom driver by using [USB host controller extension (UCX) programming interface](https://msdn.microsoft.com/library/windows/hardware/mt188009). For information, see [Developing Windows drivers for USB host controllers](developing-windows-drivers-for-usb-host-controllers.md).

    **Note**  Not [all USB devices classes](supported-usb-classes.md) are supported on Windows 10 Mobile.

     

-   **USB role-switch drivers (URS)**

    Systems can be designed such that the dual-role USB port needs Windows to configure it to either Host or Function mode. These designs will need to use the USB role switch (URS) driver stack.

    The URS driver manages the current role of the connector, host or function, and the loading and unloading of the appropriate device side or host side drivers, based on hardware events from the platform. Microsoft provides in-box client drivers for Synopsys USB 3.0 and ChipIdea USB 2.0 controllers. You can write your role-switch client driver by using the [USB dual-role controller driver programming interface](https://msdn.microsoft.com/library/windows/hardware/mt628026). To activate the role-switch drivers, you must make changes to the ACPI tables. For more information, see [USB Dual Role Driver Stack Architecture](usb-dual-role-driver-stack-architecture.md).

    On systems with USB micro-AB connectors, this decision is made based on the ID pin in the connector. ID pin detection is performed by the client driver by using interrupt resources assigned to it.

    On systems with USB Type-C connectors, the decision is made based on the CC pins. The client driver for connector performs CC detection and forwards that information to the role-switch driver.

-   **USB connector manager (UCM)**

    This set of drivers manage all aspects of the USB Type-C connector. If your system implements an embedded controller, use the Microsoft-provided [UCSI driver](ucsi.md). Otherwise you are expected to write a client driver.

    If you are writing a driver, the USB connector manager class extension follows the WDF class extension-client driver model. Your client driver communicates with the hardware and the class extension to handle tasks such as CC detection, PD messaging, Muxing, and VBus/VConn control, and select policy for power delivery and alternate mode. The class extension communicates the information reported by the client driver to the operating system. For example, the CC detection result is used to configure the role-switch drivers; USB Type-C/PD power information is used to determine the level at which the system should charge. The client driver manages USB Type-C and PD state machines. The client driver can delegate some tasks to other drivers, for example, Mux may be controlled by another driver. To write the client driver, use the [USB Type-C connector driver programming interfaces.](https://msdn.microsoft.com/library/windows/hardware/mt188011).

-   **Charging arbitration driver**

    This driver is provided by Microsoft for Windows 10 Mobile. The driver acts as the arbiter for multiple charging sources. The USB connector manager reports USB Type-C and PD charging source information to CAD, which makes a selection from that information and BC1.2 charger detection performed by the USB device-side drivers (if applicable). CAD then reports the most appropriate charging source to use to the battery subsystem.

-   **Battery drivers**

    The class driver defines the overall functionality of the batteries in the system and interacts with the power manager. The miniclass driver handles device-specific functions such as adding and removing a battery, and keeping track of its capacity and charge. The miniclass driver exports routines that the class driver calls to get information about the devices it controls.

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Busbcon\buses%5D:%20Architecture:%20USB%20Type-C%20design%20for%20a%20Windows%20system%20%20RELEASE:%20%281/26/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


