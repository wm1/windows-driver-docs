---
title: Defining WMI Instance Names
author: windows-driver-content
description: Defining WMI Instance Names
ms.assetid: 0f91710a-7bd2-462a-b677-6dd32160a861
keywords: ["WMI WDK kernel , event blocks", "event blocks WDK WMI", "data blocks WDK WMI", "WMI WDK kernel , data blocks", "blocks WDK WMI", "dynamic instance names WDK WMI", "static instance names WDK WMI", "instance names WDK WMI", "WMI WDK kernel , instance names"]
ms.author: windowsdriverdev
ms.date: 06/16/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Defining WMI Instance Names


## <a href="" id="ddk-defining-wmi-instance-names-kg"></a>


An *instance* of a WMI block contains data supplied by a particular physical device or software component. Just as a block's GUID uniquely identifies the block, an instance's name uniquely identifies that instance of a block. WMI client applications use instance names to associate the information returned in a data block with the device or component that supplied the data. WMI uses instance names to determine which device a request should be sent to. It is strongly recommended that drivers use their PDO when defining instance names.

A driver can define instance names for a block in either of two ways:

-   The driver passes a list of *static instance names* to WMI when it registers the block.

    After the block is registered, both the driver and WMI specify an instance name by its index into this list. Static instance names can be based on the [*device instance ID*](https://msdn.microsoft.com/library/windows/hardware/ff556277#wdkgloss-device-instance-id) of a driver's PDO, or a driver-defined base name; or the driver can define a list of instance name strings. Static instance names persist until the driver explicitly changes them by reregistering the block.

-   The driver generates *dynamic instance names* as instances are created.

    The driver indicates that it will generate dynamic instance names for a block when it registers the block. After the block is registered, both the driver and WMI pass dynamic instance names as strings in the buffer at **Parameters.WMI.Buffer**.

A driver should generate dynamic instance names only if the number of instances or instance names of a data block change frequently at runtime. For example, a driver might use process IDs or the IP addresses of TCP/IP connections as instance names. Such instance names should be dynamic; if they were static, the driver would incur considerable overhead because it would have to call [**IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480) to update the number and names of instances each time a change occurred.

In most cases, static instance names are preferable to dynamic instance names for the following reasons:

-   Static instance names improve a driver's performance because the driver does not need to return instance name strings in response to WMI requests, as it must for dynamic instance names.

-   WMI can detect static instance name collisions at registration and automatically modify the instance names if necessary, so that all instance names are unique for a given block no matter how many drivers register the block.

    WMI cannot detect instance name collisions for dynamic instance names, so the driver is responsible for generating unique names using [**IoWMIAllocateInstanceIds**](https://msdn.microsoft.com/library/windows/hardware/ff550429).

-   A driver can use the WMI Library routines to handle IRPs for a block that uses static instance names, as long as the names are based on the driver's PDO or a driver-defined base name.

    A driver cannot use WMI Library routines to handle IRPs for a data block that uses dynamic instance names.

A driver indicates whether a block uses static or dynamic instance names, and the type of static instance names, by setting or clearing WMIREG\_FLAG\_*XXX* in the [**WMIREGGUID**](https://msdn.microsoft.com/library/windows/hardware/ff565827) or [**WMIGUIDREGINFO**](https://msdn.microsoft.com/library/windows/hardware/ff565811) structure it passes to WMI when it registers the block. For more information, see [Registering as a WMI Data Provider](registering-as-a-wmi-data-provider.md).

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bkernel\kernel%5D:%20Defining%20WMI%20Instance%20Names%20%20RELEASE:%20%286/14/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


