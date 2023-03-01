---
title: Linux Pakete mit fpm bauen
author: Philipp Weißmann
type: post
date: 2015-05-19T19:15:13+00:00
url: /linux-pakete-mit-fpm-bauen/
categories:
  - Uncategorized
tags:
  - Administration
  - Linux

---
# Software installieren

Unter den meisten Linux Distributionen wird Software zumeist via Paketmanager  
installiert.  
Gerade in der Software-Entwicklung kommt es aber immer wieder dazu, dass  
man selbstkompilierte oder selbstentwickelte Software installieren muss.

Der übliche "Installationsmechanismus" via 

    ./configure && make && make install

führt jedoch dazu, dass die Software unversioniert installiert wird und eine  
Deinstallation nur in mühseliger Handarbeit möglich ist.  
Auch die Installation auf mehreren Rechner erfordert immer wieder den selben  
Aufwand und eine Updatemöglichkeit gibt es ebenfalls nicht.

# Pakete

Die optimale Lösung für unser Problem ist natürlich die Erstellung eines  
eigenen Pakets:  
Das Paket wird ein einziges Mal gebaut, kann jederzeit deinstalliert werden  
und die Version des Pakets ist ebenfalls protokolliert, so dass später Updates  
möglich sind.

Das Problem daran ist, dass das Entwickeln von Paketen recht Aufwändig ist.  
Eine Abhilfe schafft hierbei das  
Werkzeug [fpm][1].

# Installation

Zunächst stellen wir sicher, dass auf unserem Rechner das Paket `ruby-dev`  
installiert ist:

Bei auf Debian basierenden Systemen (z.B. Ubuntu):

    sudo apt-get install install ruby-dev

Bei auf RedHat basierenden Systemen (z.B. CentOS): 

    sudo yum install fpm

Nun können wir mit dem Ruby Paketinstaller `gem` das Programm installieren:

    gem install fpm

Nun sollte das Programm `fpm` auf der Kommandozeile zur Verfügung stehen.

# Paket bauen

Wir haben nun unsere Software wie zuvor und bauen diese - jedoch mit einem  
Präfix, z.B.:

    mkdir /tmp/place_to_install
    ./configure && make && make install DESTDIR=/tmp/place_to_install

Wenn wir nun an den Ort `/tmp/place_to_install` schauen, sehen wir dort die  
installierten Daten. Diese sollen nun in unser Paket kommen.  
Diese bauen wir mit:

    fpm -s dir -t rpm -n myprogram -v 0.1.2 -C /tmp/place_to_install bin lib

Hierbei stehen die Parameter für:

  * `-s dir`: Das Paket wird aus einem Verzeichnis gebaut (andere Möglichkeiten u.a. Python Module, rpm Dateien usw.)
  * `-t rpm`: Es soll ein rpm-Paket gebaut werden. Auch deb-Pakete sind möglich
  * `-n myprogram`: Der Name des Pakets
  * `-v 0.1.2`: Die Version des Pakets
  * `-C /tmp/place_to_install`: Das Verzeichnis, in dem sich die Dateien befinden
  * `bin lib`: Die Dateien/Verzeichnisse in dem Verzeichnis, welche auch wirklich im Zielsystem installiert werden sollen

Nach kurzer Wartezeit purzelt aus dem Werkzeugs ein installierbares Paket heraus.

# Fazit

Mit fpm lassen sich bequem, schnell und einfach Pakete bauen.  
Natürlich berücksichtigt das hier erstellte Paket keinerlei Abhängigkeiten und  
es werden auch nicht alle Möglichkeiten und Funktionen des Paketmanagements genutzt, aber  
in der Praxis erleichtert dies die Installation von Software - gerade in Teams  
ungemein.

Jetzt nur noch ein Repository-Server aufgesetzt - und schon hat man im Team  
eine komfortablen Weg Software bereit zu stellen.

 [1]: https://github.com/jordansissel/fpm