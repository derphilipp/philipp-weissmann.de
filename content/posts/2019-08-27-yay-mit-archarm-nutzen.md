---
title: yay mit archarm nutzen
author: Philipp Weißmann
type: post
date: 2019-08-27T18:28:54+00:00
url: /yay-mit-archarm-nutzen/
categories:
  - Uncategorized
tags:
  - arch
  - Linux
  - Raspberry Pi
  - Tools

---
Viele Entwickler schätzen es aktuelle Werkzeuge zu nutzen.
Ob Compiler, Editor oder Shell - neue Versionen haben neue Features, bereinigte Bugs und mehr.

Daher ist in den letzten Jahren die Linux Distribution "Arch" auch sehr beliebt geworden: [Rolling Releases][1] statt großer Versionssprünge erleichtern den Entwickleralltag.
Auch auf dem Raspberry Pi läuft diese Distribution.

<img decoding="async" src="https://philipp-weissmann.de/wp-content/uploads/2019/08/tool-1024x763.jpg" alt="" />

Aus der Community getrieben Pakete können aus dem [AUR][2] mit einem beliebigen Tool installiert werden.
Derzeit verwende ich dafür gerne [yay][3].

Um `yay` auf dem Raspberry Pi zu installieren, sind folgende Schritte notwendig:

```bash
# Notwendige Pakete installieren
sudo pacman -S git go make binutils gcc fakeroot

# yay via git clonen und installieren
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

Dann steht der Installation von Paketen aus dem AUR nichts mehr im Wege.

 [1]: https://de.wikipedia.org/wiki/Rolling_Release "Rolling Releases"
 [2]: https://wiki.archlinux.org/title/Arch_User_Repository "AUR"
 [3]: https://github.com/Jguer/yay