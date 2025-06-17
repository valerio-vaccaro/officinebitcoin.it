# Introduzione alle **Reti Mesh** e Analisi Particolare di LoRa e **LoRaWAN**

## Introduzione alle **Reti Mesh**

Le **Reti Mesh** sono un'architettura di rete in cui i nodi (dispositivi) sono interconnessi in modo non gerarchico, consentendo a ciascun nodo di comunicare direttamente con gli altri senza passare attraverso un punto centrale, come un router o un gateway. Ogni nodo potenzialmente può agire sia come trasmettitore che come ricevitore, e i dati possono essere inoltrati attraverso più percorsi per raggiungere la destinazione. 

Questa struttura offre diversi vantaggi:

- **Resilienza**: Se un nodo fallisce, i dati possono essere reindirizzati attraverso altri nodi, garantendo continuità nella comunicazione.
- **Scalabilità**: Le **Reti Mesh** possono espandersi facilmente aggiungendo nuovi nodi senza modifiche significative all'infrastruttura.
- **Copertura estesa**: L'inoltro dei dati consente di coprire aree più ampie rispetto alle reti tradizionali.
- **Flessibilità**: Adatte a molteplici applicazioni, dall'Internet of Things (IoT) alle reti domestiche e industriali.

Tuttavia, le **Reti Mesh** presentano anche alcune sfide:

- **Complessità**: La gestione di più percorsi e la coordinazione tra nodi aumentano la complessità.
- **Consumo energetico**: I nodi che inoltrano dati consumano più energia, riducendo la durata della batteria.
- **Capacità limitata**: In reti dense, la trasmissione multi-hop può introdurre latenza e ridurre la capacità complessiva.

Le **Reti Mesh** sono utilizzate in tecnologie wireless come **Zigbee**, **Bluetooth** Mesh, **Thread** e, in alcuni casi, protocolli proprietari basati su LoRa. Una delle tecnologie più rilevanti per le reti a bassa potenza e lunga portata è **LoRaWAN**, che adotta un approccio diverso rispetto alla topologia mesh tradizionale.

## **LoRa** e **LoRaWAN**: Contesto e Differenze

### **LoRa**

**LoRa** (Long Range) è una tecnologia di modulazione a spettro espanso derivata dalla tecnica Chirp Spread Spectrum (CSS), sviluppata da Cycleo (acquisita da Semtech nel 2012). 

**LoRa** rappresenta il livello fisico (Physical Layer, PHY) di una rete wireless, definendo come i dati vengono modulati e trasmessi su bande di frequenza senza licenza (es. 868 MHz in Europa, 915 MHz in Nord America, 433 MHz in alcune regioni). 

Le sue caratteristiche principali sono:
- Trasmissione su lunghe distanze (fino a 15 km in aree rurali, 2-5 km in aree urbane).
- Consumo energetico estremamente basso, ideale per applicazioni IoT con bassa velocità dati e lunga durata della batteria.

### **LoRaWAN**

**LoRaWAN** (Long Range Wide Area Network) è un protocollo di livello MAC (Media Access Control) basato su LoRa, sviluppato dalla LoRa Alliance, un’associazione no-profit fondata nel 2015 con oltre 500 membri, tra cui Semtech, Cisco, IBM e Orange. 

**LoRaWAN** definisce:
- L'architettura di rete.
- Il protocollo di comunicazione.
- Aspetti come frequenza di trasmissione, velocità dati, sicurezza e interoperabilità.

A differenza di LoRa, che gestisce solo la modulazione del segnale, **LoRaWAN** stabilisce come i dispositivi (nodi finali) comunicano con i gateway e come questi si collegano ai server di rete tramite connessioni backhaul (es. Ethernet, Wi-Fi o cellulare).

#### Confronto tra **Reti Mesh** e **LoRaWAN**

A differenza delle **Reti Mesh** tradizionali (es. **Zigbee**, **Bluetooth**), **LoRaWAN** utilizza una topologia a stella, in cui i nodi finali comunicano direttamente con i gateway, che inoltrano i dati a un server di rete centrale. Di seguito, un confronto dettagliato:

1. Topologia di Rete
**Reti Mesh**: I nodi fungono da ripetitori, inoltrando dati per estendere la copertura. Ciò aumenta la complessità e il consumo energetico.
**LoRaWAN**: Topologia a stella, con nodi che trasmettono direttamente ai gateway. Questo elimina i nodi ripetitori, semplificando la rete e riducendo il consumo energetico.

2. Consumo Energetico
**Reti Mesh**: I nodi ripetitori consumano più energia, riducendo la durata della batteria.
**LoRaWAN**: I dispositivi finali trasmettono solo quando necessario (es. Classe A con ALOHA), consentendo una durata della batteria fino a 10-15 anni.

3. Portata e Copertura
**Reti Mesh**: La portata è estesa tramite multi-hop, ma ogni hop può introdurre latenza e ridurre l’efficienza.
**LoRaWAN**: Grazie alla modulazione CSS, offre una portata fino a 15 km (rurale) o 2-5 km (urbano) senza nodi ripetitori.

