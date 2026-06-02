---
layout: default
name: "Bitcoin Starter Kit"
description: "Ein einfaches und leicht umsetzbares Starter Kit, um Bitcoin richtig zu verwenden. Lerne, eine mobile Wallet herunterzuladen und zu installieren, einen POS für Zahlungsanforderungen einzurichten und erweiterte Wallet-Einstellungen kennenzulernen."
title: "Anfangsglossar"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only-Lektion</span> <span>Dieses Projekt wird von valerio-vaccaro gepflegt</span></p>

## 🌍 Übersetzungen

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](assets/cover.webp)

Hier ist eine sehr gute Möglichkeit, Bitcoin auf möglichst korrekte Weise zu nutzen. Es folgt ein Vorschlag für ein sehr schlankes und einfach umsetzbares *starter kit*, das du selbständig einrichten kannst.

Egal ob du neugierig bist, als Profi Bitcoin als Zahlungsmethode akzeptieren willst oder als erfahrener Nutzer Lösungen für Freunde und Familie suchst, diese Anleitung ermöglicht dir:
- eine mobile Wallet herunterzuladen und zu installieren, um Bitcoin auf jeder Ebene zu nutzen (onchain für langfristige Aufbewahrung; oder Liquid und Lightning für Sofortzahlungen);
- einen POS einzurichten, der Zahlungsanforderungen ausgehend vom Preis deiner Waren/Dienstleistungen in Euro erstellt;
- erweiterte Wallet-Einstellungen kennenzulernen. Diesen Teil haben wir ans Ende der Anleitung gestellt, um den Einstieg zu vereinfachen, aber sieh ihn dir immer an, denn er ist wichtig.

Klären wir zuerst, was wir meinen, wenn wir davon sprechen, Bitcoin auf die *richtige Weise* zu verwenden.

# Anfangsglossar
- `Not your keys, not your coins`
  Wenn du dich Bitcoin zum ersten Mal näherst, ist der Satz `Not your keys, not your coins` neu für dich und seine Bedeutung reduziert sich vielleicht auf die wörtliche Übersetzung. Bitcoin funktioniert nach dem Prinzip der asymmetrischen Kryptografie, die auf Paaren aus öffentlichen und privaten Schlüsseln beruht. Nur durch den **alleinigen** Besitz und die eigene Verwaltung der privaten Schlüssel kannst du sagen, dass du Kontrolle über deine Bitcoin hast.
  
  Deshalb darfst nur du die privaten Schlüssel kennen, das Geheimnis, mit dem du die mit diesen Schlüsseln verbundenen bitcoin besitzen und später ausgeben kannst. `Not your keys, not your coins` ist praktisch ein _Mantra_ für Bitcoiner weltweit und wird auch für dich eines werden.

- `Recovery phrase`
  In seiner kurzen Geschichte hat sich das Bitcoin-Protokoll weiterentwickelt, um die Verwaltung von Geheimnissen, also privaten Schlüsseln, einfacher zu machen. Heute werden sie als Folge von 12 oder 24 englischen Wörtern dargestellt, die leichter aufzuschreiben und zu prüfen sind. Diese Wörter sind das wichtigste Geheimnis. Sie müssen auf Papier übertragen und an einem sehr sicheren Ort, etwa in einem Safe, aufbewahrt werden. Sie dürfen nie fotografiert, auf einen Computer übertragen oder gar mit anderen geteilt werden.

- `Wallet`
  Die Wallet ist das Werkzeug, mit dem du deinen Kontostand ansehen sowie Bitcoin empfangen oder ausgeben kannst. In diesem Tutorial laden wir eine auf dein Telefon. Die Wallet auf dem Telefon heißt `hot wallet`, weil sie auf einem Gerät liegt, das immer mit dem Internet verbunden ist. Für den Anfang ist das völlig in Ordnung; durch weiteres Lernen wirst du andere Methoden kennenlernen, um die Wallet-Nutzung zu verbessern.

- `Non Custodial`
  Es ist grundlegend wichtig, Bitcoin mit `non-custodial` Wallets zu verwenden, also mit solchen, die **dir die vollständige Kontrolle über die privaten Schlüssel geben**. Sei immer vorsichtig, wenn jemand dich dazu drängt, andere, sogenannte custodial Werkzeuge für den Einstieg in Bitcoin zu verwenden. Custodial Wallets sind Werkzeuge, deren Schlüssel dir nicht gehören. Es ist keine Frage des **ob**, sondern des **wann**, bis sie dir den Zugriff auf deine Gelder dauerhaft verwehren.

