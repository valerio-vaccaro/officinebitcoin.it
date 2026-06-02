---
layout: default
title: "Fullnode e hardware par un nodo"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lezion Bitcoin-only</span> <span>Sto progetto xe manteniu da valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Fullnode e hardware par un nodo

Gaver un nodo Bitcoin xe fondamentale par che el consente, co la massima privacy, de:

- validar tuta la catena de Bitcoin,
- controlar el bilancio dei nostri wallet,
- trasmeter le nostre nove transazioni
- ...

## Selezion de l'hardware

- minimo 2GB (consigliai 4GB) de memoria RAM,
- disco de almeno 1TB (consigliai 2TB) de memoria de massa,
- cpu multi-core suficientemente performante (probabilmente qualsiasi processore sviluppa nel ultimo decenio).

### Riutiliza un vecio computer

Un vecio computer pol esser riciclado come nodo, in caso de laptop se consiglia de cavar via la bateria che, tegniuda sempre soto carica, la podaria costituir un rischio. El gran vantajo xe dato dal costo pari a zero o limita solo al disco piu capiente.

### Raspberry pi e altre schede

Raspberry pi xe na scheda ARM molto doparada par la realizazion de sistemi IoT e nodi, el costo eccessivo e la necessita de un disco su presa USB tutoavia la rende no la migliore de le scelte possibili in termini de performance e de stabilita.

Odroid-M1 xe na scheda ARM performante e con uno slot interno par l'aggiunta de memoria de massa aggiuntiva.

### Thin client

Con un budget molto ridoto 30-100 euro xe possibile comprar un Thin Client usado (su ebay) che associa bassi consumi a performance suficienti par far girar el nodo.

Come esempi de Thin Client xe stai testai i seguenti modelli:

- Fujitsu Futro s920
- HP t620

## Selezion del software

Instalar manco software possibile su un nodo limita i possibili atachi e rende el sistema piu semplice da mantegnir.

Online se trova soluzioni preconfezionade (Umbrel, Mynode, ...) che le maschera i check de sicurezza e le zonta software e script (par esempio docker) de dificile controlo. In ste lezioni metaremo l'atenzion su la creazion de un nodo a man, cioe instalando manualmente tuti i software necessari.

### Step 0 - El sistema operativo

La prima scelta da far xe el sistema operativo, el consiglio xe de doparar Linux in na version LTS, cioe in cui sia garantido supporto par un numero suficientemente longo de ani. La me scelta personale casca su Debian 12.

