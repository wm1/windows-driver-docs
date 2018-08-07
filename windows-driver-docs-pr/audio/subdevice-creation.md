---
title: Subdevice Creation
description: Subdevice Creation
ms.assetid: e4ba1209-adc6-48c3-9633-247e9e3849bc
keywords:
- audio adapters WDK , subdevices
- adapter drivers WDK audio , subdevices
- subdevices WDK audio
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Subdevice Creation


## <span id="subdevice_creation"></span><span id="SUBDEVICE_CREATION"></span>


The term *subdevice* is used to describe the binding of the four components that are listed in the following table.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Component</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Miniport object</p></td>
<td align="left"><p>An object that exposes the miniport driver's IMiniport<em>Xxx</em> interface</p></td>
</tr>
<tr class="even">
<td align="left"><p>Port object</p></td>
<td align="left"><p>An object that exposes the port driver's IPort<em>Xxx</em> interface</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Resource list object</p></td>
<td align="left"><p>An object containing a list of adapter driver resources that are assigned to the subdevice</p></td>
</tr>
<tr class="even">
<td align="left"><p>Reference string</p></td>
<td align="left"><p>A name added to the device path name to specify a subdevice during filter creation</p></td>
</tr>
</tbody>
</table>

 

A subdevice's IMiniport*Xxx* and IPort*Xxx* interfaces inherit from base interfaces [IMiniport](https://msdn.microsoft.com/library/windows/hardware/ff536698) and [IPort](https://msdn.microsoft.com/library/windows/hardware/ff536842), respectively.

The PortCls system driver does not distinguish between the port driver and the miniport driver. It simply requires an object, such as the port object, with an interface that can handle system-generated requests.

Similarly, PortCls is not directly involved in managing resources. It only needs to bind the request handler (the port driver) to a resource list. The adapter driver is responsible for binding the port, miniport, and resource list objects together.

The following code example shows how the adapter driver performs these actions:

```
  //
  // Instantiate the port by calling a function supplied by PortCls.
  //
  PPORT    port;
  NTSTATUS ntStatus = PcNewPort(&port, PortClassId);

  if (NT_SUCCESS(ntStatus))
  {
      PUNKNOWN miniport;
      //
      // Create the miniport object.
      //
      if (MiniportCreate)   // a function to create a proprietary miniport
      {
          ntStatus = MiniportCreate(&miniport,
                                    MiniportClassId, NULL, NonPagedPool);
      }
      else   // Ask PortCls for one of its built-in miniports.
      {
          ntStatus = PcNewMiniport((PMINIPORT*)&miniport,
                                   MiniportClassId);
      }

      if (NT_SUCCESS(ntStatus))
      {
          //
          // Bind the port, miniport, and resources.
          //
          ntStatus = port->Init(DeviceObject,
                                Irp, miniport, UnknownAdapter, ResourceList);
          if (NT_SUCCESS(ntStatus))
          {
              //
              // Hand the port driver and the reference
              // string to PortCls.
              //
              ntStatus = PcRegisterSubdevice(DeviceObject,
                                             Name, port);
          }

          //
          // We no longer need to reference the miniport driver.
          // Either the port driver now references it,
          // or binding failed and it should be deleted.
          //
          miniport->Release();
      }

      //
      // Release the reference that existed when PcNewPort() gave us
      // the pointer in the first place. This reference must be released
      // regardless of whether the binding of the port and miniport
      // drivers succeeded.
      //
      port->Release();
  }
```

For information about the PortCls function calls in the preceding code example, see [**PcNewPort**](https://msdn.microsoft.com/library/windows/hardware/ff537715), [**PcNewMiniport**](https://msdn.microsoft.com/library/windows/hardware/ff537714), and [**PcRegisterSubdevice**](https://msdn.microsoft.com/library/windows/hardware/ff537731).

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[audio\audio]:%20Subdevice%20Creation%20%20RELEASE:%20%287/18/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