4. Capacità e Scalabilità
**Reti Mesh**: In reti dense, il multi-hop può causare colli di bottiglia e ridurre la capacità.
**LoRaWAN**: Supporta milioni di messaggi da migliaia di dispositivi, grazie alla ridondanza dei gateway e alla topologia a stella.

5. Sicurezza
**Reti Mesh**: La sicurezza dipende dal protocollo (es. **Zigbee** usa AES-128). L’inoltro multi-hop può introdurre vulnerabilità.
**LoRaWAN**: Crittografia end-to-end con chiavi di sessione AES-128 (Network Session Key e Application Session Key).

6. Complessità e Costi
**Reti Mesh**: La gestione dei percorsi di inoltro aumenta la complessità. I costi possono crescere con l’aggiunta di nodi ripetitori.
**LoRaWAN**: La topologia a stella è più semplice. I gateway possono essere costosi, ma i sensori sono economici e le bande ISM senza licenza riducono i costi.

## Analisi Particolare di **LoRa** e **LoRaWAN**
### **LoRa**: Livello Fisico
**LoRa** utilizza la modulazione Chirp Spread Spectrum (CSS), che codifica i dati con segnali sinusoidali a frequenza variabile, distribuendo il segnale su una banda più ampia per migliorare la resistenza al rumore. Offre una sensibilità elevata (-110 dBm a -140 dBm), ideale per ambienti rumorosi. 

I parametri principali includono:

- Spreading Factor (SF): Da 7 a 12, influenza velocità dati e portata. SF12 offre lunga portata ma basso bitrate (0,3 kbps); SF7 offre velocità maggiori (27 kbps) ma portata ridotta.
- Larghezza di banda (BW): 125 kHz, 250 kHz o 500 kHz, influisce su bitrate e robustezza.
- Frequenze ISM: 863-870 MHz (Europa), 902-928 MHz (Nord America), 433 MHz (altre regioni).

LoRa è ideale per applicazioni IoT con piccoli pacchetti di dati, come monitoraggio ambientale, smart metering e agricoltura intelligente.

## **LoRaWAN**: Protocollo e Architettura

**LoRaWAN** definisce tre classi di dispositivi:

- Classe A: Dispositivi bidirezionali a basso consumo con trasmissioni uplink e brevi finestre di ricezione downlink (ALOHA). Ideale per sensori a batteria.
- Classe B: Aggiunge finestre di ricezione programmate (ogni 128 secondi, sincronizzate tramite beacon GPS) per downlink pianificati.
- Classe C: Dispositivi sempre in ascolto per downlink, adatti a dispositivi alimentati dalla rete elettrica.

L’architettura **LoRaWAN** include:
- Nodi finali (End Devices): Sensori o dispositivi IoT che raccolgono e trasmettono dati.
- Gateway: Ricevono dati dai nodi e li inoltrano al server di rete tramite backhaul.
- Server di rete (Network Server): Gestisce la rete, elimina duplicati e seleziona il gateway per i downlink.
- Server delle applicazioni (Application Server): Elabora i dati per analisi o visualizzazioni.

## **Reti Mesh** con LoRa
Sebbene **LoRaWAN** utilizzi una topologia a stella, è possibile implementare una rete mesh usando la modulazione LoRa con un protocollo esterno. In una rete mesh LoRa, i nodi agiscono come ripetitori per estendere la copertura, utile in aree senza gateway. 

Tuttavia, ciò richiede:
- Protocollo personalizzato: **LoRaWAN** non supporta nativamente il mesh.
- Maggiore consumo energetico: I nodi ripetitori consumano più energia.
- Complessità: Gestione dei percorsi di inoltro e prevenzione delle collisioni (es. CSMA-CA).

Esempio: moduli LoRa (es. SX1276 di Semtech) con microcontrollori come ESP32 per **Reti Mesh** private.

Vantaggi di **LoRaWAN**

- Efficienza energetica: Topologia a stella elimina i nodi ripetitori.
- Semplicità: Comunicazione diretta con i gateway.
- Scalabilità: Supporta migliaia di dispositivi e milioni di messaggi.
- Sicurezza: Sicurezza robusta con crittografia AES-128.
- Interoperabilità: Standard aperto della LoRa Alliance.

Limitazioni di **LoRaWAN**

- Bassa velocità dati: 0,3-50 kbps, non adatto per dati voluminosi.
- Latenza: La Classe A introduce ritardi per i downlink.
- Costo dei gateway: Significativo per reti private.

# Conclusione
Le **Reti Mesh** offrono resilienza e flessibilità tramite inoltro multi-hop, ma sono complesse e consumano più energia. **LoRaWAN**, con la sua topologia a stella e modulazione LoRa, è ideale per applicazioni IoT a bassa potenza e lunga portata, grazie a semplicità, scalabilità e durata della batteria fino a 15 anni.

La scelta tra **Reti Mesh** e **LoRaWAN** dipende dai requisiti: le mesh per ambienti con nodi ravvicinati, **LoRaWAN** per comunicazioni a lunga distanza con consumi minimi. Sebbene possibile con LoRa, il mesh è meno comune rispetto a **LoRaWAN**, che domina per la sua standardizzazione e supporto dalla LoRa Alliance.
