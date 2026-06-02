---
layout: default
title: "Einführung in **Mesh Networks** und detaillierte Analyse von LoRa und **LoRaWAN**"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only-Lektion</span> <span>Dieses Projekt wird von valerio-vaccaro gepflegt</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Einführung in **Mesh Networks** und detaillierte Analyse von LoRa und **LoRaWAN**

## Einführung in **Mesh Networks**

**Mesh Networks** sind eine Netzwerkarchitektur, bei der Knoten (Geräte) nicht hierarchisch miteinander verbunden sind. Dadurch kann jeder Knoten direkt mit anderen kommunizieren, ohne einen zentralen Punkt wie einen router oder gateway zu durchlaufen. Jeder Knoten kann potenziell sowohl als Sender als auch als Empfänger dienen, und Daten können über mehrere Pfade weitergeleitet werden, um das Ziel zu erreichen.

Diese Struktur bietet mehrere Vorteile:

- **Resilienz**: Fällt ein Knoten aus, können Daten über andere Knoten umgeleitet werden, wodurch die Kommunikationskontinuität gesichert bleibt.
- **Skalierbarkeit**: **Mesh Networks** können durch Hinzufügen neuer Knoten leicht erweitert werden, ohne erhebliche Änderungen an der Infrastruktur.
- **Erweiterte Abdeckung**: Datenweiterleitung ermöglicht die Abdeckung größerer Gebiete im Vergleich zu traditionellen Netzwerken.
- **Flexibilität**: Geeignet für viele Anwendungen, vom Internet of Things (IoT) bis zu Heim- und Industrienetzwerken.

Allerdings bringen **Mesh Networks** auch einige Herausforderungen mit sich:

- **Komplexität**: Die Verwaltung mehrerer Pfade und die Koordination zwischen Knoten erhöhen die Komplexität.
- **Energieverbrauch**: Knoten, die Daten weiterleiten, verbrauchen mehr Energie, was die Batterielaufzeit reduziert.
- **Begrenzte Kapazität**: In dichten Netzwerken kann multi-hop-Übertragung Latenz einführen und die Gesamtkapazität reduzieren.

**Mesh Networks** werden in drahtlosen Technologien wie **Zigbee**, **Bluetooth** Mesh, **Thread** und in einigen Fällen proprietären Protokollen auf Basis von LoRa verwendet. Eine der wichtigsten Technologien für stromsparende Langstreckennetze ist **LoRaWAN**, das im Vergleich zur traditionellen mesh-Topologie einen anderen Ansatz verfolgt.

## **LoRa** und **LoRaWAN**: Kontext und Unterschiede

### **LoRa**

**LoRa** (Long Range) ist eine Spread-Spectrum-Modulationstechnologie, die von der Chirp Spread Spectrum (CSS)-Technik abgeleitet ist und von Cycleo entwickelt wurde (2012 von Semtech übernommen).

**LoRa** stellt die physikalische Schicht (PHY) eines drahtlosen Netzwerks dar und definiert, wie Daten auf lizenzfreien Frequenzbändern moduliert und übertragen werden (z. B. 868 MHz in Europa, 915 MHz in Nordamerika, 433 MHz in einigen Regionen).

Die wichtigsten Eigenschaften sind:
- Übertragung über große Entfernungen (bis zu 15 km in ländlichen Gebieten, 2-5 km in städtischen Gebieten).
- Extrem niedriger Energieverbrauch, ideal für IoT-Anwendungen mit niedrigen Datenraten und langer Batterielaufzeit.

### **LoRaWAN**

**LoRaWAN** (Long Range Wide Area Network) ist ein auf LoRa basierendes MAC (Media Access Control)-Schichtprotokoll, entwickelt von der LoRa Alliance, einer 2015 gegründeten gemeinnützigen Vereinigung mit über 500 Mitgliedern, darunter Semtech, Cisco, IBM und Orange.

