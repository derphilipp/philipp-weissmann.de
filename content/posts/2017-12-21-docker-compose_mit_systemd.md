---
title: Docker services via docker-compose und systemd template
author: Philipp Weißmann
type: post
date: 2017-12-21T21:05:32+00:00
url: /docker-compose_mit_systemd/
cover: /img/container.jpg
categories:
  - Uncategorized
tags:
  - Docker
  - Linux
  - Systemd

---
[Docker][1] ist das derzeit omnipresente Werkzeug um Dienste in Containern auszuführen.

Wie kann man jedoch einen logischen Verbund an Diensten mit dem System zusammen starten?

Mit der Hilfe von Docker können Anforderungen eines Dienstes (z.B. [Gitlab][2]) an die Distribution innerhalb eines Containers befriedigt werden. Das ausführende System aussenherum bleibt davon unberührt und kann auch eine inkompatible Distribution sein.

In der Praxis werden jedoch oft mehrere Dienste in einem Verbund benötigt. Diese können mit dem Tool [docker-compose][3] beschrieben und gestartet werden.

Will man nun Dienste via docker-compose mit dem System zusammen starten, bietet sich folgende Vorgehensweise an:

Als erstes definieren wir ein Dienst-Template in einer neuen Datei `/etc/systemd/system/dc@.service`

```ini
[Unit]
Description=%i service with docker compose
Requires=docker.service
After=docker.service

[Service]
Restart=always
TimeoutStartSec=1200

WorkingDirectory=/opt/dockerfiles/%i

# Remove old containers, images and volumes and update it
ExecStartPre=/usr/local/bin/docker-compose down -v
ExecStartPre=/usr/local/bin/docker-compose rm -fv
ExecStartPre=/usr/local/bin/docker-compose pull

# Compose up
ExecStart=/usr/local/bin/docker-compose up

# Compose down, remove containers and volumes
ExecStop=/usr/local/bin/docker-compose down -v

[Install]
WantedBy=multi-user.target
```

Wir gehen dabei davon aus, dass alle docker-compose Konfigurationsdateien in `/opt/dockerfiles/DIENSTNAME` liegen und sich `docker-compose` im Verzeichnis `/usr/local/bin` liegt.

Nun legen wir unsere docker-compose.yml Datei z.B. in `/opt/dockerfiles/gitlab/docker-compose.yml` ab.

Nun weisen wir systemd an, das Template zu instanziieren:

`sudo systemctl enable dc@gitlab`

Ab sofort ist der Dienst vorhanden und kann auch direkt gestartet werden:

`sudo systemctl start dc@gitlab`

Beim starten des Dienstes wird auch das Image aktualisiert - ist dies nicht gewünscht, muss lediglich die entsprechende Zeile im Template entfernt werden.

Viel Spaß!

 [1]: https://www.docker.com/
 [2]: https://gitlab.com
 [3]: https://docs.docker.com/compose/
