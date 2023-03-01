---
title: 'Myrepos: Alle meine Repositories'
author: Philipp Weißmann
type: post
date: 2015-05-17T13:15:05+00:00
url: /myrepos-alle-meine-repositories/
categories:
  - Uncategorized
tags:
  - Administration
  - Git
  - Linux
  - macOS
  - Produktivität

---
# Repository-Zentrale

Dank VCSH habe ich all meine Dotfiles hübsch in Git-Repositories verpackt.  
Das Einbinden eines einzelnen Repositories geht nun zwar schnell von der Hand,  
aber wenn nun für `vim` und `mutt` und `emacs` und und und ... lauter  
Repositories vorliegen wird es unbequem.  
Auch das updaten (`pull`) jedes einzelnen Repos ist sehr mühselig und damit  
fehleranfällig.

Abhilfe schafft hier [myrepos][1] (kurz `mr`),  
dass es erlaubt Aktionen auf mehreren Repositories auszuführen.

<!--more-->

# Installation

Wir installieren uns das Paket `myrepos` via `apt-get` oder `yaourt`

Installation unter Debian/Ubuntu:

    sudo apt-get install myrepos

oder unter Arch Linux

    yaourt -S myrepos

# Basis-Konfiguration

Wir legen eine Konfigurationsdatei mit dem Namen `~/.mrconfig` an mit folgendem  
Inhalt:

    [DEFAULT]
    git_gc = git gc "$@"
    jobs = 1
    include = cat ~/.config/mr/config.d/*

Wenn nach allen Schritten die Konfiguration zuverlässig installiert können wir  
die Anzahl der parallelen Jobs auf z.B. 4 erhöhen.

Nun legen wir folgende Verzeichnisse an:

    mkdir -p ~/.config/mr/config.d
    mkdir ~/.config/mr/available.d

In das Verzeichnis `available.d` legen wir alle Konfigurationsdateien ab.

Eine solche Konfigurationsdatei enthält den Ort Zielort des Repositories  
und auch die Anweisung, woher die Quelle kommt. 

Die Datei für eine `vim`-VCSH-Konfiguration könnte z.B. so aussehen:

Dateiname: `vim.vcsh`

    [$HOME/.config/vcsh/repo.d/vim.git]
    checkout = vcsh clone git@MEINGITSERVER:vim vim

Dabei kann myrepos vcsh oder direkt git oder auch subversion (u.v.m.) nutzen.

Nun linke (`ln -s`) ich noch alle die Konfigurationsdateien nach `available.d`,  
die auch wirklich auf all meinen Systemen nutzen möchte.

Mit dem Aufruf

    mr up

Aktualisiere (z.B. bei git: pull) ich nun alle Repositories, die ich via  
myrepos verwalte. Somit kann ich beim Wechsel von Rechnern einfach meine  
Konfiguration aktualisieren.

Auch pushen von allen Repositories ist möglich:

    mr push

usw.

# Myrepos in VCSH

Auch die Konfiguration von myrepos selbst verwalte ich mit vcsh (und  
wiederum mit Datei-Eintrag in myrepos), so dass sich auch beim Hinzukommen  
von neuen Repositories ich diese auf meinen Geräten erhalte.

# Neuer Rechner - einfacher Schritt

Bei einem neuen Rechner sind nun extrem wenige Schritte notwendig:

  1. Installieren von vcsh und myrepos (gibt es zumeist im Paketmanager)
  2. Klonen des myrepos vcsh repositories (d.h. `vcsh clone git@MEINGITSERVER:mr mr`) 
  3. Klonen aller weiteren Repos via `mr up`

# Sonderfälle

Auch einfache Programme (z.B. [youtube-dl][2])  
installiere (und update) ich via myrepos: Hierzu leg ich ich wieder eine  
Konfigurationsdatei an (z.B. `youtube-dl.git`) mit folgendem Inhalt:

    [$HOME/.local/opt/youtube-dl.git]
    checkout = git clone https://github.com/rg3/youtube-dl.git $HOME/.local/opt/youtube-dl.git
    push = echo "No pushing to public repo"

Der `push` Befehl wird hier explizit überschrieben und gibt bei `mr push` einfach die  
Nachricht aus, dass ich in dieses Repository nicht pushen möchte.

# Fazit

Myrepos ermöglicht das einfache und bequeme Verwalten und Nutzen von vielen  
Repositories. Gerade das Updaten oder initiale Klonen wird damit deutlich  
bequemer. Insbesondere im Zusammenspiel mit VCSH wird eine extrem komfortable  
Verwaltung der eigenen Dotfiles (und mehr) möglich.

 [1]: https://myrepos.branchable.com/
 [2]: https://rg3.github.io/youtube-dl/