**LoRaWAN** definiert:
- Netzwerkarchitektur.
- Kommunikationsprotokoll.
- Aspekte wie Übertragungsfrequenz, Datenrate, Sicherheit und Interoperabilität.

Im Gegensatz zu LoRa, das nur die Signalmodulation behandelt, legt **LoRaWAN** fest, wie Geräte (Endknoten) mit gateways kommunizieren und wie diese über backhaul-Verbindungen (z. B. Ethernet, Wi-Fi oder cellular) mit Netzwerkservern verbunden werden.

#### Vergleich zwischen **Mesh Networks** und **LoRaWAN**

Im Gegensatz zu traditionellen **Mesh Networks** (z. B. **Zigbee**, **Bluetooth**) verwendet **LoRaWAN** eine Sterntopologie, bei der Endknoten direkt mit gateways kommunizieren, die Daten an einen zentralen Netzwerkserver weiterleiten. Unten folgt ein detaillierter Vergleich:

1. Netzwerktopologie
**Mesh Networks**: Knoten agieren als Repeater und leiten Daten weiter, um die Abdeckung zu erweitern. Dies erhöht Komplexität und Energieverbrauch.
**LoRaWAN**: Sterntopologie, bei der Knoten direkt an gateways senden. Dadurch entfallen Repeater-Knoten, das Netzwerk wird vereinfacht und der Energieverbrauch sinkt.

2. Energieverbrauch
**Mesh Networks**: Repeater-Knoten verbrauchen mehr Energie, wodurch die Batterielaufzeit reduziert wird.
**LoRaWAN**: Endgeräte senden nur bei Bedarf (z. B. Class A mit ALOHA), wodurch Batterielaufzeiten von bis zu 10-15 Jahren möglich sind.

3. Reichweite und Abdeckung
**Mesh Networks**: Die Reichweite wird über multi-hop erweitert, aber jeder Hop kann Latenz einführen und die Effizienz verringern.
**LoRaWAN**: Dank CSS-Modulation bietet es eine Reichweite von bis zu 15 km (ländlich) oder 2-5 km (städtisch) ohne Repeater-Knoten.

4. Kapazität und Skalierbarkeit
**Mesh Networks**: In dichten Netzwerken kann multi-hop Engpässe verursachen und die Kapazität verringern.
**LoRaWAN**: Unterstützt Millionen von Nachrichten von Tausenden Geräten, dank gateway-Redundanz und Sterntopologie.

5. Sicherheit
**Mesh Networks**: Sicherheit hängt vom Protokoll ab (z. B. verwendet **Zigbee** AES-128). Multi-hop-Weiterleitung kann Schwachstellen einführen.
**LoRaWAN**: End-to-end-Verschlüsselung mit AES-128-Sitzungsschlüsseln (Network Session Key und Application Session Key).

6. Komplexität und Kosten
**Mesh Networks**: Die Verwaltung von Weiterleitungspfaden erhöht die Komplexität. Kosten können mit zusätzlichen Repeater-Knoten steigen.
**LoRaWAN**: Die Sterntopologie ist einfacher. Gateways können teuer sein, aber Sensoren sind günstig und lizenzfreie ISM-Bänder reduzieren Kosten.

## Detaillierte Analyse von **LoRa** und **LoRaWAN**
### **LoRa**: physikalische Schicht
**LoRa** verwendet Chirp Spread Spectrum (CSS)-Modulation, die Daten mit sinusförmigen Signalen variierender Frequenz codiert und das Signal über eine größere Bandbreite verteilt, um die Störfestigkeit zu verbessern. Sie bietet hohe Empfindlichkeit (-110 dBm bis -140 dBm), ideal für rauschreiche Umgebungen.

Zu den Hauptparametern gehören:

- Spreading Factor (SF): von 7 bis 12, beeinflusst Datenrate und Reichweite. SF12 bietet große Reichweite, aber niedrigen bitrate (0.3 kbps); SF7 bietet höhere Geschwindigkeiten (27 kbps), aber geringere Reichweite.
- Bandwidth (BW): 125 kHz, 250 kHz oder 500 kHz, beeinflusst bitrate und Robustheit.
- ISM-Frequenzen: 863-870 MHz (Europa), 902-928 MHz (Nordamerika), 433 MHz (andere Regionen).

