[---
title: Getting Started with TAEF
description: Getting Started with Test Authoring and Execution Framework (TAEF)
ms.assetid: 7F57C5EF-141A-4303-9B9F-2EC118324BF8
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Getting Started


## Installation


When you install the [Windows Driver Kit](https://developer.microsoft.com/en-us/windows/hardware/windows-driver-kit), the TAEF files are placed in the Testing\\Runtimes\\TAEF subdirectory of the WDK. When you set up a test computer for deployment, following the instructions to [Provision a computer for driver deployment and testing (WDK 8.1)](https://msdn.microsoft.com/library/windows/hardware/dn745909) or [Provision a computer for driver deployment and testing (WDK 8)](https://msdn.microsoft.com/library/windows/hardware/hh698272), the TAEF files are installed on the test computer.

You can also install the TAEF files manually, see [Manually installing and uninstalling TAEF on a test computer](#manually-installing-and-uninstalling-taef-on-a-test-computer).

## Authoring Tests


TAEF does not restrict users with native or managed affinity. Users can choose the most productive language while authoring tests. TAEF supports writing tests in C/C++, C#, JScript, and VBScript.

For more information, see [Authoring Tests](authoring-tests.md).

## Executing Tests


Executing tests is simply a case of passing a test file on the command prompt to the "TE.exe" tool. For example, run the following:

``` syntax
TE.exe UnitTests\Wex.Common.Tests.dll
```

For more information, see [Executing Tests](executing-tests.md).

## Manually installing and uninstalling TAEF on a test computer


Follow this procedure if you want to run tests on a computer without using the WDK and Visual Studio.

**To install TAEF manually**

1.  Install Visual Studio and the WDK on the computer you use for development.
2.  Copy the all the TAEF installation files from the computer where you installed the WDK to the test computer. The TAEF installation files (\*.msi and \*.cab files) are located in the %programfiles%\\Windows Kits\\8.0\\Testing\\Runtimes directory on your development system.
3.  On the test computer, open a Command Prompt window and navigate to the directory that contains the TAEF installation files that you just copied. Run the following command to install TAEF. Run the \*.msi that matches the architecture of the test computer.

    ``` syntax
    msiexec /i "Test Authoring and Execution Framework x64-x64_en-us.msi"
    ```

    -Or-

    ``` syntax
    msiexec /i "Test Authoring and Execution Framework x86-x86_en-us.msi"
    ```

    This will install the TAEF files to \\Program Files\\Windows Kits\\8.0\\Testing\\Runtimes\\TAEF\\ on the test system.

**To uninstall TAEF manually**

1.  Stop the Te.Service. Open the Microsoft Management Console (compmgmt.msc). Go to Services and Applications\\Services, and locate the Te.Service. Right-click the Te.Service and click **Stop**.
2.  Go to Control Panel\\Programs\\Programs and Features and uninstall the **Test Authoring and Execution Framework program**.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[taef\taef]:%20Getting%20Started%20%20RELEASE:%20%289/12/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




