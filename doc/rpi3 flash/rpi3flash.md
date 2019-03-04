Prepare
=======

rasp-config
 interfacing option
  P6 Serial
    Deactivte Kernel + Activate Hardware


cat /boot/config
enable_uart=1 

cat /boot/cmdline.txt
 remove delete "console=serial0,115200" (optional, raspi-config do it)

reboot now


Wiring
======

RPI GPIO (sdcard up)
+---+---+
| 1 | 2 |
+---+---+
| 3 | 4 |
+---+---+
| 5 | 6 |
+---+---+
| 7 | 8 |
+---+---+
| 9 | 10|
...

GPIO 8 -> RX sonoff
GPIO 10 -> TX sonoff
GPIO 6 -> GND Sonoff
GPIO 9 -> GND 3V

3V Sonoff -> 3V in

RPI powered via mini usb

Software
========

sudo apt-get install python-pip -y
sudo pip install esptool

Flash mode: power off sonoff, press button, power on keeping button pressed for 2s, release button

esptool.py --port /dev/ttyS0 erase_flash
esptool.py v2.6
Serial port /dev/ttyS0
Connecting....
Detecting chip type... ESP8266
Chip is ESP8285
Features: WiFi, Embedded Flash
MAC: 84:0d:8e:56:5e:4b
Uploading stub...
Running stub...
Stub running...
Erasing flash (this may take a while)...
Chip erase completed successfully in 1.1s
Hard resetting via RTS pin...


wget https://github.com/letscontrolit/ESPEasy/releases/download/mega-20190301/ESPEasy_mega-20190301.zip
unzip ESPEasy_mega-20190301.zip
cd bin/

Put sonoff back into flash mode. 

esptool.py --port /dev/ttyS0 write_flash -fm dout 0x0 ESP_Easy_mega-20190301_normal_ESP8266_1M.bin

miniterm.py /dev/ttyS0 115200 -e
(reboot sonoff)

INIT : Booting version: mega-20190301 (ESP82xx Core 2_4_2, NONOS SDK 2.2.1(cfd48f3), LWIP: 2.0.3 PUYA support)
504 : INIT : Cold Boot - Restart Reason: Power on
506 : FS   : Mounting...
2814 : FS   : Mount successful, used 0 bytes of 113201
RESET: Resetting factory defaults... using default settings
RESET: Warm boot, reset count: 0
RESET: formatting...
RESET: formatting done...
RESET: Succesful, rebooting. (you might need to press the reset button if you've justed flashed the firmware)

 ets Jan  8 2013,rst cause:1, boot mode:(3,7)

load 0x4010f000, len 1384, room 16
tail 8
chksum 0x2d
csum 0x2d
vbb28d4a3
~ld
 ?U74 :

INIT : Booting version: mega-20190301 (ESP82xx Core 2_4_2, NONOS SDK 2.2.1(cfd48f3), LWIP: 2.0.3 PUYA support)
75 : INIT : Warm boot #1 - Restart Reason: Software/System restart
78 : FS   : Mounting...
84 : FS   : Mount successful, used 75802 bytes of 113201
445 : CRC  : program checksum       ...OK
457 : CRC  : SecuritySettings CRC   ...OK
458 : CRC  : binary has changed since last save of Settings
479 : INIT : Free RAM:26488
481 : INIT : I2C
482 : INIT : SPI not enabled
496 : INFO : Plugins: 46 [Normal] (ESP82xx Core 2_4_2, NONOS SDK 2.2.1(cfd48f3), LWIP: 2.0.3 PUYA support)
499 : WIFI : No valid wifi settings
500 : WIFI : Could not connect to AP!
502 : WIFI : Set WiFi to AP
1424 : WIFI : AP Mode ssid will be ESP_Easy_0 with address 192.168.4.1
2762 : WD   : Uptime 0 ConnectFailures 0 FreeMem 23040 WiFiStatus 0


GOOD !!!!!!!


