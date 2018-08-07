---
title: Using the _analysis_assume Function to Suppress False Defects
description: Using the _analysis_assume Function to Suppress False Defects
ms.assetid: eb71a664-ada5-44e3-b75d-b1a7348b115f
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Using the \_analysis\_assume Function to Suppress False Defects


You can provide Static Driver Verifier (SDV) with additional information about your driver source code so that during verification you can suppress the reports of false defects. The false defects occur when SDV reports an apparent rule violation, but in a situation where the driver is acting correctly.

To provide SDV with this additional information, use the **\_\_analysis\_assume** function. The function has the following syntax:

```
__analysis_assume( expression ) 
```

Where *expression* can be any expression that is assumed to evaluate to **true**.

When you use this function, SDV assumes that the condition represented by the *expression* is **true** at the point where the **\_\_analysis\_assume** function appears. The **\_\_analysis\_assume** function is only used by the static analysis tools. The function is ignored by the compiler.

If you use **\_\_analysis\_assume**, it is critically important that you are certain of the validity of the assumption you are making. If it turns out that your assumption is **false**, either now or in the future, you could be suppressing a true defect. We recommend that you always add a comment to your code that explains why you are using the **\_\_analysis\_assume** function. If you cannot write a reason for the assumption, do not suppress the defect.

You should add the **\_\_analysis\_assume** function as needed, whenever you find false defects that you can safely suppress.

### <span id="examples"></span><span id="EXAMPLES"></span>Examples

In the following code example, the KMDF rule [RequestCompletedLocal](https://msdn.microsoft.com/library/windows/hardware/ff551609) reports a defect. This is a false defect because SDV cannot correctly interpret the **switch** statement and consequently does not enter the branch where the request is completed.

In this **switch** statement, there are six possible cases. The driver has defined six IOCTL codes, so the driver will definitely take one of the branches. If one of the branches is taken, the request is completed successfully.

```
VOID
PortIOEvtIoDeviceControl(
      __in WDFQUEUE     Queue,
      __in WDFREQUEST   Request,
      __in size_t       OutputBufferLength,
  __in size_t       InputBufferLength,
  __in ULONG        IoControlCode
     )
 
     PDEVICE_CONTEXT devContext = NULL;
     WDFDEVICE device;

     PAGED_CODE();
 
     device = WdfIoQueueGetDevice(Queue);
 
     devContext = PortIOGetDeviceContext(device);
 
     switch(IoControlCode)
         case IOCTL_GPD_READ_PORT_UCHAR:
         case IOCTL_GPD_READ_PORT_USHORT:
         case IOCTL_GPD_READ_PORT_ULONG:
             PortIOIoctlReadPort(devContext,
                                 Request,
                                 OutputBufferLength,
                                 InputBufferLength,
                                 IoControlCode);
             break;

 
         case IOCTL_GPD_WRITE_PORT_UCHAR:
         case IOCTL_GPD_WRITE_PORT_USHORT:
         case IOCTL_GPD_WRITE_PORT_ULONG:    
             PortIOIoctlWritePort(devContext,
                                  Request,
                                  OutputBufferLength,
                                  InputBufferLength,
                                  IoControlCode);
             break;
 
     }
 
}
```

To safely suppress the false defect, use the **\_\_analysis\_assume** function to specify that the *IoControlCode* is guaranteed to be one of the IOCTLs that the driver has defined.

```
VOID
PortIOEvtIoDeviceControl(
      __in WDFQUEUE     Queue,
      __in WDFREQUEST   Request,
      __in size_t       OutputBufferLength,
      __in size_t       InputBufferLength,
      __in ULONG        IoControlCode
     )
 
     PDEVICE_CONTEXT devContext = NULL;
     WDFDEVICE device;

     PAGED_CODE();
 
     device = WdfIoQueueGetDevice(Queue);
 
     devContext = PortIOGetDeviceContext(device);

/* Use __analysis_assume to suppress a false defect for the SDV RequestCompletedLocal rule. 
There are only 6 possible IOCTLs for IoControlCode; each case is covered in the switch statement.
*/

 __analysis_assume( IoControlCode == IOCTL_GPD_READ_PORT_UCHAR || \
                       IoControlCode == IOCTL_GPD_READ_PORT_USHORT|| \
                       IoControlCode == IOCTL_GPD_READ_PORT_ULONG || \
                       IoControlCode == IOCTL_GPD_WRITE_PORT_UCHAR|| \
                       IoControlCode == IOCTL_GPD_WRITE_PORT_USHORT|| \
                       IoControlCode == IOCTL_GPD_WRITE_PORT_ULONG);

     switch(IoControlCode)
         case IOCTL_GPD_READ_PORT_UCHAR:
         case IOCTL_GPD_READ_PORT_USHORT:
         case IOCTL_GPD_READ_PORT_ULONG:
             PortIOIoctlReadPort(devContext,
                                 Request,
                                 OutputBufferLength,
                                 InputBufferLength,
                                 IoControlCode);
             break;

 
         case IOCTL_GPD_WRITE_PORT_UCHAR:
         case IOCTL_GPD_WRITE_PORT_USHORT:
         case IOCTL_GPD_WRITE_PORT_ULONG:    
             PortIOIoctlWritePort(devContext,
                                  Request,
                                  OutputBufferLength,
                                  InputBufferLength,
                                  IoControlCode);
             break;
 
     }
 
}
```

For another example of how you can use **\_\_analysis\_assume**, see the example code that is used in [Using \_\_sdv\_save\_request and \_\_sdv\_retrieve\_request for Deferred Procedure Calls](using---sdv-save-request-and---sdv-retrieve-request-for-deferred-proce.md). The example shows how to use **\_\_sdv\_save\_request** and **\_\_sdv\_retrieve\_request** for DPCs (workitems, Timers and so on). The **\_\_analysis\_assume** function is used to suppress false defects that might otherwise result.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[devtest\devtest]:%20Using%20the%20_analysis_assume%20Function%20to%20Suppress%20False%20Defects%20%20RELEASE:%20%2811/17/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