LoRa ist ideal für IoT-Anwendungen mit kleinen Datenpaketen, etwa Umweltüberwachung, smart metering und Präzisionslandwirtschaft.

## **LoRaWAN**: Protokoll und Architektur

**LoRaWAN** definiert drei Geräteklassen:

- Class A: bidirektionale Niedrigenergiegeräte mit uplink-Übertragungen und kurzen downlink-Empfangsfenstern (ALOHA). Ideal für batteriebetriebene Sensoren.
- Class B: ergänzt geplante Empfangsfenster (alle 128 Sekunden, synchronisiert über GPS beacon) für geplante downlinks.
- Class C: Geräte, die ständig auf downlinks hören, geeignet für netzbetriebene Geräte.

Die **LoRaWAN**-Architektur umfasst:
- Endknoten (End Devices): Sensoren oder IoT-Geräte, die Daten sammeln und übertragen.
- Gateways: Empfangen Daten von Knoten und leiten sie über backhaul an den Netzwerkserver weiter.
- Network Server: Verwaltet das Netzwerk, entfernt Duplikate und wählt das gateway für downlinks aus.
- Application Server: Verarbeitet Daten zur Analyse oder Visualisierung.

## **Mesh Networks** mit LoRa
Obwohl **LoRaWAN** eine Sterntopologie verwendet, ist es möglich, ein mesh-Netzwerk mit LoRa-Modulation und einem externen Protokoll umzusetzen. In einem LoRa-mesh-Netzwerk agieren Knoten als Repeater, um die Abdeckung zu erweitern, was in Gebieten ohne gateways nützlich ist.

Dies erfordert jedoch:
- Benutzerdefiniertes Protokoll: **LoRaWAN** unterstützt mesh nicht nativ.
- Höheren Energieverbrauch: Repeater-Knoten verbrauchen mehr Energie.
- Komplexität: Verwaltung von Weiterleitungspfaden und Kollisionsvermeidung (z. B. CSMA-CA).

Beispiel: LoRa-Module (z. B. Semtechs SX1276) mit Mikrocontrollern wie ESP32 für private **Mesh Networks**.

Vorteile von **LoRaWAN**

- Energieeffizienz: Sterntopologie eliminiert Repeater-Knoten.
- Einfachheit: Direkte Kommunikation mit gateways.
- Skalierbarkeit: Unterstützt Tausende Geräte und Millionen Nachrichten.
- Sicherheit: Robuste Sicherheit mit AES-128-Verschlüsselung.
- Interoperabilität: Offener Standard der LoRa Alliance.

Grenzen von **LoRaWAN**

- Niedrige Datenrate: 0.3-50 kbps, nicht geeignet für umfangreiche Daten.
- Latenz: Class A führt Verzögerungen für downlinks ein.
- Gateway-Kosten: erheblich für private Netzwerke.

# Fazit
**Mesh Networks** bieten Resilienz und Flexibilität durch multi-hop-Weiterleitung, sind aber komplex und verbrauchen mehr Energie. **LoRaWAN** ist mit seiner Sterntopologie und LoRa-Modulation ideal für stromsparende, weitreichende IoT-Anwendungen, dank Einfachheit, Skalierbarkeit und Batterielaufzeiten von bis zu 15 Jahren.

Die Wahl zwischen **Mesh Networks** und **LoRaWAN** hängt von den Anforderungen ab: mesh für Umgebungen mit nahe beieinander liegenden Knoten, **LoRaWAN** für Langstreckenkommunikation mit minimalem Verbrauch. Obwohl mesh mit LoRa möglich ist, ist es im Vergleich zu **LoRaWAN** weniger verbreitet; **LoRaWAN** dominiert dank Standardisierung und Unterstützung durch die LoRa Alliance.
