---
Description: This article shows how to send commands and receive change notifications from audio device modules. from a Universal Windows Platform (UWP) app.
ms.assetid: AA053196-F331-4CBE-B032-4E9CBEAC699C
title: Configure and query audio device modules
label: Configure and query audio device modules
template: 
ms.author: drewbat
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10, uwp
---

# Configure and query audio device modules 

This article shows how to send commands and receive change notifications from audio device modules from a UWP app. An audio device module may be a hardware effect processing unit or any other audio configuration module defined by an audio driver. This feature was designed to enable module providers to create UWP apps that allow users to control and get status information from an audio processing module running in a DSP. In order to use the audio device module APIs shown in this article, you must specify the restricted *audioDeviceConfiguration* capability in your app package manifest.

## Get an instance of the AudioDeviceModulesManager class
All audio device module operations shown in this article begin by obtaining an instance of the **[AudioDeviceModulesManager](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulesmanager)**. Do this by first calling the static **[GetDefaultAudioRenderId](https://docs.microsoft.com/uwp/api/windows.media.devices.mediadevice#Windows_Media_Devices_MediaDevice_GetDefaultAudioRenderId_Windows_Media_Devices_AudioDeviceRole_)** method of the **[MediaDevice](https://docs.microsoft.com/uwp/api/windows.media.devices.mediadevice)** class. This returns the ID of the default audio render device, which is then passed into the constructor for **AudioDeviceModulesManager** to create an instance of the class that is associated with the audio device.

C#
```csharp
var endpointId = MediaDevice.GetDefaultAudioRenderId(AudioDeviceRole.Default);
var audioModuleManager = new AudioDeviceModulesManager(endpointId);
```

## Query for installed audio device modules

Query for all installed audio device modules by calling the **[FindAll](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulesmanager#Windows_Media_Devices_AudioDeviceModulesManager_FindAll)** of the the **[AudioDeviceModulesManager](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulesmanager)** class. Query for a specific set of audio device modules by calling **[FindAllById](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulesmanager#Windows_Media_Devices_AudioDeviceModulesManager_FindAllById_System_String_)** and passing in the ID of the requested modules. The following example defines an ID for a set of modules, calls **FindAllById** to retrieve a list of **[AudioDeviceModule](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodule)** objects, and then prints the details of each module to the debug output.

C#
```csharp
public const string Contoso_AudioDeviceModuleId = "F72E09C3-FEBA-4C50-93BE-2CA56123AF09";
``` 

C#
```csharp
var endpointId = MediaDevice.GetDefaultAudioRenderId(AudioDeviceRole.Default);
var audioModuleManager = new AudioDeviceModulesManager(endpointId);
var modules = audioModuleManager.FindAllById(Contoso_AudioDeviceModuleId);

foreach (var module in modules)
{
    var classId = module.ClassId;
    var name = module.DisplayName;
    var minorVersion = module.MinorVersion;
    var majorVersion = module.MajorVersion;
    var instanceId = module.InstanceId;

        Debug.WriteLine($"{classId} : {name} : {minorVersion} : {majorVersion} : {instanceId}");
}
``` 
## Send a command to an audio device module and receive result data
Send commands to an audio device module by calling **[SendCommandAsync](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodule#Windows_Media_Devices_AudioDeviceModule_SendCommandAsync_Windows_Storage_Streams_IBuffer_)** on the **[AudioDeviceModule](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodule)** object. The **SendCommandAsync** method takes a byte array as an argument. Typically this byte array contains a command identifier followed by the data associated with the command, but the command format and values are entirely vendor-defined and are treated as transparent by the system.

The **SendCommandAsync** method returns an asynchronous operation that, upon completion, returns a **[ModuleCommandResult](https://docs.microsoft.com/uwp/api/windows.media.devices.modulecommandresult)** object representing the result of the command. The **[Status](https://docs.microsoft.com/uwp/api/windows.media.devices.modulecommandresult#Windows_Media_Devices_ModuleCommandResult_Status)** property contains an enumeration value that indicates whether the system was able to execute the command. This does not necessarily indicate that the audio device module was able to execute the command successfully. The **[Result](https://docs.microsoft.com/uwp/api/windows.media.devices.modulecommandresult#Windows_Media_Devices_ModuleCommandResult_Result)** property contains a byte array that is returned by the audio device module to indicate the status of the command. Typically, this will be a value that indicates success or failure followed by the data result of the command. As with module commands, module response formats and values are vendor-defined.

The following example calls **FindAllAsync** to retrieve a set of audio device modules. A **[DataWriter](https://docs.microsoft.com/uwp/api/windows.storage.streams.datawriter)** is used to create a byte array containing an example command and data. **SendCommandAsync** is called to send the command buffer and, after the asynchronous operation completes, a **ModuleCommandResult** is returned. If the command execution was successful, a **[DataReader](https://docs.microsoft.com/uwp/api/windows.storage.streams.datareader)** is first used to read an integer status value returned from the module. If this value is the vendor-defined success value, the rest of the result data is read and used by the app, such as to update the UI.


C#
```csharp
public const byte Contoso_ReverbLevel_Command = 30; 
public const byte Contoso_SendCommand_Success = 99;
``` 

C#
```csharp
var endpointId = MediaDevice.GetDefaultAudioRenderId(AudioDeviceRole.Default);
var audioModuleManager = new AudioDeviceModulesManager(endpointId);
var modules = audioModuleManager.FindAllById(Contoso_AudioDeviceModuleId);

foreach (var module in modules)
{
    var writer = new Windows.Storage.Streams.DataWriter();
    writer.WriteByte(Contoso_ReverbLevel_Command);
    writer.WriteByte(100);

    var command = writer.DetachBuffer();

    var result = await module.SendCommandAsync(command);

    if (result.Status == SendCommandStatus.Success)
    {
        using (DataReader reader = DataReader.FromBuffer(result.Result))
        {
            int bufferStatus = reader.ReadInt32();
            if (bufferStatus == Contoso_SendCommand_Success)
            {
                byte[] data = { 0, 0 };
                reader.ReadBytes(data);
                // Do something with returned data, such as update UI
            }
        }
    }
}
```

## Receive notifications when audio device modules are modified
Apps can receive notifications when an audio device module has been updated by registering for the **[ModuleNotificationReceived](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulesmanager#Windows_Media_Devices_AudioDeviceModulesManager_ModuleNotificationReceived)** event. 

C#
```csharp
var endpointId = MediaDevice.GetDefaultAudioRenderId(AudioDeviceRole.Default);
var audioModuleManager = new AudioDeviceModulesManager(endpointId);

audioModuleManager.ModuleNotificationReceived += AudioModuleManager_ModuleNotificationReceived;
``` 

**ModuleNotificationReceived** will be raised when any audio device module associated with the current audio device is modified. To determine if the event is associated with a particular module, get an instance of **AudioDeviceModule** by accessing the **[Module](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulenotificationeventargs#Windows_Media_Devices_AudioDeviceModuleNotificationEventArgs_Module)** property of the **[AudioDeviceModuleNoticiationEventArgs](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulenotificationeventargs)** passed into the event handler, and then checking the **[ClassId](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodule#Windows_Media_Devices_AudioDeviceModule_ClassId)** property that identifies the module. The data associated with the event is passed as a byte array stored in the **[NotificationData](https://docs.microsoft.com/uwp/api/windows.media.devices.audiodevicemodulenotificationeventargs#Windows_Media_Devices_AudioDeviceModuleNotificationEventArgs_NotificationData)** property of the event args. As with commands and results, the format of the returned byte array is vendor-defined. In the example below, if the first byte of the notification data contains the example value for the module's reverb level setting, the data is read and used to update the UI.

C#
```csharp
public const byte Contoso_ReverbLevel_Data = 25;
```

C#
```csharp
private void AudioModuleManager_ModuleNotificationReceived(AudioDeviceModulesManager sender, AudioDeviceModuleNotificationEventArgs args)
{
    if (args.Module.ClassId == Contoso_AudioDeviceModuleId)
    {
        // Get the coefficient data from the reverb module.
        using (DataReader reader = DataReader.FromBuffer(args.NotificationData))
        {
            // read notification data.
            byte item = reader.ReadByte();

            // if reverb coefficient data are changed.
            if (item == Contoso_ReverbLevel_Data)
            {
                // read the new value
                byte[] data = { 0 };
                reader.ReadBytes(data);
                ReverbLevelSlider.Value = data[0];
            }
        }
    }
}
```