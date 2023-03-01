---
title: Touch Display auf Raspberry Pi mit Arch Linux
author: Philipp Weißmann
type: post
date: 2015-04-12T12:28:29+00:00
url: /touch-display-auf-raspberry-pi-mit-arch-linux/
categories:
  - Uncategorized
tags:
  - Linux
  - Raspberry Pi

---
Auf der Suche nach einem kleinen Display bin ich auf ein [Display von Watterott][1] gestoßen.  
Um das Gerät auf dem [Raspberry Pi][2] unter [Arch Linux][3] zu betreiben sind einige Schritte notwendig.

<!--more-->

  1. Für alle Schritte nehme ich als User `root` an 
  2. "Normale" Arch Linux [Installation auf dem Raspberry Pi durchführen][4] 
  3. Hilfswerkzeug `rpi-update` installieren:</p> 
        curl -L --output /usr/bin/rpi-update https://raw.githubusercontent.com/Hexxeh/rpi-update/master/rpi-update && sudo chmod +x /usr/bin/rpi-update

  4. Kernel mit passenden Treibern installieren</p> 
        REPO_URI=https://github.com/notro/rpi-firmware rpi-update

  5. X installieren</p> 
        pacman -S xorg-server xorg-xinit xorg-utils xorg-server-utils

  6. Optional: Tool zur Kalibrierung des Touch-Displays installieren</p> 
        pacman -S xinput_calibrator

  7. Konfigurationsdateien:  
    7.1. Am Ende `/boot/config.txt:` einfügen:</p> 
        dtparam=spi=on
        dtoverlay=rpi-display
    
    7.2. Am Ende von `/etc/modules-load.d/raspberrypi.conf` einfügen:
    
        snd-bcm2835
        spi_bcm2708
        fbtft_device
    
    7.3. Datei `/etc/modprobe.d/fbtft.conf` anlegen und folgenden Inhalt  
    einfügen:
    
        options fbtft_device name=mi0283qt-9a gpios=reset:23,led:18 speed=32000000 rotate=270
    
    Achtung: Je nach Ausführung des Displays unterscheiden sich die  
    Parameter - einfach in die [Liste aufGithub][5]  
    schauen.
    
    Achtung: Mit dem Parameter `rotate=270` dreht sich die Ausrichtung  
    des Displays
    
    7.4. Datei `/etc/X11/xorg.conf.d/99-fbturbo.conf` anlegen und  
    folgenden Inhalt einfügen:
    
        Section "Device"
        Identifier "Allwinner A10/A13 FBDEV"
        Driver "fbturbo"
        Option "fbdev" "/dev/fb0"
        Option "SwapbuffersWait" "true"
        EndSection
    
    7.5 Ans Ende der vorhandenen Datei `/etc/X11/xinit/xinitrc`  
    einfügen:
    
        xinput --set-prop 'ADS7846 Touchscreen' 'Evdev Axes Swap' 1
        xinput --set-prop 'ADS7846 Touchscreen' 'Evdev Axis Inversion' 0 1
    
    Achtung: Hiermit dreht sich die Ausrichtung des Touch-Displays  
    passend zu den oben eingestellten 270 Grad; </li> 
    
      * Reboot</p> 
            reboot
    
      * Nach dem Ausführen von</p> 
            startx
        
        sollte nun eine grafische Oberfläche auf dem kleinen Display laufen. </li> </ol>

 [1]: https://github.com/watterott/RPi-Display
 [2]: https://www.raspberrypi.org/
 [3]: http://archlinuxarm.org/
 [4]: http://web.archive.org/web/20150412224859/archlinuxarm.org/platforms/armv6/raspberry-pi
 [5]: https://github.com/watterott/RPi-Display/blob/5aa1b9b6c947f9e8350cb87eb8870e14a49e2450/docu/FBTFT-Install.md