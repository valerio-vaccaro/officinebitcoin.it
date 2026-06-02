---
layout: default
title: "Jade einrichten"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only-Lektion</span> <span>Dieses Projekt wird von valerio-vaccaro gepflegt</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Jade einrichten

![alt text](https://officinebitcoin.it/lezioni/jadeset/0_Cover.jpg)

Jade wird in einer Verpackung geliefert, deren Unversehrtheit geprüft werden muss. Kontrolliere dazu die beiden holografischen Manipulationsschutz-Aufkleber zwischen der Schachtel (unten) und dem Deckel (oben).

Die Verpackung enthält ein kleines Benutzerhandbuch, zwei CompactSeedQR-Vorlagen sowie das hardware wallet.

Jade wird eingeschaltet, indem du die untere Taste gedrückt hältst. Danach zeigt das Gerät die 3 Menüs:

- Setup Jade
- Scan QR
- Options

In Options kannst du je nach persönlicher Vorliebe verschiedene Parameter einstellen, aber zuerst muss die Initialisierung abgeschlossen werden.

Mit der Scroll-Taste wählst du anschließend das Menü __Setup Jade__ aus und bestätigst mit der vorderen Taste.

![alt text](https://officinebitcoin.it/lezioni/jadeset/1.jpg)

Es erscheint ein Hinweis, die Einrichtungsanleitung auf der Website https://blockstream.com/jade/ zu prüfen.

![alt text](https://officinebitcoin.it/lezioni/jadeset/2.jpg)

Für eine korrekte Durchführung wird empfohlen, die Mnemonic mit Würfelwürfen zu erzeugen und diese Entropie zur Erstellung des Wallets zu verwenden. Wähle daher __Advanced Setup__.

![alt text](https://officinebitcoin.it/lezioni/jadeset/3.jpg)

Jade weist darauf hin, dass diese Einrichtung einige fortgeschrittene technische Funktionen enthält. Es reicht aus, besonders aufmerksam zu sein und die Bestätigungstaste zu drücken.

![alt text](https://officinebitcoin.it/lezioni/jadeset/4.jpg)

Um die mit Würfel-Entropie erzeugte Mnemonic einzugeben, wähle __Restore Wallet__.

![alt text](https://officinebitcoin.it/lezioni/jadeset/5.jpg)

Jetzt musst du die Länge der Mnemonic festlegen, 12 oder 24 Wörter. Das Menü bietet außerdem die Möglichkeit, das Wallet durch Scannen eines QR-Codes wiederherzustellen: Das ist der SeedQr, der an anderer Stelle behandelt wird.

![alt text](https://officinebitcoin.it/lezioni/jadeset/6.jpg)

Aus rein didaktischen Gründen und der Geschwindigkeit wegen zeigt dieses Tutorial die Einrichtung mit einer Mnemonic aus 12 Wörtern.

Der Vorgang zur Eingabe des ersten Wortes beginnt und Jade zeigt die Tastatur zum Eingeben der jeweiligen Buchstaben. Mit der Scroll-Taste bewegst du dich ← → an die richtige Position.

In diesem Beispiel ist Wort Nr. 1 "below".

![alt text](https://officinebitcoin.it/lezioni/jadeset/7.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/8.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/9.jpg)

Nach Eingabe der ersten 3-4 Buchstaben wählt Jade Wörter aus dem BIP39-Wörterbuch aus und beginnt, eine Reihe von Vorschlägen anzuzeigen. Mit der Scroll-Taste gehst du vor oder zurück, bis du das richtige Wort findest.

![alt text](https://officinebitcoin.it/lezioni/jadeset/10.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/11.jpg)

Setze die Worteingabe fort, bis du beim letzten Wort ankommst: dem Checksum.

An diesem Punkt zeigt Jade zwei Möglichkeiten: ein bestehendes Wort eingeben oder mit der eigenen Software einen gültigen Checksum berechnen lassen.

![alt text](https://officinebitcoin.it/lezioni/jadeset/12.jpg)

Hinweis:

- Bei einer Einrichtung aus einer mit Würfelwürfen erstellten Mnemonic mit 12 Wörtern wird empfohlen, Existing zu wählen und die ersten Buchstaben des Wortes einzugeben, wobei sie aus dem durch den Würfelwurf vorgeschlagenen Bereich ausgewählt werden.
- Wenn die Einrichtung hingegen mit einer durch Würfelwürfe erzeugten Mnemonic mit 24 Wörtern beginnt, kannst du Jade alle möglichen Checksums berechnen lassen und anschließend einen auswählen. Es stimmt, dass dabei etwas Entropie verloren geht, aber nur im letzten Wort. Wenn du dich entschieden hast, deine Funds Jade anzuvertrauen, ist das ein akzeptabler Kompromiss.
- Beim Wiederherstellen eines bestehenden Wallets: Gib den korrekten Checksum ein, indem du Existing wählst.

Im weiteren Beispiel einer Einrichtung aus einer mit Würfelwürfen erzeugten Mnemonic wählen wir im vorherigen Menü Existing, um die Buchstaben einzugeben und den entsprechenden Checksum zu finden.

![alt text](https://officinebitcoin.it/lezioni/jadeset/13.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/14.jpg)

An diesem Punkt schlägt Jade vor, die Recovery Phrase als _CompactSeedQR_ zu exportieren.

Der _CompactSeedQR_ ist eine Codierung, die die Mnemonic Phrase in einen QR-Code umwandelt, der zur Wiederherstellung des Wallets auf Jade gescannt werden kann.

Wenn du das ausprobieren möchtest, lies den Abschnitt am Ende dieses Tutorials, in dem erklärt wird, wie es funktioniert.

![alt text](https://officinebitcoin.it/lezioni/jadeset/15.jpg)

Wenn du im vorherigen Menü "No" auswählst, kannst du bis zum Ende der Einrichtung fortfahren.

Das Gerät ist bereit, mit seinem watch-only wallet verbunden zu werden.

Das nächste Menü zeigt die Verbindungsmöglichkeiten:

- USB
- QR code
- Bluetooth

![alt text](https://officinebitcoin.it/lezioni/jadeset/16.jpg)

Wähle USB und bestätige mit der Bestätigungstaste.

An diesem Punkt fordert Jade dazu auf, mit einer companion app verbunden zu werden.

Im folgenden Beispiel wurde gewählt, das Gerät per USB mit Blockstream Green zu verbinden; dieses Wallet erlaubt nämlich, Firmware-Updates für Jade zu kontrollieren, und bietet durch die Kommunikation mit dem Gerät über USB eine geführte Einrichtung.

Öffne Green und prüfe die Netzwerk- und Sicherheitseinstellungen.

Wenn ein Firmware-Update verfügbar ist, meldet Green dies sofort, und es wird empfohlen, das Upgrade auszuführen.

![alt text](https://officinebitcoin.it/lezioni/jadeset/17.jpg)

Nachdem das Firmware-Update abgeschlossen ist, beginnt Green mit Jade zu interagieren.

Das Signiergerät fordert nun dazu auf, den duress PIN festzulegen. Dieser verschlüsselt die privaten Schlüssel auf Jade und macht sie für alle unzugänglich, außer für Personen, die den sechsstelligen PIN besitzen.

![alt text](https://officinebitcoin.it/lezioni/jadeset/18.jpg)

Während Green mit dem oben gezeigten Bildschirm wartet, erscheint auf Jade die Möglichkeit, den 6-stelligen PIN festzulegen und ihn durch erneute korrekte Eingabe zu bestätigen.

![alt text](https://officinebitcoin.it/lezioni/jadeset/19.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/20.jpg)

Jade erstellt persistente Daten, indem es sie auf dem Gerät verschlüsselt.

![alt text](https://officinebitcoin.it/lezioni/jadeset/21.jpg)

Am Ende des Vorgangs, der einige Augenblicke dauern kann, öffnet Green das einsatzbereite Wallet.

Wenn Jade ausgeschaltet und wieder eingeschaltet wird, erscheint das Gerät als initialisiert, mit aktualisierter Firmware und bereit zur Entsperrung (Unlock Jade) für die Verwendung mit seiner companion app.

![alt text](https://officinebitcoin.it/lezioni/jadeset/22.jpg)

## Extra: CompactSeedQR erstellen

Am Ende der Eingabe der Mnemonic haben wir den Teil zum Exportieren der Schlüssel im QR-Code-Format übersprungen, um auf die Einrichtungsphase fokussiert zu bleiben. Diese Art von Export kann jederzeit später durchgeführt werden.

Schalte Jade ein und gehe im Menü Options → Temporary Signer → Continue → 12/24 Words zurück zum Eingabemenü der Recovery Phrase. Am Ende wird der Auswahlbildschirm für den Export im SeedQR-Format angeboten.

![alt text](https://officinebitcoin.it/lezioni/jadeset/15.jpg)

Wenn du Yes auswählst, wirst du darauf hingewiesen, dass du den QR-Code auf die in der Schachtel enthaltene Vorlage zeichnen musst.

![alt text](https://officinebitcoin.it/lezioni/jadeset/24.jpg)

Der Vorgang beginnt mit einer Übersicht darüber, wie der zu zeichnende QR-Code aussehen wird (einige Teile sind aus Datenschutzgründen gelöscht).

![alt text](https://officinebitcoin.it/lezioni/jadeset/25.jpg)

Anschließend werden alle Felder des Rasters nacheinander angezeigt, von A1 bis C3 oder E5, je nach Länge der Recovery Phrase.

![alt text](https://officinebitcoin.it/lezioni/jadeset/26.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/27.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/28.jpg)

Nachdem das letzte Feld des Rasters gezeichnet wurde, zeigt Jade erneut die Übersicht für eine erste Überprüfung. Fahre fort, indem du Done bestätigst.

![alt text](https://officinebitcoin.it/lezioni/jadeset/29.jpg)

Die integrierte Kamera von Jade wird aktiviert; mit ihr musst du den gerade gezeichneten SeedQR erfassen.

![alt text](https://officinebitcoin.it/lezioni/jadeset/30.jpg)

Wenn die Zeichnung dem entspricht, was Jade im soeben abgeschlossenen Vorgang vorgeschlagen hat, wird ein Bestätigungssignal angezeigt.

![alt text](https://officinebitcoin.it/lezioni/jadeset/31.jpg)

Durch Klicken zur Bestätigung von Continue zeigt Jade wieder die Hauptmenüs und ist betriebsbereit.

Der CompactSeedQR ist ein Werkzeug zur Wiederherstellung des Wallets auf Jade.
