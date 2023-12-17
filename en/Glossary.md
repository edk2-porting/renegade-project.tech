# Glossary
This is a simple glossary that explains a few of the technical terms mentioned across all of the Renegade Project.

> Help improving the glossary with useful technical terms!
{.is-info}

## A/B slot device
 A/B slots describe a function that's present on some Qualcomm Snapdragon 835 devices and most 845 and 855 devices. It's used on Android for seamless updates and it uses two sets of partitions referred to as slots. This feature can often be "misused" for dualbooting purposes where you use one of the slots for your Android boot.img and the other one for a Renegade Project UEFI EDK2 bootloader.
 NOTE: If your device is a Xiaomi or Poco device then it might not be a A/B device.
## ABL
 APPS Bootloader 
## ACDB
 Audio Calibration Database
## ADB
 Android Debug Bridge - part of the Google platform-tools
## ADSP
 Audio Subsystem - part of the subsystem that manages the Qualcomm Aqstic audio stack
## AMSS
 Application Modem Subsystem - part of the subsystem that manages Modem and WiFi on your device.
## BCD
 Boot Configuration Data - used by Windows's boot manager
## BSOD
 Blue Screen of Death
## BT
 Bluetooth - a part of your Qualcomm Snapdragon SoC that is using UART
## CDSP
 Compute Digital Signal Processing
## CPU
 Central Processing Unit - the big heart of your Qualcomm Snapdragon device
## DTB & FDT
 Device Tree Blob & Flattened Device Tree - files which describe your device's hardware
## EDK2
 EFI Development Kit II - heart of our UEFI bootloader
## EFI
 Extensible Firmware Interface
## EFS
 Encrypted File System - partition on your device that contains radio/modem/baseband/IMEI related data
## eMMC
 Embedded Multi-Media Card - the older style flash storage used on lowercost devices
## ESP
 EFI System Partition - a partition on your UFS used by Windows to store all Windows Boot Manager related data
## fastboot
 part of the Google platform-tools
## GPU
 Graphics Processing Unit
## I²C
 I²C - multi-controller/multi-target serial communication bus used for touchscreens and possibly also other sensors and parts of your device
## ICan0
 value of the MobileNetworkingService from WP RIL used for calling on your device
## Mainline Linux
 Linux running on the latest and greatest upstream kernel without any downstream modifications from your device vendor
## MNS
 MobileNetworkingService - part of the WP RIL layer
## PD
 Power Delivery - a part of the USB specification meant for voltage/current control
## QCN
 Qualcomm Calibration Network
## Qualcomm Aqstic
 the official name for Qualcomm's audio stack on Qualcomm Snapdragon SoCs
## Qualcomm Snapdragon
 the official name for our device's SoC
 could be also abbreviated as MSMxxxx, SDMxxx or SMxxxx
## RIL
 Radio Interface Layer
## SCSS
 Sensor Compute Subsystem - part of the subsystem that manages sensors
## SPSS
 Security Processor Subsystem
## SOC
 System on a Chip - the whole Qualcomm Snapdragon processor of your device
## UART
 Universal Asynchronous Receiver/Transmitter - in simpler terms, a serial connection to your device
## UEFI
 Unified Extensible Firmware Interface
## UFS
 Universal Flash Storage - the flash storage chip used on most Qualcomm Snapdragon 835, 845 and 855 devices
## UFS LUN
 UFS Logical Unit Number - all of the Qualcomm Snapdragon devices have around 6 of these LUNs on them. They are used to separate important device related parts from your userdata.
## Windows PE
 Windows Preinstallation Environment
## WoA
 Windows on ARM
## WP RIL
 Windows Phone Radio Interface Layer - a ported part of Windows Phone's calling stack used on Qualcomm Snapdragon Windows on ARM devices
