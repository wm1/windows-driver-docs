---
title: Using a Universal INF File
description: If you are building a universal or mobile driver package, you must use a universal INF file.
ms.assetid: 2CBEB814-974D-4E8B-A44A-2CFAA8D4C94E
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Using a Universal INF File

If you are building a universal or mobile driver package, you must use a universal INF file. If you are building a desktop driver package, you don't have to use a universal INF file, but doing so is recommended because of the performance benefits.

A universal INF file uses a subset of the [INF syntax](inf-file-sections-and-directives.md) that is available to a Windows driver. A universal INF file installs a driver and configures device hardware, but does not perform any other action, such as running a co-installer.

## Why is a universal INF file required on non-desktop editions of Windows?

Some editions of Windows, such as Windows 10 Mobile, do not support the Plug and Play mechanism for driver installation. Therefore, driver installation takes place on an offline image of the target system. When Microsoft Visual Studio builds your driver for such a target system, it generates an XML-based configuration file that contains all of the registry settings to be applied. As a result, an INF file for such a system must perform only additive operations that do not depend on the runtime behavior of the system. An INF file with such restricted syntax is called a universal INF file.

A universal INF file installs predictably, with the same result each time. The results of the installation do not depend on the runtime behavior of the system. For example, co-installer references are not valid in a universal INF file because code in an additional DLL cannot be executed on an offline system.

As a result, a driver package with a universal INF file can be configured in advance and added to an offline system.

You can use the [InfVerif](../devtest/infverif.md) tool to test if your driver's INF file is universal.

## Which INF sections are invalid in a universal INF file?

You can use any INF section in a universal INF file except for the following:

-   [**INF ClassInstall32 Section**](inf-classinstall32-section.md)
-   [**INF DDInstall.CoInstallers Section**](inf-ddinstall-coinstallers-section.md)
-   [**INF DDInstall.FactDef Section**](inf-ddinstall-factdef-section.md)
-   [**INF DDInstall.LogConfigOverride Section**](inf-ddinstall-logconfigoverride-section.md)

The [**INF Manufacturer Section**](inf-manufacturer-section.md) is valid as long as the **TargetOSVersion** decoration does not contain a **ProductType** flag or **SuiteMask** flag.

## Which INF directives are invalid in a universal INF file?


You can use any INF directive in a universal INF file except for the following:

-   [**INF BitReg Directive**](inf-bitreg-directive.md)
-   [**INF DelFiles Directive**](inf-delfiles-directive.md)
-   [**INF DelProperty Directive**](inf-delproperty-directive.md)
-   [**INF DelReg Directive**](inf-delreg-directive.md)
-   [**INF DelService Directive**](inf-delservice-directive.md)
-   [**INF Ini2Reg Directive**](inf-ini2reg-directive.md)
-   [**INF LogConfig Directive**](inf-logconfig-directive.md)
-   [**INF ProfileItems Directive**](inf-profileitems-directive.md)
-   [**INF RegisterDlls Directive**](inf-registerdlls-directive.md)
-   [**INF RenFiles Directive**](inf-renfiles-directive.md)
-   [**INF UnregisterDlls Directive**](inf-unregisterdlls-directive.md)
-   [**INF UpdateIniFields Directive**](inf-updateinifields-directive.md)
-   [**INF UpdateInis Directive**](inf-updateinis-directive.md)

The following directives are valid with some caveats:

-   The [**INF AddReg Directive**](inf-addreg-directive.md) is valid if entries in the specified *add-registry-section* have a *reg-root* value of **HKR**, or in the following cases:
	-	For registration of [Component Object Model](https://msdn.microsoft.com/en-us/library/ee663262(v=vs.85).aspx) (COM) objects, a key may be written under:
		-	HKCR
		-	HKLM\SOFTWARE\Classes
	-	For creation of [Hardware Media Foundation Transforms](https://msdn.microsoft.com/en-us/library/windows/desktop/ms703138.aspx) (MFTs), a key may be written under:
		-	HKLM\SOFTWARE\Microsoft\Windows Media Foundation
		-	HKLM\SOFTWARE\WOW6432Node\Microsoft\Windows Media Foundation
		-	HKLM\SOFTWARE\WOW3232Node\Microsoft\Windows Media Foundation

-   [**INF CopyFiles Directive**](inf-copyfiles-directive.md) is valid only if the [destination directory](inf-destinationdirs-section.md) is one of the following:

    -   11 (corresponds to %WINDIR%\\System32)
    -   12 (corresponds to %WINDIR%\\System32\\Drivers)
    -   13 (corresponds to the directory under %WINDIR%\\System32\\DriverStore\\FileRepository where the driver is stored)  
        	**Note:** 13 is only valid on Windows 10 products for a limited subset of device installation scenarios. Please consult guidance and samples for your specific device class for more details.
    -   10,SysWOW64 (corresponds to %WINDIR%\\SysWOW64)
	-   10,*vendor-specific subdirectory name*  
			**Note:** In Windows 10 Fall Creators Update, using DIRID 10 with a vendor-specific subdirectory name is valid in a universal INF as measured using the [InfVerif](../devtest/infverif.md) tool.  In later releases, this value may not be supported.  We recommend moving to DIRID 13.

## See Also

* [Installing a Universal Windows driver](https://msdn.microsoft.com/windows-drivers/develop/installing_a_universal_driver)
* [InfVerif](https://msdn.microsoft.com/library/windows/hardware/dn929319)
