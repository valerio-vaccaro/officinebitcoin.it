# Fullnode e hardware per un nod

Avè un nod Bitcoin l'è fondamental poiché permet con la massima privacy de:

- validà l'intera cadena de Bitcoin,
- controllà el bilancio de i nostri wallet,
- trasmetter le nostre noeuv transazion
- ...

## Selezion de l'hardware

- minimo 2GB (raccomandad 4GB) de memoria RAM,
- disc de almen 1TB (raccomandad 2TB) de memoria de massa,
- cpu multi-core sufficentement performant (probabilment qualsivoglia processor sviluppad nell'ultim decenni).

### Riutilizza un vecc computer

Un vecc computer pö vess riciclad come nod, in cas de laptop se raccomanda de rimov la batteria che, posta semper sott carica, podaria costituì un risch. El grand vantagg l'è dat dal cost pari a zero o limità domà al disc pù capient.

### Raspberry pi e alter sched

Raspberry pi l'è una scheda ARM molt doprada per la realizzazion de sistemi IoT e nod, el cost eccessiv e la necessità de un disc su presa USB tuttavia la rend minga la miglior de le scelte possibil in termin de performance e de stabilità.

Odroid-M1 l'è una scheda ARM performant e con un slot intern per l'aggiunta de memoria de massa aggiuntiva.

### Thin client

Con un budget molt ridott 30-100 euro l'è possibil acquistà un Thin Client doprà (su ebay) che associa bass consum a performance sufficent per fà girà el nod.

Come esempi de Thin Client hann staa testad i seguent modell:

- Fujitsu Futro s920
- HP t620

## Selezion del software

Installà men software possibil su un nod limita i possibil attacc e rend el sistema pù sempliz da mantegnì.

Online se troven soluzion preconfezionad (Umbrel, Mynode, ...) che mascaren i check de sicurezza e aggiungen software e script (per esempi docker) de difficil controll. In queste lezion porrem l'attenzion sulla creazion de un nod a man ovvero installand manualment tutt i software necessari.

### Step 0 - El sistema operativ

La prima scelta da fà l'è el sistema operativ, el consigli l'è de doprà Linux in una version LTS ovvero in cui sia garantì support per un numer sufficentement long de agn. La mia personal scelta ricad su Debian 12.

El sistema operativ scelt va quindi installà sul computer e vann aggiornad tutt i pacchett (l'aggiornament l'è qualcosa che seguirà durant tutta la vita del nod).

Se raccomanda anca de installà tor (e/o altera VPN se necessaria) e ssh così da permet la manutenzion remota del nod.

Un grupp de continuità infine podaria salvà el nod da brusc cal de corrente evitand de lassà bitcoin e gli alter software in un stat inconsistent.

### Step 1 - Installem Bitcoin

Scarich core, gli hash e le firm.

```
wget https://bitcoincore.org/bin/bitcoin-core-28.1/bitcoin-28.1-x86_64-linux-gnu.tar.gz
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS.asc
```

In cas se dopri una board dotad de architettura arm el pacchett andrà corret in `bitcoin-28.1-aarch64-linux-gnu.tar.gz` ovvero nel medem pacchett ma compilad per l'architettura arm a 64 bit (aarch64) che l'è propri quella doprada da odroid.

A quest punt podem controllà che un de gli hash in SHA256SUM corrisponda all'archivi scaricad.

```
sha256sum --ignore-missing --check SHA256SUMS
```

El risultat segnala che l'è stada trovada una corrispondenza per l'archivi scaricad.

```
bitcoin-28.1-x86_64-linux-gnu.tar.gz: OK
```

Verifichiem ora le firm del file SHA256SUM, prima se necessari procurass le claav e importemle.

```
git clone https://github.com/bitcoin-core/guix.sigs
gpg --import guix.sigs/builder-keys/*
```

E infine verifichiem le firm.

```
gpg --verify SHA256SUMS.asc
```

Se vedaremm parecch volt la scritta `gpg: Good signature from ...` völ dì che hem trovad de le firm valid.

Procedem allo scompattament e all'installazion 

```
tar xzvf bitcoin-28.1-x86_64-linux-gnu.tar.gz 
sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-28.1/bin/*
```

E sem, ora hem `bitcoind`, `bitcoin-cli` e le alter utilità pronte per vess lanciad.

Per ora lanciem `bitcoind` e vedaremm un po de log. Bitcoin incomincia a sincronizzass e ora sarà present una directory con la blockchain e tutt le configurazion in `~/.bitcoin/`.

De un alter terminal podem controllà el funzionament de bitcoind lanciand el comand `tail -f ~/.bitcoin/debug.log`.

### Step 1b - Configurem Bitcoin

Come hem già vedud precedentement la directory in cui Bitcoin core salva le configurazion e la blockchain l'è directory `~/.bitcoin/` per quant riguarda el sistema operativ Linux, nel cas se voless cambà la posizion de salvatagg se poden doprà different approcci:

- creà un link simbolic de la directory su un disc pù grand mediante el comand `ln -s`,
- doprà da linea de comand o all'intern de bitcoin.conf el comand `datadir` specificand la directory de destinazion.

Bitcoin Core supporta tre tipolog de ret a cui connettess:
- `mainnet`, questa l'è la classica ret a cui tutt sem abituad e l'è el default per core,
- `testnet`, questa ret l'è analoga a mainnet ma i token minga hann alcun valor, el mining vegn semper effettuad ma in cas de assenza de blocch per 20 minutt la difficoltà vegn fatta precipità (soffr de reorg spesso important),
- `regtest`, in questa modalità se gh'ha una piccola blockchain privada che part semper da zero e in cui l'è possibil minà a difficoltà minima (serv per test local).

Un alter comand util l'è `daemon` che, se settad, minga mantegn el log de bitcoin core collegad alla console attual, per ved el funzionament sarà semper possibil doprà el comand `tail -f ~/.bitcoin/debug.log`.

Tutt le configurazion poden vess lanciad da linea de comand o tramit el file `~/.bitcoin/bitcoin.conf`, un file compatibil con un setup casaling (ovvero in cui vöret mantegnì el consum de risors al minim) podaria vess el seguent.
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

In cui el:

- server l'è scollegad de la console con `daemon=1`
- vann scaricad i sol blocch e minga la mempool `blocksonly=1`
- vann permess fin a vint connession `txindex=1`
- se spedissen informazion agli alter nod in internet per un massim de 500 megabyte al dì `maxuploadtarget=500`
- se mantegn un indice de le transazion `txindex=1`
- se mantegn un indice de i blockfilter `blockfilterindex=1`
- dem la possibilità a chiunque de collegass tramit rpc `rpcallowip=0.0.0.0/0`
- collegh rpc a tutt le sched de ret `rpcallowip=0.0.0.0/0`
- settem un username per rpc `rpcuser=username` (ovviament da sostituì)
- settem una password per rpc `rpcpassword=password` (ovviament da sostituì)

L'elenco complet de le funzionalità se pö trovà su [https://jlopp.github.io/bitcoin-core-config-generator](https://jlopp.github.io/bitcoin-core-config-generator)

Se pö anca fà tutt con un singol comand da terminal.

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

Qualora se gh'abbia a disposizion un alter nod già sincronizad se pö doprà l'opzion `connect` per collegass SOLO ED ESCLUSIVAMENT a quest nod, se tal nod l'è in ret local se guadagna temp e banda con questa sempliz configurazion.

Dalla release 26 core supporta crittazion de le comunicazion tra i nod con l'opzion `v2transport`.

Tutt le configurazion mostrad hann relative a clearnet, le configurazion per tor saran oggett de un'altera lezion.

### Step 1c - Lanciem Bitcoin

Lanciem Bitcoin costruend un file de lanci per systemd.

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
Attenzion: in quest cas stiam doprand l'utent `bitcoin` per fà partì el software.

Podem quindi registrà el script cread e lanciàll.

```
sudo systemctl enable bitcoind
sudo systemctl start bitcoind
```

Ogni volt che se vöret controllà el stat del software se pö doprà el seguent comand.

```
systemctl status bitcoind
```

### Step 2 - Installem Electrs

Installem `Electrs` che l'è un electrum server basad su `Rust`, el prim step l'è quindi installà tal linguagg.

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Installem anca clang e el pacchett build-essential.

```
apt update
apt install clang cmake build-essential -y
```

Scarich l'ultima version (attualment la 0.10.5) da Github.

```
VERSION="0.10.5"
git clone --branch v$VERSION https://github.com/romanz/electrs.git
cd electrs
```

Importem la claav del sviluppator de `Electrs` e verifichiem la firma de i commit Github.

```
curl https://romanzey.de/pgp.txt | gpg --import
git verify-tag v$VERSION
```

Se la firma l'è corretta podem passà alla compilazion ...

```
cargo build --locked --release
```

e poi all'installazion.

```
sudo install -m 0755 -o root -g root -t /usr/local/bin ./target/release/electrs
```

### Step 2b - Configurem Electrs

Per configurà `Electrs` creem el file `config.toml` con el seguent contenut.

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

Se pö anca fà tutt con un singol comand da terminal.

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

Podem lancià Elects con el comand

```
electrs --conf config.toml
```

e aspettà che electrs finissa de indicizzà tutt i blocch.

### Step 2c - Lanciem Eletrs

Come per Bitcoin podem lancià el software creand un script per systemd.

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

Attenzion: in quest cas stiam doprand l'utent `bitcoin` per fà partì el software.

Podem quindi registrà el script cread e lanciàll.

```
sudo systemctl enable electrs
sudo systemctl start electrs
```

Ogni volt che se vöret controllà el stat del software se pö doprà el seguent comand.

```
systemctl status electrs
```

### Step 3 - Installem CLN

TBD

### Step 3b - Configurem CLN

TBD

### Step 4 - Installem Mempool.space

Installem `mariadb`.

```
sudo apt-get install mariadb-server mariadb-client
```

E creem db e utent.

```
sudo mysql -e "drop database mempool;"
sudo mysql -e "create database mempool;"
sudo mysql -e "grant all privileges on mempool.* to 'mempool'@'%' identified by 'mempool';"
sudo mysql -e "flush privileges;"
```

Clonem el codice

```
git clone https://github.com/mempool/mempool
cd mempool
latestrelease=$(curl -s https://api.github.com/repos/mempool/mempool/releases/latest|grep tag_name|head -1|cut -d '"' -f4)
git checkout $latestrelease

```

Assicurass de doprà node 20.x e l'ultima version de npm.

```
sudo npm i -g npm
sudo npm i -g node@20
```

Provvedem a compilà e testà el backend

```
cd backend
npm install --no-install-links # npm@9.4.2 and later can omit the --no-install-links
npm run build

cp mempool-config.sample.json mempool-config.json
npm run start
```

Controllà attentament le configurazion de `mempool-config.json`.

Passem al frontend.

```
cd ..

cd frontend
npm install
npm run serve:local-prod
```


### Step 4b - Configurem Mempool

La configurazion del backend se trova nel file `mempool-config.json`.

### Step 4c - Lanciem Mempool

Podem lancià Mempool con pm2, che va installà.

```
sudo npm i -g pm2
pm2 startup 
```

Lanciem el backend.

```
cd ..
cd backend 
pm2 start "npm run start"
```

Lanciem poi el frontend.

```
cd ..
cd frontend
pm2 start "npm run serve:local-prod"
```

Salvem el tutt.

```
pm2 save
```

## Bitcoin con connession domà tramit tor
Iniziem con l'installà tor.


```
sudo apt install tor
```

e impostem el file de configurazion de tor per creà un noeuv hidden service esportand la porta 8333 del nod.


```
cat > /etc/tor/torrc <<EOL
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 8333 127.0.0.1:8333
EOL
```

Podem riavvì tor per applicà le modifiche, quest permet de esportà la porta 8333 del nostro nod ma minga de limità l'access al nod domà ed esclusivament tramit tor.

```
sudo systemctl restart tor
``` 

e otten l'indirizz onion del nod.

```
cat /var/lib/tor/hidden_service/hostname
```

Fad ciò podem limità l'access al nod domà ed esclusivament tramit tor modificand la configurazion de bitcoin.conf in quest mod:

```
proxy=127.0.0.1:9050
listen=1
bind=127.0.0.1:8333=onion
externalip=tor_url.onion
onlynet=onion
```

Dove `tor_url.onion` l'è l'indirizz onion del nod ottenud in precedenza.


Riavviand el nod podem verificà che el nod l'è accessibil domà ed esclusivament tramit tor.

```
sudo systemctl restart bitcoind

bitcoin-cli getnetworkinfo
```

Qui dovriem ved che el nod l'è accessibil domà ed esclusivament tramit tor, ovvero che domà la ret `onion` l'è `reachable`.

Inoltre i nostri peer saran tutt identificad da indirizz onion.

```
bitcoin-cli getpeerinfo
```

Attenzion: tor l'è estremament lent, tenì cont de ciò quand vöret sincronizzà el nod partend da zero.

## Testnet
Un util ret per impratichiss l'è `testnet` che differiss da `mainnet` in quant:

- i token minga hann valor e gh'hen sit che te offren satoshi de testnet per effettuà le prove,
- podet transà semper al minim de le fee,
- el mining l'è fluttuant (anca perchè minga se guadagna nient),
- in cas che un blocch minga vegna minad per 20 minutt la difficoltà precipita,
- spesso gh'hen reorg important (da quest punt de vista l'è peggior rispett a mainnet).

