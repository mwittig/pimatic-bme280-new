# pimatic-bme280

[![npm version](https://badge.fury.io/js/pimatic-bme280.svg)](http://badge.fury.io/js/pimatic-bme280)
[![dependencies status](https://david-dm.org/atus/pimatic-bme280/status.svg)](https://david-dm.org/atus/pimatic-bme280)
[![downloads][downloads-image]][downloads-url]

[downloads-image]: https://img.shields.io/npm/dm/pimatic-bme280.svg?style=flat
[downloads-url]: https://npmjs.org/package/pimatic-bme280

A pimatic plugin for modules based on the [BME280](https://www.bosch-sensortec.com/bst/products/all_products/bme280) sensor. It uses the `node-bme280` driver from [CLCL/node-BME280](https://github.com/CLCL/node-BME280). This is a fork of Alan Tus's plugin project which apparently is no longer maintained. 

## Configuring device

Add a device via the web UI or by editing the config file.

```
    {
      "class": "BME280Sensor"
      "id": "bme280-test",
      "name": "BME280 test",
      "device": "i2c-1",
      "address": "0x76",
      "interval": 10000,
      "xLink": "",
    }
```

Check using `dir /dev/i2c*` to see the name of your device. USe `i2cdetect` to determine the address. If you can't find this command use `sudo apt-get install -y i2c-tools`.

```
pi@raspberrypi:~/$ i2cdetect -y 1
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:          -- -- -- -- -- -- -- -- -- -- -- -- --
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
70: -- -- -- -- -- -- 76 --
```

## Raspberry Pi setup
Copied steps from here: https://learn.sparkfun.com/tutorials/raspberry-pi-spi-and-i2c-tutorial#i2c-on-pi

I2C is not turned on by default. We can use `raspi-config` to enable it.

1. Run `sudo raspi-config`.
2. Use the down arrow to select `9 Advanced Options`
3. Arrow down to `A7 I2C`.
4. Select `yes` when it asks you to enable I2C
5. Also select `yes` when it tasks about automatically loading the kernel module.
6. Use the right arrow to select the `<Finish>` button.
7. Select `yes` when it asks to reboot.

The system will reboot. when it comes back up, log in and enter `ls /dev/*i2c*`.
The Pi should respond with `/dev/i2c-1` which represents the user-mode I2C interface.
