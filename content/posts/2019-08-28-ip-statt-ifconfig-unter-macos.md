---
title: ip statt ifconfig unter macOS
author: Philipp Weißmann
type: post
date: 2019-08-28T12:41:55+00:00
url: /ip-statt-ifconfig-unter-macos/
categories:
  - Uncategorized

---
Viele moderne Linux Distributionen bieten mit [iproute2][1] eine einfache Möglichkeit Netzwerkkonfiguration durchzuführen.

So zeigt z.B.

```bash
ip a s
```

die IP Adresse der Netzwerkschnittstellen an.

MacOS bietet dieses Tool aber nicht an. Also müssen wir auf `ifconfig` ausweichen. Blöd, wenn wir zwischen den Systemen wechseln und immer umdenken müssen.

<img decoding="async" src="https://philipp-weissmann.de/wp-content/uploads/2019/08/small-but-useful-1024x683.jpg" alt="" />

Installieren wir mit der Hilfe von Homebrew ein kleines Hilfsscript:

```shell
brew install iproute2mac
```

Nun können wir auch mit

```shell
ip a s
```

die konfiguierten Netzwerkgeräte anzeigen. Wunderbar!

 [1]: https://de.wikipedia.org/wiki/Iproute2