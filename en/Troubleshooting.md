![rngd_banner_troubleshooting.png](/images/rngd_banner_troubleshooting.png)
## 0. No WiFi in OOBE

*also sometimes known as `"Oops, you've lost internet connection"`*
This usually happens when your device doesn't have working WiFi drivers. You get stuck on the `Let's connect you to a network` part of OOBE with a greyed out `Next` button.

The easiest fix is to:
- Open On Screen Keyboard in OOBE or connect a USB keyboard.
- Press Shift + F10 and wait for command line window to open.
- Write `oobe\bypassnro` and press enter *(or try `cd oobe` and `bypassnro.cmd` if the first command fails)*
- Your device should restart and you should later find a text button in OOBE's `Let's connect you to a network` part that says `I don't have internet` 

## 1. Mass storage mode hangs and reboots during operation

~~Due to Windows 11 having an updated `uaspstor` driver after 22H2, mass storage mode will not function properly due to the driver sending an unsupported command to the target device. You will need to get an older version of the driver and replace it under `C:\Windows\System32\drivers`~~

~~Of course you can extract the older driver by yourself. For convenience, we also provide one from Windows 10 (19041.1949) [uaspstor.sys](/random/uaspstor.sys)~~

Update: I finally found out there's an issue with my host PC USB bus. After directly connecting to the motherboard USB port, there's no such problem anymore. I'm using a 10-meter optical USB 3.0 extension cable with hub connected to it, which might be the problem.

## 2. Device fails to boot with *synchronous exception at xxx*
![synchronous_exception.jpg](/synchronous_exception.jpg)

You might have experienced a bug. Before seeking for help, try these first:

- Check if your UEFI image is the latest one
- Access the `logfs` partition, find `simpleinit.uefi.cfg` there and remove it.
- Try spampressing volume buttons *(weird thing, right?)*
- Unplug any USB device connected to your device *(if any?)*
- Try using an previous version of UEFI image
- Try building UEFI from latest source code

If it still doesn't work, build an UEFI image of `DEBUG` variant, take a photo of the stack trace, then open an issue in the EDK2 repository.

## 3. Device can no longer boot into fastboot

The name of one of the partitions has space in it, e.g `Microsoft Reserved Partition`. It is known that Windows disk management tools will cause such problem, like `diskpart` or `diskmgmt`.

There are several ways to fix this:

- Use `parted` to change the offending partition name. You can use it in either recovery or Android(rooted)
- If you can boot Windows on your device, try searching for a tool which allows you to change partition name
- If you can still enter UEFI, use mass storage mode and change partition name on your PC
- Enter EDL mode and flash Android factory image **(ALL DATA WILL BE LOST)**
> **Partition name** is not the same as **partition label**!
{.is-warning}

## 4. Your PC/Device needs to be repaired
![testsigning.jpg](/testsigning.jpg)
> This is usually the most common oversight people do after deploying Windows and drivers.
{.is-info}

> Be aware that you might also encounter a similiar `"Your PC/Device needs to be repaired"` error that doesn't include the `0xc0000428` error code! In case of this error, please download drivers from the correct place!
{.is-danger}


If you happen to encounter the `"Your PC/Device needs to be repaired"` error that also happens to include `"The operating system couldn't be loaded because the digital signature of a file or one of its dependencies couldn't be verified."` and the `0xc0000428` error code.

There's one way to fix it:
- Firstly access Windows partitions as stated in [Step 2.1.1 Access Windows partitions on your PC](/en/install#h-211-access-windows-partitions-on-your-pc) but **don't  execute both `format` commands**, otherwise you will format your partitions and you can start deploying Windows on ARM installation again!
- Repeat [Step 2.1.4 Enable test signing and disable Automatic Repair](/en/install#h-214-enable-test-signing-and-disable-automatic-repair) and make sure to use the correct paths

## 5. Windows Boot Manager errors
![bcd.jpg](/bcd.jpg)

> This troubleshooting step covers all issues with Windows Boot Manager that you can encounter.
{.is-warning}

These can mention that your `Boot Configuration Data (BCD)` or `application or operating system` for your device is either missing or contains errors.

There's usually only one way to fix this:
- Firstly access Windows partitions as stated in [Step 2.1.1 Access Windows partitions on your PC](/en/install#h-211-access-windows-partitions-on-your-pc) but **don't  execute both `format` commands**, otherwise you will format your partitions and you can start deploying Windows on ARM installation again!
- In the command prompt window execute:
```shell
# S: is the assigned partition letter for your EFI ESP partition
# W: is the assigned partition letter for your deployed WoA system
# change these values in case you mounted it differently

