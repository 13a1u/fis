# FIS - Feuerwehr Informationssystem

## SMS Empfänger
### Hardware
- Raspberry Pi Model B V3
- Adafruit FONA 808 Cellular + GPS Breakout
 
### Setup Raspberry Pi
- Installation Raspbian 
-  Aktualisieren der Packages & screen installieren
```sh
$ apt-get update
$ apt-get install screen
```
- Deaktivieren der seriellen Console auf GPIO [Raspberry UART](https://www.raspberrypi.org/documentation/configuration/uart.md) 
```sh
$ sudo raspi-config --> 
    Select option 5, 
    Interfacing options, 
    then option P6, Serial, and select No. 
    Exit raspi-config.
Zwei mal nein deaktiviert aber den UART komplet und /dev/ttyS0 verschwindet nach dem reboot.
Aus diesem Grund unter /boot/config.txt den Wert
    enable_uart=1
setzten.
```
- Smstools installieren
-- Download mit wget. Danach configure, make, make-install
- /etc/smsd.conf
```sh
devices = GSM1
...
loglevel = 5
incoming_utf8 = yes

[GSM1]
device = /dev/ttyS0
init = AT
incoming = yes
baudrate = 115200
```
- FONA 808 verbinden
