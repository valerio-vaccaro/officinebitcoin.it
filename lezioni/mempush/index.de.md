---
layout: default
title: "MemPush: Bitcoin-Transaktionen in der Mempool einfach senden und verwalten"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only-Lektion</span> <span>Dieses Projekt wird von valerio-vaccaro gepflegt</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# MemPush: Bitcoin-Transaktionen in der Mempool einfach senden und verwalten

MemPush (https://mempush.com/) ist eine innovative Plattform, die das Senden und Verwalten von Bitcoin-Transaktionen in der Mempool einfach, sicher und zugänglich macht. Die Mempool, das temporäre "Reservoir" von Bitcoin-Transaktionen, die auf eine Bestätigung in der Blockchain warten, steht im Zentrum dieses Dienstes, der technische Komplexität für Nutzer und Entwickler beseitigt.

## Was ist MemPush?

MemPush ist ein Webdienst, mit dem raw Bitcoin transactions (im Hexadezimalformat) direkt an die Mempool gesendet werden können, ohne dass erweiterte Konfigurationen oder eigene Bitcoin nodes erforderlich sind. MemPush wurde von Valerio Vaccaro entwickelt und unterstützt auch das Tor-Netzwerk, um den Nutzern mehr Privatsphäre zu bieten.

![alt text](https://officinebitcoin.it/lezioni/mempush/front.png)

Der Quellcode, der auf GitHub (https://github.com/valerio-vaccaro/mempush) unter einer Open-source-Lizenz verfügbar ist, ermöglicht es jedem, die Sicherheit des Projekts zu überprüfen, zu seiner Entwicklung beizutragen oder eine personalisierte Instanz des Dienstes zu hosten.

## Wie funktioniert MemPush?

Die Oberfläche von MemPush ist intuitiv und benutzerfreundlich:

1. **Website aufrufen**: Besuchen Sie https://mempush.com/.
2. **Raw transaction eingeben**: Fügen Sie die Bitcoin-Transaktion im Hexadezimalformat in das dafür vorgesehene Feld ein.
3. **Transaktion senden**: Klicken Sie auf "Submit Raw Transaction", um die Transaktion über Bitcoin nodes an die Mempool zu übertragen.
4. **Status überwachen**: Prüfen Sie den Fortschritt der Transaktion mit einem blockchain explorer.
5. **Automatische erneute Übertragung**: MemPush überträgt Transaktionen bei Bedarf automatisch erneut, um ihren Verbleib in der Mempool sicherzustellen.

![alt text](https://officinebitcoin.it/lezioni/mempush/list.png)

Eine Registrierung ist nicht erforderlich, und der Open-source-Ansatz beseitigt versteckte Risiken, wodurch MemPush auch für weniger erfahrene Nutzer ideal ist.

## Für wen ist MemPush gedacht?

MemPush wurde entwickelt, um verschiedene Anforderungen zu erfüllen:
1. **Niedrige Gebühren**: Transaktionen mit niedrigen Gebühren werden automatisch erneut übertragen, damit sie bei Verkehrsspitzen nicht aus der Mempool entfernt werden.
2. **Timelocked-Transaktionen**: Unterstützt die Überwachung und erneute Übertragung von Transaktionen mit zeitlichen Einschränkungen und gewährleistet so ihre wirksame Verwaltung.
3. **Erweiterte Überwachung**: MemPush prüft regelmäßig den Transaktionsstatus und erlaubt das Entfernen nur bestätigter oder ungültig gewordener Transaktionen (z. B. double-spends).
4. **Verbesserte Privatsphäre**: Dank der Unterstützung des Tor-Netzwerks schützt MemPush die Anonymität der Nutzer beim Senden von Transaktionen.

## Technische Merkmale

Das GitHub-Repository (https://github.com/valerio-vaccaro/mempush) zeigt eine elegante Python-Implementierung, die auf dem Flask-Framework basiert und zur Transaktionsverwaltung in eine Datenbank integriert ist. MemPush nutzt Dienste wie blockstream.info und mempool.space, um Transaktionen zu überwachen und zu übertragen; künftig ist die Integration eines lokalen Bitcoin node geplant.

Wichtigste Stärken:
- **Sicherheit**: Es werden keine sensiblen Daten oder privaten Schlüssel gespeichert, wodurch vollständiger Schutz gewährleistet wird.
- **Skalierbarkeit**: Unterstützt ein hohes Transaktionsvolumen dank direkter Verbindung mit dem Bitcoin-Netzwerk.
- **Open-source**: Der öffentliche Code ermöglicht Überprüfung, Beiträge und Anpassungen durch die Community.

## Fazit

MemPush ist eine leistungsstarke und zugängliche Lösung für alle, die Bitcoin-Transaktionen in der Mempool ohne Komplikationen senden und verwalten möchten. Mit seiner Transparenz, der Unterstützung für Privatsphäre und der einfachen Bedienung ist es eine wertvolle Ergänzung des Bitcoin-Ökosystems. Besuchen Sie https://mempush.com/, um es auszuprobieren, oder sehen Sie sich den Code unter https://github.com/valerio-vaccaro/mempush an.
