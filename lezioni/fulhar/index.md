# Fullnode ed hardware per un nodo

Avere un nodo Bitcoin è fondamentale in quanto consente con la massima privacy di:

- validare l'intera catena di Bitcoin,
- controllare il bilancio dei nostri wallet,
- trasmettere le nostre nuove transazioni
- ...

## Selezione dell'hardware

- minimo 2GB (consigliati 4GB) di memoria RAM,
- disco di almeno 1TB (consigliati 2TB) di memoria di massa,
- cpu multi-core sufficientemente performante (probabilmente qualsiasi processore sviluppato nell'ultimo decennio).

### Riutilizza un vecchio computer

Un vecchio computer può essere riciclato come nodo, in caso di laptop si consiglia di rimuovere la batteria che, posta sempre sotto carica, potrebbe costituire un rischio. Il grande vantaggio è dato dal costo pari a zero o limitato solo al disco più capiente.

### Raspberry pi ed altre schede

Raspberry pi è una scheda ARM molto utilizzata per la realizzazione di sistemi IoT e nodi, il costo eccessivo e la necessità di un disco su presa USB tuttavia la rendono non la migliore delle scelte possibili in termini di performance e di stabilità.

Odroid-M1 è una scheda ARM performante e con uno slot interno per l'aggiunta di memoria di massa aggiuntiva.

### Thin client

Con un budget molto ridotto 30-100 euro è possibile acquistare un Thin Client usato (su ebay) che associa bassi consumi a performance sufficienti a far girare il nodo.

Come esempi di Thin Client sono stati testati i seguenti modelli:

- Fujitsu Futro s920
- HP t620

## Selezione del software

Installare meno software possibile su di un nodo limita i possibili attacchi e rende il sistema più semplice da mantenere.

Online si trovano soluzioni preconfezionate (Umbrel, Mynode, ...) che mascherano i check di sicurezza ed aggiungono software e script (ad esempio docker) di difficile controllo. In queste lezioni porremo l'attenzione sulla creazione di un nodo a mano ovvero installando manualmente tutti i software necessari.

### Step 0 - Il sistema operativo

La prima scelta da fare è il sistema operativo, il consiglio è di utilizzare Linux in una versione LTS ovvero in cui sia garantito supporto per un numero sufficientemente lungo di anni. La mia personale scelta ricade su Debian 12.

Il sistema operativo scelto va quindi installato sul computer e vanno aggiornati tutti i pacchetti (l'aggiornamento è qualcosa che ci seguirà durante tutta la vita del nodo).

Si consiglia anche di installare tor ( e/o altra VPN se necessaria) ed ssh così da permettere la manutenzione remota del nodo.

Un gruppo di continuità infine potrebbe salvare il nodo da bruschi cali di corrente evitando di lasciare bitcoin e gli altri software in uno stato inconsistente.

### Step 1 - Installiamo Bitcoin

Scarichiamo core, gli hash e le firme.

```
wget https://bitcoincore.org/bin/bitcoin-core-28.1/bitcoin-28.1-x86_64-linux-gnu.tar.gz
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS.asc
```

In caso si utilizzi una board dotata di architettura arm il pacchetto andrà corretto in `bitcoin-28.1-aarch64-linux-gnu.tar.gz` ovvero nel medesimo pacchetto ma compilato per l'architettura arm a 64 bit (aarch64) che è proprio quella utilizzata da odroid.

A questo punto possiamo controllare che uno degli hash in SHA256SUM corrisponda all'archivio scaricato.

```
sha256sum --ignore-missing --check SHA256SUMS
```

Il risultato ci segnala che è stata trovata una corrispondenza per l'archivio scaricato.

```
bitcoin-28.1-x86_64-linux-gnu.tar.gz: OK
```

Verifichiamo ora le firme del file SHA256SUM, prima se necessario procuriamoci le chiavi ed importiamole.

```
git clone https://github.com/bitcoin-core/guix.sigs
gpg --import guix.sigs/builder-keys/*
```

Ed infine verifichiamo le firme.

```
gpg --verify SHA256SUMS.asc
```

Se vedremo parecchie volte la scritta `gpg: Good signature from ...` vuol dire che abbiamo trovato delle firme valide.

Procediamo allo scompattamento e all'installazione 

```
tar xzvf bitcoin-28.1-x86_64-linux-gnu.tar.gz 
sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-28.1/bin/*
```

E ci siamo, ora abbiamo `bitcoind`, `bitcoin-cli` e le altre utilità pronte per essere lanciate.

Per ora lanciamo `bitcoind` e vedremo un po di log. Bitcoin incomincia a sincronizzarsi ed ora sarà present una directory con la blockchain e tutte le configurazioni in `~/.bitcoin/`.

Da un altro terminale possiamo controllare il funzionamento di bitcoind lanciando il comando `tail -f ~/.bitcoin/debug.log`.

### Step 1b - Configuriamo Bitcoin

Come abbiamo già visto precedentemente la directory in cui Bitcoin core salva le configurazioni e la blockchain è directory `~/.bitcoin/` per quanto riguarda il sistema operativo Linux, nel caso si volesse cambiare la posizione di salvataggio si possono usare differenti approcci:

- creare un link simbolico della directory su di un disco più grande mediante il comando `ln -s`,
- usare da linea di comando o all'interno di bitcoin.conf il comando `datadir` specificando la directory di destinazione.

Bitcoin Core supporta tre tipologie diverse di reti a cui connettersi:
- `mainnet`, questa è la classica rete a cui tutti siamo abituati ed è il default per core,
- `testnet`, questa rete è analoga a mainnet ma i token non hanno alcun valore, il mining viene sempre effettuato ma in caso di assenza di blocchi per 20 minuti la difficoltà viene fatta precipitare (soffre di reorg spesso importanti),
- `regtest`, in questa modalità si ha una piccola blockchain privata che parte sempre da zero ed in cui è possibile minare a difficoltà minima (serve per test locali).

Un altro comando utile è `daemon` che, se settato, non mantiene il log di bitcoin core collegato alla console attuale, per vedere il funzionamento sarà sempre possibile usare il comando `tail -f ~/.bitcoin/debug.log`.

Tutte le configurazioni possono essere lanciate da linea di comando o tramite il file `~/.bitcoin/bitcoin.conf`, un file compatibile con un setup casalingo (ovvero in cui voglio mantenere il consumo di risorse al minimo) potrebbe essere il seguente.
file di configurazione

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

In cui il:

- server è scolleato dalla console con `daemon=1`
- vengono scaricati i solo blocchi e non la mempool `blocksonly=1`
- sono permesse fino a venti connessioni `txindex=1`
- si spediscono informazioni agli altri nodi in internet per un massimo di 500 megabyte al giorno `maxuploadtarget=500`
- si mantiene un indice delle transazioni `txindex=1`
- si mantiene un indice dei blockfilter `blockfilterindex=1`
- diamo la possibilità a chiunque di collegarsi tramite rpc `rpcallowip=0.0.0.0/0`
- colleghiamo rpc a tutte le schede di rete `rpcallowip=0.0.0.0/0`
- settimao uno username per rpc `rpcuser=username` (ovviamente da sostituire)
- settiamo una password per rpc `rpcpassword=password` (ovviamente da sostituire)

L'elenco completo delle funzionalità si può trovate su [https://jlopp.github.io/bitcoin-core-config-generator](https://jlopp.github.io/bitcoin-core-config-generator)

Si può anche fare tutto con un singolo comando da terminale.

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

Qualora si abbia a disposizione un altro nodo già sincronizzato si puo usare l'opzione `connect` per collegarsi SOLO ED ESCLUSIVAMENTE a questo nodo, se tale nodo è in rete locale si guadagna tempo e banda con questa semplice configurazione.

Dalla release 26 core supporta crittazione delle comunicazioni tra i nodi con l'opzione `v2transport`.

Tutte le configuarazioni mostrate sono relative a clearnet, le configurazioni per tor saranno oggetto di un'altra lezione.

### Step 1c - Lanciamo Bitcoin

Lanciamo Bitcoin costruendo un file di lancio per systemd.

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
Attenzione: in questo caso stiamo utilizzando l'utente `bitcoin` per far partire il software.

Possiamo quindi regitrare lo script creato e lanciarlo.

```
sudo systemctl enable bitcoind
sudo systemctl start bitcoind
```

Ogni volta che si vuole controllare lo stato del software si può utilizzare il seguente comando.

```
systemctl status bitcoind
```

### Step 2 - Installiamo Electrs

Installiamo `Electrs` che è un electrum server basato su `Rust`, il primo step è quindi installare tale linguaggio.

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Installiamo anche clang ed il pacchetto build-essential.

```
apt update
apt install clang cmake build-essential -y
```

Scarichiamo l'ultima versione (attualmente la 0.10.5) da Github.

```
VERSION="0.10.5"
git clone --branch v$VERSION https://github.com/romanz/electrs.git
cd electrs
```

Importiamo la chiave dello sviluppatore di `Electrs` e verifichiamo la firma dei commit Github.

```
curl https://romanzey.de/pgp.txt | gpg --import
git verify-tag v$VERSION
```

Se la firma è corretta possiamo passare alla compilazione ...

```
cargo build --locked --release
```

e poi all'installazione.

```
sudo install -m 0755 -o root -g root -t /usr/local/bin ./target/release/electrs
```

### Step 2b - Configuriamo Electrs

Per configurare `Electrs` creiamo il file `config.toml` con il seguente contenuto.

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

Si può anche fare tutto con un singolo comando da terminale.

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

Possiamo lanciare Elects con il comando

```
electrs --conf config.toml
```

e aspettare che electrs finisca di indicizzare tutti i blocchi.

### Step 2c - Lanciamo Eletrs

Come per Bitcoin possiamo lanciare il software creando uno script per systemd.

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

Attenzione: in questo caso stiamo utilizzando l'utente `bitcoin` per far partire il software.

Possiamo quindi regitrare lo script creato e lanciarlo.

```
sudo systemctl enable electrs
sudo systemctl start electrs
```

Ogni volta che si vuole controllare lo stato del software si può utilizzare il seguente comando.

```
systemctl status electrs
```

### Step 3 - Installiamo CLN

TBD

### Step 3b - Configuriamo CLN

TBD

## Testnet
Un utile rete per impratichirsi è `testnet` che differisce da `mainnet` in quanto:

- i token non hanno valore e ci sono siti che vi offrono satoshi di testnet per effettuare le prove,
- potete transare sempre al minimo delle fee,
- il mining è fluttuante (anche perchè non ci si guadagna nulla),
- in caso che un blocco non venga minato per 20 minuti la difficoltà precipita,
- spesso ci sono reorg importanti (da questo punto di vista è peggiore rispetto a mainnet).

Molti wallet (green, electrum, specter, sparrow, ...) supportano testnet e possono essere usati per:

- imparare senza mettere a rischio i propri fondi,
- per fini didattici,
- per sperimentare cose nuove.

Alcuni tool utili (autopromozione) per testnet:

- [BTCBouncer](http://btcbouncer.com) consete di effettuare pagamenti a vari indirizzi e di ricevere i fondi (meno una fee) nell'arco di un paio di blocchi,
- [BTCSigner](http://btcsigner.com) consete di sperimentare un multisig con un nodo core in testnet.

Ci sono molto altri tool e siti web che supportano testnet oltre ai più importanti block explorer.

## Bitcoin-cli
Bitcoin-cli è l'utilità a line di comando per interagire con Bitcoin Core.

I comandi hanno il formato:
```
bitcoin-cli [options] <command> [params]
```
e si può sempre usare `help` per avere la lista dei comandi o informazioni su di uno specifico comando.

### Comandi informativi sulla blockchain Blockchain
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

### Comandi di controllo
- help ( "command" )
- stop
- uptime
- ...

### Comandi per il mining
- getblocktemplate ( "template_request" )
- submitblock "hexdata" ( "dummy" )
- ...

### Comandi per la rete
- addnode "node" "command"
- disconnectnode ( "address" nodeid )
- getnetworkinfo
- ...

### Gestione Rawtransactions
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

Un corso completo sull'uso di Bitcoin da linea di comandi si può trovare all'indirizzo [Learning-Bitcoin-from-the-Command-Line](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line).

## Programma
L'installazione del nodo è divisa su più lezioni, qui un elenco di quelle già tenute:

| Data        | Note                                           |
|-------------|------------------------------------------------|
| 240108-2100 | Selezione dell'hardware                        |
| 240115-2200 | Installazione di core e verifica firme         |
| 240122-2200 | Configurazione minimale                        |
| 240129-2200 | Testnet                                        |
| 240205-2200 | bitcoind-cli                                   |
| 240711-2200 | electrs                                        |
