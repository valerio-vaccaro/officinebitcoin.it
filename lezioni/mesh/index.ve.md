# Ret Mesh, LoRa e LoRaWAN: Tecnologie de comunicazion

## Introduzion
Le ret mesh, LoRa e LoRaWAN xe tecnologie de comunicazion che permet de creare reti resilienti e scalabili. In questa lezion esploreremo le caratteristiche, le differenze e le applicazioni de queste tecnologie.

## Ret Mesh

### Caratteristiche
- **Resilienza**: Se un nodo fallisce, la rete continua a funzionar
- **Scalabilità**: Facile aggiunger nuovi nodi
- **Copertura**: Estensione automatica de la copertura
- **Flessibilità**: Topologia dinamica e adattiva

### Vantaggi
- Alta affidabilità
- Copertura estesa
- Basso costo de infrastruttura
- Facile manutenzion

### Svantaggi
- Complessità de gestione
- Consumo energetico variabile
- Capacità limitata
- Latenza variabile

## LoRa (Long Range)

### Caratteristiche
- **Modulazion**: Chirp Spread Spectrum (CSS)
- **Portata**: Fino a 15 km in aree rurali
- **Consumo**: Molto basso
- **Frequenza**: 433 MHz, 868 MHz, 915 MHz

### Vantaggi
- Portata molto lunga
- Basso consumo energetico
- Resistenza alle interferenze
- Costo basso

### Svantaggi
- Bassa velocità de trasmissione
- Capacità limitata
- Dipendenza dalla frequenza

## LoRaWAN

### Caratteristiche
- **Protocollo**: MAC layer su LoRa
- **Topologia**: Star-of-stars
- **Architettura**: Gateway centralizzati
- **Sicurezza**: AES-128

### Componenti
- **End Device**: Sensori e attuatori
- **Gateway**: Ricevitori centralizzati
- **Network Server**: Gestione de la rete
- **Application Server**: Applicazioni finali

### Classi de dispositivi
- **Classe A**: Bidirezionale, basso consumo
- **Classe B**: Scheduling de downlink
- **Classe C**: Downlink continuo

## Differenze tra LoRa e LoRaWAN

### LoRa
- **Livello**: Fisico (PHY)
- **Topologia**: Peer-to-peer
- **Gestione**: Manuale
- **Applicazioni**: Protocolli custom

### LoRaWAN
- **Livello**: MAC
- **Topologia**: Star
- **Gestione**: Centralizzata
- **Applicazioni**: Standardizzate

## Implementazion de ret mesh con LoRa

### Architettura
```
End Device 1 ←→ End Device 2 ←→ End Device 3
     ↓              ↓              ↓
  Gateway 1 ←→ Gateway 2 ←→ Gateway 3
     ↓              ↓              ↓
  Network Server ←→ Application Server
```

### Protocolli de routing
- **AODV**: Ad-hoc On-demand Distance Vector
- **OLSR**: Optimized Link State Routing
- **BATMAN**: Better Approach To Mobile Ad-hoc Networking

### Esempi de implementazion
```python
# Esempio de nodo mesh con LoRa
import time
from lora import LoRa

class MeshNode:
    def __init__(self, node_id):
        self.node_id = node_id
        self.lora = LoRa()
        self.neighbors = []
    
    def send_message(self, message, destination):
        # Invia messagio via LoRa
        self.lora.send(message, destination)
    
    def receive_message(self):
        # Riceve messagio
        return self.lora.receive()
    
    def route_message(self, message, destination):
        # Routing de messagio
        if destination in self.neighbors:
            self.send_message(message, destination)
        else:
            # Forward a neighbor
            next_hop = self.find_route(destination)
            self.send_message(message, next_hop)
```

## Sicurezza

### LoRa
- Criptazion a livello applicazion
- Autenticazion custom
- Gestione manuale de le chiavi

### LoRaWAN
- Criptazion AES-128
- Autenticazion automatica
- Gestione centralizzata de le chiavi

## Applicazioni

### IoT
- Sensori ambientali
- Monitoraggio agricolo
- Smart city

### Bitcoin
- Nodi Bitcoin
- Lightning Network
- Comunicazion de transazioni

### Emergenze
- Reti de emergenza
- Comunicazion in aree remote
- Backup de comunicazion

## Best Practices

### Progettazion
- Pianifica la topologia
- Considera le distanze
- Valuta il consumo energetico

### Implementazion
- Usa protocolli standard
- Implementa sicurezza
- Testa la resilienza

### Manutenzion
- Monitora le performance
- Aggiorna i firmware
- Backup de le configurazioni

## Conclusione
Le ret mesh, LoRa e LoRaWAN forniscono soluzioni potenti par comunicazion resilienti e scalabili. La scelta tra queste tecnologie dipende dai requisiti specifici de l'applicazion, considerando fattori come portata, consumo energetico, complessità e costi. 