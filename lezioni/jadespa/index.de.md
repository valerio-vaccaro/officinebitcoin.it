---
layout: default
title: "Jade airgapped mit Sparrow Wallet"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only-Lektion</span> <span>Dieses Projekt wird von valerio-vaccaro gepflegt</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Jade airgapped mit Sparrow Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/0.jpg)

Jade für vollständig airgapped Kommunikation zu verwenden, ist dank der Eigenschaften von Firmware und Hardware möglich.

Die integrierte Kamera und das Display übernehmen nämlich genau die Funktion, Nachrichten zum und vom watch-only wallet zu erfassen und zu senden.

Dieses Tutorial zeigt, wie Jade airgapped mit Sparrow Wallet verwendet wird.

Der Ablauf umfasst zuerst die Einrichtung, dann den Export des erweiterten öffentlichen Schlüssels von Jade nach Sparrow-watch-only und schließlich eine Ausgabetransaktion.

Aus didaktischen Gründen wurde entschieden, mit der Abfolge der Schritte auf Jade zu beginnen.

## Erweiterte Einrichtung

Die Entscheidung, das Gerät airgapped zu verwenden, erfordert eine echte Einrichtung, d. h. sie muss während der Initialisierung von Jade (1) erfolgen; das Gerät muss daher als nicht initialisiert erscheinen.