# Blockstream App (ex Green Wallet)
Für das starter kit laden wir Blockstream App herunter, eine `open source` Wallet, deren Code du überprüfen kannst. Die Anwendung hat eine lange Entwicklungstradition und eine solide Geschichte; die Wallet hat sich in der Vergangenheit als zuverlässig erwiesen.

---
⚠️ Die folgenden Anweisungen gelten für Download und Installation der App unter Android. Für iOS musst du den offiziellen Store verwenden.

---

## 🌍 Übersetzungen

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

Öffne den Link https://github.com/Blockstream/green_android, das offizielle Github-Repository des Entwicklers.

![img](assets/01.webp)

Wähle in der Mitte der Seite rechts im Bereich *Releases* `Latest`, um die aktuellste Version herunterzuladen.

Du gelangst auf eine Seite mit der neuesten release, zum Zeitpunkt dieses Tutorials im Dezember 2025 Version 5.1.4. Wähle auf derselben Seite aus, was du herunterladen kannst:

![img](assets/02.webp)

Lade die Datei `.apk` herunter, ohne den Play Store zu verwenden, und installiere sie auf deinem Android-Telefon.

![img](assets/03.webp)

---
⚠️ Dein Telefon kann besondere Berechtigungen verlangen, um Apps aus nicht zertifizierten Quellen herunterzuladen. Erteile diese Berechtigungen, um fortzufahren.

---
Wenn Android dich auffordert, Blockstream App zu installieren, tippe auf `Install`.

![img](assets/04.webp)

Am Ende der Installation wähle `Open`.

![img](assets/05.webp)

Blockstream App öffnet sich. Um die Wallet zu verwenden, wähle `Get Started`.

![img](assets/07.webp)

Blockstream fragt dich, ob du an der Datenerhebung teilnehmen möchtest, um den Entwicklern bei der Verbesserung der App zu helfen. Lehne die Einladung ab.

![img](assets/08.webp)

# Deine erste Wallet
Du kannst nun deine erste Wallet erstellen. Tippe auf `Set Up Mobile Wallet`.

![img](assets/09.webp)

Der Prozess zur Erstellung der Wallet beginnt.

![img](assets/10.webp)

Er endet nach wenigen Sekunden. Deine Wallet ist bereit; tippe auf `Continue`, um sie zu verwenden.

![img](assets/11.webp)

Die Wallet öffnet sich im Bildschirm `Home`. Schau ihn dir kurz an, konzentriere dich aber sofort auf das untere Menü `Security`.

# Deine Schlüssel, deine Coins

![img](assets/12.webp)

In diesem Menü wirst du aufgefordert, deine Wallet zu sichern. Dabei wird die Folge von 12 Wörtern angezeigt, die du später zur Wiederherstellung brauchst. Diese 12 Wörter sind deine Wallet: **stelle sicher, dass du dich in einer sicheren Umgebung ohne neugierige Blicke befindest und ein Notizbuch oder Blatt zum Abschreiben hast, bevor du sie an einem sicheren Ort verwahrst** (zum Beispiel in einem Safe). Tippe auf `Back Up Now` und sieh dir die 12 Wörter an.

**Notiere auch die genaue Reihenfolge der Wörter: 1, 2, 3 usw.; schreibe die Wörter zur besseren späteren Lesbarkeit in Großbuchstaben, aber denke daran, dass du sie bei einer manuellen Eingabe später klein schreiben musst**.

![img](assets/13.webp)

Nachdem du die Wörter abgeschrieben und sicher verwahrt hast, fahre mit dem starter kit fort. Alle weiteren Einstellungen findest du am Ende der Anleitung.

# TRANSACT-Menü
Die Wallet zu verwenden ist äußerst einfach:
- gehe in das Menü `Transact`
- es gibt zwei Hauptbefehle: `Send` und `Receive` (**ignoriere `Buy`**).

![img](assets/17.webp)

Wenn du Transaktionen hast, erscheinen sie im Bereich unter den Befehlen. Da du noch keine Gelder hast, kannst du `Receive` wählen, um erste Gelder zu erhalten.

