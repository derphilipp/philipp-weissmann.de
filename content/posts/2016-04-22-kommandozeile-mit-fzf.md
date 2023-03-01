---
title: Kommandozeile mit FZF
author: Philipp Weißmann
type: post
date: 2016-04-22T08:01:39+00:00
url: /kommandozeile-mit-fzf/
categories:
  - Uncategorized
tags:
  - Linux
  - macOS
  - Produktivität

---
Wer viel auf der Kommandozeile/Shell arbeitet, lernt im Lauf der Zeit einige nützliche Tools und Tastaturkürzel kennen.  
So stöbert man in `bash` bzw. `zsh`mit `Ctrl+R` in der Eingabe-History, sucht mit `find` Dateien in einem gegeben Pfad - und so weiter und so fort.

Ein nützliches Helferlein, welches die beiden Aktionen (und mehr) beschleunigt  
ist [`fzf`][1]:

<!--more-->

In [Go][2] geschrieben und fix installiert (z.B. via Arch Linux Aur, zu Fuß oder als via Vim-Plugin) kann das Werkzeug händisch genutzt werden oder in Verbindung mit `tmux` auch die oben genannten Tastaturkürzel übernehmen.

Und so sieht das ganze aus:

<img decoding="async" src="https://camo.githubusercontent.com/0b07def9e05309281212369b118fcf9b9fc7948e/68747470733a2f2f7261772e6769746875622e636f6d2f6a756e6567756e6e2f692f6d61737465722f667a662e676966" alt="Interaktives fzf" /> 

Jetzt erlaubt das Tool interaktiv und komfortabel nach Dateien zu suchen, alte Befehle aufzufinden und damit den Komfort des Arbeitens auf der Kommandozeile deutlich zu steigern.

 [1]: https://github.com/junegunn/fzf
 [2]: http://golang.org