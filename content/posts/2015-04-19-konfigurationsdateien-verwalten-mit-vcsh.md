---
title: Konfigurationsdateien verwalten mit VCSH
author: Philipp Weißmann
type: post
date: 2015-04-19T17:32:15+00:00
url: /konfigurationsdateien-verwalten-mit-vcsh/
categories:
  - Uncategorized
tags:
  - Administration
  - Git
  - Linux
  - macOS
  - Produktivität

---
# Einstellungen

Was ist der erste Schritt bei der Benutzung eines Autos, einer Stereoanlage oder eines Schreibtischstuhls?  
Die Einstellungen!  
Natürlich will man gut aus dem Fahrzeug sehen können, der Lieblings-Musik lauschen und bequem sitzen.

Doch auch Software hat Einstellungen:

  * Welchen Editor setze ich als Standard?
  * Welche Shell-Erweiterungen lade ich in `oh-my-zsh`?
  * Welches `color-theme` lade ich in vim?
  * Welche Accounts habe ich in `mutt`?

Praktischerweise liegen all diese Einstellungen in Dateien (sogenannten "Dotfiles"), welche sich einfach von A nach B kopieren lassen.  
Da ich jedoch regelmässig auf unterschiedlichen Rechnern arbeite, möchte ich diese aktuell halten.

# Dropbox

Mein erster Ansatz war es, alle Dateien in einen zentralen Dropbox Ordner zu verschieben und Links zu erstellen nach folgendem Schema

    ~/.vimrc -> ~/Dropbox/config/vimrc

Meine `.vimrc` wurde durch den Dropbox-Dienst nun auf allen Rechnern synchronisiert und immer aktuell.  
Richtete ich einen neuen Rechner ein, so musste ich "nur" Dropbox und den Link erstellen.

Dieser Ansatz hat jedoch einige Nachteile:

  1. Ich bin von der Verfügbarkeit von Dropbox abhängig (ist ok für mich)
  2. Ich muss auf allen Rechnern Dropbox installieren (ist auch noch so ok)
  3. Ich muss alle Dateien händisch verlinken (nicht ok!)
  4. Die Änderungen sind nicht dokumentiert bzw. haben keine definierten Zwischenstände (nicht ok!)
  5. Alle Änderungen werden sofort bei allen Systemen aktualisiert (außer ich stoppe Dropbox)

# VCSH

Ich wünschte mir ein System, welches die Versionierung der Konfigurationsdaten übernimmt und bin dabei auf VCHS gestoßen.

Das schöne an VCSH: Es baut einfach auf git auf und bietet somit einerseits ein vertrautes Interface. Zudem kann ich meine Konfigurationsdateien nun einfach in ein zentrales Repository (z.B. auf Github oder auf einem eigenen Server) ablegen.

## Installieren

Installieren erfolgt aus dem Repository, Debian/Ubuntu also per 

    apt-get install vcsh

oder bei Arch Linux via aur (hier mit yaourt)

    yaourt -S vcsh

## Anlegen

Ich empfehle pro Werkzeug (z.B. emacs, mutt, ...) ein eigenes Repository anzulegen um die Übersicht zu behalten.  
Die Syntax hierbei entspricht der von git, jedoch mit Namen des Werkzeugs vorangestellt, also `vcsh WERKZEUG GIT-BEFEHL` (Ausnahme: `init`-Befehl)

Wir initialisieren uns erstmal ein Repository für unsere Vim-Einstellungen...

    vcsh init vim

... fügen die Datei(en) hinzu, die wir verwalten wollen ...

    vcsh vim add ~/.vimrc

... machen unseren ersten commit ...

    vcsh vim commit -m "Mein erster Vim-commit"

... und pushen diesen auf unseren Git-Server (z.B. Github)

    vcsh vim remote add git@MEINGITSERVER:vim.git
    vcsh vim push -u origin master

## Klonen

Auf einem neuen Rechner können wir uns die Konfiguration einfach holen:

    vcsh clone git@MEINGISERVER:vim.git

## .gitignore

Da sich unsere Konfigurationsdateien im Home-Verzeichnis des Users befinden, hat VCSH (bzw. git) keine Chance zu wissen welche Dateien definitiv zu dem Projekt gehören und welche nicht.  
Also schaffen wir mit einer .gitignore-Datei Abhilfe: Alle Dateien und Verzeichnisse sollen ignoriert werden, außer den Projektdateien/Ordnern.  
Diese erstellen wir automatisch via

    vcsh write-gitignore vim

Wie fügen die ignore-Datei selbst auch dem Projekt hinzu...

    vcsh vim add -f ~/.gitignore.d/vim

... und schreiben die Datei erneut.

    vcsh write-gitignore vim

Nun kontrollieren wir die Datei `~/.gitignore.d/vim` ob sie nicht Dateien ignoriert, welche wir versionieren wollen;  
Wenn nicht: Ab damit ins Repository!

    vcsh vim add ~/.gitignore.d/vim

Alle weiteren Aktionen können wir nun in gewohnter git-manier (commit push pull) erledigen.

# Fazit

VCSH erlaubt es bequem Dotfiles zu organisieren und diese versioniert abzulegen.  
Im Alltag hilft mir es enorm meine Konfigurationsdateien auf einem Stand zu halten und Änderungen dokumentiert.

Ergänzend zu VCSH bietet sich die Benutzung von `myrepos` ab um mehrere Repositories gleichzeitig zu verwalten.