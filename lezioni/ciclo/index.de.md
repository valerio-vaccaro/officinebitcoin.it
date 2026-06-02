---
layout: default
title: "Der Lebenszyklus einer Bitcoin-Transaktion"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only-Lektion</span> <span>Dieses Projekt wird von valerio-vaccaro gepflegt</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Der Lebenszyklus einer Bitcoin-Transaktion

## Was ist eine Bitcoin-Transaktion
Eine Bitcoin-Transaktion ist eine in der Blockchain aufgezeichnete Aktion, die Wert von einer oder mehreren Eingaben (zuvor empfangenen Geldern, sogenannten UTXOs - Unspent Transaction Outputs) an eine oder mehrere Ausgaben (neue Empfänger) überträgt.
Eingaben sind Ausgaben früherer Transaktionen, die noch nicht ausgegeben wurden, während Ausgaben satoshis bestimmten Adressen zuweisen. Eine Ausnahme ist die "coinbase"-Transaktion, die erste Transaktion jedes Blocks; sie erzeugt neue bitcoins (Mining-Belohnung und Gebühren) ohne Eingaben. Wenn nicht alle Gelder einer Eingabe ausgegeben werden, geht die Differenz (change) über eine zusätzliche Ausgabe an den Absender zurück oder, wenn sie nicht verwaltet wird, für immer verloren.

## Phasen des Lebenszyklus
Dies ist der Lebenszyklus der Transaktion:

- Erstellung: Das Wallet erstellt die Transaktion, indem es auswählt, welche UTXOs ausgegeben werden sollen, ausgehend vom zu sendenden Betrag und von der Strategie zur Gebührenminimierung. Wenn die Eingabe die Ausgabe übersteigt, wird eine "change"-Ausgabe erzeugt, die an den Absender zurückgeht; dies erhöht jedoch die Transaktionsgröße und die Kosten. Einige Wallets versuchen, dies zu vermeiden.
- Signierung: Die Transaktion wird für jede Eingabe mit einer oder mehreren digitalen Signaturen signiert und dadurch authentifiziert. Dieser Schritt ist für die Gültigkeit entscheidend und kann bei multisig-Transaktionen mehrere Parteien einbeziehen.
- Übertragung: Die signierte Transaktion wird an das Netzwerk übertragen ("broadcast") und in den mempool des lokalen Nodes eingefügt. Der mempool validiert die Transaktion nach Konsensregeln (z. B. gültige Signaturen, verfügbare Gelder) und lokalen Regeln (z. B. maximale Größe von 400 KB zur Spam-Vermeidung). Danach verbreitet der Node sie an Peers, die sie validieren und in ihre mempools aufnehmen, wodurch eine kaskadierende Übertragung entsteht. Mempools unterscheiden sich zwischen Nodes aufgrund verschiedener Konfigurationen oder Verbindungen.
- Bestätigung: Ein Miner nimmt die Transaktion in einen Block auf und bestätigt sie damit auf der Blockchain. Solange sie jedoch keine weiteren Bestätigungen hat (nachfolgende Blöcke), bleibt sie anfällig für Ersetzungen oder forks. Eine Transaktion mit niedrigen Gebühren kann lange im mempool bleiben oder verworfen werden, könnte aber auch nach Monaten noch gemined werden, wenn die Eingaben unausgegeben bleiben.

## Problembehandlung
- Transaktion aus dem mempool verschwunden: Wenn eine Transaktion mit niedrigen Gebühren entfernt wird (z. B. wegen Verkehrsspitzen), kann sie mit der TXID manuell erneut übertragen werden (rebroadcast), auch mit scripts oder Explorern. Jemand könnte dies im Namen Dritter tun.
- Replace-by-Fee (RBF): Wenn die Gebühr nicht ausreicht, kann die Transaktion durch eine andere ersetzt werden, die mehr zahlt, sofern sie mit dem RBF-Flag markiert ist. Ein Vorschlag sieht vor, dass alle Transaktionen implizit ersetzbar sein sollten, da Miner ohnehin höhere Gebühren bevorzugen.
- Child Pays for Parent (CPFP): Wenn RBF nicht genutzt werden kann (z. B. weil es nicht die eigene Transaktion ist oder die Gelder aufgebraucht sind), wird eine Ausgabe der festhängenden Transaktion mit einer neuen Transaktion ausgegeben, die hohe Gebühren zahlt, wodurch beide für Miner attraktiv werden. Die Summe der Gebühren muss beide abdecken. Probleme entstehen, wenn Nodes die erste Transaktion verwerfen und damit die Kette unterbrechen; ein in Entwicklung befindliches Protokoll soll Transaktionspakete übertragen, um dies zu vermeiden.

## Endgültige Bestätigung
Eine Transaktion gilt erst mit mehreren Bestätigungen (Blöcken über ihr) als endgültig. Eine einzelne Bestätigung reicht nicht aus, da forks oder Double-Spending sie ungültig machen könnten. Das White Paper schlägt 6 Bestätigungen vor (etwa 60 Minuten, mit Blöcken im Durchschnitt alle 10 Minuten), aber die Zahl variiert je nach Betrag und Risiko. Die Varianz der Blockzeiten ist hoch, doch der Durchschnitt wird dank der Mining-Schwierigkeit aufrechterhalten.

## Fazit
Der Zyklus endet damit, dass die Transaktion in die Blockchain "eingraviert" ist und die Wertübertragung dauerhaft aufgezeichnet wird.

## Programm
Diese Lektion wurde für einen Satoshi Spritz Connect erstellt.
