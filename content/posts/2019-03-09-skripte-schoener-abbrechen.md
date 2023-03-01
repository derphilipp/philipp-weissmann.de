---
title: Skripte schöner abbrechen
author: Philipp Weißmann
type: post
date: 2019-03-09T12:34:23+00:00
url: /skripte-schoener-abbrechen/
categories:
  - Uncategorized
tags:
  - bash
  - pipefail
  - script
  - shell

---
Statt jede Zeile eines Shell-Skripts auf korrekte Ausführung zu überprüfen und gegebenenfalls abzubrechen, hilft folgendes:

<pre><code class="language-sh">#!/usr/bin/env bash
set -Eeuo pipefail</code></pre>

Diese Zeile führt beim Fehlerfall einer Zeile zum Abbruch des gesamten Skripts. Praktisch!

<img decoding="async" src="https://philipp-weissmann.de/wp-content/uploads/2019/04/exit-1024x683.jpg" alt="Exit Symbol" />