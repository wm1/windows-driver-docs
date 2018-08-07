---
title: IRP\_MN\_REGINFO
author: windows-driver-content
description: Drivers that support WMI on Microsoft Windows 98 and Microsoft Windows 2000 must handle this IRP.
ms.author: windowsdriverdev
ms.date: 08/12/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.assetid: db93b64b-a2e4-429d-850e-921fb438467c
keywords:
 - IRP_MN_REGINFO Kernel-Mode Driver Architecture
---

# IRP\_MN\_REGINFO


Drivers that support WMI on Microsoft Windows 98 and Microsoft Windows 2000 must handle this IRP. (Drivers that support Windows XP as well must also handle the [**IRP\_MN\_REGINFO\_EX**](irp-mn-reginfo-ex.md) IRP.) A driver can handle WMI IRPs either by calling [**WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834) or by handling the IRP itself, as described in [Handling WMI Requests](https://msdn.microsoft.com/library/windows/hardware/ff546968).

Major Code
----------

[**IRP\_MJ\_SYSTEM\_CONTROL**](irp-mj-system-control.md)
When Sent
---------

On Windows 98 and Windows 2000, WMI sends this IRP to query or update a driver's registration information after the driver has called [**IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480). On Windows XP and later, WMI sends the **IRP\_MN\_REGINFO\_EX** request instead.

WMI sends this IRP at IRQL = PASSIVE\_LEVEL in the context of a system thread.

## Input Parameters


**Parameters.WMI.ProviderId** points to the device object of the driver that should respond to the request. This pointer is located in the driver's I/O stack location in the IRP.

**Parameters.WMI.DataPath** is set to **WMIREGISTER** to query registration information or **WMIUPDATE** to update it.

**Parameters.WMI.BufferSize** indicates the maximum size of the nonpaged buffer at **Parameters.WMI.Buffer**. The size must be greater than or equal to the total of (**sizeof**(**WMIREGINFO**) + (*GuidCount* \* **sizeof**(**WMIREGGUID**)), where *GuidCount* is the number of data blocks and event blocks being registered by the driver, plus space for static instance names, if any.

## Output Parameters


If the driver handles WMI IRPs by calling [**WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834), WMI gets registration information for a driver's data blocks by calling its [*DpWmiQueryReginfo*](https://msdn.microsoft.com/library/windows/hardware/ff544097) routine.

Otherwise, the driver fills in a [**WMIREGINFO**](https://msdn.microsoft.com/library/windows/hardware/ff565832) structure at **Parameters.WMI.Buffer** as follows:

-   Sets **BufferSize** to the size in bytes of the **WMIREGINFO** structure plus associated registration data.

-   If the driver handles WMI requests on behalf of another driver, sets **NextWmiRegInfo** to the offset in bytes from the beginning of this **WMIREGINFO** to the beginning of another **WMIREGINFO** structure that contains registration information from the other driver.

-   Sets **RegistryPath** to the registry path that was passed to the driver's [**DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff544113) routine.

-   If **Parameters.WMI.Datapath** is set to **WMIREGISTER**, sets **MofResourceName** to the offset from the beginning of this **WMIREGINFO** to a counted Unicode string that contains the name of the driver's MOF resource in its image file.

-   Sets **GuidCount** to the number of data blocks and event blocks to register or update.

-   Writes an array of [**WMIREGGUID**](https://msdn.microsoft.com/library/windows/hardware/ff565827) structures, one for each data block or event block exposed by the driver, at **WmiRegGuid**.

The driver fills in each **WMIREGGUID** structure as follows:

-   Sets **Guid** to the GUID that identifies the block.

-   Sets **Flags** to provide information about instance names and other characteristics of the block. For example, if a block is being registered with static instance names, the driver sets **Flags** with the appropriate WMIREG\_FLAG\_INSTANCE\_*XXX* flag.

If the block is being registered with static instance names, the driver:

-   Sets **InstanceCount** to the number of instances.

-   Sets one of the following members to an offset in bytes to static instance name data for the block:
    -   If the driver sets **Flags** with WMIREG\_FLAG\_INSTANCE\_LIST, it sets **InstanceNameList** to an offset to a list of static instance name strings. WMI specifies instances in subsequent requests by index into this list.
    -   If the driver sets **Flags** with WMIREG\_FLAG\_INSTANCE\_BASENAME, it sets **BaseNameOffset** to an offset to a base name string. WMI uses this string to generate static instance names for the block.
    -   If the driver sets **Flags** with WMIREG\_FLAG\_INSTANCE\_PDO, it sets **Pdo** to an offset to a pointer to the PDO passed to the driver's [*AddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff540521) routine. WMI uses the device instance path of the PDO to generate static instance names for the block.
-   Writes the instance name strings, the base name string, or a pointer to the PDO at the offset indicated by **InstanceNameList**, **BaseName**, or **Pdo**, respectively.

If the driver handles WMI registration on behalf of another driver (such as a miniclass or miniport driver), it fills in another WMIREGINFO structure with the other driver's registration information and writes it at **NextWmiRegInfo** in the previous structure.

If the buffer at **Parameters.WMI.Buffer** is too small to receive all of the data, a driver writes the needed size in bytes as a ULONG to **Parameters.WMI.Buffer** and fails the IRP and returns STATUS\_BUFFER\_TOO\_SMALL.

## I/O Status Block


If the driver handles the IRP by calling [**WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834), WMI sets **Irp-&gt;IoStatus.Status** and **Irp-&gt;IoStatus.Information** in the I/O status block.

Otherwise, the driver sets **Irp-&gt;IoStatus.Status** to STATUS\_SUCCESS or to an appropriate error status such as the following:

STATUS\_BUFFER\_TOO\_SMALL

On success, a driver sets **Irp-&gt;IoStatus.Information** to the number of bytes written to the buffer at **Parameters.WMI.Buffer**.

Operation
---------

A driver can handle WMI IRPs either by calling [**WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834) or by handling the IRP itself, as described in [Handling WMI Requests](https://msdn.microsoft.com/library/windows/hardware/ff546968).

If a driver handles WMI IRPs by calling [**WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834), that routine calls the driver's [*DpWmiQueryReginfo*](https://msdn.microsoft.com/library/windows/hardware/ff544097) routine.

If a driver handles an **IRP\_MN\_REGINFO** request itself, it should do so only if **Parameters.WMI.ProviderId** points to the same device object as the pointer that the driver passed to [**IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480). Otherwise, the driver must forward the request to the next-lower driver.

Before handling the request, the driver must check **Parameters.WMI.DataPath** to determine whether WMI is querying registration information (**WMIREGISTER**) or requesting an update (**WMIUPDATE**).

WMI sends this IRP with WMIREGISTER after a driver calls **IoWMIRegistrationControl** with WMIREG\_ACTION\_REGISTER or WMIREG\_ACTION\_REREGISTER. In response, a driver should fill in the buffer at **Parameters.WMI.Buffer** with the following:

-   A [**WMIREGINFO**](https://msdn.microsoft.com/library/windows/hardware/ff565832) structure that indicates the driver's registry path, the name of its MOF resource, and the number of blocks to register.

-   One[**WMIREGGUID**](https://msdn.microsoft.com/library/windows/hardware/ff565827) structure for each block to register. If a block is to be registered with static instance names, the driver sets the appropriate WMIREG\_FLAG\_INSTANCE\_*XXX* flag in the **WMIREGGUID** structure for that block.

-   Any strings WMI needs to generate static instance names.

WMI sends this IRP with **WMIUPDATE** after a driver calls **IoWmiRegistrationControl** with WMIREG\_ACTION\_UPDATE\_GUIDS. In response, a driver should fill in the buffer at **Parameters.WMI.Buffer** with a WMIREGINFO structure as follows:

-   To remove a block, the driver sets WMIREG\_FLAG\_REMOVE\_GUID in its **WMIREGGUID** structure.

-   To add or update a block (for example, to change its static instance names), the driver clears WMIREG\_FLAG\_REMOVE\_GUID and provides new or updated registration values for the block.

-   To register a new or existing block with static instance names, the driver sets the appropriate WMIREG\_FLAG\_INSTANCE\_*XXX* and supplies any strings WMI needs to generate static instance names.

A driver can use the same **WMIREGINFO** structures to remove, add, or update blocks as it used initially to register all of its blocks, changing only the flags and data for the blocks to be updated. If a **WMIREGGUID** in such a **WMIREGINFO** structure matches exactly the **WMIREGGUID** passed by the driver when it first registered that block, WMI skips the processing involved in updating the block.

WMI does not send an **IRP\_MN\_REGINFO** request after a driver calls [**IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480) with WMIREG\_ACTION\_DEREGISTER, because WMI requires no further information from the driver. A driver typically deregisters its blocks in response to an [**IRP\_MN\_REMOVE\_DEVICE**](irp-mn-remove-device.md) request.

Requirements
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h (include Wdm.h, Ntddk.h, or Ntifs.h)</td>
</tr>
</tbody>
</table>

## See also


[*DpWmiQueryReginfo*](https://msdn.microsoft.com/library/windows/hardware/ff544097)

[**IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)

[**WMILIB\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff565813)

[**WMIREGGUID**](https://msdn.microsoft.com/library/windows/hardware/ff565827)

[**WMIREGINFO**](https://msdn.microsoft.com/library/windows/hardware/ff565832)

[**WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)

[**IRP\_MN\_REGINFO\_EX**](irp-mn-reginfo-ex.md)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bkernel\kernel%5D:%20IRP_MN_REGINFO%20%20RELEASE:%20%288/10/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


