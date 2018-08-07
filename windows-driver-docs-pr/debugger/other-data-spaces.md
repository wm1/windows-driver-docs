---
title: Other Data Spaces
description: Other Data Spaces
ms.assetid: f676a478-c02a-4400-8173-a1b3103c6c1b
keywords: ["Debugger Engine API, memory, data spaces"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Other Data Spaces


## <span id="ddk_other_data_spaces_dbx"></span><span id="DDK_OTHER_DATA_SPACES_DBX"></span>


In kernel-mode debugging, it is possible to read and write data to a variety of data spaces in addition to the main memory and registers. The following data spaces can be accessed:

<span id="System_Bus"></span><span id="system_bus"></span><span id="SYSTEM_BUS"></span>System Bus  
The methods [**ReadBusData**](https://msdn.microsoft.com/library/windows/hardware/ff553519) and [**WriteBusData**](https://msdn.microsoft.com/library/windows/hardware/ff561371) read and write system bus data.

<span id="Control-Space_Memory"></span><span id="control-space_memory"></span><span id="CONTROL-SPACE_MEMORY"></span>Control-Space Memory  
The methods [**ReadControl**](https://msdn.microsoft.com/library/windows/hardware/ff553524) and [**WriteControl**](https://msdn.microsoft.com/library/windows/hardware/ff561374) read and write control-space memory.

<span id="i_o_memory."></span><span id="I_O_MEMORY."></span>I/O Memory.  
The methods [**ReadIo**](https://msdn.microsoft.com/library/windows/hardware/ff553573) and [**WriteIo**](https://msdn.microsoft.com/library/windows/hardware/ff561402) read and write system and bus I/O memory.

<span id="Model_Specific_Register__MSR_"></span><span id="model_specific_register__msr_"></span><span id="MODEL_SPECIFIC_REGISTER__MSR_"></span>Model Specific Register (MSR)  
The methods [**ReadMsr**](https://msdn.microsoft.com/library/windows/hardware/ff554292) and [**WriteMsr**](https://msdn.microsoft.com/library/windows/hardware/ff561424) read and write MSRs, which are control registers that enable and disable features, and support debugging, for a particular model of CPU.

### <span id="handles"></span><span id="HANDLES"></span> Handles

In user-mode debugging, information about system objects can be obtained using system handles owned by a target process. The method [**ReadHandleData**](https://msdn.microsoft.com/library/windows/hardware/ff553542) can be used to read this information.

System handles for thread and process system objects can be obtained by using the [**GetCurrentThreadHandle**](https://msdn.microsoft.com/library/windows/hardware/ff545904) and [**GetCurrentProcessHandle**](https://msdn.microsoft.com/library/windows/hardware/ff545816) methods. These handles are also provided to the [**IDebugEventCallbacks::CreateThread**](https://msdn.microsoft.com/library/windows/hardware/ff550713) and [**IDebugEventCallbacks::CreateProcess**](https://msdn.microsoft.com/library/windows/hardware/ff550697) callback methods when create-thread and create-process debugging event occur.

**Note**   In kernel mode, the process and thread handles are artificial handles. They are not system handles.

 

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Other%20Data%20Spaces%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




