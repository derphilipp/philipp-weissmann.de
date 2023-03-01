---
title: Dateien bereinigen mit fd und sd
author: Philipp Weißmann
type: post
date: 2020-11-29T18:24:12+00:00
url: /dateien-bereinigen-mit-fd-und-sd/
categories:
  - Uncategorized
tags:
  - shell
  - software
  - Tools

---
## Das Problem

In einem Software Projekt mit mehreren Beteiligten kommen früher oder später unterschiedliche Coding-Stile zum Einsatz.  
Ob der uneinheitliche [Zeilenumbruch][1], (versehentliche) Leerzeichen am Ende einer Zeile oder der fehlende Zeilenumbruch am Ende einer Datei: Hier muss man sich auf auf eine gemeinsamen Standard einigen.

## Die Werkzeuge

Dabei kann das Projekt [Editorconfig][2] helfen.  
Man legt eine einfache Editorconfig-Datei in seinem Projekt ab und viele Editoren kümmern sich um den Rest.

Was passiert aber mit den bereits vorhandenen Dateien?  
Hier helfen ein paar einfache Kommandozeilenbefehle.  
Ich verwende dabei [sd][3] und [fd][4], die für viele System verfügbar sind.

<img decoding="async" src="https://philipp-weissmann.de/wp-content/uploads/2020/11/otvu7zmteic.jpg" alt="" /> 

## Beispiele

Allen Javascript Dateien die fehlende lezte Newline hinzufügen

<pre><code class="language-bash">fd --extension js -x sd &#039;([^\n]\z)&#039; &#039;$1\n&#039;</code></pre>

(Erklärung der Regular Expression: "Finde ein Nicht-Zeilenende vor dem Dateiende. Ersetze dies durch den gleichen Inhalt wie zuvor, aber füge ein Newline am Ende ein")

Alle Javascript Dateien "trailing whitespaces" löschen:

<pre><code class="language-bash">fd --extension js -x sd &#039; +\n&#039; &#039;\n&#039;</code></pre>

(Erklärung der Regular Expression: "Finde ein (oder mehrere) Leerzeichen vor einem Newline. Ersetze das gefundene durch eine Newline")

Alle Javascript Dateien in "unix-style" Zeilenumbrüche setzen:

<pre><code class="language-bash">fd --extension js -x dos2unix</code></pre>

## Weitere Schritte

Für die Zukunft könnten wir einen editor-config checker in unsere CI-Pipeline einbauen, der Änderungen auf unseren Standard gegenprüft.

Für jede Sprache sollte jetzt noch ein Linter zur Einhaltung des gleichen Formatierungsstandards eingesetzt werden.

## Fazit

Mit den kleinen Reparaturen können wir unser Projekt auf einen einheitlichen Standard heben. Das Editorconfig-Projekt hilft uns diese in der Zukunft einzuhalten.

 [1]: https://de.wikipedia.org/wiki/Zeilenumbruch#Codierung_des_Zeilenumbruchs
 [2]: https://editorconfig.org/
 [3]: https://github.com/chmln/sd
 [4]: https://github.com/sharkdp/fd