Es erscheint eine Reihe von *Assets*, aber konzentriere dich nur auf Bitcoin. Du kannst zwischen Bitcoin onchain (orangefarbenes Icon) und Liquid (blaues Icon) wählen. Liquid ermöglicht Sofortzahlungen ähnlich wie Lightning Network, aber über einen Mechanismus, den wir später sehen werden.

Wähle zunächst Bitcoin Onchain, das orangefarbene Icon.

![img](assets/18.webp)

Es erscheint ein QR-Code, der eine deiner Bitcoin-Adressen darstellt; unten siehst du sie auch mit `bc1q` und weiteren Zeichen. Du kannst den QR-Code einer Person zeigen, die dich bezahlen soll, um deine ersten Gelder zu erhalten, vernünftigerweise kleine Bruchteile von Bitcoin, auch `Satoshi` genannt.

![img](assets/19.webp)

Wenn du stattdessen zurückgehst und Liquid auswählst, zeigt das Menü ⚡️**Lightning Ready**. Du solltest wissen, dass Blockstream App über einen `SWAP`-Dienst fast sofortige Zahlungen empfangen, Lightning Network-Zahlungsanforderungen ausstellen oder LN-Rechnungen bezahlen kann, indem Gelder von einem Liquid-Konto derselben Wallet ein- oder ausgezahlt werden.

![img](assets/20.webp)

Im Menü, das sich danach öffnet, wähle, wie du Gelder empfangen willst: Liquid oder Lightning. Bei Liquid wird ein QR-Code ähnlich wie bei Bitcoin Onchain angezeigt; er steht für eine Adresse mit dem Präfix `lq1q` und weiteren Zeichen.

Wenn du Lightning wählst, wirst du aufgefordert, den gewünschten Empfangsbetrag einzugeben und mit `Confirm` zu bestätigen.

![img](assets/21.webp)

Blockstream App zeigt dir einen QR-Code für die LN-Rechnung, die mit jeder Lightning Network Wallet bezahlt werden kann.

![img](assets/22.webp)

---
⚠️ In unserer Simulation wollten wir 210 sats empfangen, aber der erzeugte QR-Code weist darauf hin, dass wir 160 sats erhalten. Swaps haben tatsächlich Kosten, ungefähr 50 satoshis pro empfangener Zahlung. **Das ist besonders bei Mikrozahlungen wichtig**. Für den Zahler ändert sich nichts: Er sieht den Betrag, der bei der Einrichtung angefordert wurde, nämlich 210 satoshis.

---

# Bist du Händler? Nutze den POS
Um diese Anleitung zu einem echten **starter kit** zu machen, können wir Bitcoin-Einnahmen auf dieser Wallet mit einem externen POS kombinieren.

Du kannst ihn in wenigen Schritten direkt unter https://btcpos.cash/ konfigurieren.

![img](assets/23.webp)

So kannst du Lightning-Zahlungen direkt auf deine mit Blockstream App erstellte Wallet empfangen, den Link mit Mitarbeitenden teilen und dafür nur die nächsten Schritte befolgen, um einen Link zu erstellen, den du auf dem Startbildschirm deines Telefons griffbereit hältst. Du musst den `Descriptor` deiner Wallet kopieren und in das große mittlere Feld auf der Website einfügen.

# 1. Erste Gelder im Liquid-Netzwerk empfangen
Die Anzeige der *Assets* auf dem Startbildschirm deiner Wallet muss aktiviert sein. Wenn sie gerade erstellt wurde, musst du eine LN-Rechnung bezahlt bekommen oder Gelder auf einer Liquid-Adresse empfangen.

Nach dem Empfang kannst du Liquid unter den `Assets` im Menü `Home` auswählen.

![img](assets/24.webp)

# 2. Notwendige Parameter aufrufen
Jetzt hast du, was du brauchst, um die Parameter aufzurufen, mit denen du deine Wallet zum POS „transportierst“. Technisch heißt das *Export des öffentlichen Schlüssels*; die Details lernst du durch vertieftes Studium. Für den Moment genügt es, oben rechts das Menü zu wählen:

![img](assets/25.webp)

Und im Dropdown-Menü `Watch-only` zu wählen.
![img](assets/26.webp)

`Output Descriptors` erscheint, genau der Parameter, den wir suchen. Kopiere ihn mit dem passenden Befehl und kehre zur Webseite zurück, auf der du den POS konfigurierst.

![img](assets/27.webp)

