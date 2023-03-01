---
title: Wget wiederaufnehmen
author: Philipp Weißmann
type: post
date: 2016-04-13T05:46:16+00:00
url: /wget-wiederaufnehmen/
categories:
  - Uncategorized
tags:
  - Linux
  - macOS
  - Tools

---
Beim Download großer Dateien (z.B. Iso-Images, Podcasts) ist es oft hilfreich einen bereits begonnenen Download weiterführen zu können.

Mit dem Download-Werkzeug `wget` ist dies einfach mit der Kommandozeilenoption `-r` möglich.

Damit man jedoch nicht immer daran denken muss, lässt sie dies auch als Standardverhalten einstellen.

Hierzu tragen wir die die Datei `~/.wgetrc` folgendes ein:

    continue = on

Ab sofort nimmt `wget` Downloads automatisch wieder auf.