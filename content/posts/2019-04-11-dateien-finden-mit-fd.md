---
title: Dateien finden mit fd
author: Philipp Weißmann
type: post
date: 2019-04-11T16:00:10+00:00
url: /dateien-finden-mit-fd/
cover: /img/lps.jpg
categories:
  - Uncategorized
tags:
  - Linux
  - macOS
  - Tools

---
Das Tool [find][1] ist ein praktisches Programm und Dateien und Ordner zu finden.
Find kann aber auch komplexere Aktionen wie z.B. mehrere Dateien konvertieren. Leider ist es jedoch nicht allzu einsteigerfreundlich.

Hier kommt [fd][2] ins Spiel:

Das Open-Source Programm erledigt nahezu alle Aufgaben von `find`, ist aber einfacher zu bedienen.

# Beispiel1

Finde alle Dateien mit der Zeichenfolge _schuh_ im Namen:

find:

```bash
find . -iname '*schuh*'
```

fd:

```bash
fd schuh
```

# Beispiel 2

Finde alle .jpg Dateien:

find:

```bash
find . -iname '*.jpg'
```

fd:

```bash
fd -e jpg
```

# Beispiel 3

Finde alle .png Dateien und konvertiere diese in .jpg Dateien:

find:

```bash
# Konvertiert eine nach der anderen Datei
find ./ -name '*.png' -exec bash -c 'convert $0 ${0/png/jpg}' {} \;
```

fd:

```bash
# Konvertiert parallel mehrere Dateien auf einmal
fd -e png -x convert {} {.}.jpg
```

# Fazit:

Wer `find` in- und auswendig beherrscht hat keinen Zwang zu wechseln. Der bequeme Syntax von `fd` macht das Leben jedoch leichter. Die Möglichkeit parallel mehrere Dateien zu verarbeiten ist ungemein praktisch. Daher ist `fd` für jeden Kommandozeilen-Fan absolut empfehlenswert.

 [1]: https://www.gnu.org/software/findutils/manual/html_mono/find.html
 [2]: https://github.com/sharkdp/fd