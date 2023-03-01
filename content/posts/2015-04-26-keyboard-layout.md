---
title: OS X Keyboard Layout
author: Philipp Weißmann
type: post
date: 2015-04-26T13:35:47+00:00
url: /keyboard-layout/
categories:
  - Uncategorized
tags:
  - macOS
  - Produktivität

---
# Das Problem

Als Entwickler nutze ich stetig Sonderzeichen und Symbole wie {, ] oder auch \`.

Doch welches Tastaturlayout soll ich einsetzen?  
Zwar ist ein englisches Tastaturlayout sehr attraktiv, da dort sämtliche Sonderzeichen gut erreichbar sind. Als Entwickler im deutschsprachigen Raum benötige ich jedoch ständig Umlaute und das _ß_-Zeichen.

<!--more-->

Bei der Nutzung eines deutschen Tastaturlayout finde ich jedoch Symbole wie _{_ extrem Umständlich zu erreichen.

Sonderbelegungen wie [Dvorak][1] sind zwar reizvoll, scheitern aber für mich an der Tatsache, dass die  
Umgewöhnung bei der Nutzung eines fremden Rechners zu hoch wäre.

<img decoding="async" src="https://philipp-weissmann.de/wp-content/uploads/2015/04/keyboard-1024x685.jpg" alt="Tastatur" /> 

# Lösung

Daher habe ich mir für OS X ein eigenes Tastaturlayout gebaut.  
Dieses nutzt als Basis das US-Englische Layout, nutzt jedoch die Alt-Taste für "deutsche" Sonderzeichen.

So erzeugt `Alt + [` das _ü_ Zeichen.  
Ich drücke also genau die Taste, die bei einem deutschen Keyboard ebenfalls das _ü_ erzeugt.

Somit fällt die Umgewöhnung auf die neue Eingabeform extrem leicht.

# Installation

Das Layout ist einfach zu installieren - es kann direkt von der [Projektseite auf Github][2] herunterladen werden.

Wie in der [Anleitung][3] beschrieben, muss nach dem Entpacken der Datei diese lediglich in das Verzeichnis

    ~/Library/Keyboard Layouts

kopiert werden und in dem Punkt  
_Systemeinstellungen_ -> _Tastatur_ -> _Eingabequellen_  
aktiviert werden.

# Fazit

Nach kurzer Umgewöhnungszeit ist es mir nun möglich das komfortable englische Tastaturlayout zu nutzen, ohne jedoch auf die native Eingabemöglichkeit Umlauten und Co zu verzichten.

 [1]: https://de.wikipedia.org/wiki/Dvorak-Tastaturbelegung
 [2]: https://github.com/derphilipp/english_keyboard_for_germans/releases
 [3]: https://github.com/derphilipp/english_keyboard_for_germans/