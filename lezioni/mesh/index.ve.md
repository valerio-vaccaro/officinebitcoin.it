---
layout: default
title: "Introduzion a le **Reti Mesh** e analisi particolar de LoRa e **LoRaWAN**"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lezion Bitcoin-only</span> <span>Sto progetto xe mantegnuo da valerio-vaccaro</span></p>

## 🌍 Traduzion

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Introduzion a le **Reti Mesh** e analisi particolar de LoRa e **LoRaWAN**

## Introduzione a le **Reti Mesh**

Le **Reti Mesh** xe un'architettura de rete in cui i nodi (dispositivi) xe interconnessi in modo no gerarchico, consentendo a ciascun nodo de comunicare direttamente co i altri senza passare attraverso un punto centrale, come un router o un gateway. Ogni nodo potenzialmente può agire sia come trasmettitore che come ricevitore, e i dati possono essere inoltrati attraverso più percorsi par raggiungere la destinazione. 

Sta struttura offre diversi vantaggi:

- **Resilienza**: Se un nodo fallisce, i dati possono essere reindirizzati attraverso altri nodi, garantendo continuità nella comunicazione.
- **Scalabilità**: Le **Reti Mesh** possono espandersi facilmente aggiungendo nuovi nodi senza modifiche significative all'infrastruttura.
- **Copertura estesa**: L'inoltro dei dati consente de coprire aree più ampie rispetto a le reti tradizionali.
- **Flessibilità**: Adatte a molteplici applicazioni, dall'Internet of Things (IoT) a le reti domestiche e industriali.

Tuttavia, le **Reti Mesh** presentano anca alcune sfide:

- **Complessità**: La gestion de più percorsi e la coordinazione tra nodi aumentano la complessità.
- **Consumo energetico**: I nodi che inoltrano dati consumano più energia, riducendo la durata de la batteria.
- **Capacità limitata**: In reti dense, la trasmissione multi-hop può introdurre latenza e ridurre la capacità complessiva.

Le **Reti Mesh** xe utilizzate in tecnologie wireless come **Zigbee**, **Bluetooth** Mesh, **Thread** e, in alcuni casi, protocolli proprietari basati su LoRa. Na de le tecnologie più rilevanti par le reti a bassa potenza e lunga portata xe **LoRaWAN**, che adotta un approccio diverso rispetto a la topologia mesh tradizionale.

## **LoRa** e **LoRaWAN**: Contesto e Differenze

### **LoRa**

**LoRa** (Long Range) xe na tecnologia de modulazione a spettro espanso derivata dalla tecnica Chirp Spread Spectrum (CSS), sviluppata da Cycleo (acquisita da Semtech nel 2012). 

**LoRa** rappresenta el livello fisico (Physical Layer, PHY) de na rete wireless, definendo come i dati vengono modulati e trasmessi su bande de frequenza senza licenza (es. 868 MHz in Europa, 915 MHz in Nord America, 433 MHz in alcune regioni). 

Le sue caratteristiche principali xe:
- Trasmissione su lunghe distanze (fino a 15 km in aree rurali, 2-5 km in aree urbane).
- Consumo energetico estremamente basso, ideale par applicazioni IoT co bassa velocità dati e lunga durata de la batteria.

### **LoRaWAN**

**LoRaWAN** (Long Range Wide Area Network) xe un protocollo de livello MAC (Media Access Control) basato su LoRa, sviluppato dalla LoRa Alliance, un’associazione no-profit fondata nel 2015 co oltre 500 membri, tra cui Semtech, Cisco, IBM e Orange. 

**LoRaWAN** definisce:
- L'architettura de rete.
- El protocollo de comunicazione.
- Aspetti come frequenza de trasmissione, velocità dati, sicurezza e interoperabilità.

A differenza de LoRa, che gestisce solo la modulazione del segnale, **LoRaWAN** stabilisce come i dispositivi (nodi finali) comunicano co i gateway e come sti si collegano ai server de rete tramite connessioni backhaul (es. Ethernet, Wi-Fi o cellulare).

#### Confronto tra **Reti Mesh** e **LoRaWAN**

A differenza de le **Reti Mesh** tradizionali (es. **Zigbee**, **Bluetooth**), **LoRaWAN** utilizza na topologia a stella, in cui i nodi finali comunicano direttamente co i gateway, che inoltrano i dati a un server de rete centrale. De seguito, un confronto dettagliato:

1. Topologia de Rete
**Reti Mesh**: I nodi fungono da ripetitori, inoltrando dati par estendere la copertura. Ciò aumenta la complessità e el consumo energetico.
**LoRaWAN**: Topologia a stella, co nodi che trasmettono direttamente ai gateway. Sto elimina i nodi ripetitori, semplificando la rete e riducendo el consumo energetico.

2. Consumo Energetico
**Reti Mesh**: I nodi ripetitori consumano più energia, riducendo la durata de la batteria.
**LoRaWAN**: I dispositivi finali trasmettono solo quando necessario (es. Classe A co ALOHA), consentendo na durata de la batteria fino a 10-15 anni.

3. Portata e Copertura
**Reti Mesh**: La portata xe estesa tramite multi-hop, ma ogni hop può introdurre latenza e ridurre l’efficienza.
**LoRaWAN**: Grazie a la modulazione CSS, offre na portata fino a 15 km (rurale) o 2-5 km (urbano) senza nodi ripetitori.