bcdboot W:\Windows /s S: /f UEFI
```

- You can now go back to [Step 2.1.4 Enable test signing and disable Automatic Repair](/en/install#h-214-enable-test-signing-and-disable-automatic-repair)

## 6. UEFI Shell
![uefishell.jpg](/uefishell.jpg)

> This is one of the less common roadblocks that you can encounter.
{.is-warning}

If you get to this screen, your issue is simple and clean.
Your device just doesn't have a place to start booting from either Windows PE or a deployed Windows on ARM installation that you *might* have on your device.
You can fix it by:
- Following the installation guide properly
- Deploying a Windows on ARM installation properly to your device

## 7. qcaudminiport850.sys BSOD
![pocoqcaudminiport.jpg](/pocoqcaudminiport.jpg)

> This is usually the most common issue when connecting Bluetooth Audio devices to Xiaomi Pocophone F1.
{.is-warning}

If you get to this Blue Screen Of Death after trying to connect Bluetooth Audio devices to your Xiaomi Pocophone F1:
- Turn off your Bluetooth Audio device and reboot to Windows
- Open Device Manager *(Win+X on keyboard and select Device Manager or search for devmgmt.msc)*
- Open `Sound, video and game controllers`
- Find `Qualcomm(R) Audio Miniport Device` and open it
- Remove this driver
- You can now proceed to turning back your Bluetooth Audio device and connect it to your device.

## 8. Stuck at Preparing Automatic Repair or Diagnosing your PC
![automaticrepair.jpg](/automaticrepair.jpg)

If you happen to get stuck at Preparing Automatic Repair, you can:
- Reboot your device
- Try booting once more

and if that doesn't help then:
- Disable it using [Step 2.1.4 Enable test signing and disable Automatic Repair](/en/install#h-214-enable-test-signing-and-disable-automatic-repair)

## 9. Windows Setup could not configure Windows to run on this computer's hardware
![couldnotconfigure.jpg](/couldnotconfigure.jpg)
> This is one of the least common issues.
{.is-info}

If you happen to encounter a `Windows Setup could not configure Windows to run on this computer's hardware.` message during the instalation, it's possible you made a mistake when partitioning the UFS.

To check it first:
- Boot into **a third-party recovery** which allows you to use ADB. You will also need [parted](/tools/parted)
- Then push `parted` to your device and enter ADB shell:
```bash
adb push parted /cache/
adb shell "chmod 755 /cache/parted"
adb shell
```

- After entering ADB shell:
```bash
cd /cache
./parted /dev/block/sda 
```

- Print the current partition table:
```
(parted) print
```

- Then you will see your current partition table. Find the `esp` partition we created. Below is an example of the esp partition:
```
.........
Number  Start    End      Size     File system   Name       Flags
.........
23      32GB     32.5GB   512MB    fat32         esp        boot, esp
```

- Please note that the flags column for the `esp` partition has `boot, esp`. 
- If you don't see these flags for the `esp` partition, you've probably forgot to do the following during the UFS partitioning:

```bash
# set the esp partition as `EFI system partition type`
(parted) set 23 esp on
```

- Exit the parted tool finally.
```bash
(parted) quit
```

- Redeploy Windows on ARM to your device again from [Step 2. Installation](/en/install#h-2-installation)

---

If this still didn't help, try reformatting the `esp` partition.

## 10. The computer restarted unexpectedly or encountered an unexpected error.
![restartedunexp.jpg](/restartedunexp.jpg)
> This issue is commonly seen on Qualcomm Snapdragon 845 (SDM845) OnePlus devices.
{.is-warning}

> This is **caused by getting a BSOD during the installation process. The WiFi/Modem subsystem on Qualcomm Snapdragon 845 (SDM845) OnePlus devices is unstable** and can get your device to QUALCOMM CrashDump Mode quite often.
{.is-info}

If you happen to get the `The computer restarted unexpectedly or encountered an unexpected error. Windows installation cannot proceed. To install Windows, click "OK" to restart the computer, and then restart the installation.` message after first boot on your device, try redeploying Windows on ARM to your device again from [Step 2. Installation](/en/install#h-2-installation).

## 11. QUALCOMM CrashDump Mode
![crashdump.jpg](/crashdump.jpg)
> This issue is commonly seen on Qualcomm Snapdragon 845 (SDM845) OnePlus devices.
{.is-warning}

> The WiFi/Modem subsystem on Qualcomm Snapdragon 845 (SDM845) OnePlus devices is unstable and can get your device to QUALCOMM CrashDump Mode quite often.
{.is-info}

You device can get into this mode due to numerous reasons. To get out of it:
- Disconnect all USB cables
- Press power button and both volume buttons simultaneously
- Wait for the device to reboot

## 12. INACCESSIBLE_BOOT_DEVICE BSOD ![rngd_inaccessiblebootdevice_bsod.jpg](/rngd_inaccessiblebootdevice_bsod.jpg)
This Blue Screen od Death most likely means a broken driver install.
To fix it:
- Firstly access Windows partitions as stated in [Step 2.1.1 Access Windows partitions on your PC](/en/install#h-211-access-windows-partitions-on-your-pc) but **don't  execute both `format` commands**, otherwise you will format your partitions and you can start deploying Windows on ARM installation again!
- Repeat [Step 2.1.3 Installing drivers](/en/install#h-213-installing-drivers)

## 13. DRIVER_PNP_TIMEOUT BSOD

> This BSOD on Qualcomm Snapdragon 845 devices usually means that you forgot to flash a different devcfg.img to your device. 
{.is-info}

> This BIOS on Qualcomm Snapdragon 855 devices varies currently with anything from broken drivers, weird firmware configurations on your device and else. 
{.is-info}
