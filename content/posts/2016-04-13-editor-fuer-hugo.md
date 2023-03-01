---
title: Editor für Hugo
author: Philipp Weißmann
type: post
date: 2016-04-13T14:26:13+00:00
url: /editor-fuer-hugo/
categories:
  - Uncategorized
tags:
  - Hugo

---
Hugo ist eine schöne Software um Software um statische Webseiten und Blogs zu  
erstellen.

Die in [Go][1] geschriebene Software ermöglicht das einfache  
Nutzen von Templates für neue Beiträge. Ein neuer Beitrag wird auch leichter  
Hand angelegt, z.B. `hugo new post/hugo_editor.md`.

Die Datei enthält danach alle Einträge des Templates - teilweise auch schon  
ausgefüllt.

Eine interessante Konfigurationseinstellung in der `config.toml` (bzw.  
`config.yaml`, `config.json`) ist der Eintrag `newContentEditor`:  
Gesetzt auf den Editor öffnet sich dieser dem Anlegen der Datei die Schreiberei  
kann beginnen.

    newContentEditor = "vim"

 [1]: https://golang.org/