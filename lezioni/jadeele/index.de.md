---
layout: default
title: "Jade mit Electrum Wallet"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only-Lektion</span> <span>Dieses Projekt wird von valerio-vaccaro gepflegt</span></p>

## 🌍 Übersetzungen

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Jade mit Electrum Wallet

![alt text](https://officinebitcoin.it/lezioni/jadeele/0_cover.jpg)

Nachdem Jade initialisiert wurde, kann man es verwenden. Dazu muss ein Anzeige-Wallet ausgewählt werden.

Jade ist ein Gerät, das mit verschiedenen wallets verwendet werden kann, oder mit companion apps, wie Blockstream sie auf seiner Website nennt.

In diesem Tutorial werden die Nutzungsschritte über USB mit Electrum Wallet gezeigt.

Nehmen Sie das initialisierte Jade. Direkt nach dem Einschalten sieht es so aus:


![alt text](https://officinebitcoin.it/lezioni/jadeele/001.jpg)

Wenn Sie Unlock Jade auswählen, erscheint das Menü, in dem festgelegt wird, wie das Gerät mit der companion app verbunden werden soll.

Mit Electrum kann Jade nur via USB verbunden werden, daher muss diese Option gewählt werden.

Starten Sie Electrum. Es öffnet sich mit der Standardoption, das zuletzt verwendete wallet zu öffnen.

Wenn Jade zum ersten Mal mit Electrum verbunden wird, wählen Sie Create New Wallet und anschließend Finish.

![alt text](https://officinebitcoin.it/lezioni/jadeele/1.jpg)

Geben Sie dem wallet einen Namen, zum Beispiel Jade_Officine.

![alt text](https://officinebitcoin.it/lezioni/jadeele/3.jpg)

Wählen Sie Standard Wallet

![alt text](https://officinebitcoin.it/lezioni/jadeele/4.jpg)

Bei der Auswahl des Keystores ist es entscheidend, Use a hardware device auszuwählen.

![alt text](https://officinebitcoin.it/lezioni/jadeele/5.jpg)

Electrum beginnt mit der Suche nach dem hardware-Gerät

![alt text](https://officinebitcoin.it/lezioni/jadeele/6.jpg)

Wenn das USB-Kabel an den PC angeschlossen wird (auf der USB C-Seite bereits mit Jade verbunden), zeigt das hardware wallet den Sperrbildschirm an. Jade wird entsperrt, indem der beim setup festgelegte sechsstellige PIN eingegeben wird


![alt text](https://officinebitcoin.it/lezioni/jadeele/7.jpg)

Nachdem das hardware-Gerät entsperrt wurde, erkennt Electrum Jade. Fahren Sie fort, indem Sie auf Next klicken.

![alt text](https://officinebitcoin.it/lezioni/jadeele/8.jpg)

An diesem Punkt fordert Electrum dazu auf, die script policy festzulegen; wählen Sie Native Segwit.

![alt text](https://officinebitcoin.it/lezioni/jadeele/9.jpg)

Nun beginnt die Übertragung des öffentlichen Schlüssels vom wallet auf Jade zum Electrum-Anzeige-Wallet.

![alt text](https://officinebitcoin.it/lezioni/jadeele/10.jpg)

Nach dem Export des öffentlichen Schlüssels ist der Vorgang abgeschlossen.

Das watch-only wallet ist bereit, und Electrum meldet den Abschluss mit dem folgenden Bildschirm.

![alt text](https://officinebitcoin.it/lezioni/jadeele/11.jpg)

Das wallet wurde tatsächlich erstellt und kann nun erkundet werden: Man sieht die addresses, die wallet information und vor allem unten rechts den Hinweis, dass es sich um ein aus Blockstream Jade erstelltes wallet handelt. Der grüne Punkt neben dem Blockstream-Logo zeigt an, dass das Gerät eingeschaltet und korrekt verbunden ist.

![alt text](https://officinebitcoin.it/lezioni/jadeele/12.jpg)

Empfangs- und Ausgabetransaktionen

Erzeugen Sie im Receive-Menü von Electrum ein scriptPubKey (Adresse), um Gelder zu empfangen. Beginnen Sie immer mit einem kleinen Betrag und führen Sie einen Empfangs+Ausgabe-Test durch.

![alt text](https://officinebitcoin.it/lezioni/jadeele/13.jpg)

Nachdem die sats empfangen wurden, kann ihr Eingang im History-Menü überprüft werden.

![alt text](https://officinebitcoin.it/lezioni/jadeele/14.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeele/15.jpg)

Sobald die Transaktion bestätigt wurde, kann dieses UTXO ausgegeben und der Test beendet werden.

Für die Ausgabe wird Jade zum Signieren verwendet.

Gehen Sie in Electrum zum Send-Menü, fügen Sie ein scriptPubKey ein und prüfen Sie es sorgfältig.

![alt text](https://officinebitcoin.it/lezioni/jadeele/16.jpg)

Wenn alles erledigt ist, drücken Sie Pay.

Das Transaktionsfenster öffnet sich. Dort ist es wichtig, die korrekten Transaktions-fees festzulegen. Nachdem alle Einstellungen abgeschlossen sind, klicken Sie unten rechts auf Preview.

![alt text](https://officinebitcoin.it/lezioni/jadeele/17.jpg)

Das Transaktionsfenster zeigt einige wichtige Details, an erster Stelle den status: Unsigned.

In dieser Phase ist auch der Befehl Sign zu sehen, um die Signatur mit Jade anzubringen.

![alt text](https://officinebitcoin.it/lezioni/jadeele/18.jpg)

Electrum weist darauf hin, den Anweisungen auf dem hardware-Gerät zu folgen, das bereit zum Signieren ist.

Vorher ist es jedoch besser zu prüfen, was signiert wird: Alle Parameter der gerade eingerichteten Transaktion erscheinen auch auf Jade und können vollständig überprüft werden.

![alt text](https://officinebitcoin.it/lezioni/jadeele/19.jpg)

Zum Fortfahren stellen Sie sicher, dass der Cursor immer auf dem Pfeil → steht, der zu den nächsten Schritten führt, und niemals auf dem "X", das den Vorgang abbricht.

Die Anzeige der Prüfungen endet, wenn Jade die fees anzeigt. An diesem Punkt entspricht die Bestätigung dem Anbringen der Signatur.

![alt text](https://officinebitcoin.it/lezioni/jadeele/20.jpg)

Für einen kurzen Moment verarbeitet Jade die Signatur.

![alt text](https://officinebitcoin.it/lezioni/jadeele/21.jpg)

Währenddessen kann in Electrum der status der Transaktion überprüft werden, der von Unsigned zu Signed gewechselt ist. Nun kann die Transaktion durch Klicken auf Broadcast verbreitet werden.

![alt text](https://officinebitcoin.it/lezioni/jadeele/22.jpg)

Das so getestete wallet kann verwendet werden, um UTXO zu empfangen, die sicher aufbewahrt werden sollen.

![alt text](https://officinebitcoin.it/lezioni/jadeele/23.jpg)