4. Capacità e Scalabilità
**Reti Mesh**: In reti dense, el multi-hop può cadoprar colli de bottiglia e ridurre la capacità.
**LoRaWAN**: Supporta milioni de messaggi da migliaia de dispositivi, grazie a la ridondanza dei gateway e a la topologia a stella.

5. Sicurezza
**Reti Mesh**: La sicurezza dipende dal protocollo (es. **Zigbee** usa AES-128). L’inoltro multi-hop può introdurre vulnerabilità.
**LoRaWAN**: Crittografia end-to-end co ciavi de sessione AES-128 (Network Session Key e Application Session Key).

6. Complessità e Costi
**Reti Mesh**: La gestion dei percorsi de inoltro aumenta la complessità. I costi possono crescere co l’aggiunta de nodi ripetitori.
**LoRaWAN**: La topologia a stella xe più semplice. I gateway possono essere costosi, ma i sensori xe economici e le bande ISM senza licenza riducono i costi.

## Analisi Particolare de **LoRa** e **LoRaWAN**
### **LoRa**: Livello Fisico
**LoRa** utilizza la modulazione Chirp Spread Spectrum (CSS), che codifica i dati co segnali sinusoidali a frequenza variabile, distribuendo el segnale su na banda più ampia par migliorare la resistenza al rumore. Offre na sensibilità elevata (-110 dBm a -140 dBm), ideale par ambienti rumorosi. 

I parametri principali includono:

- Spreading Factor (SF): Da 7 a 12, influenza velocità dati e portata. SF12 offre lunga portata ma basso bitrate (0,3 kbps); SF7 offre velocità maggiori (27 kbps) ma portata ridotta.
- Larghezza de banda (BW): 125 kHz, 250 kHz o 500 kHz, influisce su bitrate e robustezza.
- Frequenze ISM: 863-870 MHz (Europa), 902-928 MHz (Nord America), 433 MHz (altre regioni).

LoRa xe ideale par applicazioni IoT co piccoli pacchetti de dati, come monitoraggio ambientale, smart metering e agricoltura intelligente.

## **LoRaWAN**: Protocollo e Architettura

**LoRaWAN** definisce tre classi de dispositivi:

- Classe A: Dispositivi bidirezionali a basso consumo co trasmissioni uplink e brevi finestre de ricezione downlink (ALOHA). Ideale par sensori a batteria.
- Classe B: Aggiunge finestre de ricezione programmate (ogni 128 secondi, sincronizzate tramite beacon GPS) par downlink pianificati.
- Classe C: Dispositivi sempre in ascolto par downlink, adatti a dispositivi alimentati dalla rete elettrica.

L’architettura **LoRaWAN** include:
- Nodi finali (End Devices): Sensori o dispositivi IoT che raccolgono e trasmettono dati.
- Gateway: Ricevono dati dai nodi e li inoltrano al server de rete tramite backhaul.
- Server de rete (Network Server): Gestisce la rete, elimina duplicati e seleziona el gateway par i downlink.
- Server de le applicazioni (Application Server): Elabora i dati par analisi o visualizzazioni.

## **Reti Mesh** co LoRa
Sebbene **LoRaWAN** utilizzi na topologia a stella, xe possibile implementare na rete mesh usando la modulazione LoRa co un protocollo esterno. In na rete mesh LoRa, i nodi agiscono come ripetitori par estendere la copertura, utile in aree senza gateway. 

Tuttavia, ciò richiede:
- Protocollo personalizzato: **LoRaWAN** no supporta nativamente el mesh.
- Maggiore consumo energetico: I nodi ripetitori consumano più energia.
- Complessità: Gestione dei percorsi de inoltro e prevenzione de le collisioni (es. CSMA-CA).

Esempio: moduli LoRa (es. SX1276 de Semtech) co microcontrollori come ESP32 par **Reti Mesh** private.

Vantaggi de **LoRaWAN**

- Efficienza energetica: Topologia a stella elimina i nodi ripetitori.
- Semplicità: Comunicazione diretta co i gateway.
- Scalabilità: Supporta migliaia de dispositivi e milioni de messaggi.
- Sicurezza: Sicurezza robusta co crittografia AES-128.
- Interoperabilità: Standard aperto de la LoRa Alliance.

Limitazioni de **LoRaWAN**

- Bassa velocità dati: 0,3-50 kbps, no adatto par dati voluminosi.
- Latenza: La Classe A introduce ritardi par i downlink.
- Costo dei gateway: Significativo par reti private.

# Conclusione
Le **Reti Mesh** offrono resilienza e flessibilità tramite inoltro multi-hop, ma xe complesse e consumano più energia. **LoRaWAN**, co la sua topologia a stella e modulazione LoRa, xe ideale par applicazioni IoT a bassa potenza e lunga portata, grazie a semplicità, scalabilità e durata de la batteria fino a 15 anni.

La scelta tra **Reti Mesh** e **LoRaWAN** dipende dai requisiti: le mesh par ambienti co nodi ravvicinati, **LoRaWAN** par comunicazioni a lunga distanza co consumi minimi. Sebbene possibile co LoRa, el mesh xe meno comune rispetto a **LoRaWAN**, che domina par la sua standardizzazione e supporto dalla LoRa Alliance.
