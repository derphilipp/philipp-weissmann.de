---
title: Systemdateien editieren mit sudoedit
author: Philipp Weißmann
type: post
date: 2016-05-18T11:44:20+00:00
url: /systemdateien-editieren-mit-sudoedit/
categories:
  - Uncategorized
tags:
  - Linux
  - sudoedit

---
Praktisch jeder Entwickler und jeder Administrator hat seine eigene Editor-Konfiguration.  
Ob Farbschema, Plugins, eigene Kürzel oder Optionen - kaum ein Werkzeug wird  
so intensiv den eigenen Vorstellungen, Wünschen und Vorlieben angepasst wie ein  
Editor.

Muss jedoch eine Datei editiert werden, die nicht dem Benutzer "gehört" (z.B.  
Konfigurationsdateien eines Webservers), funktioniert der "eigene" Editor nicht  
mehr.

<!--more-->

So öffnet sich beim Aufruf via `sudo vim /etc/nginx/nginx.conf` zwar der Editor  
vim, aber die schöne eigene Konfiguration wird nicht geladen, da ja der Editor  
unter einem anderen Benutzer gestartet wird.

Abhilfe schafft hier das auf modernen Systemen installierte `sudoedit`.  
Dieses Helferlein öffnet den präferierten Editor des Benutzers (setzen mit  
Umgebungsvariable `EDITOR`) unter dessen Kontext.

So kann mit `sudoedit /etc/nginx/nginx.conf`, wie zuvor mit `sudo`,  
die Konfigurationsdatei des Webservers editiert werden - und das mit den  
Editor-Einstellungen des Benutzers.