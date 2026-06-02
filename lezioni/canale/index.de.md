---
layout: default
title: "Lightning Network non-custodial"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only-Lektion</span> <span>Dieses Projekt wird von valerio-vaccaro gepflegt</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](https://officinebitcoin.it/lezioni/canale/01cover.webp)

# Lightning Network non-custodial
Phoenix von Acinq ist ein natives Lightning Network wallet, non-custodial, das ein effizientes Wallet nach BIP39-Standard bietet, gut angebunden ist und den Nutzern die volle Kontrolle lässt.

Du wirst bald feststellen, dass Phoenix einen LN-Kanal öffnet, für dessen Guthaben du zu 100 % verantwortlich bist.
Um gut mit Phoenix zu arbeiten, genügen ein wenig Aufmerksamkeit und Grundkenntnisse der Lightning Network. Du lernst zum Beispiel, die Liquidität deines Kanals im Blick zu behalten, ihn entsprechend deinen Bedürfnissen auszugleichen und dafür zu sorgen, dass Acinq dich online sieht, damit der Kanal offen bleibt und die LN-Infrastruktur erhalten wird.

# Grundlegende Vorgänge
Nachdem du die [Phoenix apk heruntergeladen und verifiziert](https://officinebitcoin.it/lezioni/verifica/index.html) hast, kannst du die App auf deinem Telefon installieren.

Phoenix startet mit der Frage, ob du ein neues Wallet erstellen oder ein früheres wiederherstellen möchtest. Wenn dies deine erste Erfahrung mit Phoenix ist, wähle `Create new wallet`. Danach folgt eine Reihe von Willkommensbildschirmen, die dort endet, wo du `Get started` drückst.

![img](https://officinebitcoin.it/lezioni/canale/03.webp)

## Backup
Sobald Phoenix geöffnet ist, **ist der erste Vorgang, wie immer, das Backup des Wallets**.

Phoenix verwendet den BIP39-Standard, Ableitungspfad m/84'/0'/0', und stellt eine Folge von 12 Wörtern bereit, die du auf Papier abschreiben und an einem sicheren Ort aufbewahren solltest.

![img](https://officinebitcoin.it/lezioni/canale/04.webp)

Öffne die Menüs und lass dir von Phoenix die *Recovery phrase* anzeigen, indem du auf `Display seed` klickst.

![img](https://officinebitcoin.it/lezioni/canale/05.webp)

Wenn du fertig bist, denke daran, den Bildschirm ganz nach unten zu scrollen, um zu bestätigen, dass du das Backup durchgeführt hast und die Benachrichtigung samt Warnung nicht mehr angezeigt wird.

![img](https://officinebitcoin.it/lezioni/canale/06.webp)

Phoenix ist im Wesentlichen einsatzbereit. Dein neues Wallet hat ein Guthaben von null und kann konfiguriert werden. Unten links findest du den Befehl, um erneut in die Einstellungen zu gelangen und nützliche Optionen für den täglichen Gebrauch zu konfigurieren.

![img](https://officinebitcoin.it/lezioni/canale/07.webp)

## Nutzung mit Tor
Seit mehreren Phoenix-Versionen hat Acinq die integrierte Tor-Engine deaktiviert. Wenn du Phoenix mit Tor-Schutz nutzen möchtest, sind zwei Schritte erforderlich:
- Tor in den Phoenix-Einstellungen aktivieren
- eine Drittanbieter-App verwenden, um den Wallet-Traffic durch das Onion-Netzwerk zu leiten.

Öffne die Einstellungen und wähle Tor, aktiviere dann `Enable Tor` und leite den Traffic schließlich über die App, die du normalerweise verwendest (Orbot, Invizible Pro usw.). Ohne eine dieser Drittanbieter-Apps, aber mit aktiviertem Tor in den Phoenix-Einstellungen, kann sich das Wallet nicht mit dem Internet verbinden.

![img](https://officinebitcoin.it/lezioni/canale/09.webp)

## Weitere Einstellungen
Du kannst eine Reihe von Funktionen ändern oder festlegen:
- den Namen des Wallets, indem du oben auf das Wort `Wallet` klickst;
- die Referenzwährung im Untermenü `Display`.
- Gebühren in `Channel management` festlegen, eine wichtige Einstellung, weil ein zu niedriger Gebührenwert die Kanalöffnung gefährden könnte: standardmäßig ist er auf 5,000 sats gesetzt, erhöhe ihn auf 15,000; Phoenix verwendet zum jeweiligen Zeitpunkt ohnehin den passenden Wert;
- du solltest im Untermenü `Access control` alle Sicherheitsvorkehrungen aktivieren, die du zuverlässig handhaben kannst: PIN zum Ausgeben, PIN oder biometrische Kontrolle für den App-Zugriff;
- deinen eigenen `Electrum server` im gleichnamigen Menü einrichten, wobei zu beachten ist, dass Phoenix ein gültiges SSL-Zertifikat verlangt (zum Beispiel Let's Encrypt);
- `Experimental features` aktivieren, um eine wiederverwendbare Bolt12-LN-Adresse anzufordern
- eventuelle Kanal-Schließungen oder das Erstellen/Löschen mehrerer Wallets verwalten.

![img](https://officinebitcoin.it/lezioni/canale/08.webp)

# LN-Kanal öffnen ⚡️

Wähle auf dem Phoenix-Hauptbildschirm den Befehl `Receive`

![img](https://officinebitcoin.it/lezioni/canale/10.webp)

Das Wallet bietet dir zwei Empfangsarten, beide mit QR-Code: Lightning und Onchain.

## Eine Lightning-Rechnung bezahlen

![img](https://officinebitcoin.it/lezioni/canale/11.webp)

Ein schneller Weg, deinen LN-Kanal zu öffnen, besteht darin, mit Phoenix eine Rechnung zu erstellen und sie mit einem anderen LN-Wallet zu bezahlen.

Die erste eingehende Zahlung bestimmt die Öffnung eines Kanals, dessen Liquidität durch den Betrag der gerade erstellten Rechnung definiert wird (abzüglich der Gebühren für die Onchain-Transaktion zur Kanalöffnung).

Die Mittel könnten sofort verfügbar sein, obwohl vorübergehend ein Hinweis zum Warten auf Onchain-Bestätigungen angezeigt wird. Oder du musst möglicherweise warten, bevor du sie verwenden kannst.

## Onchain-Transaktion
Das Öffnen eines LN-Kanals ist immer eine Onchain-Transaktion, 2-von-2-Multisig: Du und die Gegenpartei (Acinq) legen die Bedingungen mit deinen Mitteln fest.

Wenn du keine Möglichkeit hast, eine Lightning-Rechnung zu bezahlen oder zu empfangen, aber Onchain-Mittel besitzt, kannst du die Onchain-Adresse verwenden, die Phoenix dir anzeigt.

Nach der Transaktion sieht Phoenix so aus:

![img](https://officinebitcoin.it/lezioni/canale/12.webp)

Die App weist dich darauf hin, dass du 3 Blockchain-Bestätigungen abwarten musst, bevor du die Mittel verwenden kannst.

# Kanal-Liquidität verwalten
Sobald du die 3 Bestätigungen erhalten hast, ist dein LN-Wallet einsatzbereit.

Anfangs hat es die gesamte Liquidität ausgehend, und du kannst nur ausgeben; das siehst du unter `Settings -> Advanced -> Payment Channels`

![img](https://officinebitcoin.it/lezioni/canale/13.webp)

Du kannst eingehende Liquidität schaffen, indem du eine oder mehrere Lightning Network Rechnungen bezahlst.

# Das Wallet verwenden

Die Verwendung von Phoenix wallet ist angenehm und sehr einfach.

Die einzigen Dinge, die du beachten solltest, sind:
1. der Kanal, den du gerade erstellt hast, ist ein smart contract zwischen dir und Acinq, finanziert mit deinen Mitteln;
2. die aufwendige Arbeit des Backups von Kanalzuständen und der Wartung der Infrastruktur übernimmt Acinq, das dir für die von dir ausgeführten Zahlungsvorgänge ein paar zusätzliche sat an Gebühren berechnet;
3. greife regelmäßig auf dein Wallet zu, öffne es und führe von Zeit zu Zeit Vorgänge aus, denn wenn die Gegenpartei deine Abwesenheit bemerkt und dich als "zombie" betrachtet, könnte sie beschließen, den Kanal zu schließen. Acinq schließt Kanäle, um keine Ressourcen und Zeit für die Pflege von Backups und ruhenden Kanälen aufzuwenden;
4. du kannst dich auch dafür entscheiden, diesen Kanal zu schließen, falls du ihn nicht mehr benötigst.
5. im Fall einer Kanal-Schließung ist das Verfahren `cooperative closure` am besten, weil es viele Probleme vermeidet.

## Splicing
Eine besondere Erwähnung verdient die von Acinq implementierte Technik `Splicing`, mit der du die gesamte Kanalkapazität erhöhen oder verringern kannst.

Splicing ist interessant: Wenn du einen Kanal mit Kapazität `tot` hast, kannst du ihn erweitern oder verkleinern. Es mag so wirken, als hingen diese Vorgänge von den Bedürfnissen jeder Person ab, **aber so einfach ist es nicht**.

Du musst immer im Kopf behalten, dass **Phoenix ein Lightning Network wallet ist** und, auch wenn es Unterstützung für Bitcoins Layer1 hat, für kleine Zahlungen auf Layer2 verwendet werden sollte.

**Tatsächlich wird jede Onchain-Operation von Acinq als Grund interpretiert, die Kanalkapazität zu ändern**:
- Empfang eines Betrags von `xsats` auf Phoenix von einem Onchain-Wallet: Acinq erweitert den Kanal und bringt die Kapazität von `tot` auf `tot + xsats`
- Zahlung eines Betrags von `ysats` von Phoenix an eine Onchain-Adresse: Acinq reduziert den Kanal und bringt die Kapazität von `tot` auf `tot - ysats`.

`Splicing` ist eine Onchain-Transaktion (2-von-2-Multisig), die Gebühren verursacht. Obwohl diese niedriger sind als bei Kanalöffnung/-schließung, können solche Vorgänge unvorsichtig oder zum falschen Zeitpunkt unnötig hohe Kosten verursachen.

Um von LN zu Onchain und umgekehrt zu wechseln, versuche geeignete `swap`-Tools zu verwenden und nutze Phoenix Wallet nicht dafür.

# Mittel wiederherstellen
Zuletzt, aber am wichtigsten: Hier kommt die Bedeutung von **non-custodial** Werkzeugen ins Spiel.

Wenn und sobald der Kanal geschlossen wird, kannst du deine Onchain-Mittel wiederherstellen, **indem du die 12 Backup-Wörter in ein Wallet importierst, das den BIP39-Standard unterstützt**.

Electrum wallet ist unter anderem eine Option, die diesen Vorgang einfach und intuitiv macht.

Wenn das Wallet dagegen *custodial* ist und du die Schlüssel nicht besitzt, kannst du auf Probleme stoßen, von Schwierigkeiten im Umgang mit einem *unpersönlichen Kundendienst* über ein aufwendiges `kyc`, um sie zurückzubekommen, **bis hin zur Unmöglichkeit, deine Mittel wiederherzustellen (unabhängig vom Gesamtbetrag)**.

Ist es das wert?

# Lernunterstützung
Wenn du an der Live-Präsentation auf Telegram teilgenommen hast, kannst du sie als weiteren Schritt zu deiner persönlichen Souveränität betrachten (nicht nur finanziell).
Wenn du sie verpasst hast, **verzweifle nicht**: Diese Notizen dienen genau dazu, aufzuholen, und außerdem solltest du wissen, dass wir sie bei Officine erneut anbieten werden.

Um die nächste Präsentation nicht zu verpassen, tritt der [Telegram-Gruppe](https://t.me/officinebitcoin) bei, um ständig auf dem Laufenden zu bleiben.

![img](https://officinebitcoin.it/lezioni/canale/14.webp)

Du kannst auch den nächstgelegenen [Satoshi Spritz](https://satoshispritz.it/) finden. Ein Satoshi Spritz ist ein lokales Meetup, bei dem ausschließlich über Bitcoin gesprochen wird, wo du deine Fragen mitbringen und Antworten von anderen erfahrenen bitcoiners erhalten kannst. Unter dem Link findest du die Karte der Halbinsel.

![img](https://officinebitcoin.it/lezioni/canale/15.webp)

Wenn du schließlich kein Meetup in deiner Nähe findest, kannst du die wöchentlichen Live-Streams von [SatoshiSpritz Connect](https://t.me/SatoshiSpritzConnect) nutzen, einem virtuellen Meetup für alle, die nicht an Satoshi Spritz teilnehmen können, oder zur Unterstützung kleinerer Meetups beim Notizenmachen und beim Finden von Inspiration für ihre eigenen Präsentationen.

![img](https://officinebitcoin.it/lezioni/canale/16.webp)
