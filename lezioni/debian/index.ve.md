# Installazion de Debian: Guida completa

## Introduzion
Debian xe na distribuzion Linux stabile e affidabile, perfetta par nodi Bitcoin e server. In questa lezion impareremo come installar e configurar Debian par un ambiente Bitcoin sicuro.

## Preparazion

### Requisiti hardware
- **RAM**: Minimo 4GB, raccomandato 8GB
- **Disco**: Minimo 100GB SSD
- **CPU**: Qualsiasi CPU moderna
- **Rete**: Connession internet stabile

### Download
1. Vai su https://www.debian.org/download
2. Scarica l'immagine ISO de Debian 12 (Bookworm)
3. Verifica l'hash SHA256
4. Crea un USB bootabile

### Creazion USB bootabile
```bash
# Su Linux/macOS
sudo dd if=debian-12.0.0-amd64-netinst.iso of=/dev/sdX bs=4M status=progress

# Su Windows
# Usa Rufus o balenaEtcher
```

## Installazion

### Boot da USB
1. Inserisci l'USB nel computer
2. Avvia da USB (F12 o Del par entrare nel BIOS)
3. Scegli "Install" o "Graphical install"

### Configurazion iniziale
1. **Lingua**: Italiano
2. **Posizion**: Italia
3. **Layout tastiera**: Italiano
4. **Nome computer**: bitcoin-node (o altro)
5. **Nome utente**: bitcoin (o altro)
6. **Password utente**: Password forte
7. **Password root**: Password forte

### Partizionamento
**RACCOMANDATO**: Rimuovi la partizion swap

1. Scegli "Partizionamento manuale"
2. Seleziona il disco SSD
3. Crea partizion:
   - `/` (root): 50GB
   - `/home`: resto del spazio
4. **IMPORTANTE**: Non creare partizion swap

### Configurazion rete
1. **Hostname**: bitcoin-node
2. **Domain name**: lascia vuoto
3. **Proxy**: lascia vuoto (se non necessario)

### Repository
1. **Mirror**: Scegli un mirror italiano
2. **Participazion survey**: No (raccomandato)

### Software
1. **Desktop environment**: Nessuno (solo console)
2. **Software aggiuntivo**: 
   - SSH server
   - Standard system utilities

## Configurazion post-installazion

### Aggiornamenti
```bash
sudo apt update
sudo apt upgrade -y
```

### Installazion software essenziale
```bash
sudo apt install -y \
    curl \
    wget \
    git \
    htop \
    mc \
    nano \
    vim \
    ufw \
    fail2ban \
    logwatch \
    rkhunter \
    chkrootkit
```

### Configurazion firewall
```bash
# Abilita firewall
sudo ufw enable

# Regole base
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw allow 8333  # Bitcoin
sudo ufw allow 8332  # Bitcoin RPC (se necessario)
```

### Configurazion SSH
```bash
# Backup configurazion originale
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup

# Modifica configurazion
sudo nano /etc/ssh/sshd_config
```

Aggiungi/modifica:
```
Port 2222  # Cambia porta default
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
```

### Configurazion chiavi SSH
```bash
# Su computer locale
ssh-keygen -t ed25519 -C "bitcoin-node"

# Copia chiave pubblica
ssh-copy-id -i ~/.ssh/id_ed25519.pub bitcoin@IP_SERVER

# Testa connession
ssh -p 2222 bitcoin@IP_SERVER
```

### Installazion Tor
```bash
sudo apt install -y tor

# Configurazion Tor
sudo nano /etc/tor/torrc
```

Aggiungi:
```
HiddenServiceDir /var/lib/tor/bitcoin/
HiddenServicePort 8333 127.0.0.1:8333
```

```bash
# Riavvia Tor
sudo systemctl restart tor
sudo systemctl enable tor

# Mostra onion address
sudo cat /var/lib/tor/bitcoin/hostname
```

## Configurazion sistema

### Timezone
```bash
sudo timedatectl set-timezone Europe/Rome
```

### NTP
```bash
sudo apt install -y ntp
sudo systemctl enable ntp
sudo systemctl start ntp
```

### Log rotation
```bash
sudo nano /etc/logrotate.conf
```

### Monitoraggio
```bash
# Installa monitoring tools
sudo apt install -y \
    iotop \
    nethogs \
    iftop \
    nload
```

## Sicurezza

### Fail2ban
```bash
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

### Rootkit detection
```bash
# Configura rkhunter
sudo rkhunter --update
sudo rkhunter --propupd

# Aggiungi a crontab
sudo crontab -e
```

Aggiungi:
```
0 2 * * * /usr/bin/rkhunter --cronjob --update --quiet
```

### Logwatch
```bash
sudo nano /etc/cron.daily/00logwatch
```

Aggiungi:
```
/usr/sbin/logwatch --output mail --mailto root --detail high
```

## Backup

### Script backup
```bash
#!/bin/bash
# backup.sh

DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_DIR="/backup"
SOURCE_DIRS=("/home" "/etc" "/var/log")

mkdir -p $BACKUP_DIR

for dir in "${SOURCE_DIRS[@]}"; do
    tar -czf $BACKUP_DIR/backup_${DATE}_$(basename $dir).tar.gz $dir
done

# Mantien solo ultimi 7 backup
find $BACKUP_DIR -name "backup_*.tar.gz" -mtime +7 -delete
```

### Crontab backup
```bash
sudo crontab -e
```

Aggiungi:
```
0 1 * * * /home/bitcoin/backup.sh
```

## Conclusione
Con questa configurazion avrai un sistema Debian sicuro e ottimizzato par nodi Bitcoin. Ricorda de:
- Mantener aggiornati i pacchetti
- Monitorar i log
- Fare backup regolari
- Testar le procedure de recovery 