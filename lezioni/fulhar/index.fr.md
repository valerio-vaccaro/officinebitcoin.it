---
layout: default
title: "Fullnode et matériel pour un nœud"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Leçon Bitcoin-only</span> <span>Ce projet est maintenu par valerio-vaccaro</span></p>

## 🌍 Traductions

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Fullnode et matériel pour un nœud

Avoir un nœud Bitcoin est fondamental, car il permet avec un maximum de confidentialité de :

- valider toute la chaîne de Bitcoin,
- contrôler le solde de nos wallets,
- transmettre nos nouvelles transactions,
- ...

## Choix du matériel

- minimum 2GB de RAM, 4GB recommandés,
- disque d'au moins 1TB de stockage, 2TB recommandés,
- cpu multi-core suffisamment performante, probablement n'importe quel processeur développé au cours de la dernière décennie.

### Réutiliser un vieil ordinateur

Un vieil ordinateur peut être recyclé comme nœud. Dans le cas d'un laptop, il est conseillé de retirer la batterie qui, toujours en charge, pourrait représenter un risque. Le grand avantage est le coût nul, ou limité seulement au disque plus capacitif.

### Raspberry pi et autres cartes

Raspberry pi est une carte ARM très utilisée pour réaliser des systèmes IoT et des nœuds. Toutefois, son coût excessif et la nécessité d'un disque sur port USB en font un choix qui n'est pas le meilleur possible en termes de performances et de stabilité.

Odroid-M1 est une carte ARM performante avec un slot interne pour ajouter du stockage supplémentaire.

### Thin client

Avec un budget très réduit, 30-100 euros, il est possible d'acheter un Thin Client d'occasion, sur ebay, qui associe faible consommation et performances suffisantes pour faire tourner le nœud.

Les modèles de Thin Client suivants ont été testés comme exemples :

- Fujitsu Futro s920
- HP t620

## Choix du logiciel

Installer le moins de logiciels possible sur un nœud limite les attaques possibles et rend le système plus simple à maintenir.

On trouve en ligne des solutions prêtes à l'emploi, comme Umbrel, Mynode et autres, qui masquent les contrôles de sécurité et ajoutent des logiciels et scripts, par exemple docker, difficiles à contrôler. Dans ces leçons, nous nous concentrerons sur la création d'un nœud à la main, c'est-à-dire en installant manuellement tous les logiciels nécessaires.

### Étape 0 - Le système d'exploitation

Le premier choix à faire est celui du système d'exploitation. Le conseil est d'utiliser Linux dans une version LTS, c'est-à-dire avec un support garanti pendant un nombre d'années suffisamment long. Mon choix personnel est Debian 12.

Le système d'exploitation choisi doit ensuite être installé sur l'ordinateur et tous les paquets doivent être mis à jour. La mise à jour nous accompagnera pendant toute la vie du nœud.

Il est aussi conseillé d'installer tor, et/ou un autre VPN si nécessaire, ainsi que ssh, afin de permettre la maintenance distante du nœud.

Enfin, un onduleur pourrait sauver le nœud des coupures brutales de courant, en évitant de laisser bitcoin et les autres logiciels dans un état incohérent.

### Étape 1 - Installons Bitcoin

Téléchargeons core, les hashes et les signatures.

```
wget https://bitcoincore.org/bin/bitcoin-core-28.1/bitcoin-28.1-x86_64-linux-gnu.tar.gz
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS.asc
```

Si l'on utilise une board dotée d'une architecture arm, le paquet devra être corrigé en `bitcoin-28.1-aarch64-linux-gnu.tar.gz`, c'est-à-dire le même paquet mais compilé pour l'architecture arm 64 bits, aarch64, qui est précisément celle utilisée par odroid.

Nous pouvons maintenant vérifier qu'un des hashes dans SHA256SUMS correspond à l'archive téléchargée.

```
sha256sum --ignore-missing --check SHA256SUMS
```

Le résultat nous signale qu'une correspondance a été trouvée pour l'archive téléchargée.

```
bitcoin-28.1-x86_64-linux-gnu.tar.gz: OK
```

Vérifions maintenant les signatures du fichier SHA256SUMS. Au besoin, récupérons d'abord les clés et importons-les.