# 3. POS konfigurieren
Füge den descriptor in das passende Feld ein und klicke auf `GENERATE POS LINK`. Das System erstellt eine eindeutige URL, gültig nur für dich und deine Wallet.

![img](assets/28.webp)

Du kannst auch zuerst die Referenzwährung festlegen und im Dropdown-Menü bei `Currency` zwischen USD, CHF und EUR wählen.
![img](assets/29.webp)

# 4. Zahlung mit dem POS anfordern und einnehmen
Nachdem du auf `GENERATE POS LINK` geklickt hast, zeigt die Seite das Ergebnis: **der Link wurde erfolgreich erstellt**. Du kannst ihn kopieren, denn der Link bleibt unter der erzeugten URL immer **nur für deine Wallet** erreichbar.

![img](assets/30.webp)

Du kannst den POS auch öffnen und verwenden:
![img](assets/31.webp)

Angenommen, du möchtest eine Rechnung über 3.351 sats mit Beschreibung erzeugen.

![img](assets/32.webp)

Mit `CREATE INVOICE` zeigt der POS den QR-Code oder die Textrechnung, die du einem möglichen Kunden vorlegst.

![img](assets/33.webp)

Wenn der Kunde die Rechnung bezahlt hat, auf der er die *description* korrekt liest (hier Coppa del Nonno), meldet der POS den Zahlungseingang.

![img](assets/34.webp)

Das ist auch in der Wallet korrekt sichtbar.
![img](assets/35.webp)

Jetzt musst du dir nur den POS-Link merken und ihn griffbereit halten, um ihn bei Bedarf auch auf dem Telefon zu nutzen, auf dem die Wallet installiert ist.

![img](assets/36.webp)

Als Link/App zum Startbildschirm hinzufügen

![img](assets/37.webp)

# ⚠️ WICHTIGER HINWEIS
Wenn du die gerade ausgeführten Schritte zur Rechnungseinziehung im letzten Beispiel noch einmal liest, fallen zwei wichtige Dinge auf:
1. dem Kunden wurde eine Rechnung über 3.351 sats angezeigt
2. unsere Wallet hat 3.293 sats erhalten.

Bevor man sich empört, muss man zum Startbildschirm des POS zurückgehen, der den Text im folgenden Bild zeigt:

![img](assets/38.webp)

Die Differenz zwischen 3.351 (Rechnung an den Kunden) und 3.293 (dein Eingang) erklärt sich so:
- 50 sats für jede erzeugte Rechnung
- 0,25 % Servicegebühr (8 sats = 0,25 % von 3.351)
- Insgesamt erhalten: 3.293

#### Du fängst gerade erst an und dies ist ein starter kit. Eine kleine Gebühr ist der Kompromiss, um Bitcoin in self-custody ohne Vermittler zu nutzen und alle Möglichkeiten einschließlich kleiner Sofortzahlungen zu verwenden.

#### Durch Lernen wirst du andere Werkzeuge verwenden, die keine zusätzlichen Gebühren außer den auch für erfahrene Nutzer üblichen erfordern.

---
# Weitere Einstellungen

Es ist Zeit, deine erste Wallet gut kennenzulernen. Einstellungen sind wichtig, weil sie dir im Alltag helfen.

## Menü
Die Menüs der Blockstream App befinden sich unten und heißen:
- Home
- Transact
- Security
- Settings

Fahre mit der Konfiguration deiner Wallet im Menü `Security` fort. Neben der Möglichkeit, die Wörter der `Recovery phrase` anzusehen und abzuschreiben, stellt dieses Menü weitere wichtige Funktionen bereit.

Du kannst zum Beispiel den Login zur Wallet per biometrischer Kontrolle einrichten (wenn auf deinem Telefon aktiviert) oder eine sechsstellige PIN für den Zugriff hinzufügen. Diese Optionen sind sehr wichtig, weil sie verhindern, dass Fremde deine Wallet öffnen und ansehen, falls sie dein Telefon in der Hand haben.

![img](assets/14.webp)

In diesem Menü kannst du auch die *Logout*-Zeit festlegen, also wann die Wallet nach einigen Minuten Inaktivität getrennt wird. Standardmäßig steht sie auf *5 minutes*; du kannst sie je nach Bedarf länger oder kürzer einstellen.
![img](assets/15.webp)
# SETTINGS-Menü
Ein sehr wichtiges Menü, denn es enthält alle Wallet-Einstellungen. Hier kannst du zum Beispiel die Wallet umbenennen: In unserem Beispiel heißt sie *Starter Kit*. Wallets umzubenennen ist wichtig, wenn du mehrere auf demselben Gerät nutzt und verstehen/auswählen musst, welche du verwenden willst.

