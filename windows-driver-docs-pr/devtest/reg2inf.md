---
title: Reg2inf
description: Reg2inf is a tool that converts registry keys to make a driver package universal.
ms.assetid: e43a137e-c08a-4715-84f7-32cda67399e3
ms.author: windowsdriverdev
ms.date: 08/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Reg2inf
 
The Driver Package INF Registry Conversion Tool (`reg2inf.exe`) tool converts a registry key and its values or a COM .dll implementing a [**DllRegisterServer**](https://msdn.microsoft.com/library/windows/desktop/ms682162) routine into a set of [INF AddReg directives](../install/inf-addreg-directive.md) for inclusion into a driver package INF file.  This tool is particularly useful for converting existing [INF RegisterDlls directives](../install/inf-registerdlls-directive.md) into INF AddReg directives in order to make an INF file universal.  For more info about universal INF files, see [Using a Universal INF File](../install/using-a-universal-inf-file.md).
 
The tool currently ships as part of the WDK 10 installation in current Windows 10 Insider Preview builds. You can find it in the \tools subdirectory of your WDK 10 installation, for example `c:\Program Files(x86)\Windows Kits\10\tools\`. 

While Reg2inf attempts to generate a COM registration, it may not capture the full registry state that the COM registration provides. As always, you should inspect the output of the tool for completeness and correctness, and test the results. 

## Running Reg2inf from the command line 
 
This section lists the command line options for Reg2inf.

```
USAGE: reg2inf.exe [/key <path> | /dll <filename>] [/targetkey <path>]

/key <registry key path>
    Process a specific registry key, e.g.: reg2inf /key HKEY_LOCAL_MACHINE\SOFTWARE\Fabrikam
/dll <module filename>
    Process a COM DLL module that implements DllRegisterServer entrypoint, typically called by regsvr32 or legacy INF RegisterDlls directive in order to register COM class under HKEY_CLASSES_ROOT, e.g.: reg2inf /dll %SystemRoot%\System32\fabkobj.dll
/targetkey <registry key path>
    Remap target registry key to be under a different base key path, e.g.: reg2inf /key HKLM\SYSTEM\Temp /targetkey HKR\Parameters
```

**Note** Reg2inf requires that the full path length must not exceed 259 characters. 
