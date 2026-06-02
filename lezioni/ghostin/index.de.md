---
layout: default
title: "Ghostinbox.it: E-Mail nutzen, ohne eine E-Mail-Adresse zu besitzen"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only-Lektion</span> <span>Dieses Projekt wird von valerio-vaccaro gepflegt</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Ghostinbox.it: E-Mail nutzen, ohne eine E-Mail-Adresse zu besitzen

Ghostinbox ist eine Webplattform, mit der Nutzer temporäre E-Mail-Adressen erstellen können, um Nachrichten zu empfangen, ohne ihre echte E-Mail-Adresse preiszugeben. Der Dienst eignet sich ideal für schnelle Registrierungen, Kontoüberprüfungen, Tests der E-Mail-Zustellbarkeit oder jede Situation, in der man Spam vermeiden oder die eigene Identität schützen möchte.

Im Gegensatz zu herkömmlichen E-Mail-Diensten erfordert Ghostinbox keine Registrierung und speichert keine personenbezogenen Daten. Damit ist es eine ausgezeichnete Wahl für alle, die Datenschutz priorisieren. Zusätzlich ermöglicht die Unterstützung des Tor-Netzwerks den anonymen Zugriff auf den Dienst, indem die IP-Adresse des Nutzers verborgen wird. Der open-source Charakter des Projekts sorgt für Transparenz und ermöglicht Entwicklern, den Code auf mögliche Schwachstellen oder Anpassungsmöglichkeiten zu prüfen.

