---
title: Skripte schöner abbrechen
author: Philipp Weißmann
type: post
date: 2019-03-09T12:34:23+00:00
url: /skripte-schoener-abbrechen/
cover: /img/exit.jpg
categories:
  - Uncategorized
tags:
  - bash
  - pipefail
  - script
  - shell

---
Statt jede Zeile eines Shell-Skripts auf korrekte Ausführung zu überprüfen und gegebenenfalls abzubrechen, hilft folgendes:

```sh
#!/usr/bin/env bash
set -Eeuo pipefail
```

Diese Zeile führt beim Fehlerfall einer Zeile zum Abbruch des gesamten Skripts. Praktisch!