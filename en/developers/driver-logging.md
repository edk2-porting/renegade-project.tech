> This guide is copied from original Renegade website, it should and will get improved.
{.is-warning}


> Currently this guide shows the easiest way to get log from drivers. For further debugging, you should refer to Microsoft documents.
{.is-info}


Clone [WOA-Drivers-debug](https://github.com/edk2-porting/WOA-Drivers-debug) on your computer

Import a registry file in the `WOA-Drivers-debug\reg` folder **on your phone**, and reboot your phone

After rebooting, you'll find etl files in `C:\Renegade\Logfiles\`. Copy them to your computer.

Run the following command to get readable log file

> Remember to install Windows Driver Kit (WDK) to get `tracefmt` tool

```plaintext
tracefmt.exe .\whatever.etl -p D:\PathTo\WOA-Drivers-debug\tmf -o whatever.log
```
