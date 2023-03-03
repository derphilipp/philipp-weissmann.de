---
title: Simples deployment via git
author: Philipp Weißmann
type: post
date: 2019-04-16T19:59:37+00:00
url: /simples-deployment-via-git/
cover: /img/distribute.jpg
categories:
  - Uncategorized
tags:
  - Git
  - Linux
  - macOS
  - Produktivität
  - Tools

---
# Das Problem

Egal ob Homepage, Konfigurationsdateien oder Programmcode: Für praktisch alle Projekte verwendet man heute [git][1].

Möchte man jedoch Versionen automatisch ausrollen (z.B. statische HTML Dateien einer Webseite), benötigt man einige Skripte oder einen Build-Dienst wie z.B. Gitlab-CI, Jenkins oder CircleCI.

Oftmals reicht es jedoch die Daten auf das Zielsystem zu kopieren. Aber auch das geht mit git:

# Ausgangssituation

Wie haben einen Server (für die Homepage), einen Laptop (für die Entwicklungsarbeit), sowie ein Git-Projekt (z.B. bei Github).
Auf Github befindet sich unser Projekt.
Auf Laptop wie auch auf dem Server haben wir uns mit `git clone` das Projekt eingerichtet.

# Vorgehen

Das Projekt auf dem Server soll beim Empfangen neuer Dateien diese auch in das "Working Directory" schreiben. Dies aktivieren wir mit:


```bash
# auf Server, im Projektverzeichnis
git config receive.denyCurrentBranch updateInstead
```

Nun müssen wir unserem Projekt auf dem Laptop das neue Ziel beibringen:

```bash
# auf Laptop, im Projektverzeichnis
git remote add deploy benutzer@servername:/pfad/zu/projektordner/auf/server
# jetzt noch sagen: schiebe den lokalen branch _master_ auf den server (nur 1 mal notwendig)
git push --set-upstream deploy master
```


Unsere Änderungen können wir weiterhin zu Github schieben:

```bash
git push origin
```

Aber nun auch neu: Auf dem Server direkt ausrollen:

```bash
git push deploy
```

Es ist sogar möglich mittels `push-url` mehrere Ziele auf einmal zu definieren.

# Fazit

Natürlich ersetzt unser kleiner Workflow keinen Build-Server oder ausgetüftelte Deployment Prozesse. Aber für Kleinst-Projekte kann das vorgehen mit `updateInstead` sehr praktisch sein.

**Aber Achtung**: Verwenden wir diese Möglichkeit um Webseiten zu versionieren: Nicht vergessen, den `.git` Ordner nicht auszuliefern.

 [1]: https://de.wikipedia.org/wiki/Git