## Wie funktioniert Ghostinbox?
![alt text](https://officinebitcoin.it/lezioni/ghostin/front.png)

Die Nutzung von Ghostinbox ist äußerst intuitiv und erfordert keine technischen Kenntnisse:

1. **Website aufrufen**: Besuche https://ghostinbox.it/ (oder nutze Tor für mehr Anonymität).
2. **Temporäre E-Mail-Adresse erzeugen**: Klicke auf den Button, um eine neue temporäre E-Mail-Adresse zu erstellen (zum Beispiel random@ghostinbox.it). Die Adresse ist sofort aktiv und einsatzbereit.
3. **Nachrichten empfangen**: Verwende die erzeugte Adresse, um Emails zu empfangen, zum Beispiel für Registrierungen bei Online-Diensten, Kontoüberprüfungen oder Tests. Die Nachrichten erscheinen in Echtzeit im Posteingang auf der Website.
4. **Nachrichten überwachen**: Öffne den temporären Posteingang direkt auf Ghostinbox, um die empfangenen Nachrichten anzusehen. Ein externer E-Mail-Client ist nicht erforderlich.

![alt text](https://officinebitcoin.it/lezioni/ghostin/email.png)

Der Dienst ist auf Schnelligkeit und geringe Reibung ausgelegt: Es muss kein Konto erstellt werden, und die minimalistische Oberfläche macht die Nutzung auch für nicht technische Nutzer flüssig. Der Zugriff über Tor fügt eine zusätzliche Schutzebene für alle hinzu, die vollständige Anonymität wahren möchten.

## Vom Alias zur E-Mail
Um den Dienst zu nutzen, muss ein Alias gewählt werden, der lang und zufällig genug ist, damit er nicht von anderen Nutzern erraten werden kann. Dieser Alias dient wie ein Passwort für den Zugriff auf die E-Mail und sollte daher nicht vergessen werden.

Aus diesem Alias wird eine E-Mail-Adresse HASH@ghostinbox.it abgeleitet, wobei HASH `sha256(alias)` entspricht, also dem Hash des Alias mit SHA-256; anschließend kann ein Nutzer diese E-Mail (im Empfangsschema angezeigt) verwenden, um Emails zu empfangen. Die Empfangsseite aktualisiert sich automatisch und zeigt empfangene Emails an. Ein Nutzer kann eine E-Mail-Adresse erstellen, ohne auf den Dienst zuzugreifen, und die Website nur zur Einsicht verwenden.

Durch Klicken auf die E-Mail kann man ihren Text lesen und bei Bedarf Links kopieren, um sie zu öffnen; das E-Mail-Format ist bewusst reiner Text und zeigt daher keine grafischen Elemente von HTML-basierten Emails an.

## Wer braucht Ghostinbox?
Ghostinbox deckt verschiedene Bedürfnisse im Zusammenhang mit Datenschutz und temporärer E-Mail-Verwaltung ab:

1. **Spam-Schutz**: Durch die Nutzung einer temporären Adresse können Nutzer verhindern, dass ihre echte E-Mail-Adresse mit Spam oder unerwünschten Newslettern überflutet wird.
2. **Sichere Registrierungen**: Perfekt für die Anmeldung bei Online-Diensten, Foren oder Plattformen, die eine E-Mail-Verifizierung verlangen, ohne die persönliche E-Mail zu gefährden.
3. **Tests der Zustellbarkeit**: Entwickler und Marketingfachleute können Ghostinbox nutzen, um das Senden und Empfangen von Emails zu testen, ohne echte Adressen einzubeziehen.
4. **Erweiterter Datenschutz**: Dank Tor-Unterstützung ist der Dienst ideal für Nutzer, die bei der Interaktion mit Websites oder Online-Diensten anonym bleiben möchten.
5. **Temporäre Nutzung**: Geeignet für Situationen, in denen eine Wegwerf-E-Mail-Adresse benötigt wird, etwa für Aktionen, kostenlose Testversionen oder kurzfristige Kommunikation.

![alt text](https://officinebitcoin.it/lezioni/ghostin/stats.png)

## Technische Merkmale
Das GitHub-Repository von Ghostinbox (https://github.com/valerio-vaccaro/ghostinbox.it) zeigt eine schlanke Implementierung, hauptsächlich in Python mit dem Flask-Framework geschrieben, mit folgenden Merkmalen:

- **Serverless-Ansatz**: Es gibt keinen E-Mail-Server; stattdessen wird ein kostenloser E-Mail- und E-Mail-Weiterleitungsdienst genutzt, wodurch die Dienstarchitektur äußerst einfach und wirtschaftlich bleibt.
- **Architektur**: Ghostinbox verwendet eine Client-Server-Architektur auf Basis von Flask, um die Erzeugung temporärer E-Mail-Adressen und die Anzeige von Nachrichten zu verwalten. Die Einfachheit des Designs sorgt auch bei hohem Anfragevolumen für hohe Leistung.
- **Adressgenerierung**: Temporäre E-Mail-Adressen werden dynamisch anhand des eingegebenen Alias erzeugt.
- **Tor-Unterstützung**: Der Dienst ist so konfiguriert, dass er über onion routing erreichbar ist, wodurch sichergestellt wird, dass die IP-Adresse des Nutzers während der Interaktion mit der Website nicht nachverfolgt wird.
- **Nachrichtenverwaltung**: Empfangene Nachrichten werden nach 30 Tagen gelöscht.
- **Sicherheit**: Personenbezogene Daten oder Nachrichten werden nicht dauerhaft gespeichert. Das Design des Dienstes minimiert Risiken durch Sicherheitsverletzungen, und der Verzicht auf Registrierung macht die Angabe sensibler Informationen überflüssig.
- **Open-source**: Der öffentliche Code ermöglicht Entwicklern, die Integrität des Systems zu überprüfen, Verbesserungen beizutragen oder eine angepasste Instanz zu hosten.

Technische Stärken:
- **Absolute Privatsphäre**: Die Löschung von Emails nach 30 Tagen und die Tor-Unterstützung gewährleisten eine anonyme und sichere Nutzung.
- **Leichtgewichtig**: Die Flask-Implementierung ist für geringe Ressourcen optimiert, wodurch der Dienst skalierbar und schnell ist.
- **Transparenz**: Die open-source Lizenz ermöglicht Code-Audits und Anpassungen und erhöht damit das Vertrauen der Nutzer.

## Fazit
Ghostinbox ist eine elegante und funktionale Lösung für alle, die einen schnellen, sicheren und datenschutzorientierten temporären E-Mail-Dienst suchen. Mit seiner intuitiven Oberfläche, der Tor-Unterstützung und der Transparenz des open-source Codes spricht es sowohl normale Nutzer an, die ihren Posteingang vor Spam schützen möchten, als auch Entwickler, die ein zuverlässiges System für Tests oder temporäre Registrierungen benötigen. Um Ghostinbox auszuprobieren, besuche https://ghostinbox.it/. Um den Code anzusehen oder zum Projekt beizutragen, konsultiere das Repository unter https://github.com/valerio-vaccaro/ghostinbox.it.

