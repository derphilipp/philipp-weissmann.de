---
title: Vollbackup mit rsync
author: Philipp Weißmann
type: post
date: 2016-04-12T13:04:04+00:00
url: /vollbackup-mit-rsync/
categories:
  - Uncategorized
tags:
  - Linux
  - macOS
  - Tools

---
Das Tool Nummer eins um Daten von A nach B zu spiegeln ist `rsync`.  
Es kann über Rechnergrenzen hinweg eingesetzt werden (z.B. via `ssh`), beherrscht inkrementelles Kopieren und vieles mehr.

<!--more-->

Um einen (Linux) Rechner vollständig zu sichern nutze ich zumeist:

    rsync -aAXv --exclude={\
        "/dev/*","/proc/*","/sys/*","/tmp/*",\
        "/run/*","/mnt/*","/media/*","/lost+found"\
        } / /path/to/backup/folder

Der Befehl kopiert alle Dateien (mit Ausnahme der Verzeichnisse in der Aufzählung) - und das inkrementell.  
Abbrechen und Wiederaufnehmen ist also problemlos möglich.

Damit wird rsync zum perfekten Tool um eine Vollsicherung vor einer Neuinstallation vorzunehmen.