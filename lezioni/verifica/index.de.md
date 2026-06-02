---
layout: default
title: "Voraussetzungen für dieses Tutorial"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only-Lektion</span> <span>Dieses Projekt wird von valerio-vaccaro gepflegt</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](https://officinebitcoin.it/lezioni/verifica/1cover.webp)
Das Verifizieren kryptografischer Signaturen ist eine grundlegende Sicherheitspraxis, die **jeder Nutzer von open-source Software in seine guten Gewohnheiten aufnehmen sollte**.

Open source ist von Natur aus veränderbar, was bedeutet, dass theoretisch jeder backdoors, Angriffe oder bösartigen Code in die Anwendungen einbringen kann, die du zum Üben beim Lernen des Bitcoin-Protokolls verwendest.

Als Nutzer, der sein Studium vertieft, hast du die Möglichkeit, persönlich zu überprüfen, ob die heruntergeladene Software manipuliert wurde, und du solltest das tun, bevor du sie installierst und verwendest.

Bevor wir beginnen, bringen wir auch einen Klassiker aus Präsentationen zu Officine Bitcoin mit: das Meme. Es wird keine schwere Präsentation, aber entspannen wir die Atmosphäre gleich zu Beginn.

![meme](https://officinebitcoin.it/lezioni/verifica/2meme.webp)

## Wie macht man das?
Entwickler veröffentlichen neue Softwareversionen immer zusammen mit einer kryptografischen Signatur.
Das bedeutet, dass sie zusätzlich zur Aktualisierung der Software deren Veröffentlichung damit zertifizieren, dass sie sie an eine bestimmte fingerprint gebunden haben. Erinnerung: Die mit dem privaten Schlüssel erzeugte digitale Signatur ist einzigartig und unveränderlich.

Alles, was du brauchst, ist die GPG-Suite, um mit der Signaturprüfung fortzufahren.

![img](https://officinebitcoin.it/lezioni/verifica/3.webp)

# Voraussetzungen für dieses Tutorial
- Eine kurze Wiederholung der asymmetrischen Kryptografie
- Die zu verifizierenden Elemente:
  - software (binary, apk, etc.)
  - die digitale Signatur des Entwicklers, normalerweise eine `.asc`-, `.sig`-Datei oder ein checksum.
- Die Werkzeuge für die Verifikation:
  - GPG-Suite
  - ein Terminal (funktioniert sowohl unter Linux als auch unter Windows)
# Asymmetrische Kryptografie

![img](https://officinebitcoin.it/lezioni/verifica/4.webp)

Hier gibt es zwei miteinander verbundene Schlüssel: einen öffentlichen und einen privaten Schlüssel. Wie die Namen nahelegen:
- Der öffentliche Schlüssel ist frei verfügbar und kann mit jedem geteilt werden.
- Der private Schlüssel wird von seinem Besitzer sicher verwahrt.

Daten, die mit dem öffentlichen Schlüssel verschlüsselt wurden, können nur mit dem entsprechenden privaten Schlüssel entschlüsselt werden. So kann jeder verschlüsselte Daten an den Besitzer des Schlüsselpaares senden, ohne vorher den geheimen Teil zu teilen.

Public-key Kryptografie ist langsamer als symmetrische Kryptografie und nicht geeignet, große Datenmengen zu verschlüsseln. Sie ermöglicht jedoch die sichere Verteilung von Verschlüsselungsschlüsseln.
Zu den häufig verwendeten Algorithmen für public-key Kryptografie gehören RSA, ECC, ElGamal und DSA.

## Entwicklerseite: neues Update

Der Entwickler veröffentlicht den open source Code, der von Natur aus nicht verschlüsselt ist.
Er erstellt einen kryptografischen Hash (der den `checksum` erzeugt) und verschlüsselt den digest mit seinem privaten Schlüssel: Dadurch entsteht die Signatur, jene zuvor erwähnte `.sig`- oder `.asc`-Datei.

Nach diesem Prozess lädt der Entwickler beide Dateien auf die Website oder in ein GitHub-Repository hoch. Dort beginnt dein Download.

![img](https://officinebitcoin.it/lezioni/verifica/5.webp)

Dann brauchst du den öffentlichen Schlüssel des Entwicklers. Manchmal liegt er im GitHub-Repository, manchmal auf öffentlichen Servern (*keyservers*). Auch wenn die Suche Mühe kosten kann, ist der öffentliche Schlüssel ein wesentliches Element zur Verifizierung der Software, also bemühe dich, ihn zu bekommen.

Wenn du Schwierigkeiten hast, stelle Fragen in der Telegram-Gruppe von Officine Bitcoin, wo du Anweisungen zum Erhalt eines bestimmten öffentlichen Schlüssels findest.

![img](https://officinebitcoin.it/lezioni/verifica/6.webp)

Um die Datenintegrität zu überprüfen, entschlüsselt der Empfänger die Signatur mit dem öffentlichen Schlüssel des Absenders und erhält ein Ergebnis:

a. die Daten gelten als authentisch und während der Übertragung unverändert.
b. die Daten wurden möglicherweise manipuliert.

Durch das Verschlüsseln des Hash-Werts mit dem privaten Schlüssel **garantieren PGP-Signaturen, dass der checksum selbst geschützt und mit der Identität des Absenders verknüpft ist. Das verhindert Signaturfälschungen auf veränderten Daten**.

Signaturen können verwendet werden, um alles Mögliche zu verifizieren: Dateien, emails, Dokumente und Softwaredownloads. Wenn du eine PGP-Signatur prüfst, weist du nach, dass die Daten tatsächlich aus einer vertrauenswürdigen Quelle stammen und intakt sind.

Und es ist die Verifizierung eines mobilen apk, die du jetzt durchführen kannst.

Wir verwenden als Beispiel den Download von Phoenix, einem non-custodial LN wallet, damit wir es an einem zukünftigen Abend von Officine Bitcoin gezielt behandeln können.

# Phoenix Wallet (Acinq) herunterladen und verifizieren
Wenn du bereits auf der Website von [Acinq](https://phoenix.acinq.co/), dem Entwickler von Phoenix, warst, weißt du schon, dass der Download in den offiziellen Stores für Android und iOS verfügbar ist.
Vielleicht ist dir nie aufgefallen, dass für Android auch die apk-Datei verfügbar ist.

![img](https://officinebitcoin.it/lezioni/verifica/8.webp)

[Gehen wir dorthin!](https://github.com/ACINQ/phoenix/releases), um die Dateien `apk` und `Signature` zu finden, die du mit `wget` herunterladen wirst.
Im Fall von Phoenix heißt die Datei, die die Signatur für die Verifikation enthält, **`SHA256SUMS.ASC`**.

![img](https://officinebitcoin.it/lezioni/verifica/9.webp)

Im selben Repository gibt es auch Anweisungen zum Herunterladen des öffentlichen Schlüssels, der zur *signing key E04E48E72C205463* gehört (eindeutige fingerprint von Drouinfs Schlüsseln).
Kopiere den Link und lade ihn mit `wget` herunter, oder folge den Anweisungen im entsprechenden Abschnitt des repo.

![img](https://officinebitcoin.it/lezioni/verifica/10.webp)

---
⚠️**Der öffentliche Schlüssel muss importiert werden, nicht nur heruntergeladen**.
⚠️ Die Datei-Downloads müssen im selben Verzeichnis erfolgen.

---
# Terminal öffnen
Navigiere mit dem Terminal in das Verzeichnis, in dem das apk und die Datei `SHA256SUMS.ASC` heruntergeladen wurden, und führe die Befehle der Reihe nach aus.

![img](https://officinebitcoin.it/lezioni/verifica/11.webp)

![img](https://officinebitcoin.it/lezioni/verifica/12.webp)

Wenn die Verifikation ein positives Ergebnis zurückgibt, kannst du das apk auf dein Telefon übertragen und die app installieren.

---
# Schwierige Verifikation
Es kann mehrere Gründe geben, warum die Signaturprüfung nicht einfach ist, und sie sind fast immer auf Unordnung oder Unerfahrenheit zurückzuführen:
1. die apk- und/oder .asc-Dateien wurden mehrfach heruntergeladen, sodass sie im Verzeichnis zum Beispiel mit seltsamen Namen wie **filename-1** oder **filename(1)** erscheinen
2. apk und .asc befinden sich nicht im selben Verzeichnis
3. der öffentliche Schlüssel wurde heruntergeladen, aber nicht in den gpg keyring importiert.

Es können auch andere Situationen auftreten, in denen die Verifikation trotz korrekter Vorgehensweise fehlschlägt.
Es ist wichtig, den Fehler zu prüfen, der im Terminal erscheint, ihn zu kopieren und im Internet nach der Lösung zu suchen.

# Verifikation mit Sparrow Wallet
Wenn du Sparrow Wallet bereits verwendest, kannst du Downloads mit dieser Software verifizieren, **deren Download und Installation eine sorgfältige und strenge Verifikation mit GPG vorausgehen muss**.

Starte Sparrow wallet und suche im Menü `Tools` -> `Verify Downloads`.

![img](https://officinebitcoin.it/lezioni/verifica/13.webp)

Eine Oberfläche öffnet sich und fordert dich auf, die frisch heruntergeladenen Dateien einzufügen. Durch Klicken auf `Browse` öffnet sich der Dateimanager, um jede Datei in das erforderliche Feld zu laden.

![img](https://officinebitcoin.it/lezioni/verifica/14.webp)

Manchmal füllt sich das Formular der Oberfläche selbst aus. Wenn nicht, fülle alle Felder mit den passenden Dateien aus.

![img](https://officinebitcoin.it/lezioni/verifica/15.webp)

Das positive Ergebnis wird grafisch durch grüne Häkchen und die Bestätigung *`Ready to install`* + < filename > angezeigt.

# Lernunterstützung
Wenn du an der Live-Präsentation auf Telegram teilgenommen hast, kannst du sie als weiteren Schritt zu deiner persönlichen Souveränität betrachten (nicht nur finanziell).
Wenn du sie verpasst hast, **verzweifle nicht**: Diese Notizen dienen genau dazu, aufzuholen, und außerdem solltest du wissen, dass wir sie bei Officine erneut anbieten werden.

Um die nächste Präsentation nicht zu verpassen, tritt der [Telegram-Gruppe](https://t.me/officinebitcoin) bei, um ständig auf dem Laufenden zu bleiben.

![img](https://officinebitcoin.it/lezioni/verifica/17.webp)

Du kannst auch den [Satoshi Spritz](https://satoshispritz.it/) in deiner Nähe finden. Ein Satoshi Spritz ist ein lokales meetup, bei dem ausschließlich über Bitcoin gesprochen wird, wo du deine Fragen mitbringen und Antworten von anderen erfahrenen bitcoiners erhalten kannst. Unter dem Link findest du die Karte der Halbinsel.

![img](https://officinebitcoin.it/lezioni/verifica/16.webp)

Wenn du schließlich kein meetup in deiner Nähe findest, kannst du die wöchentlichen Live-Streams von [SatoshiSpritz Connect](https://t.me/SatoshiSpritzConnect) nutzen, einem virtuellen meetup für diejenigen, die nicht an Satoshi Spritz teilnehmen können, oder um kleineren meetups zu helfen, Notizen zu machen und Inspiration für eigene Präsentationen zu finden.

![img](https://officinebitcoin.it/lezioni/verifica/18.webp)
