# Fullnode e Hardware par un nodo Bitcoin

## Introduzion
Un fullnode Bitcoin xe na componente essenziale de la rete che valida transazioni, mantien una copia completa de la blockchain e contribuisce alla sicurezza del sistema. In questa lezion esploreremo come scegliere l'hardware e configurar un nodo Bitcoin.

## Perché un fullnode?

### Validazion
- Verifica autonomamente le transazioni
- Non dipende da terzi
- Garantisce la sicurezza dei propri fondi

### Privacy
- Non rivela le proprie transazioni a terzi
- Mantien il controllo completo dei dati
- Evita la sorveglianza

### Sovranità
- Controllo completo del software
- Indipendenza da servizi esterni
- Contribuzion alla rete

## Scelta dell'hardware

### Requisiti minimi
- **RAM**: 2GB (4GB raccomandato)
- **Disco**: 500GB SSD (1TB raccomandato)
- **CPU**: Dual-core 1.5GHz
- **Rete**: 50GB/mese upload

### Requisiti raccomandati
- **RAM**: 8GB
- **Disco**: 2TB SSD
- **CPU**: Quad-core 2.0GHz
- **Rete**: 100GB/mese upload

### Opzioni hardware

#### Computer vecchi
- **Vantaggi**: Basso costo, riutilizzo
- **Svantaggi**: Consumo energetico alto
- **Esempi**: Desktop/Laptop 5-10 anni

#### Raspberry Pi
- **Vantaggi**: Basso consumo, silenzioso
- **Svantaggi**: Performance limitate
- **Modelli**: Pi 4 8GB raccomandato

#### Odroid-M1
- **Vantaggi**: Performance migliori del Pi
- **Svantaggi**: Costo più alto
- **Specifiche**: 8GB RAM, ARM Cortex-A76

#### Thin Client
- **Vantaggi**: Basso costo, silenzioso
- **Svantaggi**: Hardware limitato
- **Esempi**: HP T620, Dell Wyse

## Scelta del software

### Sistema operativo
- **Linux**: Raccomandato (Debian, Ubuntu)
- **Windows**: Possibile ma non ottimale
- **macOS**: Possibile ma limitato

### Distribuzion Linux
- **Debian**: Stabile, sicura
- **Ubuntu**: Facile da usare
- **Arch Linux**: Rolling release

## Configurazion base

### Installazion Bitcoin Core
```bash
# Aggiungi repository
sudo add-apt-repository ppa:bitcoin/bitcoin
sudo apt update

# Installa Bitcoin Core
sudo apt install bitcoin-qt bitcoin-cli
```

### Configurazion bitcoin.conf
```bash
# Crea directory
mkdir ~/.bitcoin

# Crea file configurazion
nano ~/.bitcoin/bitcoin.conf
```

Configurazion base:
```
# RPC
rpcuser=bitcoin
rpcpassword=password_sicura
rpcallowip=127.0.0.1

# Rete
txindex=1
blockfilterindex=1

# Performance
dbcache=450
maxorphantx=10
maxmempool=50

# Sicurezza
blocksonly=1
```

### Avvio del nodo
```bash
# Avvia bitcoind
bitcoind -daemon

# Verifica status
bitcoin-cli getblockchaininfo
```

## Ottimizzazioni

### SSD
- **Importante**: Usa sempre SSD
- **Raccomandato**: NVMe SSD
- **Capacità**: Minimo 1TB

### RAM
- **Minimo**: 4GB
- **Raccomandato**: 8GB
- **Configurazion**: dbcache=450

### CPU
- **Minimo**: Dual-core
- **Raccomandato**: Quad-core
- **Architettura**: x86_64 o ARM64

### Rete
- **Upload**: Minimo 50GB/mese
- **Velocità**: Minimo 10 Mbps
- **Stabilità**: Connession sempre attiva

## Configurazion avanzata

### Tor
```bash
# Installa Tor
sudo apt install tor

# Configura bitcoin.conf
proxy=127.0.0.1:9050
listen=1
bind=127.0.0.1
externalip=ONION_ADDRESS
onlynet=onion
```

### Electrum Personal Server
```bash
# Installa EPS
git clone https://github.com/chris-belcher/electrum-personal-server
cd electrum-personal-server
pip3 install -r requirements.txt

# Configura
cp config.ini_sample config.ini
nano config.ini
```

### Mempool.space
```bash
# Installa mempool.space
git clone https://github.com/mempool/mempool
cd mempool
npm install
npm run build
```

## Monitoraggio

### Script di monitoraggio
```bash
#!/bin/bash
# monitor.sh

# Verifica status Bitcoin
if ! bitcoin-cli getblockchaininfo > /dev/null 2>&1; then
    echo "Bitcoin Core non risponde"
    exit 1
fi

# Verifica spazio disco
DISK_USAGE=$(df / | awk 'NR==2 {print $5}' | sed 's/%//')
if [ $DISK_USAGE -gt 90 ]; then
    echo "Spazio disco critico: ${DISK_USAGE}%"
fi

# Verifica memoria
MEM_USAGE=$(free | awk 'NR==2{printf "%.0f", $3*100/$2}')
if [ $MEM_USAGE -gt 90 ]; then
    echo "Memoria critica: ${MEM_USAGE}%"
fi
```

### Crontab
```bash
# Aggiungi a crontab
*/5 * * * * /home/bitcoin/monitor.sh
```

## Sicurezza

### Firewall
```bash
# Configura UFW
sudo ufw enable
sudo ufw default deny incoming
sudo ufw allow ssh
sudo ufw allow 8333
```

### Backup
```bash
# Backup wallet
cp ~/.bitcoin/wallet.dat /backup/

# Backup configurazion
cp ~/.bitcoin/bitcoin.conf /backup/
```

### Aggiornamenti
```bash
# Script aggiornamento
#!/bin/bash
sudo apt update
sudo apt upgrade -y
sudo systemctl restart bitcoind
```

## Troubleshooting

### Problemi comuni
- **Sincronizazion lenta**: Verifica SSD e RAM
- **Connession persa**: Verifica rete e firewall
- **Spazio disco**: Monitora uso disco

### Log
```bash
# Verifica log
tail -f ~/.bitcoin/debug.log

# Filtra errori
grep "ERROR" ~/.bitcoin/debug.log
```

## Conclusione
Un fullnode Bitcoin xe un investimento importante par la sicurezza e la privacy. La scelta dell'hardware e la configurazion corretta garantiscono un nodo affidabile e performante che contribuisce alla salute della rete Bitcoin. 