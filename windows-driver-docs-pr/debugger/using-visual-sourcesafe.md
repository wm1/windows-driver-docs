---
title: Using Visual SourceSafe
description: Using Visual SourceSafe
ms.assetid: a315a1c5-1427-4432-aec0-314dbb6d7ae5
keywords: ["Visual SourceSafe", "source servers, Visual SourceSafe", "SrcSrv, Visual SourceSafe", "Visual SourceSafe, SrcSrv", "Visual SourceSafe, overview"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Using Visual SourceSafe


Visual SourceSafe is an x86-based application, and the source indexing scripts and tools associated with it are installed only with the x86 package of Debugging Tools for Windows.

To successfully use Visual SourceSafe with SrcSrv, several defaults must be set in the system, including the Visual SourceSafe default database, the current project, and the working folder. You must also stamp each build project with a label so that Visual SourceSafe can differentiate between versions of a given file. Finally, you must set up any credentials needed to access the Visual SourceSafe database.

### <span id="visual_sourcesafe_database"></span><span id="VISUAL_SOURCESAFE_DATABASE"></span>Visual SourceSafe Database

The default Visual SourceSafe database can be set with the SSDIR environment variable. If it is not set there, the SrcSrv indexing script can usually determine this from the registry. If it cannot, the script prompts you to set SSDIR. Regardless, this database value must be listed in your [Srcsrv.ini](the-srcsrv-ini-file.md) file along with a simple alias to identify the database. More instructions can be found in the comments in Srcsrv.ini. You should add the entry in the variables section of Srcsrv.ini using the following syntax:

```
MYDATABASE=\\server\VssShare
```

### <span id="current_project"></span><span id="CURRENT_PROJECT"></span>Current Project

Visual SourceSafe uses the concept of a *current project*. The SrcSrv indexing script respects this value and limits processing to those source files that are part of the current project. To display the current project, use the following command:

```
ss.exe project
```

To change the current project, use the following command:

```
ss.exe cp Project
```

where *Project* indicates the current project. For example, to process all projects, set the current project to the root:

```
ss.exe cp $/
```

### <span id="working_folder"></span><span id="WORKING_FOLDER"></span>Working Folder

Visual SourceSafe projects are associated with *working folders*. A working folder is the location on the client computer that corresponds to the root of a project. However it is possible for such a computer to obtain and build source without a working folder being specified, usually when creating projects through the Visual Studio interface or by using the command:

```
ss.exe get -R
```

However, this mode of operation is incompatible with SrcSrv indexing. SrcSrv requires that a working folder be specified. To set the working folder, use the command:

```
ss.exe workfold Project Folder
```

where *Project* indicates the current project and *Folder* indicates the location corresponding to the root of the project.

### <span id="labels"></span><span id="LABELS"></span>Labels

Visual SourceSafe cannot determine what version of a file exists within the working directory of a build machine. Consequently, you must use labels to stamp the project with an identifier that is used to extract source files on the debugger client. Thus, before indexing, you must verify that all changes are checked into the database and then apply a label to the project. Labels can be applied using the command:

```
ss.exe label Project
```

where *Project* indicates the current project.

In the following example, the label "VERSION\_3" is applied to a project called "$/sdktools":

```
E:\nt\user>ss.exe label $/sdktools
 Label for $/sdktools: VERSION_3
 Comment for $/sdktools:
 This is a comment.
```

After the label is applied, you can specify this label to the SrcSrv indexing script by setting the environment variable, SSLABEL, or by passing it as a command-line parameter, as in the following example:

```
vssindex.cmd -label=VERSION_3
```

Again, this label is required for SrcSrv indexing to work. Note that if you pass a label that does not exist in the project, it can take a long time for the script to complete and the results are of no use.

### <span id="credentials"></span><span id="CREDENTIALS"></span>Credentials

If your Visual SourceSafe database requires a user and optional password for access, these values must be set through the SSUSER and SSPWD environment variables. This applies not only at the time the build is indexed, but also on the debugger client.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Using%20Visual%20SourceSafe%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




