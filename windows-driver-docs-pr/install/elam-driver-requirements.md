---
title: ELAM Driver Requirements
description: Driver installation must use existing tools for online and offline installation, registering a driver through typical INF processing.
ms.assetid: B00B4361-B531-4D28-A521-0F8B3B48CEA4
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# ELAM Driver Requirements


Driver installation must use existing tools for online and offline installation, registering a driver through typical INF processing.  For sample ELAM driver code, please see the following:
https://github.com/Microsoft/Windows-driver-samples/tree/master/security/elam 

## AM Driver Installation


To ensure driver install compatibility, an ELAM driver advertises itself as a boot-start driver similar to all other boot-start drivers. The INF sets the start type to SERVICE\_BOOT\_START (0), which indicates that the driver should be loaded by the boot loader and initialized during kernel initialization. An ELAM Driver advertises its group as “Early-Launch”. The early launch behavior for drivers in this group will be implemented in Windows, as described in the next section.

The following is an example of the driver install section of an ELAM driver INF.

```
[SampleAV.Service]
DisplayName    = %SampleAVServiceName%
Description    = %SampleAVServiceDescription%
ServiceType    = 1       ; SERVICE_KERNEL_DRIVER
StartType      = 0       ; SERVICE_BOOT_START
ErrorControl   = 3       ; SERVICE_ERROR_CRITICAL
LoadOrderGroup = “Early-Launch”
```

Because an AM driver does not own any devices, it is necessary to install the AM driver as a Legacy so the driver is only added as a service into the registry. (If the AM driver is installed as a normal PNP driver, it will be added to the enum section of the registry and therefore will have a PDO reference, which will lead to unwanted behavior when unloading the driver.)

## Backup Driver Installation


To provide a recovery mechanism in the event that the ELAM driver is inadvertently corrupted, the ELAM installer also installs a copy of the driver in a backup location. This will allow WinRE to retrieve the clean copy and recover the installation.

