---
title: 'Geräte unter eigenem Namen: udev rules'
author: Philipp Weißmann
type: post
date: 2019-04-13T18:32:50+00:00
url: /geraete-unter-eigenem-namen-udev-rules/
cover: /img/rule.jpg
categories:
  - Uncategorized
tags:
  - Linux

---
# Das Problem

Unter Linux wird jedem verbundenen Gerät ein Pfad zugeordnet.
So erscheint z.B. ein verbundener Esp8266 Microcontroller als (serielle) Schnittstelle `/dev/ttyUSB0`.
Sind noch mehr Geräte verbunden, so erscheinen diese als `/dev/ttyUSB1`, `/dev/ttyUSB2` usw.

Welches Gerät ist aber nun welche Schnittstelle? Und sind diese nach dem Reboot noch gleich?

# Die Lösung: udev rules

Um dies sicher zu stellen erstellt man eine Regel mit _udev_:

Zunächst identifizieren wir, welches Gerät wir haben wollen. Als Beispiel nutzen wir hier einen Microcontroller, der unter `/dev/ttyUSB0` eingehängt ist.

```bash
udevadm info --name=/dev/ttyUSB0 --attribute-walk
```

Aus der Ausgabe von `udevadm` suchen wir uns einige Werte heraus: Die von `ATTRS{idVendor}`, `ATTRS{idProduct}` und `ATTRS{serial}`.
Dies sollte zum eindeutigen Identifizieren des Gerätes ausreichen.

Nun legen wir uns eine Regel-Datei an:

Eine neu erstellte `/etc/udev/rules.d/20-mydevice.rules` füllen wir nun mit den gesammelten Informationen. Natürlich müssen hier echte Werte eingesetzt werden:

    SUBSYSTEM=="tty", ATTRS{idVendor}=="1234", ATTRS{idProduct}=="abcd", ATTRS{serial}=="01010101010101010101010101010", SYMLINK+="ttyUSB_mydevice"

Nun noch die neuen Regeln anlegen:

```bash
sudo udevadm trigger
```

und den `udev` Dienst neu starten:

```bash
sudo systemctl restart udev
```

Nun sollte unsere Regel angewendet werden und ein neuer Eintrag `/dev/ttyUSB_mydevice` angelegt sein. Dieser ist ein Link auf das "echte" Gerät. Somit können wir uns immer auf den selbstgewählten Namen verlassen - auch wenn sich der automatisch Vergebene Name nach einem Neustart ändern kann.