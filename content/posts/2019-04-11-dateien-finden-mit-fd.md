---
title: Dateien finden mit fd
author: Philipp Weißmann
type: post
date: 2019-04-11T16:00:10+00:00
url: /dateien-finden-mit-fd/
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

<img decoding="async" src="https://philipp-weissmann.de/wp-content/uploads/2019/04/lps-1024x680.jpg" alt="LPs" /> 

# Beispiel1

Finde alle Dateien mit der Zeichenfolge _schuh_ im Namen:

find: 

<pre><code class="language-bash">find . -iname &#039;*schuh*&#039;</code></pre>

fd:

<pre><code class="language-bash">fd schuh</code></pre>

# Beispiel 2

Finde alle .jpg Dateien:

find: 

<pre><code class="language-bash">find . -iname &#039;*.jpg&#039;</code></pre>

fd:

<pre><code class="language-bash">fd -e jpg</code></pre>

# Beispiel 3

Finde alle .png Dateien und konvertiere diese in .jpg Dateien:

find:

<pre><code class="language-bash">find ./ -name &#039;*.png&#039; -exec bash -c &#039;convert $0 ${0/png/jpg}&#039; {} \;
# Konvertiert eine nach der anderen Datei</code></pre>

fd:

<pre><code class="language-bash">fd -e png -x convert {} {.}.jpg
# Konvertiert parallel mehrere Dateien auf einmal</code></pre>

# Fazit:

Wer `find` in- und auswendig beherrscht hat keinen Zwang zu wechseln. Der bequeme Syntax von `fd` macht das Leben jedoch leichter. Die Möglichkeit parallel mehrere Dateien zu verarbeiten ist ungemein praktisch. Daher ist `fd` für jeden Kommandozeilen-Fan absolut empfehlenswert.

 [1]: https://www.gnu.org/software/findutils/manual/html_mono/find.html
 [2]: https://github.com/sharkdp/fd