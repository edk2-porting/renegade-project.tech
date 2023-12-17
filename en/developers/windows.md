> This page is under construction
{.is-warning}

This wiki page will only cover useful tips and information regarding debugging Windows drivers on Qualcomm Snapdragon arm64 platforms.

For details on WinDbg usage, please refer to Microsoft documents.

# Prerequisite

## BCD settings

```shell
# Prevent going to recovery when boot fails
bcdedit /store BCD /set "{default}" bootstatuspolicy IgnoreAllFailures
bcdedit /store BCD /set "{default}" recoveryenabled no
# Enable KDNET debugging
bcdedit /store BCD /set "{default}" debug on
bcdedit /store BCD /dbgsettings net HOSTIP:169.254.255.255 PORT:50000 KEY:1.2.3.4 NODHCP
```

## Installing WinDbg

You can get WinDbg Preview from [Microsoft Store](https://apps.microsoft.com/store/detail/windbg-preview/9PGJGD53TN86)

After installing, open WinDbg Preview and navigate to `Start Debugging`, choose `Attach to kernel`, `Port Number: 50000`, `Key: 1.2.3.4`, then click OK. You can now connect your device to PC and boot it.

# Driver tracing

You must either get TMF (trace message format) files or PDB files to do tracing. Currently we only provide TMF files on [GitHub](https://github.com/edk2-porting/WOA-Drivers-debug).

## Real-time tracing

Check `Break on connection` in the `Start debugging` page. After connecting to target, do an initial break:
```shell
bp ACPI!DriverEntry;g;g
```
After it breaks, set up wmitrace sessions:
```shell
!wmitrace.start whatever -kd
!wmitrace.searchpath C:\path\to\tmf\files
!wmitrace.enable whatever EF49A24A-40CD-46D0-8A8A-3623B7A18969 -level 0xFF
!wmitrace.enable whatever CE0458F5-EE40-403A-AF35-A3E7FACC2BD0 -level 0xFF
# one wmitrace instance can have multiple sessions
```

Then go:
```
g
```
The above GUIDs could be found in [Driver Tracing GUIDs](/en/developers/windows/trace-guid)

## Autologger

> to be filled
{.is-info}
