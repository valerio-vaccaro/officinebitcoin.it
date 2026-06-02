---
layout: default
title: "Einführung in das Mining"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only-Lektion</span> <span>Dieses Projekt wird von valerio-vaccaro gepflegt</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Einführung in das Mining
Bitcoin-Mining ist ein grundlegender Prozess des Protokolls, der dazu dient, eine Reihenfolge der in der mempool vorhandenen Transaktionen vorzuschlagen, eine Teilmenge auszuwählen, um einen neuen Block zu erstellen, und den Zustand der Blockchain zu aktualisieren.

Mining ist darauf ausgelegt, dezentral und zufällig zu sein (in Anführungszeichen, da es auf einem kryptografischen Rätsel basiert) und so eine zentrale Transaktionsverwaltung zu vermeiden.

## Zweck des Minings
Mining löst Probleme im Zusammenhang mit Zentralisierung, zum Beispiel:

- Zensur: Eine zentrale Stelle könnte einige Transaktionen blockieren, aber mit dezentralen Minern haben Transaktionen bessere Chancen, aufgenommen zu werden.
- Double Spending: Ohne einen korrumpierbaren Miner ist es schwierig, die Geschichte umzuschreiben oder eine Transaktion auf Kosten einer anderen zu bevorzugen.
- Timestamping: Es stellt eine sichere und gemeinsame zeitliche Ordnung bereit, die nicht von einer zentralen Autorität abhängt, sondern vom Konsens zwischen Minern und Nodes.

# Wie Mining funktioniert
Der Mining-Prozess lässt sich Schritt für Schritt erklären:

- Transaktionsauswahl: Der Miner wählt Transaktionen aus der mempool aus und bevorzugt oft jene mit höheren Gebühren, um den Gewinn zu optimieren (ein NP-complete-Problem ähnlich dem "knapsack problem").
- Coinbase-Konstruktion: Der Miner erstellt eine spezielle Transaktion (coinbase), die ihm selbst die Blockbelohnung (derzeit 3.125 BTC, alle vier Jahre halbiert) plus die Gebühren der ausgewählten Transaktionen zuweist.
- Merkle Root: Die ausgewählten Transaktionen werden in einer Baumdatenstruktur (Merkle Tree) organisiert, die eine Merkle Root erzeugt, einen Hash, der alle Transaktionen und ihre Reihenfolge repräsentiert.
- Block Header: Der Miner baut den Prototyp des Block-Headers, einschließlich:
1. Des timestamp.
2. Des Hashes des vorherigen Blocks.
3. Der Merkle Root.
4. Der Schwierigkeit (target), die vom Netzwerk abhängt.
5. Eines nonce (Zufallszahl, zum Beispiel mit null initialisiert).
- Kryptografisches Rätsel: Der Miner wendet den SHA-256-Algorithmus zweimal auf den Header an und prüft, ob das Ergebnis eine ausreichende Anzahl führender Nullen hat (unterhalb der Schwierigkeitsschwelle). Falls nicht, verändert er den nonce oder andere Felder (z. B. timestamp oder Transaktionsreihenfolge) und wiederholt die Berechnung. Das ist Brute-Force-Arbeit ohne Abkürzungen, dank der Eigenschaften von SHA-256.

## Optimierungen
Um den Prozess zu beschleunigen, können Miner den ersten SHA-256 über die ersten 64 Bytes des Headers berechnen (unveränderlich) und danach nur über den Rest iterieren, indem sie den nonce ändern. Die Spezialisierung hat zu Hardware (ASIC) geführt, die Milliarden von Versuchen pro Sekunde ausführt.

# Validierungsprozess
Wenn ein Miner eine Lösung findet, überträgt er den vollständigen Block (Header + Transaktionen) an das Netzwerk. Nodes validieren:
- den Header-Hash (ein einzelner SHA-256 zur Bestätigung).
- die Korrektheit der Blockinformationen (timestamp, Hash des vorherigen Blocks, Merkle Root und nonce).
- die Reproduzierbarkeit der Merkle Root nach Prüfung der Korrektheit aller zugehörigen Transaktionen.

Wenn der Block gültig ist, wird er der Blockchain hinzugefügt. Die Belohnung (coinbase + Gebühren) kann erst nach 100 Bestätigungen (etwa 16 Stunden) ausgegeben werden, um Stabilität zu gewährleisten.

# Mining-Kosten und Belohnungen
Kosten:

- Strom: wichtigste variable Kosten.
- Hardware: teure und kurzlebige ASICs, die schnell von effizienteren Modellen überholt werden.
- Infrastruktur: Kühlung, Installation, Wartung (z. B. sind Solarpaneele nicht "kostenlos").

Belohnungen:

- Feste Belohnung (2024 auf 3.125 BTC halbiert).
- Variable Transaktionsgebühren.

Der Miner muss die Konsensregeln einhalten: Ein ungültiger Block wird verworfen, wodurch Ressourcen ohne Belohnung verschwendet werden. Selbst ein gültiger Block kann "verwaisen", wenn ein anderer Miner das Rennen gewinnt, was Verluste verursacht.

## Wirtschaftliche Strategie
Mining ist wettbewerbsintensiv: Miner versuchen, die Betriebszeit zu maximieren, um Fixkosten zu amortisieren. Punktuelle Nutzung (z. B. Miner nur bei überschüssiger Energie einzuschalten) ist unpraktisch, da die Anfangskosten Kontinuität erfordern. Die Kapitalrendite kann langwierig und unsicher sein.

# Solo- und Pool-Mining

- Solo Mining: Der Miner arbeitet allein und baut den Block mit einem Full Node oder eigener Software. Wenn er einen Block findet, erhält er die gesamte Belohnung, aber die Wahrscheinlichkeit ist extrem niedrig (mit einem einzelnen ASIC könnte es Jahrhunderte dauern).
- Pool Mining: Protokolle wie Stratum ermöglichen Minern die Zusammenarbeit:
1. Der Pool liefert eine Vorlage (coinbase, Merkle Root usw.).
2. Miner senden shares (Versuche mit einer bestimmten Anzahl von Nullen, unterhalb der Blockschwierigkeit) als Arbeitsnachweis.
3. Wenn ein Pool-Miner einen Block findet, wird die Belohnung proportional zu den gesendeten shares aufgeteilt.
- Stratum v2: Weiterentwicklung, die es Minern erlaubt, Transaktionen auszuwählen, wodurch die Zentralisierung des Pools reduziert wird, obwohl Prüfungen erforderlich sind, um die Korrektheit sicherzustellen (z. B. Gebühren für den Pool).

# Hashrate-Schätzung
Die Hashrate (Rechenleistung) wird geschätzt:
- In einem Pool: durch Zählen der in einer Zeiteinheit empfangenen shares, multipliziert mit der Share-Schwierigkeit. Es ist eine Schätzung, die durch Glück beeinflusst werden kann.
- Global: anhand der Bitcoin-Schwierigkeit und der durchschnittlichen Zeit zwischen Blöcken (etwa 10 Minuten). Schwankungen sind normal, aber der Durchschnitt ist zuverlässig.

Hardware wie Nerd Miner verwendet interne Zähler für präzise Daten, während Pools auf variablere Schätzungen angewiesen sind, die in schwankenden Diagrammen sichtbar werden.

# Programm
Diese Lektion wurde für einen Satoshi Spritz Connect erstellt.