```
git clone https://github.com/bitcoin-core/guix.sigs
gpg --import guix.sigs/builder-keys/*
```

Et enfin vérifions les signatures.

```
gpg --verify SHA256SUMS.asc
```

Si nous voyons plusieurs fois le texte `gpg: Good signature from ...`, cela signifie que nous avons trouvé des signatures valides.

Procédons à la décompression et à l'installation.

```
tar xzvf bitcoin-28.1-x86_64-linux-gnu.tar.gz 
sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-28.1/bin/*
```

Nous y sommes : nous avons maintenant `bitcoind`, `bitcoin-cli` et les autres utilitaires prêts à être lancés.

Pour l'instant, lançons `bitcoind` et nous verrons un peu de log. Bitcoin commence à se synchroniser et un répertoire contenant la blockchain et toutes les configurations sera présent dans `~/.bitcoin/`.

Depuis un autre terminal, nous pouvons contrôler le fonctionnement de bitcoind en lançant la commande `tail -f ~/.bitcoin/debug.log`.

### Étape 1b - Configurons Bitcoin

Comme nous l'avons déjà vu, le répertoire dans lequel Bitcoin Core enregistre les configurations et la blockchain sous Linux est `~/.bitcoin/`. Si l'on souhaite changer l'emplacement d'enregistrement, plusieurs approches sont possibles :

- créer un lien symbolique du répertoire vers un disque plus grand avec la commande `ln -s`,
- utiliser en ligne de commande ou dans bitcoin.conf la commande `datadir` en indiquant le répertoire de destination.

Bitcoin Core prend en charge trois types de réseaux auxquels se connecter :
- `mainnet`, le réseau classique auquel nous sommes tous habitués et qui est le défaut de core,
- `testnet`, un réseau analogue à mainnet mais dont les tokens n'ont aucune valeur ; le mining est toujours effectué, mais en absence de blocs pendant 20 minutes, la difficulté chute fortement ; il souffre souvent de reorg importants,
- `regtest`, mode dans lequel on dispose d'une petite blockchain privée qui repart toujours de zéro et où il est possible de miner à difficulté minimale ; il sert aux tests locaux.

Une autre commande utile est `daemon`, qui, si elle est définie, ne garde pas le log de Bitcoin Core attaché à la console actuelle. Pour voir le fonctionnement, il sera toujours possible d'utiliser `tail -f ~/.bitcoin/debug.log`.

Toutes les configurations peuvent être lancées en ligne de commande ou au moyen du fichier `~/.bitcoin/bitcoin.conf`. Un fichier compatible avec un setup domestique, où je veux maintenir la consommation de ressources au minimum, pourrait être le suivant.
fichier de configuration

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

Où :

- le serveur est détaché de la console avec `daemon=1`
- seuls les blocs sont téléchargés, et non la mempool, `blocksonly=1`
- jusqu'à vingt connexions sont permises, `txindex=1`
- on envoie des informations aux autres nœuds sur internet jusqu'à un maximum de 500 mégaoctets par jour, `maxuploadtarget=500`
- un index des transactions est maintenu, `txindex=1`
- un index des blockfilter est maintenu, `blockfilterindex=1`
- nous donnons à quiconque la possibilité de se connecter via rpc, `rpcallowip=0.0.0.0/0`
- nous lions rpc à toutes les interfaces réseau, `rpcallowip=0.0.0.0/0`
- nous définissons un username pour rpc, `rpcuser=username`, évidemment à remplacer
- nous définissons une password pour rpc, `rpcpassword=password`, évidemment à remplacer

