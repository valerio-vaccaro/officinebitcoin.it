---
layout: default
name: "Manuelles Coin Control verstehen"
description: "Umfassender Leitfaden zur manuellen UTXO-Auswahl. Verstehe, warum sie wichtig ist, und lerne, wie du sie mit verschiedenen Software Wallets (Desktop und Mobile) nutzt"
title: "Manuelles Coin Control verstehen"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only-Lektion</span> <span>Dieses Projekt wird von valerio-vaccaro gepflegt</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](https://officinebitcoin.it/lezioni/coinco/cover.webp)

# Manuelles Coin Control verstehen

## Einführung

Die Robustheit des Bitcoin-Protokolls wird durch einfache Grundkonzepte garantiert. Unter ihnen sticht Transparenz hervor: Alle Bitcoin-Transaktionen sind öffentlich und für jeden leicht überprüfbar. Diese Eigenschaft ist zwar ein Grundpfeiler des Protokolls, weil sie Betrug verhindert und die Echtheit der Mittel sicherstellt, sie kann aber auch eine Herausforderung für die Vertraulichkeit darstellen. **Hast du dich jemals gefragt, ob so viel Transparenz deine Privatsphäre beeinträchtigen kann?**

Das solltest du. Während das Ansammeln von non-KYC satoshis recht einfach ist, ist deine Privatsphäre in der Ausgabenphase am stärksten gefährdet.

## Was passiert, wenn du einen UTXO ausgibst
Bitcoin auszugeben bedeutet nicht einfach, Wert an jemand anderen zu übertragen.

Wenn du einen deiner UTXOs verbrauchst, musst du die Bedingungen erfüllen, die für die Transparenz des Protokolls gelten, weil du den Besitz dieser Mittel nachweisen musst. Du musst daher:
- deinen öffentlichen Schlüssel offenlegen;
- eine digitale Signatur erzeugen.

Der Moment des Ausgebens ist daher der kritischste: **bitcoin auszugeben ist ein Vorgang, der bewusst und mit möglichst viel Kontrolle erfolgen sollte**.

## Coin Control
Im Bitcoin-Protokoll gibt es keine Elemente wie "Konto" oder "Geldeinheit". Das Konzept des UTXO ist nicht der Schwerpunkt dieser Lektion, aber ich lade dich ein, deinem vertrauten Satoshi Spritz Fragen zu stellen oder hier bei Officine Bitcoin eine Lektion anzufordern.
Was du wissen musst: Bei Bitcoin sind das, was du ansammelst und später ausgibst, kleine oder große Rechnungseinheiten, gemessen in satoshis, dargestellt durch `unspent transaction outputs`, die **UTXOs**, auch `coins` genannt.
Wenn du UTXOs verwendest, um eine Transaktion zu erstellen, werden sie vollständig zerstört und an ihrer Stelle werden neue UTXOs erzeugt.

Software Wallets sind so entwickelt, dass sie diese Auswahl automatisch treffen, indem sie "zufällig" ausgewählte coins verwenden, mit dem einzigen Kriterium, den benötigten Ausgabenbetrag abzudecken.

`Coin Control`, auch `Coin Selection` genannt, ist eine Funktion einiger Software Wallets, mit der du **die UTXOs, die beim Erstellen deiner Transaktion ausgegeben werden sollen, manuell auswählen** kannst.

Angenommen, du hast eine wallet mit 3 UTXOs, nämlich 21,000, 42,000 und 63,000 satoshis.

![img](https://officinebitcoin.it/lezioni/coinco/01.webp)

Wenn du 24,000 sats ausgeben musst und die Software automatisch auswählen lässt, könnte eine gute wallet UTXO1 + UTXO2 kombinieren, um die 24k sats und die Miner-Gebühren zu bezahlen, und dabei Wechselgeld erzeugen, das an eine interne Adresse der ursprünglichen wallet zurückgeht.

![img](https://officinebitcoin.it/lezioni/coinco/02.webp)

Nach der Transaktion lässt sich die neue Situation in der wallet, nur die UTXOs betrachtet, wie folgt zusammenfassen.

![img](https://officinebitcoin.it/lezioni/coinco/03.webp)

Mit der richtigen Software und deinem Bewusstsein hättest du jedoch eine andere und korrektere Wahl treffen können. Zum Beispiel, indem du nur UTXO2 (42,000 sats) auswählst.

![img](https://officinebitcoin.it/lezioni/coinco/04.webp)

Mit einer abschließenden UTXO-Situation in deiner wallet, die anders aussieht.

![img](https://officinebitcoin.it/lezioni/coinco/05.webp)

## Warum UTXOs manuell auswählen?
![img](https://officinebitcoin.it/lezioni/coinco/06.webp)

In unserem Beispiel ist der Kontostand tatsächlich derselbe: `108,280 sats`. Nach dem Ausgeben von 24,000 sats hätten wir ohne coin control 2 UTXOs in der wallet; mit manuellem coin control haben wir insgesamt 3.

**Warum das alles?**

Es gibt, oder könnte, mehrere Gründe geben, warum wir `UTXO1` nicht verwendet haben **und sie alle erklären, warum es beim Ausgeben eine gute Praxis ist, manuelles coin control zu aktivieren**.

## Privatsphäre
Der Hauptvorteil, wenn wir über manuelle coin-Auswahl sprechen, ist **mehr Privatsphäre für den Ausgebenden**.

Nehmen wir unser Beispiel erneut: 24,000 satoshis _ohne coin control_ ausgeben. Da die Bitcoin-Blockchain ein öffentliches Register ist, kann ein externer Beobachter ohne Zweifel feststellen, dass die inputs `UTXO1 of 21,000 sats` und `UTXO2 of 42,000 sats` sowie das Wechselgeld `UTXO5 of 38,280 sats` **alle demselben Nutzer gehören**.

Wenn du hingegen `UTXO2` manuell auswählst, bleibt `UTXO1` vollständig privat im UTXO set und wartet darauf, zu einem passenderen Zeitpunkt ausgegeben zu werden.

`UTXO1` könnte aus einer KYC-Quelle stammen, zum Beispiel aus einer Zahlung für Waren und Dienstleistungen, während die anderen UTXOs das nicht tun.

**Wenn es deine wallet wäre, würdest du wollen, dass ein externer Beobachter deine Identität mit solcher Sicherheit zurückverfolgen kann?** Wallets, die manuelle UTXO-Auswahl implementieren, erlauben zum Beispiel die **Trennung eines oder mehrerer UTXOs**, eine Funktion, die du nutzen solltest, wenn solche Situationen auftreten.

Auch wenn ich glaube, dass KYC-Mittel in einer separaten wallet von non-KYC bitcoin gehalten werden sollten, ist es in diesem Fall eine grundlegende Hilfe, einige deiner Adressen zu trennen. Das erreichst du, indem du lernst, deine Ausgaben-inputs manuell auszuwählen.

## Gebühren sparen
Den richtigen UTXO für eine Ausgabe auszuwählen, erlaubt dir, Gebühren zu optimieren. Auch in unserem Beispiel hat die Software Wallet zwei UTXOs ausgewählt, um die Ausgabe abzudecken. Zwei UTXOs bedeuten zwei Signaturen, die dem Netzwerk gezeigt werden müssen, also ein höheres Transaktionsgewicht in vBytes.

Mit manuellem coin control kannst du nur einen auswählen, der ausreicht, um den Betrag abzudecken, und Gebühren sparen, weil das "Gewicht" der Transaktion sinkt.

Wenn die Gebühren hoch sind, du aber gezwungen bist, bitcoin on-chain auszugeben (z. B. um einen Lightning Network-Kanal zu öffnen), wird coin control zum richtigen wirtschaftlichen Anreiz, es zu nutzen.

## Wechselgeld aggregieren
Wenn du eine Zahlung tätigst und Bitcoin on-chain nutzt, wird die Möglichkeit, Wechselgeld zu erhalten, fast immer zur Gewissheit. Jedes Wechselgeld ist selbst ein kleiner Verlust an Privatsphäre, weil es dem Netzwerk eine deiner Adressen offenlegt, die mit deinem ursprünglichen input verbunden werden kann.

Da die besten HD wallets spezielle Adressen für Wechselgeld erzeugen, kannst du sie leicht erkennen und das gesamte Wechselgeld aus verschiedenen Transaktionen "trennen"; wenn es einen bestimmten Betrag erreicht, kannst du es manuell auswählen und konsolidieren oder es im Lightning Network tauschen (meine bevorzugte Methode), um die beim Ausgeben verlorene Privatsphäre zurückzugewinnen.

## Aus einer cold wallet ausgeben
Eine cold wallet ist ein Werkzeug, mit dem du vernünftigerweise ein gutes Sicherheitsniveau erreichen kannst, um beliebige Beträge langfristig beiseitezulegen. Dennoch können unvorhergesehene Ereignisse eintreten, die dich zwingen, auf deine Ersparnisse zuzugreifen und unerwartete Ausgaben zu decken.

Mein Rat lautet: **Gib niemals direkt aus der cold wallet aus, um zu vermeiden, dass Wechselgeld an Adressen derselben wallet zurückkommt**. Lerne, die UTXOs, die zur Deckung der Ausgabe benötigt werden, manuell auszuwählen, übertrage sie auf eine hot wallet und bereite deine Transaktion von dort aus vor. Etwaiges Wechselgeld kannst du dann an eine cold-wallet-Adresse zurücksenden (wenn der Betrag angemessen ist) oder für andere Zwecke verwenden.

## Praktische Demonstration
Nach dieser langen Einführung sehen wir uns an, wie coin control mit verschiedenen Desktop- und Mobile-Softwares praktisch eingesetzt wird. Wir verwenden immer dieselbe HD wallet, die in jedes der ausgewählten Werkzeuge importiert wird, um dir die kleinen Unterschiede zwischen ihnen zu zeigen.

## Desktop Wallets

## Sparrow
Wenn du Sparrow verwendest, öffne deine wallet und wähle _UTXOs_ im linken Menü. Du siehst die Liste aller UTXOs, die mit deiner wallet verbunden sind.

Klicke einfach auf einen und wähle dann _Send Selected_. Sparrow zeigt dir neben dem Befehl auch die Gesamtsumme an, die für die Ausgabe ausgewählt wurde.

![img](https://officinebitcoin.it/lezioni/coinco/07.webp)

Du kannst auch mehr als einen auswählen. Verwende die Taste _CTRL_, um nicht benachbarte UTXOs in der Liste auszuwählen.

![img](https://officinebitcoin.it/lezioni/coinco/08.webp)

Nachdem du die UTXOs manuell ausgewählt hast, zeigt Sparrow dir grafisch klar, wie deine Transaktion aufgebaut ist, die du dann finalisieren und abschließen kannst.

![img](https://officinebitcoin.it/lezioni/coinco/09.webp)

### UTXO-Trennung
Mittel zu trennen bedeutet, sie innerhalb der wallet zu "sperren", sodass sie nicht als Transaktions-inputs verwendet werden können.

Sparrow erlaubt diese Funktion, erreichbar über das Menü _UTXOs_. Fahre mit der Maus über den zu "sperrenden" UTXO und klicke mit der rechten Maustaste. Unter den Optionen findest du _Freeze_. So kannst du mit Sparrow Wallet einen UTXO trennen.

![img](https://officinebitcoin.it/lezioni/coinco/29.webp)

## Electrum
Wenn deine desktop wallet Electrum ist, kannst du UTXOs sowohl über die Menüs _Addresses_ als auch _Coins_ manuell auswählen.
In beiden Menüs erfolgt die Auswahl, indem du mit der Maus auf den UTXO zeigst und nach einem Rechtsklick _Add to coin control_ auswählst.

![img](https://officinebitcoin.it/lezioni/coinco/10.webp)

Du kannst auch mehr als einen UTXO auswählen, mit der Taste _CTRL_, wenn sie nicht benachbart sind.

![img](https://officinebitcoin.it/lezioni/coinco/11.webp)

Electrum hebt ausgewählte UTXOs grafisch grün hervor, und unten zeigt eine Leiste in derselben Farbe den nach coin control verfügbaren Saldo.

![img](https://officinebitcoin.it/lezioni/coinco/12.webp)

Sobald die output(s) ausgewählt sind, kannst du deine Transaktion wie gewohnt über das Menü _Send_ erstellen.

### UTXO-Trennung
Electrum bietet diese Option im Menü _Coins_, indem du einen bestimmten UTXO auswählst und dann mit der rechten Maustaste _Freeze_ wählst. Du kannst auch eine Adresse ohne Mittel über das Menü _Addresses_ "einfrieren", oder die "coin", um Ausgaben zu verhindern.

![img](https://officinebitcoin.it/lezioni/coinco/28.webp)

## Nunchuk
Nunchuk ermöglicht dir, UTXOs nach dem Öffnen über das Hauptmenü auszuwählen.
Starte Nunchuk und klicke auf _View coins_.

![img](https://officinebitcoin.it/lezioni/coinco/13.webp)

Es öffnet sich ein Fenster mit allen UTXOs deiner wallet, in dem du einen oder mehrere auswählen kannst, indem du das Kästchen neben jedem Betrag markierst. Nach der Auswahl fährst du mit _Create transaction_ fort.

![img](https://officinebitcoin.it/lezioni/coinco/14.webp)

Danach kannst du die Zieladresse eingeben sowie Betrag und Gebühren festlegen.

![img](https://officinebitcoin.it/lezioni/coinco/15.webp)

## Blockstream App
Blockstream App desktop, früher als Green bekannt, erlaubt coin-Auswahl, sobald du begonnen hast, die Transaktion zu erstellen. Öffne deine wallet und klicke auf _Send_.

![img](https://officinebitcoin.it/lezioni/coinco/16.webp)

Füge die Zieladresse in das passende Feld ein und wähle dann _Manual coin selection_.
![img](https://officinebitcoin.it/lezioni/coinco/17.webp)
Ein Fenster öffnet sich, in dem du einen oder mehrere UTXOs auswählen kannst. Im folgenden Beispiel haben wir zwei coins ausgewählt. Bestätige die Auswahl anschließend mit _Confirm Coin Selection_.

![img](https://officinebitcoin.it/lezioni/coinco/18.webp)

Lege Betrag und Gebühren fest und fahre dann wie gewohnt mit deiner Transaktion fort.

![img](https://officinebitcoin.it/lezioni/coinco/19.webp)

⚠️ Hinweis: Im Menü _Coins_ von Green gibt es Optionen _Lock_/_Unlock_, die die Möglichkeit nahelegen, UTXOs zu trennen. Das ist nur in sogenannten multisig-Konten verfügbar; die Funktion wird nur für sehr kleine UTXOs nahe der `Dust`-Schwelle aktiviert.

## Mobile Wallets

## Blue Wallet
Auch mobil kannst du wallets wählen, die manuelle UTXO-Auswahl erlauben. Schauen wir uns zuerst Blue Wallet an.

Wenn du diese Software nutzt, öffne deine wallet und klicke, um in die Befehlsbildschirme einer deiner wallets zu gelangen. Um auf coin control zuzugreifen, musst du in die Ausgabenphase wechseln, also klicke auf _Send_.

![img](https://officinebitcoin.it/lezioni/coinco/21.webp)

Wähle im nächsten Bildschirm das Menü, das durch die drei Punkte oben rechts angezeigt wird. Ein Dropdown-Fenster mit mehreren Befehlen öffnet sich. Wähle den letzten: _Coin Control_.

![img](https://officinebitcoin.it/lezioni/coinco/22.webp)

An dieser Stelle zeigt Blue Wallet alle deine UTXOs. Zusätzlich zu den Beträgen werden sie grafisch durch verschiedene Farben unterschieden.

![img](https://officinebitcoin.it/lezioni/coinco/27.webp)

Wähle den UTXO aus und dann _Use Coin_.

![img](https://officinebitcoin.it/lezioni/coinco/23.webp)

Blue Wallet bringt dich zurück zum Fenster _Send_, um die Transaktion weiter zu erstellen. Passe Betrag und Gebühren an und wähle dann _Next_.

![img](https://officinebitcoin.it/lezioni/coinco/24.webp)

Jetzt kannst du die Transaktion wie gewohnt abschließen.

### UTXO-Trennung
Blue Wallet erlaubt dir auch, UTXOs zu trennen und sie damit für Ausgaben unverfügbar zu machen, was für eine mobile wallet eine gute Funktion ist.

Greife wie oben erklärt auf coin control zu und wähle nach Auswahl des UTXO _Freeze_ statt _Use Coin_.

![img](https://officinebitcoin.it/lezioni/coinco/26.webp)

## Nunchuk
Die mobile Version von Nunchuk erlaubt Nutzern ebenfalls coin control. Wenn du diese app mobil nutzt, öffne sie und gehe zum Menü _Wallet_. Wähle von dort _View coins_.

![img](https://officinebitcoin.it/lezioni/coinco/30.webp)

Klicke im Fenster mit der Liste der UTXOs auf _Select_.

![img](https://officinebitcoin.it/lezioni/coinco/38.webp)

Neben jedem UTXO erscheint die Auswahlfunktion. Wie in der Desktop-Version erfolgt die manuelle Auswahl in Nunchuk mobile durch Markieren des Kästchens neben dem Betrag. Der Bildschirm zeigt die Anzahl der ausgewählten UTXOs und den gesamten verfügbaren Betrag. Wenn du fertig bist, ist das ₿-Symbol unten links der Befehl, um mit dem Erstellen der Transaktion zu beginnen.

![img](https://officinebitcoin.it/lezioni/coinco/31.webp)

Jetzt kannst du die Transaktion abschließen, indem du den Betrag auswählst und auf _Continue_ klickst.

![img](https://officinebitcoin.it/lezioni/coinco/32.webp)

Fahre wie gewohnt fort, indem du eine Zieladresse, eine Beschreibung und die Gebühreneinstellungen einfügst bzw. anpasst.

## Bitcoin Keeper
Bitcoin Keeper ist die letzte wallet, die wir in diesem Leitfaden sehen. Sehen wir uns seine coin-control-Funktion mit einer single-sig wallet an, auch wenn eine solche Nutzung nicht der Hauptzweck dieser speziellen app ist.

Nachdem du Keeper auf deinem Telefon eingerichtet hast, starte es und öffne eine wallet, die einige UTXOs enthält. Klicke in der Mitte des Hauptbildschirms auf _View All Coins_.

![img](https://officinebitcoin.it/lezioni/coinco/34.webp)

Keeper zeigt eine Übersicht der UTXOs. Um auf den Auswahlbildschirm zuzugreifen, klicke auf _Select To Control_.

![img](https://officinebitcoin.it/lezioni/coinco/35.webp)

Du kannst coins auswählen, indem du sie markierst und den entsprechenden Befehl anklickst. Wenn du fertig bist, klicke auf _Send_.

![img](https://officinebitcoin.it/lezioni/coinco/36.webp)

Bitcoin Keeper bringt dich direkt zum Menü _Send_, wo du die Transaktion mit den ausgewählten UTXOs erstellen kannst.

![img](https://officinebitcoin.it/lezioni/coinco/37.webp)

## Hardware wallet
Jede der in diesem Leitfaden gezeigten Software Wallets kann die watch-only-Schnittstelle für deine hardware wallet sein. Das bedeutet, dass coin control für ein offline signierendes Gerät mit den bisher gezeigten Schritten durchgeführt wird.

## Allgemeine Empfehlungen
Coin control ist eine sehr wirksame Praxis, um deine Transaktions-inputs auszuwählen. Die manuelle Auswahl ist noch effizienter, wenn du beim Empfang deiner Mittel die Herkunft deiner satoshis gut beschriftet hast. Wenn du diese Technik beherrschen möchtest, empfehle ich das Tutorial:

https://planb.network/tutorials/privacy/on-chain/utxo-labelling-d997f80f-8a96-45b5-8a4e-a3e1b7788c52
