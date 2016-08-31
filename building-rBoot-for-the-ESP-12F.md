# Building rBoot for the ESP-12F

The following document describe how to building binaries for the ESP8266 that support OTA updates using raburton's rboot.

### Installing Prerequisites

##### ESP8266 NONOS SDK

https://espressif.com/en/support/download/sdks-demos

At the time of writing, the "ESP8266 NONOS SDK V2.0.0 20160719" and the "ESP8266 NONOS SDK V2.0.0 patch 20160809" were the latest NONOS SDK files. Just download both .zip archives, unzip, and copy the files from the patch into the appropriate locations in the full 2.0.0 folder.

Note: RTOS is Espressif's SDK based on the open source real time operating system OpenRTOS. Since we didn't need RTOS capabilities we use the "NONOS" version of the SDK.

##### Xtensa lx106 toolchain

https://github.com/pfalcon/esp-open-sdk

I recommend installing the esp-open-sdk because it does a lot of things for you and gives you a foolproof way of getting the Xtensa lx106 compiler that we need. I also recommend making the the non-standalone version to avoid build problems. Note that we are only using the esp-open-sdk for the Xtensa compiler and nothing else.

```
make STANDALONE=no
```

##### esptool2

https://github.com/raburton/esptool2

```
make
```

Just 'make' should do it.

##### rboot

https://github.com/raburton/rboot

To use the Makefile set SDK_BASE to point to the root of the Espressif SDK and either set XTENSA_BINDIR to the gcc xtensa bin directory that you made when you built the esp-open-sdk, or include it in your PATH. These can be set as environment variables or by editing the Makefile.

Also note that the ESPTOOL2 path in the Makefile is set to "../esptool2/esptool2". If this doesn't match where you placed esptool2, then you need to change this value so that it does.

### Creating your app

##### Forking rboot-sample

https://github.com/raburton/rboot-sample

Make a fork of rboot-sample. Follow the instructions in the README.

##### Testing

Apparently, serial output won't work until you run this line in your user program.

```
wifi_set_opmode(0);
```

### Flashing the ESP-12F

```
cd /path-to-your-fork-of-rboot-sample/

python /path-to-your-esptool/esptool.py -p /dev/ttyUSB0 -b 115200 write_flash -fs 32m -ff 80m -fm dio 0x00000 rboot.bin 0x02000 firmware/rom0.bin 0x82000 firmware/rom1.bin 0xFC000 blank4.bin 0x3FC000 /path-to-your-sdk/ESP8266_NONOS_SDK/bin/esp_init_data_default.bin
```

WARNING: Don't use a crappy USB to Serial converter. I spent many hours debugging strange flashing errors because the converter that we bought sucked. What's strange is that it worked fine for flashing roms built with the Arduino IDE, but esptool.py would consistently stall. I bet Arduino intelligently retries or something if it detects a failure.

The faulty FTDI USB to Serial that I used was the Gikfun FT232RL (https://www.amazon.com/gp/product/B01HXT8DZ4/ref=oh_aui_detailpage_o00_s00?ie=UTF8&psc=1)

The good one that I used is the TOOGOO(R)6pin that uses the CP2102 chip (https://www.amazon.com/6Pin-CP2102-Module-Converter-Replace/dp/B01HXCLDMG/ref=sr_1_44?s=electronics&ie=UTF8&qid=1472064044&sr=1-44&keywords=cp2102)

Error examples indicating a USB to Serial failure:

https://vilimpoc.org/blog/2016/05/03/esptool-ck-esp8266-and-ftdi-bug-hunting/

```
Running Cesanta flasher stub... 
Writing 4096 @ 0x0... 
A fatal error occurred: Timed out waiting for packet header
```

### OTA update

In the Makefile of your fork of rboot-sample you should have defined the SSID and PASSWORD for your WiFi. Also, you need to edit the server info for your firmware location in rboot-ota.h BEFORE you build. From there, if you serve the file name and location that you specified in rboot-ota.h, then you should be golden.
