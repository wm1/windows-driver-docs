---
title: Static Driver Verifier commands (MSBuild)
description: Commands used with Static Driver Verifier
ms.assetid: F0663631-AD7B-4BFE-8E07-7BB2FFC72911
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

#  Static Driver Verifier commands (MSBuild)


You can run Static Driver Verifier (SDV) in a **Visual Studio Command Prompt** window. Navigate to the directory where the driver's project file or the library's project file is stored. The parameters can appear in any order on the command line.

**Note**  Previously available in the Windows Driver Kit (WDK) as a stand-alone tool, SDV is now integrated into Visual Studio and can be run as an MSBuild target, or from the **Driver** menu in Visual Studio.

 

```
msbuild /t:sdv /p:Inputs="Parameters" ProjectFile /p:Configuration=configuration /p:Platform=platform     
```

You must select a Release configuration (for example, **/p:Configuration="Windows 7 Release"**). For the list of supported Release Configurations, see [Building a Driver](https://msdn.microsoft.com/windows-drivers/develop/building_a_driver). The Platform can be **Win32** (for x86) or **x64** (for example, **/p:Platform=Win32**).

**Note**  Be sure to check your computer's power management plan to ensure the computer will not go into a sleep state during the analysis.

 

## <span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


### <span id="parameters"></span><span id="PARAMETERS"></span>

<span id="_scan"></span><span id="_SCAN"></span>/**scan**  
Scans the driver's source code for function role type declarations. For information about how to declare the driver supplied callback functions and dispatch routines, see [Using Function Role Type Declarations](using-function-role-type-declarations.md). During this scan, SDV tries to detect the driver entry points that it needs to verify the driver. It records the results of the scan in [Sdv-map.h](sdv-map-h.md), a file that it creates in the driver's project directory.

For more information, see [Preparing your source code](using-static-driver-verifier-to-find-defects-in-drivers.md#preparing_your_source_code).

<span id="________check_Rule____Rule_..._"></span><span id="________check_rule____rule_..._"></span><span id="________CHECK_RULE____RULE_..._"></span> **/check:***Rule* | \[*Rule*,...\]  
Starts a verification with the specified rule(s). You can specify more than one rule by enclosing the list of rules in square brackets and separating each rule with a comma. Run the **/check:** command and specify the driver's Visual Studio project file (\*.vcxproj).

*Rule* is the name of one [rule](static-driver-verifier-rule.md) or a rule name pattern that includes wildcard characters (**\***) to represent one or more characters. When used alone, the wildcard character (**\***) represents all rules.

<span id="________check_rulelist.sdv______"></span><span id="________CHECK_RULELIST.SDV______"></span> **/check:***RuleList***.sdv**   
Starts a verification with the rules in the specified rule list file. You can list only one file with this parameter. In the rule list file, each line can be the name of one rule or it can be a wildcard character (\*), which represents all SDV rules. You can also use the wildcard character (\*) in a rule name to mean any character or characters. Run **/check:***RuleList***.sdv** command and specify the driver's Visual Studio project file (\*.vcxproj).

*RuleList***.sdv** is the fully qualified path and file name of a [rule list file](static-driver-verifier-rule-list-file.md). The file must have the **.sdv** file name extension. Unless the file is in the local directory, the path is required. If the path or file name includes spaces, you must enclose *RuleList.***sdv** in quotation marks.

If you specify the **/check:** option without specifying a rule, SDV runs with the default rule set for the driver model.

<span id="_______________________refine______"></span><span id="_______________________REFINE______"></span> **/refine**   
If SDV directs you to use this option, **/refine** performs *a per entry* verification for the rule or rules you had specified. The **/refine** option partitions the verification process into groups of related entry points. This allows SDV to produce useful results for larger drivers. SDV automatically generates a rule file called Refine.sdv in the same directory as your project. This file contains those rules which might benefit from further verification. Follow the instructions SDV provides in the results summary and continue the analysis.

<span id="________lib______"></span><span id="________LIB______"></span> **/lib**   
Processes the library in the current directory. SDV calls MSBuild.exe to compile and build the library for external use, and it generates the files that it needs to include the library in the driver verification.

Use this parameter before verifying drivers that require the library. Run the **msbuild /t:sdv /p:Inputs="/lib"** command and specify the Visual Studio project file (\*.vcxproj) for the library.

For more information about the use and effect of the **/lib** parameter, see [Library Processing in Static Driver Verifier](library-processing-in-static-driver-verifier.md).

<span id="________view______"></span><span id="________VIEW______"></span> **/view**   
Opens Static Driver Verifier. Run **/view** commands and specify the driver's Visual Studio project file (\*.vcxproj).

The results are available as soon as a verification is complete, and remain available until you use a **/clean** command to delete the SDV files from the driver's project directory.

<span id="________clean______"></span><span id="________CLEAN______"></span> **/clean**   
Deletes SDV files from the directory. Because these files are used to generate the Static Driver Verifier Report display, the **/clean** command also deletes the report of the verification.

Run a **/clean** command and specify the Visual Studio project file (\*.vcxproj) for the driver or library. The command deletes SDV files only for the project specified.

Run a **/clean** command for a driver project before each verification.

Run a **/clean** command for a library when the library files are outdated, such as when the library code changes.

A **/clean** command does not remove the Sdv-map.h file, if the approved flag is set to true in the Sdv-map.h file (Approved=true). SDV can then use this file for future verifications.

<span id="________cleanalllibs______"></span><span id="________CLEANALLLIBS______"></span> **/cleanalllibs**   
Deletes the library-processing files that SDV created in all directories on the computer's hard disk drives. It does not affect driver data.

You can run a **/cleanalllibs** command in any directory of the build environment window.

Use this parameter to remove all library processing files that SDV created or when the code in several libraries has changed. For more information, see [Library Processing in Static Driver Verifier](library-processing-in-static-driver-verifier.md).

<span id="_______________"></span> **/?**   
Displays usage for SDV commands. Commands that use this parameter do not have to be run in a build environment window.

### <span id="comments"></span><span id="COMMENTS"></span>Comments

Running **msbuild /t:/sdv p:/Inputs= /? ** without parameters displays usage for the SDV commands.

A **/clean** command deletes the files that SDV uses to create the Static Driver Verifier Report display for a verification. After running this command, the Static Driver Verifier Report display for the verification is no longer available.

### <span id="examples"></span><span id="EXAMPLES"></span>Examples

<span id="To_run_SDV_using_all_rules_on_the_driver_files_in_the_local_directory_for_the_mydriver_project_"></span><span id="to_run_sdv_using_all_rules_on_the_driver_files_in_the_local_directory_for_the_mydriver_project_"></span><span id="TO_RUN_SDV_USING_ALL_RULES_ON_THE_DRIVER_FILES_IN_THE_LOCAL_DIRECTORY_FOR_THE_MYDRIVER_PROJECT_"></span>To run SDV using all rules on the driver files in the local directory for the mydriver project:  
```
msbuild /t:sdv /p:Inputs="/check:*" mydriver.VcxProj /p:Configuration="Windows 7 Release"/p:Platform=Win32
```

<span id="To_run_SDV_using_all_rules_that_begin_with__Irql__on_the_driver_files_in_the_local_directory_"></span><span id="to_run_sdv_using_all_rules_that_begin_with__irql__on_the_driver_files_in_the_local_directory_"></span><span id="TO_RUN_SDV_USING_ALL_RULES_THAT_BEGIN_WITH__IRQL__ON_THE_DRIVER_FILES_IN_THE_LOCAL_DIRECTORY_"></span>To run SDV using all rules that begin with "Irql" on the driver files in the local directory:  
```
msbuild /t:sdv /p:Inputs="/check:Irql*" mydriverVcxProj /p:Configuration="Windows 7 Release" /p:Platform=Win32
```

<span id="To_run_SDV_using_the_CancelSpinLock_rule_on_the_driver_files_in_the_local_directory_"></span><span id="to_run_sdv_using_the_cancelspinlock_rule_on_the_driver_files_in_the_local_directory_"></span><span id="TO_RUN_SDV_USING_THE_CANCELSPINLOCK_RULE_ON_THE_DRIVER_FILES_IN_THE_LOCAL_DIRECTORY_"></span>To run SDV using the [CancelSpinLock](https://msdn.microsoft.com/library/windows/hardware/ff542478) rule on the driver files in the local directory:  
```
msbuild /t:sdv /p:Inputs="/check:CancelSpinLock" mydriver.VcxProj /p:Configuration="Windows 7 Release" /p:Platform=Win32
```

<span id="to_run_sdv_using_the_rule_that_is_specified_in_the_rules1.sdv_rule_list_file_in_the_d__sdv_directory_"></span><span id="TO_RUN_SDV_USING_THE_RULE_THAT_IS_SPECIFIED_IN_THE_RULES1.SDV_RULE_LIST_FILE_IN_THE_D__SDV_DIRECTORY_"></span>To run SDV using the rule that is specified in the Rules1.sdv rule list file in the D:\\SDV directory:  
```
msbuild /t:sdv /p:Inputs="/check:D:\SDV\Rules1.sdv" mydriver.VcxProj /p:Configuration="Windows 7 Release" /p:Platform=Win32
```

<span id="to_run_sdv_again__this_time_using_the__clean_option."></span><span id="TO_RUN_SDV_AGAIN__THIS_TIME_USING_THE__CLEAN_OPTION."></span>To run SDV again, this time using the /clean option.  
```
msbuild /t:sdv /p:Inputs="/clean" mydriver.VcxProj /p:Configuration="Windows 7 Release"/p:Platform=Win32
```

<span id="to_run_sdv__using_the__refine_option__if_sdv_directs_you_to_do_so_."></span><span id="TO_RUN_SDV__USING_THE__REFINE_OPTION__IF_SDV_DIRECTS_YOU_TO_DO_SO_."></span>To run SDV, using the /refine option (if SDV directs you to do so).  
```
msbuild /t:sdv /p:Inputs="/refine" mydriver.VcxProj /p:Configuration="Windows 7 Release"/p:Platform=Win32
```

<span id="To_display_Static_Driver_Verifier__so_that_you_can_view_the_results_for_the_most_recent_verification_of_the_driver_in_the_local_directory_"></span><span id="to_display_static_driver_verifier__so_that_you_can_view_the_results_for_the_most_recent_verification_of_the_driver_in_the_local_directory_"></span><span id="TO_DISPLAY_STATIC_DRIVER_VERIFIER__SO_THAT_YOU_CAN_VIEW_THE_RESULTS_FOR_THE_MOST_RECENT_VERIFICATION_OF_THE_DRIVER_IN_THE_LOCAL_DIRECTORY_"></span>To display Static Driver Verifier so that you can view the results for the most recent verification of the driver in the local directory:  
```
msbuild /t:sdv /p:Inputs="/view" mydriver.VcxProj /p:Configuration="Windows 7 Release" /p:Platform=Win32
```

## <span id="related_topics"></span>Related topics


[Using Static Driver Verifier to Find Defects in Windows Drivers](using-static-driver-verifier-to-find-defects-in-drivers.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[devtest\devtest]:%20%20Static%20Driver%20Verifier%20commands%20%28MSBuild%29%20%20RELEASE:%20%2811/17/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





