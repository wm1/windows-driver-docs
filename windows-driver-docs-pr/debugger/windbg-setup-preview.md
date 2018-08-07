---
title: WinDbg Preview - Settings and workspaces
description: This section describes how to setup the WinDbg preview debugger.
ms.author: windowsdriverdev
ms.date: 08/17/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

> [!NOTE]
> The information in this topic is preliminary. Updated information will be provided in a later release of the documentation. 
>

# WinDbg Preview - Settings and workspaces

This section describes how to setup and configure the WinDbg Preview debugger.


## Settings

Use the settings menu to set the source and symbol path as well as choose the light and dark theme for the debugger. 

![Screen shot of feedback hub showing feedback options including the add new feedback button](images/windbgx-settings-menu.png)

For more information on setting the paths, see [Accessing Symbols for Debugging](accessing-symbols-for-debugging.md) and [Source Code Debugging in WinDbg](source-window.md).

## Workspaces

Workspaces allows you to save configuration information in the target connection information file.

The options in workspaces are saved upon closing the debugger or can be manually saved using *File* -> *Save Workspace*. 

Workspaces are automatically loaded when launching from the recent targets list or they can be manually loaded in the file menu. 

In addition to the target connection information, the following settings are stored in the workspaces file.

#### General Settings 
> [!NOTE]
> This list and format isn't final and is subject to change.

Setting | Default | Description
--- | --- | ---
FinalBreak |true | If true, ignores the final breakpoint (-g command-line option).
SourceDebugging |true  | Toggles between source or assembly mode.
DebugChildProcesses | false| (User mode only) If true will debug child processes launched by the target application. (-o command-line option).
Noninvasive | false  |  Specifies non-invasive attach (-pv command-line option).
NoDebugHeap | false  |  Specifies the debug heap should not be used (-hd command-line option).
Verbose | false  | When verbose mode is turned on, some display commands (such as register dumping) produce more detailed output. (-v command-line option).
Elevate | - |  Used internally by WinDbg - Do not modify.
Restartable | - |  Used internally by WinDbg - Do not modify.
UseImplicitCommandLine | false | Use implicit command-line (-cimp command-line option). This starts teh debugger with an implicit command line instead of an explicit process to run.

For more information about the command line options, see [WinDbg Command-Line Options](windbg-command-line-options.md).


#### Symbol Settings 

Setting | Default | Description
--- | --- | ---
SymbolOptionsOverride | 0 | An explicit symbol option mask, in the form of a single hex number.
ShouldOverrideSymbolOptions | false | If set to *true* override all of the symbol options listed below with the provided  symbol option mask, described  above.
SymOptExactSymbols | false | This option causes the debugger to perform a strict evaluation of all symbol files.
SymOptFailCriticalErrors | false | This symbol option causes file access error dialog boxes to be suppressed.
SymOptIgnoreCvRec | false | This option causes the symbol handler to ignore the CV record in the loaded image header when searching for symbols. 
SymOptIgnoreNtSympath | false | This option causes the debugger to ignore the environment variable settings for the symbol path and the executable image path. 
SymOptNoCpp | false | This symbol option turns off C++ translation. When this symbol option is set, :: is replaced by __ in all symbols. 
SymOptNoUnqualifiedLoads | false | This symbol option disables the symbol handler's automatic loading of modules. When this option is set and the debugger attempts to match a symbol, it will only search modules which have already been loaded. 
SymOptAutoPublics | false | This symbol option causes DbgHelp to search the public symbol table in a .pdb file only as a last resort. If any matches are found when searching the private symbol data, the public symbols will not be searched. This improves symbol search speed. 
SymOptDebug | false | This symbol option turns on noisy symbol loading. This instructs the debugger to display information about its search for symbols.

For more information on symbol options, see [Symbol Options](symbol-options.md).


#### Window layout settings

 Window layout is saved globally and are not saved in the workspaces file. 


#### Workspaces XML file

The workspace and target connection information is stored in XML format. 

The following file, shows an example workspaces configuration file.

```
<?xml version="1.0" encoding="utf-8"?>
<TargetConfig Name="C:\paint.dmp" LastUsed="2017-08-03T21:34:20.1013837Z">
  <EngineConfig />
  <EngineOptions>
    <Property name="FinalBreak" value="true" />
    <Property name="SourceDebugging" value="true" />
    <Property name="DebugChildProcesses" value="false" />
    <Property name="Noninvasive" value="false" />
    <Property name="NoDebugHeap" value="false" />
    <Property name="Verbose" value="false" />
    <Property name="SymbolOptionsOverride" value="0" />
    <Property name="ShouldOverrideSymbolOptions" value="false" />
    <Property name="SymOptExactSymbols" value="false" />
    <Property name="SymOptFailCriticalErrors" value="false" />
    <Property name="SymOptIgnoreCvRec" value="false" />
    <Property name="SymOptIgnoreNtSympath" value="false" />
    <Property name="SymOptNoCpp" value="false" />
    <Property name="SymOptNoUnqualifiedLoads" value="false" />
    <Property name="SymOptAutoPublics" value="false" />
    <Property name="SymOptDebug" value="false" />
    <Property name="Elevate" value="false" />
    <Property name="Restartable" value="true" />
    <Property name="UseImplicitCommandLine" value="false" />
  </EngineOptions>
  <TargetOptions>
    <Option name="OpenDump">
      <Property name="DumpPath" value="C:\paint.dmp" />
    </Option>
  </TargetOptions>
</TargetConfig>

```

Note that this file format will continue to evolve as more features are added to the WinDbg Preview debugger.


---
 
## See Also

[Debugging Using WinDbg Preview](debugging-using-windbg-preview.md)
 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Debugging%20Using%20WinDbg%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




