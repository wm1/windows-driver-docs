---
title: How to Collect IRP Coverage Data
description: How to Collect IRP Coverage Data
ms.assetid: f65422fe-f524-41c1-a532-a2c615d65f72
keywords:
- Driver Coverage Toolkit WDK , collecting data
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# How to Collect IRP Coverage Data


**Note**  The Driver Coverage Toolkit is no longer needed in Windows 10 and the installer is no longer included in the WDK. To perform tasks described here in Windows 10, instead use [Driver Verifier](driver-verifier.md) and [IRP Logging](irp-logging.md).

 

The following steps describe how to collect coverage data of I/O request packets (IRPs) by using the Driver Coverage tools and [Driver Coverage filter driver](driver-coverage-filter-driver.md). The tools are available as part of the [Device Fundamentals Tests](device-fundamentals-tests.md), under the Coverage category.

For information about setting up the WDK and the Visual Studio test environment, see [How to test a driver at runtime using Visual Studio](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime). For information about selecting and configuring tests and tool parameters, see [How to select and configure the Device Fundamentals tests](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests) and [Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests).

1.  Install the [Driver Coverage filter driver](driver-coverage-filter-driver.md) on the test computer.

    -   To install the filter driver and enable IRP coverage on specified device(s), run the **Enable IRP coverage data collection** tool. The tool is available as part of the [Device Fundamentals Tests](device-fundamentals-tests.md), under Coverage.

    -   To install the filter driver and enable IRP coverage on specified device(s), use the *DQ* parameter to specify the device(s) to monitor.

    -   To install the Driver Coverage filter driver as an upper-filter driver or a lower-filter driver for the device(s) use the *UpperFilter* parameter. For information about the coverage filter driver and guidelines about how to install the driver, see [Driver Coverage filter driver](driver-coverage-filter-driver.md)

    For information running the tools, see [How to test a driver at runtime using Visual Studio](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime) and [How to select and configure the Device Fundamentals tests](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests).

2.  Erase the current IRP coverage data.

    Before you start your code coverage tests on one or more devices, first clear the IRP coverage data that has already been collected by the [Driver Coverage filter driver](driver-coverage-filter-driver.md). To do this, run the **Clear IRP Coverage Data** tool on the test computer.

3.  Restart the test computer.

    After you have installed the [Driver Coverage filter driver](driver-coverage-filter-driver.md) on one or more devices, restart the test computer to load the Driver Coverage filter driver and start IRP coverage.

4.  Verify the [Driver Coverage filter driver](driver-coverage-filter-driver.md) installation.

    After the test computer has restarted, verify that the filter driver is installed and the correct devices are enabled for IRP coverage. To do this, run the **Display Devices enabled for IRP coverage data collection** tool on the test computer.

    ```
    Drvcov /D
    ```

    The following example shows sample output from this tool:

    ```
    |------------------------------------------------------------------
    | List of devices we can get coverage data from.
    |------------------------------------------------------------------
    |  Device # : 1 
    |  Devnode #: 3884 Class:  USB Desc:  USB Root Hub
    |  Device ID: " USB\ROOT_HUB\4&413399C&0"
    |------------------------------------------------------------------
    | 1 device(s) found.
    |------------------------------------------------------------------
    ```

5.  Collect the IRP coverage data.

    You are now ready to collect IRP coverage data for your device(s). First run your code coverage tests on the test computer. When you are finished running your code coverage tests, you can view IRP coverage reports. To do this, run the **Display collected IRP coverage data** tool on the test computer.

    For information about how to analyze the IRP coverage data, see [How to Analyze IRP Coverage Data](how-to-analyze-irp-coverage-data.md).

6.  Disable IRP Coverage and uninstall the [Driver Coverage filter driver](driver-coverage-filter-driver.md).

    After you have fully exercised your code coverage tests, you can disable IRP coverage all devices by running the **Disable IRP coverage data collection** tool on the test computer.

    When the last device has been disabled for IRP coverage, the filter driver will no longer load whenever you restart the test computer. However, to unload the filter driver from memory, you must restart the test computer.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[devtest\devtest]:%20How%20to%20Collect%20IRP%20Coverage%20Data%20%20RELEASE:%20%2811/17/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




