---
title: Using a Source Server
description: Using a Source Server
ms.assetid: b3467f26-1ce3-42cb-a8c8-a7d10efc5079
keywords: ["source server (srcsrv.dll)", "source server (srcsrv.dll), overview", "SrcSrv (srcsrv.dll)", "SrcSrv (srcsrv.dll), overview"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Using a Source Server


A source server enables the debugger to automatically retrieve the source files that match the current target. To use a source server, you must be debugging binaries that have been source indexed at build time and whose source file locations are embedded in the PDB files.

Debugging Tools for Windows includes the source server [SrcSrv](srcsrv.md) (Srcsrv.exe).

### <span id="using_srcsrv_with_a_debugger"></span><span id="USING_SRCSRV_WITH_A_DEBUGGER"></span>Using SrcSrv with a Debugger

[SrcSrv](srcsrv.md) can be used with WinDbg, KD, NTSD, or CDB.

To use [SrcSrv](srcsrv.md) with the debugger, enter the following command to set the source path to srv\*.

```
.srcfix
```

You can get the same result by entering the following command.

```
.srcpath srv*
```

Setting the source path to srv\* tells the debugger that it should retrieve source files from locations specified in the target modules' symbol files.

If you want to use [SrcSrv](srcsrv.md) and also include a list of directories in your source path, use semicolons to separate `srv*` from any directories that are in the path.

For example:

```
.srcpath srv*;c:\someSourceCode 
```

If the source path is set as shown in the preceding example, the debugger first uses [SrcSrv](srcsrv.md) to retrieve source files from locations specified in the target modules' symbol files. If SrcSrv is unable to retrieve a source file, the debugger attempts to retrieve it from c:\\someSourceCode. Regardless of whether srv\* is the first element in the path or appears later, the debugger always uses SymSrv before it searches any other directories listed in the path.

You can also use [**.srcfix+**](-srcfix---lsrcfix--use-source-server-.md) to append `srv*` to your existing source path, as shown in the following example.

```
3: kd> .srcpath c:\mySource
Source search path is: c:\mySource
3: kd> .srcfix+
Source search path is: c:\mySource;SRV*
```

If a source file is retrieved by the source server, it will remain on your hard drive after the debugging session is over. Source files are stored locally in the src subdirectory of the home directory (unlike the symbol server, the source server does not specify a local cache in the `srv*` syntax itself). The home directory defaults to the debugger installation directory; it can be changed by using the [**!homedir**](-homedir.md) extension or by setting the DBGHELP\_HOMEDIR environment variable. If this subdirectory does not already exist, it will be created.

If you use the [**.open (Open Source File)**](-open--open-source-file-.md) command to open a new source file through [SrcSrv](srcsrv.md), you must include the -m Address parameter.

For information on how to index your sources, or if you plan to create your own source control provider module, see [SrcSrv](srcsrv.md).

### <span id="using_agestore_to_reduce_the_cache_size"></span><span id="USING_AGESTORE_TO_REDUCE_THE_CACHE_SIZE"></span>Using AgeStore to Reduce the Cache Size

Any source files downloaded by [SrcSrv](srcsrv.md) will remain on your hard drive after the debugging session is over. To control the size of the source cache, the AgeStore tool can be used to delete cached files that are older than a specified date, or to reduce the contents of the cache below a specified size. For details, see [AgeStore](agestore.md).

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Using%20a%20Source%20Server%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




