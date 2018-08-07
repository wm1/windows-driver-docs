---
title: Handling Notifications
author: windows-driver-content
description: Handling Notifications
ms.assetid: ace7f59d-fe9f-4810-91db-2cf20c9591cf
keywords: ["filtering registry calls WDK kernel , notification options", "registry filtering drivers WDK kernel , notification options", "notifications WDK filter registry call", "filtering registry calls WDK kernel , monitoring calls", "registry filtering drivers WDK kernel , monitoring calls", "filtering registry calls WDK kernel , blocking calls", "registry filtering drivers WDK kernel , blocking calls", "filtering registry calls WDK kernel , modifying calls", "registry filtering drivers WDK kernel , modifying calls", "blocking calls WDK filter registry call", "monitoring registry calls"]
ms.author: windowsdriverdev
ms.date: 06/16/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Handling Notifications


The [*RegistryCallback*](https://msdn.microsoft.com/library/windows/hardware/ff560903) routine receives a pointer to a **REG\_*XXX*\_KEY\_INFORMATION** structure that contains information about the registry operation that is occurring.

The *RegistryCallback* routine can monitor, block, or modify a registry operation.

### Monitoring Registry Calls

If a registry filtering driver is monitoring registry operations, its *RegistryCallback* routine can update counters or perform other bookkeeping operations and then return STATUS\_SUCCESS. Whenever a *RegistryCallback* routine returns STATUS\_SUCCESS, the configuration manager continues performing the registry operation.

Monitoring registry calls is supported in Windows XP and later versions of Windows.

### Blocking Registry Calls

A registry filtering driver can block registry operations if its *RegistryCallback* routine returns a status value for which [NT\_SUCCESS](using-ntstatus-values.md)(*status*) equals **FALSE** (that is, a non-success NTSTATUS value). When the configuration manager receives a non-success return value, it immediately returns to the calling thread with the driver-specified status value. Therefore, a registry filtering driver can use pre-notifications to prevent registry operations from being processed.

If a *RegistryCallback* routine returns a status value for which NT\_SUCCESS(*status*) equals **FALSE** for a pre-notification, the operation's post-notification callback does not occur.

Blocking registry calls is supported in Windows XP and later versions of Windows. For Windows Vista and later, the driver can modify the values that the registry operation returns to the calling thread. These values are contained in the **REG\_*XXX*\_KEY\_INFORMATION** structures for Windows Vista and later.

### Modifying Registry Calls

A registry filtering driver can modify a registry operation's output parameters or return value. Additionally, the driver can completely process a registry operation instead of allowing the registry to handle the operation.

When a registry filtering driver's *RegistryCallback* routine receives a post-notification, it can:

-   Modify the output parameters that its **REG\_*XXX*\_KEY\_INFORMATION** structure contains and then return STATUS\_SUCCESS. The configuration manager returns the modified output parameters to the calling thread.

    Modifying output parameters is supported in Windows Vista and later.

-   Modify the registry operation's return value by providing a status value for the **ReturnStatus** member of the [**REG\_POST\_OPERATION\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff560971) structure and then returning STATUS\_CALLBACK\_BYPASS. The configuration manager returns the specified return value to the calling thread.

    **Note**  If the driver changes a status code from success to failure, it might have to deallocate objects that the configuration manager allocated. Alternatively, if the driver changes a status code from failure to success, it might have to provide appropriate output parameters.

     

    Modifying return values is supported in Windows Vista and later.

When a registry filtering driver's *RegistryCallback* routine receives a pre-notification, the routine can handle the registry operation itself and then return STATUS\_CALLBACK\_BYPASS. When the registry receives STATUS\_CALLBACK\_BYPASS from the driver, it just returns STATUS\_SUCCESS to the calling thread and does not process the operation. The driver preempts the registry operation and must completely handle it, and the driver must be careful to return valid output values in the **REG\_*XXX*\_KEY\_INFORMATION** structure.

Drivers can preempt registry operations in Windows Vista and later.

If a *RegistryCallback* routine returns STATUS\_CALLBACK\_BYPASS for a pre-notification, the operation's post-notification callback does not occur.

**Note**  Several registry system calls are not documented because they are rarely used, and, when they are used, it is usually to achieve some unconventional result in the registry. Modifying the operations performed by these calls is difficult and error-prone. Driver developers are discouraged from trying to modify the following registry system calls:
-   **NtRestoreKey**
-   **NtSaveKey**
-   **NtSaveKeyEx**
-   **NtLoadKeyEx**
-   **NtUnloadKey2**
-   **NtUnloadKeyEx**
-   **NtReplaceKey**
-   **NtRenameKey**
-   **NtSetInformationKey**

 

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bkernel\kernel%5D:%20Handling%20Notifications%20%20RELEASE:%20%286/14/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


