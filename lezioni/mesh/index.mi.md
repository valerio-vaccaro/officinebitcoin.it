---
layout: default
title: "Introduzion a i **Reti Mesh** e analisi particolar de LoRa e **LoRaWAN**"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lezion Bitcoin-only</span> <span>Quest progett l'e mantegnuu da valerio-vaccaro</span></p>

## 🌍 Traduzion

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Introduzion a i **Reti Mesh** e analisi particolar de LoRa e **LoRaWAN**

## Introduzion a le **Reti Mesh**

I **Reti Mesh** hinn un'architettura de rete in cui i nodi (dispositivi) hinn interconnessi in modo minga gerarchico, consentendo a ciascun nodo de comunicare direttamente con i altri senza passare attraverso on punto centrale, come on router o on gateway. Ogni nodo potenzialmente può agire sia come trasmettitore che come ricevitore, e i dati possono essere inoltrati attraverso più percorsi per raggiungere la destinazion. 

Questa struttura offre diversi vantaggi:

- **Resilienza**: Se on nodo fallisce, i dati possono essere reindirizzati attraverso altri nodi, garantendo continuità nella comunicazion.
- **Scalabilità**: I **Reti Mesh** possono espandersi facilmente aggiungendo nuovi nodi senza modifiche significative all'infrastruttura.
- **Copertura estesa**: L'inoltro di dati consente de coprire aree più ampie rispetto a le reti tradizionali.
- **Flessibilità**: Adatte a molteplici applicazion, dall'Internet of Things (IoT) a le reti domestiche e industriali.

Tuttavia, i **Reti Mesh** presentano anca alcune sfide:

- **Complessità**: La gestion de più percorsi e la coordinazion tra nodi aumentano la complessità.
- **Consumo energetico**: I nodi che inoltrano dati consumano più energia, riducendo la durata de la batteria.
- **Capacità limitata**: In reti dense, la trasmissione multi-hop può introdurre latenza e ridurre la capacità complessiva.

I **Reti Mesh** hinn utilizzate in tecnologie wireless come **Zigbee**, **Bluetooth** Mesh, **Thread** e, in alcuni casi, protocolli proprietari basati su LoRa. Ona di tecnologie più rilevanti per i reti a bassa potenza e lunga portata l'è **LoRaWAN**, che adotta on approccio diverso rispetto a la topologia mesh tradizionale.

## **LoRa** e **LoRaWAN**: Contesto e Differenze

### **LoRa**

**LoRa** (Long Range) l'è ona tecnologia de modulazion a spettro espanso derivata dalla tecnica Chirp Spread Spectrum (CSS), sviluppata da Cycleo (acquisita da Semtech nel 2012). 

**LoRa** rappresenta el livello fisico (Physical Layer, PHY) de ona rete wireless, definendo come i dati vengono modulati e trasmessi su bande de frequenza senza licenza (es. 868 MHz in Europa, 915 MHz in Nord America, 433 MHz in alcune regioni). 

I sue caratteristiche principali hinn:
- Trasmissione su lunghe distanze (fino a 15 km in aree rurali, 2-5 km in aree urbane).
- Consumo energetico estremamente basso, ideale per applicazion IoT con bassa velocità dati e lunga durata de la batteria.

### **LoRaWAN**

**LoRaWAN** (Long Range Wide Area Network) l'è on protocollo de livello MAC (Media Access Control) basato su LoRa, sviluppato dalla LoRa Alliance, on’associazion no-profit fondata nel 2015 con oltre 500 membri, tra cui Semtech, Cisco, IBM e Orange. 

**LoRaWAN** definisce:
- L'architettura de rete.
- El protocollo de comunicazion.
- Aspetti come frequenza de trasmissione, velocità dati, sicurezza e interoperabilità.

A differenza de LoRa, che gestisce domà la modulazion del segnale, **LoRaWAN** stabilisce come i dispositivi (nodi finali) comunicano con i gateway e come questi si collegano ai server de rete tramite connessioni backhaul (es. Ethernet, Wi-Fi o cellulare).

#### Confronto tra **Reti Mesh** e **LoRaWAN**

A differenza di **Reti Mesh** tradizionali (es. **Zigbee**, **Bluetooth**), **LoRaWAN** utilizza ona topologia a stella, in cui i nodi finali comunicano direttamente con i gateway, che inoltrano i dati a on server de rete centrale. De seguito, on confronto dettagliato:

1. Topologia de Rete
**Reti Mesh**: I nodi fungono da ripetitori, inoltrando dati per estendere la copertura. Ciò aumenta la complessità e el consumo energetico.
**LoRaWAN**: Topologia a stella, con nodi che trasmettono direttamente ai gateway. Quest elimina i nodi ripetitori, semplificando la rete e riducendo el consumo energetico.

2. Consumo Energetico
**Reti Mesh**: I nodi ripetitori consumano più energia, riducendo la durata de la batteria.
**LoRaWAN**: I dispositivi finali trasmettono domà quand necessario (es. Classe A con ALOHA), consentendo ona durata de la batteria fino a 10-15 anni.

3. Portata e Copertura
**Reti Mesh**: La portata l'è estesa tramite multi-hop, ma ogni hop può introdurre latenza e ridurre l’efficienza.
**LoRaWAN**: Grazie a la modulazion CSS, offre ona portata fino a 15 km (rurale) o 2-5 km (urbano) senza nodi ripetitori.