El sistema operativo scelto va quindi instalado sul computer e va atualizai tuti i paccheti (l'aggiornamento xe qualcossa che ne seguira durante tuta la vita del nodo).

Se consiglia anca de instalar tor ( e/o altra VPN se necessaria) e ssh cussi da permetar la manutenzion remota del nodo.

Un gruppo de continuita infine podaria salvar el nodo da bruschi cali de corrente evitando de lassar bitcoin e i altri software in un stato inconsistente.

### Step 1 - Instalemo Bitcoin

Scaricamo core, i hash e le firme.

```
wget https://bitcoincore.org/bin/bitcoin-core-28.1/bitcoin-28.1-x86_64-linux-gnu.tar.gz
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS.asc
```

In caso se dopari na board dotada de architetura arm el paccheto andra coreto in `bitcoin-28.1-aarch64-linux-gnu.tar.gz`, cioe nel medesimo paccheto ma compilado par l'architetura arm a 64 bit (aarch64) che xe proprio quela doparada da odroid.

A sto punto podemo controlar che uno dei hash in SHA256SUM corisponda a l'archivio scaricado.

```
sha256sum --ignore-missing --check SHA256SUMS
```

El risultato ne segnala che xe stada trovata na corispondenza par l'archivio scaricado.

```
bitcoin-28.1-x86_64-linux-gnu.tar.gz: OK
```

Verifichiamo ora le firme del file SHA256SUM, prima se necessario procuramose le chiavi e importemole.

```
git clone https://github.com/bitcoin-core/guix.sigs
gpg --import guix.sigs/builder-keys/*
```

E infine verifichiamo le firme.

```
gpg --verify SHA256SUMS.asc
```

Se vedaremo parecie volte la scrita `gpg: Good signature from ...` vol dir che gavemo trovado de le firme valide.

Procedemo a lo scompattamento e a l'instalazion

```
tar xzvf bitcoin-28.1-x86_64-linux-gnu.tar.gz 
sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-28.1/bin/*
```

E ghe semo, ora gavemo `bitcoind`, `bitcoin-cli` e le altre utilita pronte par esser lanciate.

Par ora lancemo `bitcoind` e vedaremo un poco de log. Bitcoin scominzia a sincronizarse e ora sara presente na directory con la blockchain e tute le configurazioni in `~/.bitcoin/`.

Da un altro terminale podemo controlar el funzionamento de bitcoind lanciando el comando `tail -f ~/.bitcoin/debug.log`.

### Step 1b - Configuremo Bitcoin

Come gavemo za visto prima, la directory in cui Bitcoin core salva le configurazioni e la blockchain xe la directory `~/.bitcoin/` par quanto riguarda el sistema operativo Linux; nel caso se volesse cambiar la posizion de salvataggio se pol doparar diversi aprocci:

- crear un link simbolico de la directory su un disco piu grande tramite el comando `ln -s`,
- doparar da linea de comando o dentro de bitcoin.conf el comando `datadir` specificando la directory de destinazion.

Bitcoin Core supporta tre tipologie diverse de reti a cui coneterse:
- `mainnet`, questa xe la classica rete a cui tuti semo abituai ed xe el default par core,
- `testnet`, sta rete xe analoga a mainnet ma i token no ga alcun valor, el mining vien sempre fato ma in caso de assenza de blocchi par 20 minuti la dificolta vien fata precipitar (la sofre de reorg spesso importanti),
- `regtest`, in sta modalita se ga na picola blockchain privada che parte sempre da zero e in cui xe possibile minar a dificolta minima (serve par test locali).

Un altro comando utile xe `daemon` che, se setado, no mantien el log de bitcoin core colegado a la console atuale; par veder el funzionamento sara sempre possibile doparar el comando `tail -f ~/.bitcoin/debug.log`.

Tute le configurazioni pol esser lanciate da linea de comando o tramite el file `~/.bitcoin/bitcoin.conf`, un file compatibile con un setup casalingo (cioe in cui vojo tegnir el consumo de risorse al minimo) podaria esser el seguente.
file de configurazion

```
daemon=1  
blocksonly=1  
maxconnections=20  
maxuploadtarget=500  
txindex=1  
blockfilterindex=1

rpcallowip=0.0.0.0/0
rpcallowip=0.0.0.0/0
rpcuser=username
rpcpassword=password
```

In cui:

- el server xe scolegado da la console con `daemon=1`
- vien scaricai solo i blocchi e no la mempool `blocksonly=1`
- xe permesse fino a venti connessioni `txindex=1`
- se spedisse informazioni ai altri nodi in internet par un massimo de 500 megabyte al giorno `maxuploadtarget=500`
- se mantien un indice de le transazioni `txindex=1`
- se mantien un indice dei blockfilter `blockfilterindex=1`
- demo la possibilita a chiunque de colegarse tramite rpc `rpcallowip=0.0.0.0/0`
- coleghemo rpc a tute le schede de rete `rpcallowip=0.0.0.0/0`
- setemo uno username par rpc `rpcuser=username` (ovviamente da sostituir)
- setemo na password par rpc `rpcpassword=password` (ovviamente da sostituir)

L'elenco completo de le funzionalita se pol trovar su [https://jlopp.github.io/bitcoin-core-config-generator](https://jlopp.github.io/bitcoin-core-config-generator)

Se pol anca far tuto con un singolo comando da terminale.

```
cat >bitcoin.conf <<EOL
daemon=1  
blocksonly=1  
maxconnections=20  
maxuploadtarget=500  
txindex=1  
blockfilterindex=1

rpcallowip=0.0.0.0/0
rpcbind=0.0.0.0
rpcuser=username
rpcpassword=password
EOL
```

Qualora se gabia a disposizion un altro nodo za sincroniza se pol doparar l'opzion `connect` par colegarse SOLO ED ESCLUSIVAMENTE a sto nodo; se tal nodo xe in rete locale se guadagna tempo e banda con sta semplice configurazion.

Da la release 26 core supporta crittazion de le comunicazioni tra i nodi con l'opzion `v2transport`.

Tute le configurazioni mostrate xe relative a clearnet, le configurazioni par tor le sara oggetto de un'altra lezion.

### Step 1c - Lancemo Bitcoin

Lancemo Bitcoin costruendo un file de lancio par systemd.

```
sudo  sh -c "cat > /etc/systemd/system/bitcoind.service <<EOL
[Unit]
Description=Bitcoin daemon
After=network.target

[Service]
User=bitcoin
Group=bitcoin
Type=forking
PIDFile=/home/bitcoin/.bitcoin/bitcoind.pid
ExecStart=/usr/local/bin/bitcoind -pid=/home/bitcoin/.bitcoin/bitcoind.pid
KillMode=process
Restart=always
TimeoutSec=120
RestartSec=30

[Install]
WantedBy=multi-user.target
EOL"
```
Atension: in sto caso stemo doparando l'utente `bitcoin` par far partir el software.

Podemo quindi registrar el script creado e lanciarlo.

```
sudo systemctl enable bitcoind
sudo systemctl start bitcoind
```

Ogni volta che se vol controlar el stato del software se pol doparar el seguente comando.

```
systemctl status bitcoind
```

### Step 2 - Instalemo Electrs

Instalemo `Electrs` che xe un electrum server basa su `Rust`, el primo step xe quindi instalar sto linguaggio.

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Instalemo anca clang e el paccheto build-essential.

```
apt update
apt install clang cmake build-essential -y
```

Scaricamo l'ultima version (atualmente la 0.10.5) da Github.

```
VERSION="0.10.5"
git clone --branch v$VERSION https://github.com/romanz/electrs.git
cd electrs
```

Importemo la chiave de lo sviluppatore de `Electrs` e verifichiamo la firma dei commit Github.

```
curl https://romanzey.de/pgp.txt | gpg --import
git verify-tag v$VERSION
```

Se la firma xe coreta podemo passar a la compilazion ...

```
cargo build --locked --release
```

e po a l'instalazion.

```
sudo install -m 0755 -o root -g root -t /usr/local/bin ./target/release/electrs
```

### Step 2b - Configuremo Electrs

Par configurar `Electrs` creemo el file `config.toml` col seguente contenuto.

```
# bitcoin core configuration
auth = "username:password"
daemon_rpc_addr = "127.0.0.1:8332"
daemon_p2p_addr = "127.0.0.1:8333"

# electrs configuration
db_dir = ".electrum"
network = "bitcoin"
electrum_rpc_addr = "127.0.0.1:50001"
log_filters = "INFO"
```

Se pol anca far tuto con un singolo comando da terminale.

```
cat >config.toml <<EOL
# bitcoin core configuration
auth = "username:password"
daemon_rpc_addr = "127.0.0.1:8332"
daemon_p2p_addr = "127.0.0.1:8333"

# electrs configuration
db_dir = ".electrum"
network = "bitcoin"
electrum_rpc_addr = "127.0.0.1:50001"
log_filters = "INFO"
EOL
```

Podemo lanciar Elects col comando

```
electrs --conf config.toml
```

e spetar che electrs finissa de indicizar tuti i blocchi.

### Step 2c - Lancemo Eletrs

Come par Bitcoin podemo lanciar el software creando un script par systemd.

```
sudo  sh -c "cat > /etc/systemd/system/electrs.service <<EOL
[Unit]
Description=Electrs daemon
After=bitcoind.target

[Service]
User=bitcoin
Group=bitcoin
Type=forking
ExecStart=/usr/local/bin/electrs --conf /home/bitcoin/electrs_config.toml
KillMode=process
Restart=always
TimeoutSec=120
RestartSec=30

[Install]
WantedBy=multi-user.target
EOL"
```

Atension: in sto caso stemo doparando l'utente `bitcoin` par far partir el software.

Podemo quindi registrar el script creado e lanciarlo.

```
sudo systemctl enable electrs
sudo systemctl start electrs
```

Ogni volta che se vol controlar el stato del software se pol doparar el seguente comando.

```
systemctl status electrs
```

### Step 3 - Instalemo CLN

Da completar

### Step 3b - Configuremo CLN

Da completar

### Step 4 - Instalemo Mempool.space

Instalemo `mariadb`.

```
sudo apt-get install mariadb-server mariadb-client
```

E creemo db e utente.

```
sudo mysql -e "drop database mempool;"
sudo mysql -e "create database mempool;"
sudo mysql -e "grant all privileges on mempool.* to 'mempool'@'%' identified by 'mempool';"
sudo mysql -e "flush privileges;"
```

Clonemo el codice

```
git clone https://github.com/mempool/mempool
cd mempool
latestrelease=$(curl -s https://api.github.com/repos/mempool/mempool/releases/latest|grep tag_name|head -1|cut -d '"' -f4)
git checkout $latestrelease

```

Assicuremose de doparar node 20.x e l'ultima version de npm.

```
sudo npm i -g npm
sudo npm i -g node@20
```

Provvedemo a compilar e testar el backend

```
cd backend
npm install --no-install-links # npm@9.4.2 and later can omit the --no-install-links
npm run build

cp mempool-config.sample.json mempool-config.json
npm run start
```

Controlar atentamente le configurazioni de `mempool-config.json`.

Passemo al frontend.

```
cd ..

cd frontend
npm install
npm run serve:local-prod
```


### Step 4b - Configuremo Mempool

La configurazion del backend se trova nel file `mempool-config.json`.

### Step 4c - Lancemo Mempool

Podemo lanciar Mempool con pm2, che va instalado.

```
sudo npm i -g pm2
pm2 startup 
```

Lancemo el backend.

```
cd ..
cd backend 
pm2 start "npm run start"
```

Lancemo po el frontend.

```
cd ..
cd frontend
pm2 start "npm run serve:local-prod"
```

Salvemo tuto.

```
pm2 save
```

## Bitcoin con conession solo tramite tor
Scominziemo col instalar tor.


```
sudo apt install tor
```

e impostemo el file de configurazion de tor par crear un novo hidden service esportando la porta 8333 del nodo.


```
cat > /etc/tor/torrc <<EOL
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 8333 127.0.0.1:8333
EOL
```

Podemo riaviar tor par aplicar le modifiche, questo ne permette de esportar la porta 8333 del nostro nodo ma no de limitar l'accesso al nodo solo ed esclusivamente tramite tor.

```
sudo systemctl restart tor
``` 

e otener l'indirizzo onion del nodo.

```
cat /var/lib/tor/hidden_service/hostname
```

Fato cio podemo limitar l'accesso al nodo solo ed esclusivamente tramite tor modificando la configurazion de bitcoin.conf in sto modo:

```
proxy=127.0.0.1:9050
listen=1
bind=127.0.0.1:8333=onion
externalip=tor_url.onion
onlynet=onion
```

Dove `tor_url.onion` xe l'indirizzo onion del nodo otenudo in precedenza.


Riaviando el nodo podemo verificar che el nodo xe acessibile solo ed esclusivamente tramite tor.

```
sudo systemctl restart bitcoind

bitcoin-cli getnetworkinfo
```

Qua dovariimo veder che el nodo xe acessibile solo ed esclusivamente tramite tor, cioe che solo la rete `onion` xe `reachable`.

Inoltre i nostri peer sara tuti identificai da indirizzi onion.

```
bitcoin-cli getpeerinfo
```

Atension: tor xe estremamente lento, tegnive conto de cio co vole sincronizar el nodo partendo da zero.

## Testnet
Na rete utile par impratichirse xe `testnet` che diferisse da `mainnet` in quanto:

- i token no ga valor e ghe xe siti che ve offre satoshi de testnet par efetuar le prove,
- pode transar sempre al minimo de le fee,
- el mining xe flutuante (anca parche no se ghe guadagna gnente),
- in caso che un blocco no vegna minado par 20 minuti la dificolta precipita,
- spesso ghe xe reorg importanti (da sto punto de vista xe pegiore rispetto a mainnet).

Molti wallet (green, electrum, specter, sparrow, ...) supporta testnet e i pol esser doparai par:

- imparar senza meter a rischio i propri fondi,
- par fini didattici,
- par sperimentar robe nove.

Alcuni tool utili (autopromozion) par testnet:

- [BTCBouncer](http://btcbouncer.com) consente de efetuar pagamenti a vari indirizzi e de ricever i fondi (manco na fee) nel arco de un per de blocchi,
- [BTCSigner](http://btcsigner.com) consente de sperimentar un multisig con un nodo core in testnet.

Ghe xe molti altri tool e siti web che supporta testnet oltre ai piu importanti block explorer.

## Bitcoin-cli
Bitcoin-cli xe l'utilita a linea de comando par interagir con Bitcoin Core.

I comandi ga el formato:
```
bitcoin-cli [options] <command> [params]
```
e se pol sempre doparar `help` par gaver la lista dei comandi o informazioni su un comando specifico.

### Comandi informativi su la blockchain Blockchain
- getbestblockhash
- getblock "blockhash"
- getblockchaininfo
- getblockcount
- getblockhash height
- getblockheader "blockhash"
- getmempoolentry "txid"
- getmempoolinfo
- getrawmempool
- gettxoutproof ["txid",...]
- ...

### Comandi de controlo
- help ( "command" )
- stop
- uptime
- ...

### Comandi par el mining
- getblocktemplate ( "template_request" )
- submitblock "hexdata" ( "dummy" )
- ...

### Comandi par la rete
- addnode "node" "command"
- disconnectnode ( "address" nodeid )
- getnetworkinfo
- ...

### Gestion Rawtransactions
- analyzepsbt "psbt"
- combinepsbt ["psbt",...]
- combinerawtransaction ["hexstring",...]
- createpsbt [{"txid":"hex","vout":n,"sequence":n},...] [{"address":amount,...},{"data":"hex"},...] ( locktime replaceable )
- createrawtransaction [{"txid":"hex","vout":n,"sequence":n},...] [{"address":amount,...},{"data":"hex"},...] ( locktime replaceable )
- decodepsbt "psbt"
- decoderawtransaction "hexstring" ( iswitness )
- finalizepsbt "psbt" ( extract )
- getrawtransaction "txid" ( verbose "blockhash" )
- sendrawtransaction "hexstring" ( maxfeerate )
- signrawtransactionwithkey "hexstring" ["privatekey",...] ( [{"txid":"hex","vout":n,"scriptPubKey":"hex","redeemScript":"hex","witnessScript":"hex","amount":amount},...] "sighashtype" )
- testmempoolaccept ["rawtx",...] ( maxfeerate )
- ...

### Utility
- signmessagewithprivkey "privkey" "message"
- validateaddress "address"
- verifymessage "address" "signature" "message"
- ...

### Wallet
- createwallet "wallet_name" ( disable_private_keys blank "passphrase" avoid_reuse descriptors load_on_startup external_signer )
- getaddressinfo "address"
- getbalance ( "dummy" minconf include_watchonly avoid_reuse )
- getnewaddress ( "label" "address_type" )
- gettransaction "txid" ( include_watchonly verbose )
- getwalletinfo
- importaddress "address" ( "label" rescan p2sh )
- importdescriptors "requests"
- importprivkey "privkey" ( "label" rescan )
- listunspent ( minconf maxconf ["address",...] include_unsafe query_options )
- lockunspent unlock ( [{"txid":"hex","vout":n},...] persistent )
- rescanblockchain ( start_height stop_height )
- send [{"address":amount,...},{"data":"hex"},...] ( conf_target "estimate_mode" fee_rate options )
- sendmany "" {"address":amount,...} ( minconf "comment" ["address",...] replaceable conf_target "estimate_mode" fee_rate verbose )
- sendtoaddress "address" amount ( "comment" "comment_to" subtractfeefromamount replaceable conf_target "estimate_mode" signmessage "address" "message"
- signrawtransactionwithwallet "hexstring" ( [{"txid":"hex","vout":n,"scriptPubKey":"hex","redeemScript":"hex","witnessScript":"hex","amount":amount},...] "sighashtype" )
- ...

Un corso completo su l'uso de Bitcoin da linea de comandi se pol trovar a l'indirizzo [Learning-Bitcoin-from-the-Command-Line](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line).

## Programa
L'instalazion del nodo xe divisa su piu lezioni, qua un elenco de quele za tegnude:

| Data        | Note                                           |
|-------------|------------------------------------------------|
| 240108-2100 | Selezion de l'hardware                        |
| 240115-2200 | Instalazion de core e verifica firme          |
| 240122-2200 | Configurazion minimale                        |
| 240129-2200 | Testnet                                        |
| 240205-2200 | bitcoind-cli                                   |
| 240711-2200 | electrs                                        |
