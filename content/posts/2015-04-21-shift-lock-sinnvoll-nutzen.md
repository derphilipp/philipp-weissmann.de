---
title: Shift Lock sinnvoll nutzen
author: Philipp Weißmann
type: post
date: 2015-04-21T19:01:17+00:00
url: /shift-lock-sinnvoll-nutzen/
categories:
  - Uncategorized
tags:
  - Linux
  - macOS
  - Produktivität
  - Windows

---
# Shift-Lock

Die Shift-Lock Taste alias "Feststelltaste" ist für die meisten Menschen ein Ärgernis und  
Relikt aus der Zeit der Schreibmaschinen.

Doch anstatt die Taste zu deaktivieren oder gar auszubauen kann die Taste auch gut für andere  
Zwecke verwendet werden.

Ich habe die Shift-Lock Taste auf die "Ctrl" (Steuerung) Taste gemappt, was Shortcuts wie _Ctrl+C_ in vim deutlich attraktiver macht

# So gehts

<!--more-->

## Windows

Unter Windows erstellen wir eine Datei mit der Endung .reg, z.B. `shift.reg` mit folgendem Inhalt:

     REGEDIT4
    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout]
     "Scancode Map"=hex:00,00,00,00,00,00,00,00,02,00,00,00,1d,00,3a,00,00,00,00,00

Nach dem Importieren in die Registry (i.d.R. Doppellick auf die neue Datei) und einem Neustart sollte die Tastet nun die neue Funktion haben.

## OS X

Unter OS X fällt die Einstellung etwas einfacher aus:  
In den "System Preferences" wählen wir den Punkt "Keyboard" aus.  
Dort, im Reiter "Keyboard", befindet sich ein Knopf namens "Modifier Keys...".

Hier können wir die Belegung von "Caps Lock" (d.h. Shift Lock), "Control", "Option" und auch "Command" ändern.

Achtung: Diese Einstellung ist nur für das aktuelle Keyboard gültig, d.h. bei  
Notebook mit externer Tastatur muss diese Einstellung sowohl für die eingebaute als auch die externe Tastatur durchgeführt werden.

## Linux, BSD, u.a.

Unter Linux/BSD kann diese Einstellung oftmals in den jeweiligen Systemwerkzeugen getroffen werden.  
Eine "eher universale" Möglichkeit für X ergibt sich mit folgendem Befehl:

    setxkbmap -option ctrl:nocaps

# Fazit

Mit geringem Aufwand kann man die "nervige" Shift-Lock Taste in eine wertvolle Taste  
verwandeln.  
Nach etwas Umgewöhnung nutze ich die "normale" Control Taste praktisch gar nicht mehr und bei der Nutzung von `vim` gehen Shortcuts wie _Ctrl+C_  
(in den _normal mode_ wechseln) und _Ctrl+V_ (_visual block mode_) deutlich leichter von der Hand.