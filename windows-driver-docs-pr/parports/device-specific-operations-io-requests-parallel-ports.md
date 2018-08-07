---
title: Device-specific operations for I/O requests for parallel ports
author: windows-driver-content
description: Documents device-specific operations for I/O requests for parallel ports
keywords: ["Parallel ports WDK", "Parallel drivers WDK", "Parallel IRP codes"]
---

# Device-specific operations for I/O requests for parallel ports
This topic documents the following device-specific operations for I/O requests for parallel ports:

* [IRP_MJ_CREATE](#irp_mj_create)
* [IRP_MJ_INTERNAL_DEVICE_CONTROL](#irp_mj_internal_device_control)


## <a href="" id="irp_mj_create"></a> IRP_MJ_CREATE 
The [IRP_MJ_CREATE](https://msdn.microsoft.com/library/windows/hardware/ff550729) request opens a parallel port.

### When Sent
A client must use an [IRP_MJ_CREATE](https://msdn.microsoft.com/library/windows/hardware/ff550729) request to open a parallel port before it can access the port or a device connected to the port.

### Input Parameters
None.

### Output Parameters
None.

### I/O Status Block
The **Information** member is set to zero.

The **Status** member is set to one of the following values:


STATUS_SUCCESS
 
The parallel port was successfully opened.

STATUS_DELETE_PENDING 

The device is in the process of being removed by the Plug and Play manager.

### Operation
A parallel port is a shared device. When the system-supplied function driver for parallel ports receives an open request for an parallel port, it simply increments the count of open files on the parallel port.


## <a href="" id="irp_mj_internal_device_control"></a>  IRP_MJ_INTERNAL_DEVICE_CONTROL
The [IRP_MJ_INTERNAL_DEVICE_CONTROL](https://msdn.microsoft.com/library/windows/hardware/ff550766) request sets internal operating modes on a parallel port.

### When Sent
A client sends an internal device control request to do the following types of operations:

* Obtain information about the port
* Allocate the port or select a device on the port
* Set the communication mode

See [Internal Device Control Requests for Parallel Ports](https://msdn.microsoft.com/library/windows/hardware/ff543963).

### Input Parameters
The input is request-specific.

### Output Parameters
The output is request-specific.

### I/O Status Block
The Information member is request-specific. 

The Status member is set to a request-specific value or to one of the following generic status values:


STATUS_SUCCESS 

The request was completed successfully.

STATUS_CANCELLED 

The request was canceled.

STATUS_DELETE_PENDING 

The drive is in the process of being removed.

STATUS_INVALID_PARAMETER 

The system-supplied function driver for parallel ports does not support the request.

STATUS_PENDING 

The request is pending.

### Operation
The operation is request-specific.

## Related topics

[Internal Device Control Requests for Parallel Ports](https://msdn.microsoft.com/library/windows/hardware/ff543963)

[Operating a Parallel Device Attached to a Parallel Port](https://msdn.microsoft.com/windows/hardware/drivers/parports/operating-a-parallel-device-attached-to-a-parallel-port.md)

--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bprint\print%5D:%20Slicer%20settings%20%20RELEASE:%20%289/2/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default. "Send comments about this topic to Microsoft")