---
title: Metadata Files for Analysis Extension Plug-ins
description: When you write an analysis extension plug-in, you also write a metadata file that describes the situations for which you want your plug-in to be called.
ms.assetid: 13B9B7A5-1D68-49A3-825B-454AC070FCC1
---

# Metadata Files for Analysis Extension Plug-ins


When you write an analysis extension plug-in, you also write a metadata file that describes the situations for which you want your plug-in to be called. When the [**!analyze**](-analyze.md) debugger command runs, it uses metadata files to determine which plug-ins to load.

Create a metadata file that has the same name as your analysis extension plug-in and an extension of .alz. For example, if your analysis extension plug-in is named MyAnalyzer.dll, your metadata file must be named MyAnalyzer.alz. Place the metadata file in the same directory as your analysis extension plug-in.

A metadata file for an analysis extension plug-in is an ASCII text file that contains key-value pairs. Keys and values are separated by white space. A key can have any non-whitespace character. Keys are not case sensitive.

After the key and the following white space, the corresponding value begins. A value can have one of the following forms.

-   Any set of characters to the end of the line. This form works for values that do not contain any newline characters.

    **Important**  If the last value in the metadata file has a value of this form, the line must end with a newline character.

     

-   Any set of characters between braces { }. The form works for values that contain newline characters.

A line beginning with \# is a comment and is ignored. Comments can start only where keys are expected.

You can use the following keys in a metadata file.

| Key            | Description                                                                                                                                                                                                                                                                                       |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PluginId       | String - Identifies the plug-in.                                                                                                                                                                                                                                                                  |
| DebuggeeClass  | String - Possible values are “Kernel” and "User". Indicates that the plug-in is interested in analyzing only kernel-mode failures or only user-mode failures.                                                                                                                                     |
| BugCheckCode   | 32-bit bug check code - Indicates that the plug-in is interested in analyzing this [bug check code](bug-check-code-reference2.md). A single metadata file can specify multiple bug check codes.                                                                                                  |
| ExceptionCode  | 32-bit exception code - Indicates that the plug-in is interested in analyzing this [exception code](http://go.microsoft.com/fwlink/p?LinkID=282670). A single metadata file can specify multiple exception codes.                                                                                 |
| ExecutableName | String - Indicates that the plug-in is interested only in sessions where this is the running executable of the process to be analyzed. A single metadata file can specify multiple executable names.                                                                                              |
| ImageName      | String - Indicates that the plug-in is only interested only in sessions where the default analysis considers this image (dll, sys, or exe) to be at fault. The plug-in is invoked after analysis has determined which image is at fault. A single metadata file can specify multiple image names. |
| MaxTagCount    | Integer - The maximum number of custom tags that the plug-in needs. Custom tags are tags other than the ones defined in extsfns.h.                                                                                                                                                                |

 

## <span id="Example_Metadata_Files"></span><span id="example_metadata_files"></span><span id="EXAMPLE_METADATA_FILES"></span>Example Metadata Files


The following metadata file describes a plug-in that is interested in analyzing bug check code 0xE2. (Recall that the last line must end with a newline character.)

```
PluginId      MyPlugin
DebuggeeClass Kernel
BugCheckCode  0xE2
```

The following metadata file describes a plug-in that is interested in analyzing bug checks 0x8, 0x9, and 0xA if MyDriver.sys is considered to be the module at fault.

```
PluginId      MyPlugin
DebuggeeClass Kernel
BugCheckCode  0x8
BugCheckCode  0x9
BugCheckCode  0xA
ImageName     MyDriver.sys
```

The following metadata file describes a plug-in that is interested in analyzing exception code 0xC0000005 if MyApp.exe is the running executable of the process being analyzed. Also, the plug-in might create as many as three custom tags.

```
PluginId        MyPlugin
DebuggeeClass   User
ExceptionCode   0xC0000005
ExecutableName  MyApp.exe
```

Debugging Tools for Windows has a sample that you can use to build a debugger extension module named dbgexts.dll. This extension module implements several debugger extension commands, but it can also serve as an analysis extension plug-in; that is, it exports an [**\_EFN\_Analyze**](https://msdn.microsoft.com/library/windows/hardware/jj983432) function. Here is a metadata file that describes dbgexts.dll as an analysis extension plug-in.

```
PluginId         PluginSample
DebuggeeClass   User
ExceptionCode   0xc0000005
ExecutableName      cdb.exe
ExecutableName      windbg.exe
#
# Custom tag descriptions 
#
TagDesc         0xA0000000  SAMPLE_PLUGIN_DEBUG_TEXT    {Sample debug
help text from plug-in analysis}
#
```

## <span id="related_topics"></span>Related topics


[Writing an Analysis Extension Plug-in to Extend !analyze](writing-an-analysis-extension-to-extend--analyze.md)

[**\_EFN\_Analyze**](https://msdn.microsoft.com/library/windows/hardware/jj983432)

[**!analyze**](-analyze.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Metadata%20Files%20for%20Analysis%20Extension%20Plug-ins%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





