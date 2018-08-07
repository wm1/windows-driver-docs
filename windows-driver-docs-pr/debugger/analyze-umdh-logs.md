---
title: Analyze UMDH Logs
description: Use the following commands to analyze User-Mode Dump Heap (UMDH) logs that were created by running UMDH with the syntax described in Analyze a Running Process.
ms.assetid: 66e559b2-0335-4a1d-ba6c-dde6b826dc5f
keywords: ["Analyze UMDH Logs Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- Analyze UMDH Logs
api_type:
- NA
---

# Analyze UMDH Logs


Use the following commands to analyze User-Mode Dump Heap (UMDH) logs that were created by running UMDH with the syntax described in [**Analyze a Running Process**](analyze-a-running-process.md). This analysis focuses on allocations, instead of stack traces.

You can analyze a single log file or compare logs from different runs to detect the changes in the program or driver's memory dump allocations over time.

```
umdh [-d] [-v] [-l] File1 [File2] [-h | ?]
```

## <span id="ddk_analyze_umdh_logs_dtools"></span><span id="DDK_ANALYZE_UMDH_LOGS_DTOOLS"></span>Parameters


<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
Displays numeric data in decimal numbers. The default is hexadecimal.

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
Verbose mode. Includes the traces, as well as summary information. The traces are most helpful when analyzing a single log file.

<span id="_______-l______"></span><span id="_______-L______"></span> **-l**   
Includes file names and line numbers in the log. (Please note that the parameter is the lowercased letter "L," not the number one.)

<span id="_______File1__File2_"></span><span id="_______file1__file2_"></span><span id="_______FILE1__FILE2_"></span> *File1* \[*File2*\]  
Specifies the UMDH log files to analyze.

UMDH creates log files when you run it in the [**analyze a running process**](analyze-a-running-process.md) mode and save the log content in a text file (**-f**).

When you specify one log file, UMDH analyzes the file and displays the function calls in each trace in descending order of bytes allocated.

When you specify two log files, UMDH compares the files and displays in descending order the function calls whose allocations have grown the most between the two trials.

<span id="_______-h____"></span><span id="_______-H____"></span> **-h | ?**  
Displays help.

### <span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>Sample Usage

```
umdh dump.txt
umdh -d -v dump.txt
umdh dump1.txt dump2.txt
```

Remarks
-------

Suppose you have two computers: a *logging computer* where you create a UMDH log and an *analysis computer* where you analyze the UMDH log. The symbol path on your analysis computer must point to the symbols for the version of Windows that was loaded on the logging computer at the time the log was made. Do not point the symbol path on the analysis computer to a symbol server. If you do, UMDH will retrieve symbols for the version of Windows that is running on the analysis computer, and UMDH will not display meaningful results.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Analyze%20UMDH%20Logs%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




