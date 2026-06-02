---
layout: default
title: "Mnemonics & Dice: Lerne, deine Mnemonic zu erstellen"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only-Lektion</span> <span>Dieses Projekt wird von valerio-vaccaro gepflegt</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Mnemonics & Dice: Lerne, deine Mnemonic zu erstellen

## Einführung
Das Erstellen der Mnemonic mit einer eigenen Entropiequelle reduziert die Angriffsfläche einer Bitcoin-Wallet; dennoch müssen einige Faktoren berücksichtigt werden:

- der Prozess muss so einfach und schnell wie möglich sein, ohne Schnörkel oder unnötige Wiederholungen,
- die Entropie sollte nicht auf unnötige Geräte kopiert werden, und die Notwendigkeit von Berechnungen oder Verarbeitung sollte auf ein Minimum beschränkt bleiben,
- die Verwendung von Software/Skripten/Programmen sollte vermieden werden, sofern du nicht eine genaue Codeprüfung und eine Prüfung aller Abhängigkeiten durchgeführt hast,
- unterschiedliche Setups können leicht unterschiedliche Prozesse erfordern.

## Erstellung der Wörter
Der erste Schritt ist die Berechnung der 12 oder 24 Wörter der Mnemonic; 12 Wörter sind normalerweise mehr als ausreichend für die Sicherheit einer Bitcoin-Wallet.

Für die Worterzeugung kannst du die in [TRGM](https://github.com/valerio-vaccaro/TRMG) beschriebene Methode verwenden, mit 3 Würfeln, von denen 1 Würfel 8 Seiten und 2 Würfel 16 Seiten haben. JEDER Würfelwurf entspricht EINEM UND NUR EINEM Wort; um es zu finden, musst du lediglich die Tabelle der Website durchsuchen und die Entsprechung der Würfel zum ausgeführten Wurf finden (der erste Würfel ist IMMER der mit 8 Seiten). Die Wortspalte enthält das gesuchte Wort.

Empfohlen wird, alle 12 oder 24 Wörter zu erzeugen und gegebenenfalls das letzte zu korrigieren oder in jedem Fall die Würfel zu verwenden, um die Entropie für das letzte Wort zu erzeugen.

## Berechnung des Checksum
Das letzte Wort wird nicht vollständig von uns festgelegt, sondern enthält einen Kontrollteil; das heißt, wir können nicht alle 11 Entropiebits, aus denen es besteht, vollständig wählen. Stattdessen können wir bei einer Mnemonic mit 12 Wörtern die ersten 7 oder bei einer Mnemonic mit 24 Wörtern die ersten 3 wählen.

Nehmen wir an, unser letztes Wort ist BACON, entsprechend den Würfen 1, 9 und 11 (denk daran, dass der erste Würfel IMMER der mit 8 Seiten ist). Die Tabelle enthält auch Group 12 und Group 24, mit denen wir Wörter gruppieren können, indem nur die Entropie der ersten beiden Würfe (group 12) oder nur des ersten Wurfs (group 24) berücksichtigt wird.

Nehmen wir an, wir möchten eine Mnemonic mit 12 Wörtern erstellen; das bedeutet, dass der checksum eines der 16 möglichen Wörter sein wird, die dieselbe group 12 wie bacon haben, also 0001000. Die möglichen Wörter sind:

|First|Second|Third|Index|Word	|Index in binary|Group 12	|Group 24|
|---|---|---|-------|-----------|---------------|-----------|---|
|1  |9	|1	|128	|avoid	    |00010000000	|0001000	|000|
|1  |9	|2	|129	|awake	    |00010000001	|0001000	|000|
|1  |9	|3	|130	|aware	    |00010000010	|0001000	|000|
|1  |9	|4	|131	|away	    |00010000011	|0001000	|000|
|1  |9	|5	|132	|awesome	|00010000100	|0001000	|000|
|1  |9	|6	|133	|awful	    |00010000101	|0001000	|000|
|1  |9	|7	|134	|awkward	|00010000110	|0001000	|000|
|1  |9	|8	|135	|axis	    |00010000111	|0001000	|000|
|1  |9	|9	|136	|baby	    |00010001000	|0001000	|000|
|1  |9	|10	|137	|bachelor	|00010001001	|0001000	|000|
|1  |9	|11	|138	|bacon	    |00010001010	|0001000	|000|
|1  |9	|12	|139	|badge	    |00010001011	|0001000	|000|
|1  |9	|13	|140	|bag    	|00010001100	|0001000	|000|
|1  |9	|14	|141	|balance	|00010001101	|0001000	|000|
|1  |9	|15	|142	|balcony	|00010001110	|0001000	|000|
|1  |9	|16	|143	|ball   	|00010001111	|0001000	|000|

Wie findet man unter den verschiedenen Möglichkeiten das einzige richtige Wort? Das hängt von deinem Setup ab; sehen wir uns einige Beispiele an:

- bruteforce, also alle nacheinander ausprobieren, bis das richtige gefunden ist (bei Mnemonics mit 24 Wörtern sehr mühsam); dies ist die Methode für Ledger oder Electrum (dabei sicherstellen, dass die BIP39-Option ausgewählt ist),
- alle möglichen Wörter mit den ersten 11 oder 23 Wörtern berechnen und nach dem einzigen suchen, das in dieser Menge liegt; diese Methode ist mit Jade und mit anderen hardware wallets nutzbar, die alle möglichen letzten Wörter einer Mnemonic berechnen können,
- die vollständige Mnemonic eingeben und die hardware wallet sie für uns korrigieren lassen, wie es Specter-DIY zum Beispiel sehr elegant macht.

## Backup (Thema einer anderen Lektion)
Eine gute Backup-Strategie ist grundlegend, daher:
- mehrere Backups,
- auf mehreren Medien und
- möglichst verschlüsselt oder aufgeteilt (aber man muss wissen, wie man es richtig macht).

## Bibliographie

- [TRMG](https://github.com/valerio-vaccaro/TRMG)

## Wiederholungen
Diese Lektion ist wiederkehrend und wird jeden Monat wiederholt. Unten steht eine Liste der bereits durchgeführten Wiederholungen.

| Date        | Notes                                          |
|-------------|------------------------------------------------|
| 240102-2100 | First lesson                                   |
