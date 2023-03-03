---
title: Umbenennen mit dem Lieblingseditor
author: Philipp Weißmann
type: post
date: 2019-09-14T08:11:33+00:00
url: /umbenennen-mit-dem-lieblingseditor/
categories:
  - Uncategorized
tags:
  - Linux
  - macOS
  - Tools

---
Dateien umbenennen ist oft mühsam.  
Wenn man ein Extra-Werkzeug benutzt, muss man es erst lernen.  
Das schreiben eines extra Skriptes kann aber oft zu aufwendig sein.  
Es wäre doch schön, wenn man direkt im Lieblingseditor die Dateinamen verändern könnte.

Hier kommt die Werkzeugsammlung `renameutils` zum Einsatz.

## Installation

<img decoding="async" src="https://philipp-weissmann.de/wp-content/uploads/2019/09/qvm7scmftvc-683x1024.jpg" alt="" />  
Installiert wird das ganze aus den üblichen Paketmanagern, also z.B.

```bash
brew install renameutils # macOS / Linuxbrew
```

```bash
pacman-S renameutils # Arch based
```

```bash
sudo apt install renameutils # Debian based
```

## Benutzung

Nun gibt es die Befehle: `qmv` und `qcp`, mit denen Dateien umbenannt, bzw. kopiert werden können.

Beispiel:

    ls *.txt

Ausgabe:

    Kopie von hallo.txt
    Kopie von gutentag.txt
    Kopie von abrechnung.txt

Nun verwenden wir unser neues Werkzeug:

```bash
qmv *.txt
```

Nun öffnet sich unser eingestellter Editor mit einer Dateiliste und wir können die Datei-Umbenennungen direkt im Editor vornehmen.

## Fazit

Das Verwenden von Shell-Kommandos zum Umbennen ist oft schnell.  
So geht das Umbenennen aller `.txt` Dateien in `.md` schnell von der Hand.

Für komplexe Fälle können wir `qmv` verwenden. Damit können wir unseren vertrauten Editor und alle darin vorhandenen Funktionen nutzen.  
Insbesondere, wenn wir keine einfachen Regeln zum Umbenennen formulieren können, helfen uns die `renameutils` hier stark weiter.

So ist bei mir der Alias

```bash
alias ren=qmv --format=destination-only
```

fest in meine Werkzeugkiste eingezogen.