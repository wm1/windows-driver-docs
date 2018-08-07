---
title: Building WdbgExts Extensions
description: Building WdbgExts Extensions
ms.assetid: a3923de6-bed5-40e0-a9cb-99e0f4354448
keywords: ["Build utility (build.exe), building WdbgExts extensions", "WdbgExts extensions, building", "WdbgExts extensions, compiling"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Building WdbgExts Extensions


## <span id="ddk_building_wdbgexts_extensions_dbwx"></span><span id="DDK_BUILDING_WDBGEXTS_EXTENSIONS_DBWX"></span>


All debugger extensions should be compiled and built with the Build utility. The Build utility is included in the Windows Driver Kit (WDK) and in earlier versions of the Windows DDK.

For more information on the Build utility, see the WDK documentation.

Note the following points:

-   The WDK has several different build environment windows. Each of these has a corresponding shortcut placed in the **Start** menu when the WDK is installed. To build a debugger extension, you must use the latest Windows build environment, regardless of what platform you will be running the extension on.

-   The Build utility is usually not able to compile code that is located in a directory path that contains spaces. Your extension code should be located in a directory whose full path contains no spaces. (In particular, this means that if you install Debugging Tools for Windows to the default location -- Program Files\\Debugging Tools for Windows -- you will not be able to build the sample extensions.)

**To build a debugger extension**

1.  Open the window for the latest Windows build environment. (You can choose either the "free" version or the "checked" version -- they will give identical results unless you have put **\#ifdef DBG** statements in your code.)

2.  Set the variable \_NT\_TARGET\_VERSION to indicate the oldest version of Windows on which you want to run the extension. \_NT\_TARGET\_VERSION can be set to the following values.

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">Value</th>
    <th align="left">Versions of Windows</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>_NT_TARGET_VERSION_WIN2K</p></td>
    <td align="left"><p>Windows 2000 and later.</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>_NT_TARGET_VERSION_WINXP</p></td>
    <td align="left"><p>Windows XP and later.</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>_NT_TARGET_VERSION_WS03</p></td>
    <td align="left"><p>Windows Server 2003 and later.</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>_NT_TARGET_VERSION_LONGHORN</p></td>
    <td align="left"><p>Windows Vista and later.</p></td>
    </tr>
    </tbody>
    </table>

     

    If \_NT\_TARGET\_VERSION is not set, the extension will only run on the version of Windows for which the build window was opened (and later versions). For example, putting the following line in your Sources file will build an extension that will run on Windows XP and later versions of Windows:

    ```
    _NT_TARGET_VERSION = $(_NT_TARGET_VERSION_WINXP) 
    ```

3.  3.Set the DBGSDK\_INC\_PATH and DBGSDK\_LIB\_PATH environment variables to specify the paths to the debugger SDK headers and the debugger SDK libraries, respectively. If *%debuggers%* represents the root of your Debugging Tools for Windows installation, these variables should be set as follows:

    ```
    set DBGSDK_INC_PATH=%debuggers%\sdk\inc
    set DBGSDK_LIB_PATH=%debuggers%\sdk\lib
    ```

    If you have moved these headers and libraries to a different location, specify that location instead.

4.  4.Change the current directory to the directory that contains your extension's Dirs file or Sources file.

5.  5.Run the Build utility:
    ```
    build -cZMg
    ```

For a full explanation of these steps, and for a description of how to create a Dirs file and a Sources file, see the Build utility documentation in the WDK.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Building%20WdbgExts%20Extensions%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




