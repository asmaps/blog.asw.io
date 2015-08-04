---
layout: post
title: "HowTo: Flash ESP8266 with NodeMCU firmware"
description: ""
category: ESP8266 
tags: ["howto", "esp8266", "lua", "hardware", "flashing"]
---

# Hardware Requirements

## Option 1

Less soldering, more "out-of-the-box"

### Mandatory
* ESP8266 NodeMCU dev board (a lot less soldering needed)
  [AliExpress](http://s.click.aliexpress.com/e/Iqna2RZVb?af=717073896)
  * already includes:
    * ESP8266 chip
    * USB/Serial communication unit
    * Power regulaor/converter
    * other helpful stuff (like buttons for reset/flash, etc)

## Option 2

More soldering than option 1, but more DIY

### 2.1: Mandatory
* ESP8266 (plain) [AliExpress](http://s.click.aliexpress.com/e/Rby3bEEaE?af=717073896)
* USB to Serial Cable e.g. PL2303HX
  [AliExpress](http://s.click.aliexpress.com/e/vNjEu3RRz?af=717073896) or in the electronics dispenser at shackspace (2€)
* 3.3V Converter e.g. LM1117
  [AliExpress](http://s.click.aliexpress.com/e/yNbieUjyb?af=717073896)

### 2.2: Recommended
* 4.7 µF capacitors to buffer variations in power usage [AliExpress (set of a few different
  sizes including 4.7µF)](http://s.click.aliexpress.com/e/vnIamMVZB?af=717073896)
* ESP-12 breakout board
  [AliExpress](http://s.click.aliexpress.com/e/iiuJunIUN?af=717073896)
* alternative to LM1117 that can be put on the back of the ESP breakout board: XC6206P332PR (50pcs is smallest available
  package size) [AliExpress](http://s.click.aliexpress.com/e/BEiQVR7qj?af=717073896)

## Suitable for both options

### Sensors
* DHT22 temperature and humidity sensor [AliExpress](http://s.click.aliexpress.com/e/rnuvFMrny?af=717073896)
* Dust sensor [AliExpress](http://s.click.aliexpress.com/e/m6Q7emu7Q?af=717073896)
* Door/Window reed contacts [AliExpress](http://s.click.aliexpress.com/e/F6UnMFU7Q?af=717073896) 

### Additional stuff to make it work
Stuff around to make it work, like resistors, cables, etc. Choose what you think suits your needs.

* breadboard starter set [AliExpress](http://s.click.aliexpress.com/e/aMnaQzv7Q?af=717073896)
* Male Header Pins [AliExpress](http://s.click.aliexpress.com/e/6eAqjMJeU?af=717073896)
* Female Headers [AliExpress](http://s.click.aliexpress.com/e/UjyZRJ2ji?af=717073896)
* Prototype board [AliExpress](http://s.click.aliexpress.com/e/IUrzn2nMr?af=717073896)
* WS2812B RGB LED with integrated PWM controller [AliExpress](http://s.click.aliexpress.com/e/vrFiM3bi2?af=717073896)
* Connectors (2 pin) [AliExpress](http://s.click.aliexpress.com/e/UzJuzfy7M?af=717073896)
* Connectors (4 pin) [AliExpress](http://s.click.aliexpress.com/e/FiUzfa2nA?af=717073896)
* Resistor Set [AliExpress](http://s.click.aliexpress.com/e/uvrRbQRNJ?af=717073896)
* As you like: more/other LEDs, buttons, cables, ...


# Software requirements

You will need `git`, `screen` and `python`. Please install them if you don't already have them.

Check out the following repos (git):

* https://github.com/4refr0nt/luatool.git
* https://github.com/themadinventor/esptool.git
* https://github.com/nodemcu/nodemcu-firmware.git

# Connecting everything

## With the NodeMCU dev board

If you have the devboard just connect a micro usb cable and your ready to go.

## With the white breakout board

Solder the ESP on your board.

### Without XC6206P332PR (small voltage regulator on the back of the board)

Measure the resitor in the middle below the ESP between VCC and GND, it should be a zero resitor/bridge => 0 Ohm. There are
some boards that have a wrong part there: a 10k Ohm. If you have that you need to remove that resistor and bridge it
with something else (small cable, solder, ...).  
You will need to connect VCC of the board to 3.3V now.

### With XC6206P332PR

Remove the resistor in the middle below the ESP between VCC and GND. Then solder the XC6206P332PR onto the back of the
white board.
You can now connect up to 6V to VCC and it will be regulated to 3.3V. (Minimum voltage needed has to be more than 3.3V)

### Connecting with the white board
With the white breakout board you have to connect GND, VCC (voltage depends on if you have XC6206P332PR), RX and TX of
your serial cable to flash the ESP. Also to enter flash mode you have to pull down GPIO0 to GND during startup
(just connect it).

# Flashing

TBD