4. Capacità e Scalabilità
**Reti Mesh**: In reti dense, el multi-hop può cadoprà colli de bottiglia e ridurre la capacità.
**LoRaWAN**: Supporta milioni de messaggi da migliaia de dispositivi, grazie a la ridondanza di gateway e a la topologia a stella.

5. Sicurezza
**Reti Mesh**: La sicurezza dipende dal protocollo (es. **Zigbee** usa AES-128). L’inoltro multi-hop può introdurre vulnerabilità.
**LoRaWAN**: Crittografia end-to-end con ciav de sessione AES-128 (Network Session Key e Application Session Key).

6. Complessità e Costi
**Reti Mesh**: La gestion di percorsi de inoltro aumenta la complessità. I costi possono crescere con l’aggiunta de nodi ripetitori.
**LoRaWAN**: La topologia a stella l'è più sempliz. I gateway possono essere costosi, ma i sensori hinn economici e i bande ISM senza licenza riducono i costi.

## Analisi Particolare de **LoRa** e **LoRaWAN**
### **LoRa**: Livello Fisico
**LoRa** utilizza la modulazion Chirp Spread Spectrum (CSS), che codifica i dati con segnali sinusoidali a frequenza variabile, distribuendo el segnale su ona banda più ampia per migliorare la resistenza al rumore. Offre ona sensibilità elevata (-110 dBm a -140 dBm), ideale per ambienti rumorosi. 

I parametri principali includono:

- Spreading Factor (SF): Da 7 a 12, influenza velocità dati e portata. SF12 offre lunga portata ma basso bitrate (0,3 kbps); SF7 offre velocità maggiori (27 kbps) ma portata ridotta.
- Larghezza de banda (BW): 125 kHz, 250 kHz o 500 kHz, influisce su bitrate e robustezza.
- Frequenze ISM: 863-870 MHz (Europa), 902-928 MHz (Nord America), 433 MHz (altre regioni).

LoRa l'è ideale per applicazion IoT con piccoli pacchetti de dati, come monitoraggio ambientale, smart metering e agricoltura intelligente.

## **LoRaWAN**: Protocollo e Architettura

**LoRaWAN** definisce tre classi de dispositivi:

- Classe A: Dispositivi bidirezionali a basso consumo con trasmissioni uplink e brevi finestre de ricezion downlink (ALOHA). Ideale per sensori a batteria.
- Classe B: Aggiunge finestre de ricezion programmate (ogni 128 secondi, sincronizzate tramite beacon GPS) per downlink pianificati.
- Classe C: Dispositivi semper in ascolto per downlink, adatti a dispositivi alimentati dalla rete elettrica.

L’architettura **LoRaWAN** include:
- Nodi finali (End Devices): Sensori o dispositivi IoT che raccolgono e trasmettono dati.
- Gateway: Ricevono dati dai nodi e li inoltrano al server de rete tramite backhaul.
- Server de rete (Network Server): Gestisce la rete, elimina duplicati e seleziona el gateway per i downlink.
- Server di applicazion (Application Server): Elabora i dati per analisi o visualizzazion.

## **Reti Mesh** con LoRa
Sebbene **LoRaWAN** utilizzi ona topologia a stella, l'è possibile implementare ona rete mesh usando la modulazion LoRa con on protocollo esterno. In ona rete mesh LoRa, i nodi agiscono come ripetitori per estendere la copertura, utile in aree senza gateway. 

Tuttavia, ciò richiede:
- Protocollo personalizzato: **LoRaWAN** minga supporta nativamente el mesh.
- Maggiore consumo energetico: I nodi ripetitori consumano più energia.
- Complessità: Gestione di percorsi de inoltro e prevenzion di collisioni (es. CSMA-CA).

Esempio: moduli LoRa (es. SX1276 de Semtech) con microcontrollori come ESP32 per **Reti Mesh** private.

Vantaggi de **LoRaWAN**

- Efficienza energetica: Topologia a stella elimina i nodi ripetitori.
- Semplicità: Comunicazion diretta con i gateway.
- Scalabilità: Supporta migliaia de dispositivi e milioni de messaggi.
- Sicurezza: Sicurezza robusta con crittografia AES-128.
- Interoperabilità: Standard aperto de la LoRa Alliance.

Limitazion de **LoRaWAN**

- Bassa velocità dati: 0,3-50 kbps, minga adatto per dati voluminosi.
- Latenza: La Classe A introduce ritardi per i downlink.
- Costo di gateway: Significativo per reti private.

# Conclusione
I **Reti Mesh** offrono resilienza e flessibilità tramite inoltro multi-hop, ma hinn complesse e consumano più energia. **LoRaWAN**, con la sua topologia a stella e modulazion LoRa, l'è ideale per applicazion IoT a bassa potenza e lunga portata, grazie a semplicità, scalabilità e durata de la batteria fino a 15 anni.

La scelta tra **Reti Mesh** e **LoRaWAN** dipende dai requisiti: i mesh per ambienti con nodi ravvicinati, **LoRaWAN** per comunicazion a lunga distanza con consumi minimi. Sebbene possibile con LoRa, el mesh l'è meno comune rispetto a **LoRaWAN**, che domina per la sua standardizzazion e supporto dalla LoRa Alliance.
