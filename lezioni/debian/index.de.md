---
layout: default
title: "Debian installieren"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only-Lektion</span> <span>Dieses Projekt wird von valerio-vaccaro gepflegt</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Debian installieren
Wir bereiten ein USB-Laufwerk mit dem Debian-Image vor, das von der offiziellen Website heruntergeladen wurde.

Wir verbinden alle Kabel (display, keyboard, mouse, and ethernet).

![alt text](https://officinebitcoin.it/lezioni/debian/1.jpg)

Wir schließen das USB-Installationslaufwerk an.

![alt text](https://officinebitcoin.it/lezioni/debian/2.jpg)

Wir schalten den Computer ein und stellen sicher, dass unser USB-Laufwerk mit Debian startet.

![alt text](https://officinebitcoin.it/lezioni/debian/3.jpg)

## Installation
Wenn alles korrekt funktioniert hat, sollte das Debian-Installationsprogramm starten und wir landen auf dem folgenden Bildschirm.

![alt text](https://officinebitcoin.it/lezioni/debian/4.jpg)

Wir wählen die erste Zeile und starten die grafische Installation.

Das Erste, wonach wir gefragt werden, ist die Sprache; für diese Installation wähle ich "English", da ich das verständlicher finde als jede andere Übersetzung.

![alt text](https://officinebitcoin.it/lezioni/debian/5.jpg)

An dieser Stelle werden wir nach unserem geografischen Standort gefragt; um Italien zu finden, müssen wir OTHER->EUROPE->ITALY auswählen.

![alt text](https://officinebitcoin.it/lezioni/debian/6.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/7.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/8.jpg)

Für die Lokalisierung wähle ich auch hier English.

![alt text](https://officinebitcoin.it/lezioni/debian/9.jpg)

Und ich konfiguriere die italienische Tastatur, da mir diese zur Verfügung steht.

![alt text](https://officinebitcoin.it/lezioni/debian/10.jpg)

Dann wählen wir einen Benutzernamen und lassen die Domain leer.

![alt text](https://officinebitcoin.it/lezioni/debian/11.jpg)

An dieser Stelle fordert Debian Sie auf, ein Passwort für den root-Benutzer festzulegen...

![alt text](https://officinebitcoin.it/lezioni/debian/12.jpg)

und einen Benutzer mit dem jeweiligen Passwort zu erstellen.

![alt text](https://officinebitcoin.it/lezioni/debian/13.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/14.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/15.jpg)

Jetzt müssen wir die Installationsfestplatte auswählen; wir verwenden die gesamte Festplatte und müssen die Festplatte auswählen, auf der die Installation durchgeführt werden soll.

![alt text](https://officinebitcoin.it/lezioni/debian/16.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/17.jpg)

Dann müssen wir die Partitionsstruktur auswählen; vorerst lassen wir alles in einer einzigen Partition.

![alt text](https://officinebitcoin.it/lezioni/debian/18.jpg)

Debian schlägt eine Partitionstabelle vor, aber... es hat swap hinzugefügt, was wir nicht wollen, also wählen wir ihn aus und entfernen ihn aus der Liste.

![alt text](https://officinebitcoin.it/lezioni/debian/19.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/20.jpg)

Nachdem wir ihn entfernt haben, können wir unsere Tabelle endlich schreiben.

![alt text](https://officinebitcoin.it/lezioni/debian/21.jpg)

Debian möchte zur Konfiguration der Partitionstabelle zurückkehren, aber wir lehnen die Einladung ab.

![alt text](https://officinebitcoin.it/lezioni/debian/22.jpg)

Und wir bestätigen die Absicht, die aktualisierte Tabelle zu schreiben.

![alt text](https://officinebitcoin.it/lezioni/debian/23.jpg)

Nun werden wir gefragt, ob wir einen Debian-mirror verwenden möchten; wir entscheiden uns dafür.

![alt text](https://officinebitcoin.it/lezioni/debian/24.jpg)

Wir wählen unser Land.

![alt text](https://officinebitcoin.it/lezioni/debian/25.jpg)

Normalerweise ist der GARR-mirror schnell und zuverlässig; verwenden wir diesen.

![alt text](https://officinebitcoin.it/lezioni/debian/26.jpg)

Ich habe keinen Proxy, also lasse ich das Feld leer.

![alt text](https://officinebitcoin.it/lezioni/debian/27.jpg)

Aber welche Programme sollen installiert werden? Da wir einen Server einrichten, deaktivieren wir die grafische Umgebung (indem wir die ersten beiden Häkchen entfernen) und wählen SSH aus, das wir für den Fernzugriff benötigen.

![alt text](https://officinebitcoin.it/lezioni/debian/28.jpg)

Die Installation beginnt.

Am Ende werden wir gefragt, ob wir grub installieren möchten, das uns erlaubt, Linux zu starten; wir antworten zustimmend und wählen dieselbe Festplatte, auf der wir das Betriebssystem installiert haben.

![alt text](https://officinebitcoin.it/lezioni/debian/29.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/30.jpg)

Yuhuuu, wir sind fertig; jetzt ist es Zeit, das USB-Laufwerk zu entfernen und die Maschine neu zu starten.

![alt text](https://officinebitcoin.it/lezioni/debian/31.jpg)

Wenn alles korrekt funktioniert hat, sollten wir vor einem Terminal stehen, das uns auffordert, uns mit einem der während der Installation erstellten Profile anzumelden.

## Konfiguration

### Verbinden wir uns
Wir verbinden uns mit unserem Server über `ssh username@ip`, wobei username der während der Installation gewählte Name ist und ip die IP-Adresse des Computers, auf dem wir installiert haben.

Dieser Schritt kann natürlich übersprungen werden, wenn Sie mit Monitor und Tastatur installieren, statt sich über das Netzwerk zu verbinden.

Beachten Sie, dass Debian es VERBIETET, sich per ssh mit Superuser-Zugangsdaten (also root) zu verbinden.

### Repository
Jetzt aktualisieren wir die Repositories.

Wir werden mit dem Befehl `su` und der Eingabe des root-Passworts zum Superuser.

Wir bearbeiten die Repository-Datei mit dem Befehl `nano /etc/apt/sources.list` und entfernen alle vorhandenen Zeilen.

Wir fügen die folgenden Zeilen hinzu.

```                                                                    
deb http://deb.debian.org/debian/ bookworm contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm contrib main non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-updates contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm-updates contrib main non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-proposed-updates contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm-proposed-updates contrib main non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-backports contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm-backports contrib main non-free non-free-firmware

deb http://deb.debian.org/debian-security/ bookworm-security contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian-security/ bookworm-security contrib main non-free non-free-firmware

```

Danach können wir die Datei speichern, indem wir `CTRL+x` und anschließend `y` drücken.

Mit dem Befehl `apt update` können wir prüfen, ob alles reibungslos gelaufen ist, und die Paketliste aktualisieren.

### System aktualisieren
Um das System zu aktualisieren, führen wir einfach die folgenden Befehle aus:

- `apt update`, um die Paketliste zu aktualisieren,
- `apt upgrade`, um installierte Pakete zu aktualisieren, für die eine neue Version existiert.

### tor installieren und mit ssh verwenden
Um tor zu installieren, verwenden wir einfach den Befehl `apt install tor`.

Nach der Installation können wir es mit dem folgenden Befehl konfigurieren: `nano /etc/tor/torrc`.

Am Ende der Datei fügen wir die folgenden Zeilen hinzu.

```
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 22 127.0.0.1:22
```

Und wir starten tor mit `systemctl restart tor` neu; nun können wir unsere onion-Adresse mit `cat /var/lib/tor/hidden_service/hostname` finden.

Mit tor können wir uns jetzt von überall auf der Welt mit unserer Maschine verbinden: `torify ssh username@onionaddress.onion`.

## Programm
Die Debian-Installation ist eine wiederkehrende Lektion; hier ist eine Liste der bereits abgehaltenen:

| Datum       | Notizen                                        |
|-------------|------------------------------------------------|
| 240415-2200 | Erste Lektion                                  |
