---
title: Handling SRB_FUNCTION_IO_CONTROL
author: windows-driver-content
description: Handling SRB_FUNCTION_IO_CONTROL
ms.assetid: 92d09a49-d8e8-4d97-b334-c42d5b04ee8d
keywords:
- SCSI miniport drivers WDK storage , HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_IO_CONTROL
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Handling SRB\_FUNCTION\_IO\_CONTROL


## <span id="ddk_handling_srb_function_io_control_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_IO_CONTROL_KG"></span>


Whether a miniport driver handles SRB\_FUNCTION\_IO\_CONTROL requests depends on whether the HBA is to provide dedicated support for a user-mode application. Supporting this request allows a set of driver-defined ("private") I/O control requests to be sent directly to the miniport driver. For SRBs with the **Function** member set to SRB\_FUNCTION\_IO\_CONTROL, the **DataBuffer** member contains a pointer to a system-defined SRB\_IO\_CONTROL structure containing the driver-defined and application-specified **ControlCode**.

All system-defined, required device I/O control requests sent to NT-based operating system storage class drivers are mapped to SRBs with the **Function** member set to SRB\_FUNCTION\_EXECUTE\_SCSI, not to SRB\_FUNCTION\_IO\_CONTROL.

 

 


--------------------