![img](assets/39.webp)

Im Untermenü `Denomination` findest du sehr nützliche Einstellungen zur Währung.
![img](assets/40.webp)

Ich empfehle `satoshi/sats` als Einheit für Bitcoin-Beträge. Der Satoshi ist die kleinste Einheit von BTC, ein Hundertmillionstel Bitcoin. Außerdem erscheint die Auswahl der Referenzbörse für die Umrechnung. Verwende eine, mit der du Beträge in EUR anzeigen und festlegen kannst.

![img](assets/41.webp)

Schließlich kannst du im Menü `Settings` die aktuell verwendete Version von Blockstream App prüfen, sehen, ob ein Update nötig ist, und direkt *in-app* Support anfordern.
![img](assets/42.webp)

# HOME-Menü
`Home` in Blockstream App ist das Menü, in dem deine Wallet bei jedem neuen Zugriff geöffnet wird. Wenn du nach unten scrollst, findest du die Option, Bitcoin über eine integrierte Exchange zu kaufen. **Verwende sie nicht**.

![img](assets/16.webp)

# Wiederherstellung der Wallet
Wenn du während der Nutzung feststellst, dass du das Telefon wechseln oder die *Starter Kit* Wallet auf mehreren Geräten verwenden musst, kannst du das mit Blockstream App tun.

Dazu musst du nur das unten erklärte Wiederherstellungsverfahren lernen, einschließlich der Schritte für den Fall, dass du den Zugriff auf das Telefon verlierst, auf dem du die Wallet zuerst verwendet hast.

Deine Gelder sind nämlich nicht „auf dem Gerät“ oder „in der Wallet“. Die Gelder liegen im Bitcoin-Netzwerk, egal ob Onchain, Lightning oder Liquid. Die Wallet, genauer die öffentlichen und privaten Schlüssel deiner Wallet, ist das Werkzeug, um auf die genutzten Adressen und damit auf den zugehörigen Kontostand zuzugreifen.

Für dieses Verfahren hast du die 12 Wörter abgeschrieben und sicher verwahrt... **Hast du das getan, richtig?** Denn ohne diese Wörter hast du keinen Zugriff mehr auf deine Gelder.

# a. Neue Installation von Blockstream App
Installiere zuerst Blockstream App erneut mit dem am Anfang gezeigten Verfahren. Inzwischen kann eine neue release erschienen sein; verwende die aktuellste.

Starte Blockstream App auf dem neuen Gerät, tippe auf `Get Started` und lehne die Datenerhebung ab.

# b. Aus Backup wiederherstellen
Hier enden die Ähnlichkeiten mit der ersten Installation. Wenn der Bildschirm zur Wallet-Erstellung erscheint, wähle statt `Set Up Mobile Wallet` wie beim ersten Mal `Restore from backup`.

![img](assets/43.webp)

Wenn du das Hauptnetz von Bitcoin nutzt, also das mit echten Geldern, wähle im nächsten Bildschirm `Mainnet`.

![img](assets/43.webp)

Es erscheint der Bildschirm mit den Feldern für die Wörter der `Recovery phrase`. Schreibe sie in der richtigen Reihenfolge korrekt ein und wähle dann `Continue`, um die Wallet auf dem neuen Gerät neu zu erstellen.

![img](assets/45.webp)

Die Wiederherstellung kann einige Minuten dauern; warte geduldig, bis sie erfolgreich abgeschlossen ist. Am Ende findest du deine Wallet mit Kontostand und Transaktionshistorie wieder.

![img](assets/46.webp)

---
⚠️ Die auf dem neuen Gerät wiederhergestellte Wallet ist zu 100 % aktiv. Das bedeutet, dass sie auch die privaten Schlüssel zum Ausgeben besitzt. Bedenke das, falls du sie einem Mitarbeitenden für dein Geschäft überlassen möchtest.

**Nutze für Mitarbeitende lieber den POS-Link, denn er wurde nur mit dem öffentlichen Schlüssel (dem `descriptor`) erstellt**.

---

# Wie weiterlernen?

![img](assets/47.webp)
![img](assets/48.webp)
