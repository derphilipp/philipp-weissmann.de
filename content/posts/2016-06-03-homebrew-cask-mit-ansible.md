---
title: Homebrew Cask mit Ansible
author: Philipp Weißmann
type: post
date: 2016-06-03T06:52:45+00:00
url: /homebrew-cask-mit-ansible/
categories:
  - Uncategorized
tags:
  - Ansible
  - Konfigurationsmanagement
  - macOS

---
Paketmanager auf modernen Betriebssystemen sind ein wahrer Segen: Programme
können einfach installiert, auf den aktuellsten Stand gebracht und restlos
deinstalliert werden.
Auch können mit einfachen Mitteln definierte Installationen bzw.
Systemkonfigurationen erstellt werden.

<!--more-->

Unter OS X steht derzeit [Homebrew][1] als Paketmanager mit
tausenden von (zumeist vorkompilierten) Paketen hoch in der Gunst der Nutzer.

Doch was, wenn Benutzer Software wie
[Photoshop][2],
[Omnigraffle][3] oder
[Pycharm][4] installiert brauchen?
Auch hier hilft Homebrew weiter: Mit der Erweiterung [HomebrewCask][5] kann Software aus externen Installern
auf das eigene System gebracht werden - automatisiert und nachvollziehbar.

Hierzu ist nach der Installation von Homebrew lediglich ein Einbinden des
Homebrew Cask Repository notwendig:

    brew tap caskroom/cask

Schon ist mit dem Befehl `brew cask install firefox` der Firefox Browser im
eigenen System installiert werden.
Ist man auf _nightly builds_ oder _alte_ Versionen einer Software angewiesen,
hilft zu dem das optionale Repository `caskroom/versions`.

    brew tap caskroom/versions

Mit der Hilfe von [Ansible][6] kann dieser Prozess
(sowie die Installation der Software) nun zentral erfolgen.

Wir legen uns eine Konfiguration an.
Hierzu erstellen wir einen Tasks zur Installation von Homebrew Cask und allen Applikationen:
`roles/apps/tasks/main.yml`

```yaml
- name: Check if homebrew cask installed
  homebrew: name=cask state=present

- name: Check if caskroom/versions is installed
  homebrew_tap: tap=caskroom/versions state=present

- name: Install applications
  homebrew_cask: name={{ item  }} state=present
  become: yes
    with_items:
      - firefox
      - vivaldi
      - gimp
```

Ansible installiert beim Aufruf nun alle aufgezählten Applikationen.
Aber Achtung: Da Homebrew als Nutzer ausgeführt werden sollte, die Installation
mancher Applikationen jedoch Administrator-Rechte verlangt, ist es hier
sinnvoll, die beiden Tasks `homebrew` und `homebrew_tab` als Nutzer laufen zu
lassen, den `homebrew_cask` Prozess jedoch als Administrator (Siehe
[become][7]).

Nun haben wir die Möglichkeit zentral, dokumentiert und nachvollziehbar
Software zu installieren, die aus Installern stammt.

 [1]: http://brew.sh/
 [2]: https://de.wikipedia.org/wiki/Adobe_Photoshop
 [3]: https://www.omnigroup.com/omnigraffle
 [4]: https://www.jetbrains.com/pycharm/
 [5]: https://github.com/Caskroom
 [6]: https://www.ansible.com/
 [7]: https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_privilege_escalation.html