![alt text](https://officinebitcoin.it/lezioni/jadespa/1.jpg)

Es erscheint ein Hinweis, die Einrichtungsanleitung auf der Website https://blockstream.com/jade/ zu prüfen.

![alt text](https://officinebitcoin.it/lezioni/jadespa/2.jpg)

Die Konfiguration von Jade für airgapped Nutzung kann nur durch Auswahl von Advanced Setup erfolgen.

![alt text](https://officinebitcoin.it/lezioni/jadespa/3.jpg)

Jade weist darauf hin, dass diese Einrichtung einige fortgeschrittene technische Funktionen enthält. Es reicht aus, besonders aufmerksam zu sein und die Bestätigungstaste zu drücken.

![alt text](https://officinebitcoin.it/lezioni/jadespa/4.jpg)

Um die mit Würfel-Entropie erzeugte Mnemonic einzugeben, wähle Restore Wallet.

![alt text](https://officinebitcoin.it/lezioni/jadespa/5.jpg)

Jetzt musst du die Länge der Mnemonic festlegen, 12 oder 24 Wörter. Das Menü bietet außerdem die Möglichkeit, das Wallet durch Scannen eines QR-Codes wiederherzustellen: Das ist der SeedQr, der im speziellen Setup-Tutorial behandelt wurde.

![alt text](https://officinebitcoin.it/lezioni/jadespa/6.jpg)

Aus rein didaktischen Gründen und der Geschwindigkeit wegen zeigt dieses Tutorial die Einrichtung mit einer Mnemonic aus 12 Wörtern.

Der nächste Schritt muss wie beschrieben befolgt werden, um auf die airgapped Funktion zugreifen zu können. Du musst nämlich wählen, die Recovery Phrase im CompactSeedQR-Format zu exportieren, indem du Yes auswählst.

![alt text](https://officinebitcoin.it/lezioni/jadespa/7.jpg)

Nach der Auswahl wirst du darauf hingewiesen, dass du den QR-Code auf die in der Schachtel enthaltene Vorlage zeichnen musst, wie im Abschnitt "Extra" der Setup-Lektion gezeigt.

![alt text](https://officinebitcoin.it/lezioni/jadespa/8.jpg)

Am Ende des Vorgangs musst du überprüfen, ob die Zeichnung dem vom Gerät angezeigten CompactSeedQR entspricht. Dafür wird die integrierte Kamera von Jade aktiviert, mit der du den gerade gezeichneten SeedQR erfassen musst.

![alt text](https://officinebitcoin.it/lezioni/jadespa/9.jpg)

Wenn die Zeichnung dem entspricht, was das Gerät im soeben abgeschlossenen Vorgang vorgeschlagen hat, wird ein Bestätigungssignal angezeigt.

![alt text](https://officinebitcoin.it/lezioni/jadespa/10.jpg)

Jetzt zeigt Jade die Optionen zum Verbinden des Geräts mit einer companion app: Wähle QR.

![alt text](https://officinebitcoin.it/lezioni/jadespa/11.jpg)

Der nächste Schritt erfordert ebenfalls eine Entscheidung des Benutzers: die verschlüsselten Schlüssel auf dem Gerät speichern oder sie bei jeder Sitzung durch Scannen des gerade gezeichneten SeedQR laden.

![alt text](https://officinebitcoin.it/lezioni/jadespa/12.jpg)

Hinweis:

Es ist nützlich, diese beiden Zugriffsoptionen zu verstehen:

- QR PIN Unlock: Während der Initialisierung speichert Jade die Wallet-Daten, indem es sie auf dem Gerät verschlüsselt; sie sind immer zugänglich, indem Jade mit dem QR PIN-Verfahren entsperrt wird.
- SeedQR: Der SeedQR muss jedes Mal von Jade gescannt werden, wenn du die Schlüssel auf das Gerät laden möchtest.

Aus didaktischen Gründen wurde in der vorherigen Option SeedQR gewählt; das Gerät wird daher stateless verwendet: Jade weist darauf hin, dass die Sitzung temporär ist und die Schlüssel vom Gerät "vergessen" werden, wenn es ausgeschaltet wird.

![alt text](https://officinebitcoin.it/lezioni/jadespa/13.jpg)

Export des öffentlichen Schlüssels

Nachdem Jade nun speziell für den vollständig airgapped Betrieb konfiguriert ist, gehen wir zur sensiblen Phase des Exports des öffentlichen Schlüssels über.
 
Ausgehend von Jade, das zu den Anfangsmenüs zurückgekehrt ist, wähle Options.

![alt text](https://officinebitcoin.it/lezioni/jadespa/14.jpg)

Hinweis: Dass Jade im Temporary Signer-Modus ist, erkennt man am Uhrsymbol neben der Anzeige Active.

Wähle in Options den Punkt Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/15.jpg)

Wähle anschließend Export Xpub

![alt text](https://officinebitcoin.it/lezioni/jadespa/16.jpg)

An diesem Punkt zeigt das Display von Jade einen dynamischen QR-Code, der den erweiterten öffentlichen Schlüssel darstellt. In Options dieses Untermenüs kannst du den Export von multisig/singlesig und den Derivation Path wählen.

Für dieses Tutorial wurde der Export eines full segwit singlesig gewählt.

![alt text](https://officinebitcoin.it/lezioni/jadespa/17.jpg)

In dieser Phase kommt Sparrow ins Spiel. Starte das Programm und erstelle ein neues Wallet, indem du New Wallet auswählst.

![alt text](https://officinebitcoin.it/lezioni/jadespa/18.jpg)

Gib dem Wallet einen Namen und klicke dann auf Create Wallet.

![alt text](https://officinebitcoin.it/lezioni/jadespa/19.jpg)

Klicke im nächsten Einstellungsbildschirm auf Airgapped Hardware Wallet.

![alt text](https://officinebitcoin.it/lezioni/jadespa/20.jpg)

Ein Sparrow-Fenster öffnet sich und zeigt die implementierten hardware wallets. Wähle Jade.

![alt text](https://officinebitcoin.it/lezioni/jadespa/21.jpg)

An diesem Punkt wird die Kamera des PCs aktiviert, mit dem du arbeitest.

![alt text](https://officinebitcoin.it/lezioni/jadespa/22.jpg)

Wenn mehr als eine Webcam verfügbar ist, wähle die beste im Dropdown-Menü aus, in dem Default Camera erscheint.

Nimm jetzt Jade (das weiterhin den dynamischen QR-Code des Xpub anzeigt) und halte das Display vor die PC-Kamera, wobei der QR-Code innerhalb des gestrichelten Bereichs bleiben muss.

![alt text](https://officinebitcoin.it/lezioni/jadespa/23.jpg)

Unter dem Kamerabild befindet sich eine Fortschrittsleiste, die blau wird.

Der Fortschritt der Xpub-Erfassung in Sparrow wird auf diese Weise angezeigt: von 0 bis 100%.

In dieser Phase können einige Anpassungen nötig sein: Helligkeit des Jade-Displays sowie die Frontbeleuchtung erhöhen/verringern oder im Dropdown-Menü von Sparrow Use HD Capture bzw. eine geringere Auflösung wählen.

Lass dich von diesen Details nicht abschrecken: Sobald deine persönliche Arbeitsumgebung eingerichtet ist, laufen diese Schritte bequem und einfach ab. (2)

Der Export ist tatsächlich erfolgt, wenn sich das Kamerafenster schließt und nach der Rückkehr zu den Settings von Sparrow alle Daten des watch-only wallet erscheinen.

![alt text](https://officinebitcoin.it/lezioni/jadespa/24.jpg)

Aufgrund der Struktur von Sparrow muss nun die script policy durch Klicken auf Apply angewendet werden.

Die Wallet-Erstellung wird fortgesetzt, indem ein Passwort zum Verschlüsseln der Wallet-Datei eingegeben und bestätigt wird.

![alt text](https://officinebitcoin.it/lezioni/jadespa/25.jpg)

Sie ist abgeschlossen, wenn die Fortschrittsleiste unten rechts das Feld zu 100% gefüllt hat.

![alt text](https://officinebitcoin.it/lezioni/jadespa/26.jpg)

## Ausgabetransaktion

Wenn Jade hypothetisch die Rolle eines persönlichen hardware wallet übernimmt, ist davon auszugehen, dass es Funds enthält und diese in Zukunft ausgegeben werden müssen.

Nachdem Sparrow als watch-only wallet und Jade als Signiergerät gewählt wurden, sehen wir, wie man mit diesen beiden Werkzeugen eine Transaktion erstellt, signiert und propagiert.

![alt text](https://officinebitcoin.it/lezioni/jadespa/27.jpg)

Im Beispiel ist ein Gesamtguthaben von 56,598 sats verfügbar.

Wähle im linken Menü von Sparrow Send und beginne mit dem Aufbau der Ausgabetransaktion. Nachdem alles eingestellt ist, klicke unten rechts auf Create transaction.

![alt text](https://officinebitcoin.it/lezioni/jadespa/28.jpg)

Ein erweitertes Transaktionsfenster erscheint, in dem sichtbar ist, dass Sparrow Jade als Signiergerät erkennt (Signing Wallet).

Wenn die Einstellungen passen, klicke auf Finalize Transaction.

![alt text](https://officinebitcoin.it/lezioni/jadespa/29.jpg)

Der Signaturbildschirm erscheint. In einem airgapped System erfolgt der Export der .psbt über QR-Code; klicke daher in Sparrow unten links auf Show QR.

![alt text](https://officinebitcoin.it/lezioni/jadespa/30.jpg)

Ein Fenster mit einem dynamischen QR-Code erscheint, der die psbt darstellt und anschließend mit der Kamera von Jade gescannt werden muss.

![alt text](https://officinebitcoin.it/lezioni/jadespa/31.jpg)

Nimm Jade und wähle in den Hauptmenüs Scan QR.

![alt text](https://officinebitcoin.it/lezioni/jadespa/32.jpg)

Erfasse mit der nun aktivierten Kamera von Jade den dynamischen QR-Code, den Sparrow erzeugt. Eine blaue Fortschrittsleiste auf dem Display des hardware wallet zeigt den Prozentsatz des Lesevorgangs an.

Sobald der Import der psbt abgeschlossen ist, zeigt Jade die Transaktionsdetails zur Überprüfung: Zieladresse und Betrag auf einem ersten Bildschirm

![alt text](https://officinebitcoin.it/lezioni/jadespa/33.jpg)

und die Gebühren auf einem zweiten Bildschirm. Durch Bestätigung auf diesem zweiten Bildschirm wird die Signatur mit Jade angewendet.

![alt text](https://officinebitcoin.it/lezioni/jadespa/34.jpg)

Automatisch zeigt das Display von Jade einen weiteren dynamischen QR-Code: Es ist die signierte Transaktion.

Unter den Optionen auf diesem Bildschirm kannst du die Dichte erhöhen/verringern, um die Kommunikation mit der wallet app zu verbessern.

![alt text](https://officinebitcoin.it/lezioni/jadespa/35.jpg)

In der Zwischenzeit muss Sparrow, das wir mit der Anzeige eines dynamischen QR-Codes verlassen haben, darauf eingestellt werden, die signierte Transaktion zur Propagation zu empfangen.

Du musst daher auf Scan QR klicken, um die Webcam des PCs wieder zu aktivieren.

![alt text](https://officinebitcoin.it/lezioni/jadespa/36.jpg)

Halte das Display von Jade vor die Webcam und lass Sparrow die signierte Transaktion importieren.

![alt text](https://officinebitcoin.it/lezioni/jadespa/37.jpg)

Die Fortschrittsleiste unter dem Bild muss bis 100% laufen, bis der Import erfolgt, den Sparrow wie folgt anzeigt.

![alt text](https://officinebitcoin.it/lezioni/jadespa/38.jpg)

Jetzt wird die gesamte Transaktion erneut überprüft, und wenn alles passt, kannst du sie durch Klicken auf Broadcast Transaction propagieren.

Im Menü Transactions erscheint die ausgehende Transaktion.

![alt text](https://officinebitcoin.it/lezioni/jadespa/39.png)

Hinweise

- (1) – Wenn Jade bereits initialisiert ist, gehe einfach zu Options → Settings → Factory reset
- (2) – Jade Original hat ein sehr kleines Display, und um den dynamischen QR-Code in dem von Sparrow angezeigten gestrichelten Bereich zu erfassen, muss das Display auf wenige Zentimeter herangeführt werden. Es kann daher nötig sein, eine sehr hochauflösende Webcam mit geeigneter Brennweite zu verwenden oder auf Apps wie Iriun zurückzugreifen, um ein Telefon in die Kamera des PCs zu "verwandeln". Telefone haben nämlich eine bessere Fokussierfähigkeit im Nahbereich.