La liste complète des fonctionnalités se trouve sur [https://jlopp.github.io/bitcoin-core-config-generator](https://jlopp.github.io/bitcoin-core-config-generator)

On peut aussi tout faire avec une seule commande de terminal.

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

Si l'on dispose d'un autre nœud déjà synchronisé, on peut utiliser l'option `connect` pour se connecter UNIQUEMENT ET EXCLUSIVEMENT à ce nœud. Si ce nœud est sur le réseau local, on gagne du temps et de la bande passante avec cette configuration simple.

Depuis la release 26, core prend en charge le chiffrement des communications entre les nœuds avec l'option `v2transport`.

Toutes les configurations montrées concernent clearnet ; les configurations pour tor feront l'objet d'une autre leçon.

### Étape 1c - Lançons Bitcoin

Lançons Bitcoin en construisant un fichier de lancement pour systemd.

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
Attention : dans ce cas, nous utilisons l'utilisateur `bitcoin` pour démarrer le logiciel.

Nous pouvons donc enregistrer le script créé et le lancer.

```
sudo systemctl enable bitcoind
sudo systemctl start bitcoind
```

Chaque fois que l'on veut contrôler l'état du logiciel, on peut utiliser la commande suivante.

```
systemctl status bitcoind
```

### Étape 2 - Installons Electrs

Installons `Electrs`, qui est un serveur electrum basé sur `Rust` ; la première étape consiste donc à installer ce langage.

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Installons aussi clang et le paquet build-essential.

```
apt update
apt install clang cmake build-essential -y
```

Téléchargeons la dernière version, actuellement la 0.10.5, depuis Github.

```
VERSION="0.10.5"
git clone --branch v$VERSION https://github.com/romanz/electrs.git
cd electrs
```

Importons la clé du développeur de `Electrs` et vérifions la signature des commits Github.

```
curl https://romanzey.de/pgp.txt | gpg --import
git verify-tag v$VERSION
```

Si la signature est correcte, nous pouvons passer à la compilation ...

```
cargo build --locked --release
```

puis à l'installation.

```
sudo install -m 0755 -o root -g root -t /usr/local/bin ./target/release/electrs
```

### Étape 2b - Configurons Electrs

Pour configurer `Electrs`, créons le fichier `config.toml` avec le contenu suivant.

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

On peut aussi tout faire avec une seule commande de terminal.

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

Nous pouvons lancer Elects avec la commande

```
electrs --conf config.toml
```

et attendre qu'electrs finisse d'indexer tous les blocs.

### Étape 2c - Lançons Electrs

Comme pour Bitcoin, nous pouvons lancer le logiciel en créant un script pour systemd.

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

Attention : dans ce cas, nous utilisons l'utilisateur `bitcoin` pour démarrer le logiciel.

Nous pouvons donc enregistrer le script créé et le lancer.

```
sudo systemctl enable electrs
sudo systemctl start electrs
```

Chaque fois que l'on veut contrôler l'état du logiciel, on peut utiliser la commande suivante.

```
systemctl status electrs
```

### Étape 3 - Installons CLN

À compléter

### Étape 3b - Configurons CLN

À compléter

### Étape 4 - Installons Mempool.space

Installons `mariadb`.

```
sudo apt-get install mariadb-server mariadb-client
```

Et créons la db et l'utilisateur.

```
sudo mysql -e "drop database mempool;"
sudo mysql -e "create database mempool;"
sudo mysql -e "grant all privileges on mempool.* to 'mempool'@'%' identified by 'mempool';"
sudo mysql -e "flush privileges;"
```

Clonons le code

```
git clone https://github.com/mempool/mempool
cd mempool
latestrelease=$(curl -s https://api.github.com/repos/mempool/mempool/releases/latest|grep tag_name|head -1|cut -d '"' -f4)
git checkout $latestrelease

```

Assurons-nous d'utiliser node 20.x et la dernière version de npm.

```
sudo npm i -g npm
sudo npm i -g node@20
```

Procédons à la compilation et au test du backend

```
cd backend
npm install --no-install-links # npm@9.4.2 and later can omit the --no-install-links
npm run build

cp mempool-config.sample.json mempool-config.json
npm run start
```

Contrôler attentivement les configurations de `mempool-config.json`.

Passons au frontend.

```
cd ..

cd frontend
npm install
npm run serve:local-prod
```


### Étape 4b - Configurons Mempool

La configuration du backend se trouve dans le fichier `mempool-config.json`.

### Étape 4c - Lançons Mempool

Nous pouvons lancer Mempool avec pm2, qui doit être installé.

```
sudo npm i -g pm2
pm2 startup 
```

Lançons le backend.

```
cd ..
cd backend 
pm2 start "npm run start"
```

Lançons ensuite le frontend.

```
cd ..
cd frontend
pm2 start "npm run serve:local-prod"
```

Sauvegardons le tout.

```
pm2 save
```

## Bitcoin avec connexion uniquement via tor
Commençons par installer tor.


```
sudo apt install tor
```

et configurons le fichier de configuration de tor pour créer un nouveau hidden service en exportant le port 8333 du nœud.


```
cat > /etc/tor/torrc <<EOL
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 8333 127.0.0.1:8333
EOL
```

Nous pouvons redémarrer tor pour appliquer les modifications. Cela nous permet d'exporter le port 8333 de notre nœud, mais pas de limiter l'accès au nœud uniquement et exclusivement via tor.

```
sudo systemctl restart tor
``` 

et obtenir l'adresse onion du nœud.

```
cat /var/lib/tor/hidden_service/hostname
```

Cela fait, nous pouvons limiter l'accès au nœud uniquement et exclusivement via tor en modifiant la configuration de bitcoin.conf de cette façon :

```
proxy=127.0.0.1:9050
listen=1
bind=127.0.0.1:8333=onion
externalip=tor_url.onion
onlynet=onion
```

Où `tor_url.onion` est l'adresse onion du nœud obtenue auparavant.


En redémarrant le nœud, nous pouvons vérifier qu'il est accessible uniquement et exclusivement via tor.

```
sudo systemctl restart bitcoind

bitcoin-cli getnetworkinfo
```

Ici, nous devrions voir que le nœud est accessible uniquement et exclusivement via tor, c'est-à-dire que seul le réseau `onion` est `reachable`.

De plus, tous nos peers seront identifiés par des adresses onion.

```
bitcoin-cli getpeerinfo
```

Attention : tor est extrêmement lent ; tenez-en compte lorsque vous voulez synchroniser le nœud à partir de zéro.

## Testnet
Un réseau utile pour s'exercer est `testnet`, qui diffère de `mainnet` car :

- les tokens n'ont aucune valeur et il existe des sites qui vous offrent des satoshi de testnet pour faire des essais,
- vous pouvez toujours faire des transactions avec le minimum de fees,
- le mining est fluctuant, notamment parce qu'on n'y gagne rien,
- si aucun bloc n'est miné pendant 20 minutes, la difficulté chute fortement,
- il y a souvent des reorg importants ; de ce point de vue, c'est pire que mainnet.

De nombreux wallets, green, electrum, specter, sparrow et autres, prennent en charge testnet et peuvent être utilisés pour :

- apprendre sans mettre ses fonds en danger,
- à des fins didactiques,
- expérimenter de nouvelles choses.

Quelques outils utiles, autopromotion, pour testnet :

- [BTCBouncer](http://btcbouncer.com) permet d'effectuer des paiements vers différentes adresses et de recevoir les fonds, moins une fee, en l'espace de quelques blocs,
- [BTCSigner](http://btcsigner.com) permet d'expérimenter un multisig avec un nœud core en testnet.

Il existe beaucoup d'autres outils et sites web qui prennent en charge testnet, en plus des block explorer les plus importants.

## Bitcoin-cli
Bitcoin-cli est l'utilitaire en ligne de commande pour interagir avec Bitcoin Core.

Les commandes ont le format :
```
bitcoin-cli [options] <command> [params]
```
et on peut toujours utiliser `help` pour obtenir la liste des commandes ou des informations sur une commande spécifique.

### Commandes d'information sur la blockchain
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

### Commandes de contrôle
- help ( "command" )
- stop
- uptime
- ...

### Commandes pour le mining
- getblocktemplate ( "template_request" )
- submitblock "hexdata" ( "dummy" )
- ...

### Commandes pour le réseau
- addnode "node" "command"
- disconnectnode ( "address" nodeid )
- getnetworkinfo
- ...

### Gestion des Rawtransactions
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

### Utilitaires
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

Un cours complet sur l'utilisation de Bitcoin en ligne de commande se trouve à l'adresse [Learning-Bitcoin-from-the-Command-Line](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line).

## Programme
L'installation du nœud est divisée en plusieurs leçons ; voici une liste de celles déjà tenues :

| Date        | Notes                                          |
|-------------|------------------------------------------------|
| 240108-2100 | Choix du matériel                              |
| 240115-2200 | Installation de core et vérification signatures |
| 240122-2200 | Configuration minimale                         |