Molti wallet (green, electrum, specter, sparrow, ...) supporten testnet e poden vess doprad per:

- imparà sensa mett a risch i propri fond,
- per fin didattic,
- per sperimentà cose noeuv.

Alcun tool util (autopromozion) per testnet:

- [BTCBouncer](http://btcbouncer.com) permet de effettuà pagament a vari indirizz e de ricev i fond (men una fee) nell'arco de un par de blocch,
- [BTCSigner](http://btcsigner.com) permet de sperimentà un multisig con un nod core in testnet.

Gh'hen molt alter tool e sit web che supporten testnet oltra ai pù important block explorer.

## Bitcoin-cli
Bitcoin-cli l'è l'utilità a linea de comand per interagì con Bitcoin Core.

I comand hann el format:
```
bitcoin-cli [options] <command> [params]
```
e se pö semper doprà `help` per avè la lista de i comand o informazion su un specific comand.

### Comand informativ sulla blockchain Blockchain
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

### Comand de controll
- help ( "command" )
- stop
- uptime
- ...

### Comand per el mining
- getblocktemplate ( "template_request" )
- submitblock "hexdata" ( "dummy" )
- ...

### Comand per la ret
- addnode "node" "command"
- disconnectnode ( "address" nodeid )
- getnetworkinfo
- ...

### Gestión Rawtransactions
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

Un cors complet sull'us de Bitcoin da linea de comand se pö trovà all'indirizz [Learning-Bitcoin-from-the-Command-Line](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line).

## Program
L'installazion del nod l'è divisa su pù lezion, qui un elenco de quelle già tenuu:

| Data        | Note                                           |
|-------------|------------------------------------------------|
| 240108-2100 | Selezion de l'hardware                        |
| 240115-2200 | Installazion de core e verifica firm         |
| 240122-2200 | Configurazion minimal                        |
| 240129-2200 | Testnet                                        |
| 240205-2200 | bitcoind-cli                                   |
| 240711-2200 | electrs                                        | 