The installer reads the backup file location from the **BackupPath** key stored in

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\EarlyLaunch
```

The installer then places the backup copy in the folder specified in the regkey.
## AM Driver Initialization


The Windows boot loader, Winload, loads all boot-start drivers and their dependent DLLs into memory prior to handoff to the Windows kernel. The boot-start drivers represent the device drivers that need to be initialized before the disk stack has been initialized. These drivers include, among others, the disk stack and volume manager, and file system driver and bus drivers for the operating system device.

## AM Driver Callback Interface


The kernel PnP manager provides new callback functionality to ELAM drivers. Existing registry callbacks are also available. The ELAM drivers can use the callbacks to provide the PnP manager with a description of every boot image (driver and dependent DLL), and it can classify every boot image as a known good binary, known bad binary, or an unknown binary. Using operating system policy and the classification provided by the AM driver, PnP either initializes the boot image or skips the initialization of the boot image.

**Registry Callbacks**

The Early Launch drivers can use registry callbacks to monitor and validate the configuration data used as input for each boot-start driver. The configuration data is stored in the System registry hive, which is loaded by Winload and is available at the time of boot driver initialization. These callbacks are valid through the lifetime of the ELAM driver and will be unregistered when the driver is unloaded. The callback functions, [**CmRegisterCallbackEx**](https://msdn.microsoft.com/library/windows/hardware/ff541921), [**CmRegisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff541918), and [**CmUnRegisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff541928), as well as the associated type and structure definitions, are documented on MSDN.

**Boot Driver Callbacks**

The PnP manager exposes new callbacks to ELAM drivers. The callbacks enable an AM driver to classify every boot-start driver and dependent DLL as known good, known bad, or unknown. The PnP manager uses the classification with operating system policy to decide whether a boot-start driver or dependent DLL should be initialized. By default, known bad drivers and DLLs are not initialized. Policy can be configured to load known bad images or to not initialize unknown images. The operating system policy can be configured and is measured by Winload as part of boot attestation. The same callback is also used to provide status updates from Windows to an ELAM driver, including when all boot-start drivers have been initialized and the callback facility is no longer functional. All callback functions, types, and structures are documented on MSDN.

**Callback Registration**

The ELAM driver can use the [**IoRegisterBootDriverCallback**](https://msdn.microsoft.com/library/windows/hardware/hh439379) and [**IoUnRegisterBootDriverCallback**](https://msdn.microsoft.com/library/windows/hardware/hh439394) functions to register and unregister for the boot driver callbacks.

**Callback Function**

The Boot Driver Callback Facility leverages the EX Callback interface defined in the WDK and documented on MSDN. The format of the callback function shares its definition with [**EX\_CALLBACK\_FUNCTION**](https://msdn.microsoft.com/library/windows/hardware/ff560903), receiving a pointer to a context structure registered with the API as the first input parameter and receiving a callback type and a system-provided context structure for the specific callback type.

An error returned from a status update callback is treated as a fatal error and leads to a system bug check. This provides an ELAM driver the ability to indicate when a state is reached outside of AM policy. For example, if an AM runtime driver was not loaded and initialized, the Early Launch driver can fail the prepare-to-unload callback to prevent Windows from entering a state without an AM driver loaded.

An image is treated as unknown when an error is returned from the initialize image callback. Unknown drivers are initialized or have their initialization skipped based on OS policy.

The [**BDCB\_CALLBACK\_TYPE enumeration**](https://msdn.microsoft.com/library/windows/hardware/hh406352) describes two types of callbacks:

-   Callbacks that provide status updates to an ELAM driver (BdCbStatusUpdate)
-   Callbacks used by the AM driver to classify boot-start drivers and dependent DLLs before initializing their images (BdCbInitializeImage)

The two callback types have unique context structures that provide additional information specific to the callback. The context structure for the status update callback contains a single enumerated type describing the Windows callout. The context structure for the initialize image callback is more complex, containing hash and certificate information for each loaded image. The structure additionally contains a field that is treated as an output parameter, where the AM driver writes the classification type for the driver.

## Malware Signatures


The malware signature data is determined by the AM ISV, but should include, at a minimum, an approved list of driver hashes. The signature data is stored in the registry in a new “Early Launch Drivers” hive under HKLM that is loaded by Winload. Each AM driver has a unique key in which to store their signature binary large object (BLOB). The registry path and key has the format:

```
HKLM\ELAM\\<VendorName>\
```

Within the key, the vendor is free to define and use any of the values.
There are three defined binary blob values that are measured by Measured Boot, and the vendor may use each:

-   Measured
-   Policy
-   Config

The ELAM hive is unloaded after its use by Early Launch Antimalware for performance. If a user mode service wants to update the signature data, it should mount the hive file from the file location \\Windows\\System32\\config\\ELAM. The storage and retrieval format of these data BLOBs is left up to the ISV, but the signature data must be signed so that the AM driver can verify the integrity of the data.

**Verifying Malware Signatures**

The method for verifying the integrity of the malware signature data is left up to each AM ISV. The [CNG Cryptographic Primitive Functions](https://msdn.microsoft.com/library/windows/desktop/aa833130) are available to assist in verifying digital signatures and certificates on the malware signature data.

**Malware Signature Failure**

If the ELAM driver checks the integrity of the signature data, and that check fails, or if there is no signature data, the initialization of the ELAM driver still succeeds. In this case, for each boot driver the ELAM driver must return “unknown” for each initialization callback. Additionally, the ELAM driver should pass this information onto the runtime AM component once it has started.

## Unloading the AM Driver


When the callback StatusType is BdCbStatusPrepareForUnload, this is an indication to the AM driver that all boot drivers have been initialized and that the AM driver should prepare to be unloaded. Before unloading, the early launch AM driver needs to deregister its callbacks. Deregistration cannot happen during a callback; rather, it has to happen in the DriverUnload function, which a driver can specify during DriverEntry.

To maintain continuity in malware protection and to ensure proper handoff, the runtime AM engine should be started prior to the early launch AM driver being unloaded. This means that the runtime AM engine should be a boot driver that is verified by the early launch AM driver.

## Performance


The driver must meet the performance requirements defined in the following table:

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Scenario(s)</p></td>
<td align="left"><p>Start Time</p></td>
<td align="left"><p>End Time</p></td>
<td align="left"><p>Upper Bound</p></td>
</tr>
<tr class="even">
<td align="left"><p>Evaluate loaded boot critical driver before allowing it to initialize. This also includes status update callbacks.</p></td>
<td align="left"><p>Kernel calls back to antimalware driver to evaluate loaded boot critical driver.</p></td>
<td align="left"><p>Antimalware driver returns evaluation result.</p></td>
<td align="left"><p>0.5ms</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Evaluate all loaded boot critical drivers</p></td>
<td align="left"><p>Kernel calls back to antimalware driver to evaluate the first loaded boot critical driver.</p></td>
<td align="left"><p>Antimalware driver returns evaluation result for last boot critical driver.</p></td>
<td align="left"><p>50 ms</p></td>
</tr>
<tr class="even">
<td align="left"><p>Footprint (driver + configuration data in memory)</p></td>
<td align="left"><p>N/A</p></td>
<td align="left"><p>N/A</p></td>
<td align="left"><p>128kB</p></td>
</tr>
</tbody>
</table>

 

## Initializing Drivers


Once the boot drivers are evaluated by the ELAM driver, the Kernel uses the classification returned by ELAM to decide whether to initialize the driver. This decision is dictated by policy and is stored here in the registry at:

```
HKLM\System\CurrentControlSet\Control\EarlyLaunch\DriverLoadPolicy
```

This can be configured through Group Policy on a domain-joined client. An antimalware solution may want to expose this functionality to the end user in nonmanaged scenarios. The following values are defined for DriverLoadPolicy:
```
PNP_INITIALIZE_DRIVERS_DEFAULT 0x0  (initializes known Good drivers only)
PNP_INITIALIZE_UNKNOWN_DRIVERS 0x1  
PNP_INITIALIZE_BAD_CRITICAL_DRIVERS 0x3 (this is the default setting)
PNP_INITIALIZE_BAD_DRIVERS 0x7
```

## Boot Failures


If a boot driver is skipped due to the initialization policy, the Kernel continues to attempt to initialize the next boot driver in the list. This continues until either the drivers are all initialized, or the boot failed because a boot driver that was skipped was critical to the boot. If the crash occurs after the disk stack is started, then there is a crash dump, and it contains some information about the reason or the crash, to include information about missing drivers. This can be used in WinRE to determine the cause of the failure and to attempt to remediate.

## ELAM Driver Backup


When the ELAM driver is installed, a backup copy of the driver must also be installed. The back-up location will be stored in the **BackupPath** key stored in

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\EarlyLaunch
```

In the event of a failure to load or initialize the primary driver due to a corruption, WinRE looks in this location to restore the driver from the backup copy.

## ELAM and Measured Boot


If the ELAM driver detects a policy violation (a rootkit, for example), it can invalidate the PCRs that indicated that the system was in a good state by using the Tbsi\_Revoke\_Attestation() function:

```
TBS_RESULT WINAPI
Tbsi_Revoke_Attestation();
```

**Parameters**:

None

**Return value**:

If the function succeeds, the function returns TBS\_SUCCESS (0).

**Remarks**:

This function extends PCR by an unspecified value and increments the event counter in the TPM. Both actions are necessary, so the trust is broken in all quotes that are created from here forward. As a result, the Measured Boot logs will not reflect the current state of the TPM for the remainder of the time that the TPM is powered up, and remote systems will not be able to form trust in the security state of the system.

 

 





