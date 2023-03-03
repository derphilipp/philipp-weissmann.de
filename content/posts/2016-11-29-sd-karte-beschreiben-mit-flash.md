---
title: SD Karte beschreiben mit „flash“
author: Philipp Weißmann
type: post
date: 2016-11-29T08:30:27+00:00
url: /sd-karte-beschreiben-mit-flash/
cover: /img/sd-karte-beschreiben-mit-flash.jpg
categories:
  - Uncategorized
tags:
  - Linux
  - macOS
  - Raspberry Pi

---
Um einen Raspberry Pi in Betrieb zu nehmen, ist es notwendig eine SD Karte mit einem Betriebssystem zu beschreiben.
Dabei ist es in der Regel nicht mit einem einfachen Datei kopieren getan.

Unter Windows bietet sich [Win32 Disk Imager][1] an,
unter macOS das Tool [ApplePi Baker][2] und unter Linux nutzt man einfach `dd`.

Nun wünscht man sich bei häufiger Nutzung ein einfaches Kommandozeilentool, dass diese Aufgabe komfortabel übernimmt.

Genau das erledigt das Tool [flash][3].
Das in [bash][4] geschrieben Werkzeug ist schnell installiert:

    curl -O https://raw.githubusercontent.com/hypriot/flash/master/$(uname -s)/flash
    chmod +x flash
    sudo mv flash /usr/local/bin/flash

Wie in der [Installationsanleitung auf Github][3] zu sehen, sind noch optionale Abhängigkeiten auf einige Tools zu installieren (u.a. `curl`, `pv`, `unzip`).
Nach erfolgreicher Installation durch den Paketmanager des Vertrauens, können Raspberry Images geschrieben werden:

    flash jessie-light.zip

Dabei übernimmt `flash` das entpacken (bzw. Download) der Datei und fordert den Benutzer anschließend auf, die SD Karte einzulegen. Nach Identifizieren des Speichermediums braucht man lediglich selbiges zu bestätigen und der Schreibeprozess beginnt.

Zum Abschluss des Ganzen werden auch alle Dateisystem ausgehängt und die Speicherkarte kann in den Raspberry Pi wandern.

Für mich ist `flash` _das_ Werkzeug zum Schreiben von SD Karten geworden.
Minimalistisch, komfortabel und einfach zu handhaben erleichtert mit das kleine Helferlein den Alltag.

 [1]: https://sourceforge.net/projects/win32diskimager/
 [2]: http://www.tweaking4all.com/software/macosx-software/macosx-apple-pi-baker/
 [3]: https://github.com/hypriot/flash
 [4]: https://de.wikipedia.org/wiki/Bash_(Shell)