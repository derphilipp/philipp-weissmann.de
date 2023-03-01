---
title: Python auf dem ESP8266
author: Philipp Weißmann
type: post
date: 2017-01-20T17:00:02+00:00
url: /python-auf-dem-esp8266/
categories:
  - Uncategorized
tags:
  - Embedded
  - Esp8266
  - Micropython
  - Python

---
Der [ESP8266][1] ist ein kleiner Mikrocontroller, den es für kleines Geld in verschiedenen Ausführungen und von verschiedensten Herstellern gibt.  
Das kleine 32-Bit Board besticht neben einfacher Zugänglichkeit, niedrigem Preis und einem on-board WLAN Modul.

Für viele Zwecke lohnt sich ein Blick auf [Micropython][2] als Alternative zu "klassischer" Arduino C++ Entwicklung für das kleine Wunderwerk.

<img decoding="async" src="https://philipp-weissmann.de/wp-content/uploads/2017/01/esp8266.jpg" alt="ESP8266 Microcontroller" /> 

Diese auf Python 3 basierende, spezialisierte Version von Python bringt vieles mit, was man sich auf einer Entwicklungsplattform wünscht:

  * Interaktive Programmierung/Nutzung des Geräts mit [REPL][3]
  * Bibliotheken für Netzwerkkonfiguration
  * Bibliotheken für Schnittstellen (Pins, I2C, SPI, ...)  
    <!--more-->

Für den einfachen Einstieg mit dem ESP8266 laden wir uns zunächst die aktuellste (stable) Version für das Board [hier][4] herunter.

Als nächstes installieren wir uns das Tool [esptool][5], welches zum Flashen des Microcontrollers mit unserem Micropython-Image genutzt wird.  
Dies geschieht am einfachsten mit 

    pip3 install esptool

bzw.

    sudo -H pip3 install esptool

falls notwendig.

Unter Windows und OS X ist es nun notwendig, den passenden Treiber für das Board zu installieren. Dieser sorgt dafür, dass das Gerät als serielle Schnittstelle auftaucht - unter aktuellen GNU/Linux Versionen ist dies in der Regel nicht notwendig.

Nun sollte das Gerät beim Anschliessen via USB auftauchen:  
So meldet sich der ESP8266 der Variante "Nodemcu" als  
`/dev/cu.SLAB_USBtoUART` bzw `/dev/tty.SLAB_USBtoUART`.

Dies unterscheidet sich nach Treiber und Betriebssystem. 

**Bei allen folgenden Beispielen muss `/dev/cu.SLAB_USBtoUART` mit dem passenden Pfad ersetzt werden.**

Zunächst löschen wir den vorhandenen Flash des Geräts vollständig:

    esptool.py --port /dev/cu.SLAB_USBtoUART erase_flash

Dann schreiben wir das heruntergeladene Image auf unser Board.

    esptool.py \
        --port /dev/cu.SLAB_USBtoUART \
        -b 460800 \
        write_flash \
        --flash_size=detect --flash_mode=dio 0 \
        /Pfad/Zu/Image/esp8266-20170108-v1.8.7.bin --verify

<img decoding="async" src="https://philipp-weissmann.de/wp-content/uploads/2019/04/python-1024x683.jpg" alt="Python" /> 

Bei Problemen kann die Baud-Rate (hier: 460800) verringert werden. Zudem  
sollte man dringend auf die Spannungsversorgung des Geräts achten. Schlechte  
USB Hubs können hier für viel Ärger sorgen.

Nun können wir bereits mit dem ESP8266 kommunizieren:

    screen /dev/cu.SLAB_USBtoUART -b 115200

Wir sehen (spätestens beim Drücken des Reset-Buttons des ESPs) unsere vertrauten Python REPL, welche nun interaktive Benutzung auf dem Gerät zulässt.

Entwickelt man jedoch etwas länger für das Gerät, möchte man natürlich seine gewohnte Entwicklungsumgebung/Editor einsetzen. Nun kommt das Tool [ampy][6] ins Spiel:

Dieses kleine Helferlein erlaubt es uns Dateien von und auf den ESP8266 zu  
kopieren und ein Skript auszuführen. Zur Installation kommt abermals kommt pip zum Einsatz:

    pip3 install adafruit-ampy

bzw.

    sudo -H pip3 install adafruit-ampy

Nun können wir unsere Bibliotheken-Dateien auf den ESP kopieren.

Auch unser Hauptprogramm (auf dem Gerät immer `main.py`) können wir so auf das Gerät bringen.  
Dieses startet bei jedem Neustart des Geräts automatisch.

    ampy -p /dev/cu.SLAB_USBtoUART put main.py

Wollen wir das Programm gleich ohne Reset starten, können wir auch dies einfach mit `ampy` erledigen:

    ampy -p /dev/cu.SLAB_USBtoUART run -n main.py

Mit diesen Werkzeugen ist es nun möglich in wenigen Sekunden automatisiert neue Versionen von Software auf das Gerät aufzuspielen um diese auszuprobieren.  
Dies verringert die Zeit des klassischen Workflows von "Programmieren, (Cross)-Kompilieren, Flashen" drastisch und erlaubt Fans von Python ein komfortables Arbeiten mit dem ESP8266.

Viel Spaß!

 [1]: https://de.wikipedia.org/wiki/ESP8266
 [2]: https://micropython.org/
 [3]: https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop
 [4]: https://micropython.org/download
 [5]: https://github.com/espressif/esptool
 [6]: https://github.com/adafruit/ampy