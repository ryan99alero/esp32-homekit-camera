# esp32-homekit-camera

Firmware for esp32-camera module to act as Apple Homekit IP camera.

Based on [esp-homekit](https://github.com/maximkulkin/esp-homekit).

## Configuration

Before compiling, you need to alter several settings in menuconfig (`make
menuconfig`):
* Partition Table
    * Partition Table = **Custom partition table CSV**
    * Custom partition CSV file = **partitions.csv**
* Component config
    * Driver Configuration
        * Driver Configuration
            * Support array 'rtc_gpio_desc' for ESP32 = **check**
    * ESP32-specific
        * Support for external, SPI-connected RAM = **check**
        * SPI RAM config
            * Initialize SPI RAM when booting the ESP32 = **check**
            * SPI RAM access method = **Make RAM allocatable using malloc() as well**
    * Camera configuration
        * OV2640 Support = **check**
    * HomeKit
        * SPI flash address for storing HomeKit data = 0x3A0000
* ESP32 HomeKit Camera
    * WiFi SSID and WiFi Password
    * Camera Pins
        * Select Camera Pinout = *your variant of module*

## Patching script **esp32-camera.patch**
Patch xclk.c with esp32-camera.patch
Find file that patch needs to update by Executing **patch -p 1 < esp32-camera.patch** in directory of patch file.  In this case its file esp32-camera.patch in the esp32-homekit-camera root directly.  The -p 1 portion of cmd will show you the full directory path of the file its wanting to patch.  This file is also listed inside the patch file.

For this patch with the obtained info we will do the following. 

cd /home/ryan/esp/esp32-homekit-camera/components/esp32-camera/driver
patch < /home/ryan/esp/esp32-homekit-camera/esp32-camera.patch
