---
title: "HA OS installation on Blue/N2/N2+ "
description: "Using Petitboot and OTG-USB to flash the eMMC on your Odroid N2"
---
A USB module writer may be used in order to flash Hardkernel's eMMC module. After connecting the eMMC module to the adapter, it can be flashed using the same method used for an SD and a USB SD adapter.

An alternative to using the module writer is to use the Petitboot bootloader on the Odroid N2/N2+. Using an OTG-USB connection the board can be connected, flashed, and accessed as though it were a USB drive.

## What you will need

In order to flash your eMMC using Petitboot and OTG-USB you will need the following items:

- HDMI cable and monitor
- USB keyboard
- A USB 2.0 to micro-usb cable

---

### Enabling SPI boot mode

Remove the case of your Odroid N2/N2+

<img src='/images/hassio/screenshots/cased-removed.jpg' />

Next, locate the toggle for boot mode and switch it from MMC to SPI. Connect the micro-usb cable.

<img src='/images/hassio/screenshots/toggle_spi.png' />

Connect a USB keyboard and HDMI connected monitor to your N2+, and then connect power.

### HA OS Installation via PC using OTG

This following steps will allow for flashing HA OS directly to the eMMC from a PC over USB to the N2+’s OTG port.

Select `Exit to shell` from the menu.

<img src='/images/hassio/screenshots/exit-shell.png' />

Use the following command at the console to confirm the storage device node:

`$ ls /dev/mmc*`

Set the storage device on the N2+ as a mass storage device using `ums` (USB Mass storage mode)
This will configure the N2+ and OTG to act as a memory card reader.

`$ ums /dev/mmcblk0`

If you have not done so already, connect the other end of the micro-usb cable to your PC and wait for it to be recognized as a USB connected storage device.

You can now flash the eMMC with Etcher using the latest stable version of Home Assistant OS for the [Odroid N2+](https://github.com/home-assistant/operating-system/releases/download/4.16/hassos_odroid-n2-4.20.img.gz)

When the flash process is complete, disconnect the N2+ from your PC and remove the power cable. Remove the USB and HDMI cable, and make sure to toggle the boot mode switch back to MMC.

Once it is back in its case, connect your N2+ to your network with an Ethernet cable and plug in power. If your router supports mDNS, you will be able to reach your installation on `http://homeassistant.local:8123`  If it doesn’t support mDNS, then you’ll have to use the IP address of your N2+ instead of `homeassistant.local`. For example, `http://192.168.0.9:8123`. You should be able to find the IP address of your N2+ from the admin interface of your router.
