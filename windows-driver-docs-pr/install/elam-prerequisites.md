---
title: ELAM Prerequisites
description: Early Launch Antimalware drivers must adhere to the following program requirements to be signed by WHQL and loaded by Windows.
ms.assetid: 48759EB3-F8F9-4881-BD30-6D1252F08DFE
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# ELAM Prerequisites


Early Launch Antimalware drivers must adhere to the following program requirements to be signed by **WHQL** and loaded by Windows.

## Antimalware Vendor Participation Requirements


Microsoft requires that Early Launch Antimalware vendors either be members of the [**Microsoft Virus Initiative (MVI)**](https://www.microsoft.com/en-us/wdsi/alliances/virus-initiative) or pre-approved members of the [**Virus Information Alliance (VIA)**](https://www.microsoft.com/en-us/wdsi/alliances/virus-information-alliance). This membership ensures that the vendors are active antimalware community participants with a positive industry reputation. Please reach out to [**mvi@microsoft.com**](mailto:mvi@microsoft.com) if you have questions about ELAM driver signing or becoming a pre-approved VIA member.

## Hardware Certification Kit Tests


Each driver targeting a pre-Windows 10 operating system must pass the following HCK tests, which are administered by the ISV:

PERFORMANCE TEST
-   CALLBACK LATENCY - Each early launch AM driver is required to return the driver verification callbacks from the kernel within .5ms. This time is measured from when the kernel issues the callback to the driver to the time the driver returns the callback.
-   MEMORY ALLOCATION - Each early launch AM driver is required to limit its footprint in memory to 128 KB, for both the driver image as well as its configuration (signature) data.
-   UNLOAD BLOCKING - Each early launch AM driver receives a synchronous callback after the last boot driver has been initialized, which indicates that the AM driver will be unloaded. The AM driver can use this as an indication that it needs to do “cleanup” and save any status information that can be used by the runtime AM driver. However, the early launch AM driver must return the callback for the driver to be unloaded and for boot to continue.

SIGNATURE DATA TEST - Each early launch AM driver must get its malware signature data from a single, well-known location and no other. This allows measurement and protection of that data by Windows. This test ensures that each AM driver only reads its configuration data from the registry hive that is created for that driver.
BACKUP DRIVER TEST - The early launch AM driver, upon installation, must also install a backup copy of the driver to the backup driver store. This requirement is to help with remediation in the case that the primary driver gets corrupted. This test ensures that for an installed early launch AM driver, there is a corresponding driver in the backup store.
## Signed Binaries


Each driver .sys file must be code signed by Microsoft, using a special certificate indicating that it is an Early Launch AM Driver.

## Driver Binaries


The AM driver must be a single binary (not import any other DLLs).

## Windows Hardware Quality Lab (WHQL) submission

-   Submit your driver for verification as documented at [ELAM Driver Submission](elam-driver-submission.md)
-   The **WHQL** process will verify that the vendor is permitted to submit early launch drivers.  Your submission will fail if you are not an MVI member, or a pre-approved VIA member.

 

 





