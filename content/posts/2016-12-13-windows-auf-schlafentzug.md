---
title: Windows auf Schlafentzug
author: Philipp Weißmann
type: post
date: 2016-12-13T08:59:09+00:00
url: /windows-auf-schlafentzug/
categories:
  - Uncategorized
tags:
  - Tools
  - Windows

---
Um seinen Rechner vor fremden Zugriff zu schützen, ist es sinnvoll, eine automatische Sperre nach einer definierten Zeit zu setzen.  
Doch es gibt Situationen, in denen kann diese Sperre hinderlich sein: Hält man eine  
Präsentation und der Bildschirm sperrt sich, hilft nur noch entsperren und weitermachen.

<!--more-->

Zwar verhindert manche Präsentationssoftware die lästige Sperre, aber spätestens bei Präsentationen aus PDF Dateien oder im Browser schlägt die Sperre erneut zu.

Abhilfe verschafft ein kleines Snippet, welches Tastatureingaben simuliert:

<pre><code class="language-vbscript">Dim objResult

Set objShell = WScript.CreateObject("WScript.Shell")    
i = 0

Do While i = 0
  objResult = objShell.sendkeys("{NUMLOCK}{NUMLOCK}")
    Wscript.Sleep (6000)
Loop</code></pre>

<img decoding="async" src="https://philipp-weissmann.de/wp-content/uploads/2019/04/schlaflos-1024x681.jpg" alt="Schlaflos" /> 

Einfach als `schlaflos.vbs` abspeichern und ausführen. Nun wird alle sechs Sekunden die `Numlock` zwei Mal gedrückt.  
Nun haben wir ein schlafloses Windows, welches nach dem Beenden des Skriptes, spätestens aber zum nächsten Neustart auch wieder schlafen darf. 

Gute Nacht Windows!