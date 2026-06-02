---
layout: default
title: "Fullnode und Hardware für einen Node"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only-Lektion</span> <span>Dieses Projekt wird von valerio-vaccaro gepflegt</span></p>

## 🌍 Übersetzungen

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Fullnode und Hardware für einen Node

Einen Bitcoin-Node zu betreiben ist grundlegend, weil er mit maximaler Privatsphäre ermöglicht:

- die gesamte Bitcoin-Kette zu validieren,
- den Kontostand unserer Wallets zu prüfen,
- unsere neuen Transaktionen zu übertragen,
- ...

## Auswahl der Hardware

- mindestens 2GB RAM, empfohlen 4GB,
- Datenträger mit mindestens 1TB Massenspeicher, empfohlen 2TB,
- ausreichend leistungsfähige Multi-Core-CPU, wahrscheinlich jeder Prozessor aus dem letzten Jahrzehnt.

### Einen alten Computer wiederverwenden

Ein alter Computer kann als Node recycelt werden. Bei einem Laptop empfiehlt es sich, den Akku zu entfernen, weil ein dauerhaft geladener Akku ein Risiko darstellen kann. Der große Vorteil sind Kosten von null oder nur die Kosten für einen größeren Datenträger.

### Raspberry Pi und andere Boards

Der Raspberry Pi ist ein ARM-Board, das häufig für IoT-Systeme und Nodes verwendet wird. Der hohe Preis und die Notwendigkeit eines Datenträgers über USB machen ihn jedoch hinsichtlich Leistung und Stabilität nicht zur besten möglichen Wahl.

Odroid-M1 ist ein leistungsfähiges ARM-Board mit einem internen Steckplatz für zusätzlichen Massenspeicher.

### Thin Clients

Mit einem sehr kleinen Budget von 30-100 Euro kann man einen gebrauchten Thin Client kaufen, etwa bei ebay, der niedrigen Verbrauch mit ausreichender Leistung für den Node verbindet.

Als Beispiele für Thin Clients wurden die folgenden Modelle getestet:

- Fujitsu Futro s920
- HP t620

## Auswahl der Software

So wenig Software wie möglich auf einem Node zu installieren begrenzt mögliche Angriffe und macht das System einfacher zu warten.

Online findet man vorgefertigte Lösungen wie Umbrel, Mynode und andere, die Sicherheitsprüfungen verbergen und Software sowie Skripte hinzufügen, zum Beispiel docker, die schwer zu kontrollieren sind. In diesen Lektionen konzentrieren wir uns auf den manuellen Aufbau eines Nodes, also auf die manuelle Installation aller nötigen Software.

### Schritt 0 - Das Betriebssystem

Die erste Wahl betrifft das Betriebssystem. Empfohlen wird Linux in einer LTS-Version, also mit Unterstützung für ausreichend viele Jahre. Meine persönliche Wahl fällt auf Debian 12.

Das gewählte Betriebssystem muss dann auf dem Computer installiert werden und alle Pakete müssen aktualisiert werden. Updates werden uns während der gesamten Lebensdauer des Nodes begleiten.

Es empfiehlt sich außerdem, tor und/oder eine andere VPN bei Bedarf sowie ssh zu installieren, damit der Node aus der Ferne gewartet werden kann.

Eine USV kann den Node schließlich vor abrupten Stromausfällen schützen und vermeiden, dass bitcoin und andere Software in einem inkonsistenten Zustand bleiben.

### Schritt 1 - Bitcoin installieren

Wir laden Core, die Hashes und die Signaturen herunter.

```
wget https://bitcoincore.org/bin/bitcoin-core-28.1/bitcoin-28.1-x86_64-linux-gnu.tar.gz
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS.asc
```

Falls ein Board mit ARM-Architektur verwendet wird, muss das Paket zu `bitcoin-28.1-aarch64-linux-gnu.tar.gz` geändert werden, also zum gleichen Paket, aber für die 64-Bit-ARM-Architektur aarch64 kompiliert, die auch Odroid verwendet.

Nun können wir prüfen, dass einer der Hashes in SHA256SUMS zum heruntergeladenen Archiv passt.

```
sha256sum --ignore-missing --check SHA256SUMS
```

Das Ergebnis zeigt an, dass eine Übereinstimmung für das heruntergeladene Archiv gefunden wurde.

```
bitcoin-28.1-x86_64-linux-gnu.tar.gz: OK
```

Jetzt prüfen wir die Signaturen der Datei SHA256SUMS. Falls nötig, besorgen und importieren wir zuerst die Schlüssel.

```
git clone https://github.com/bitcoin-core/guix.sigs
gpg --import guix.sigs/builder-keys/*
```

Zum Schluss prüfen wir die Signaturen.

```
gpg --verify SHA256SUMS.asc
```

Wenn mehrfach `gpg: Good signature from ...` erscheint, bedeutet das, dass wir gültige Signaturen gefunden haben.

Wir fahren mit dem Entpacken und der Installation fort.

```
tar xzvf bitcoin-28.1-x86_64-linux-gnu.tar.gz 
sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-28.1/bin/*
```

Damit sind `bitcoind`, `bitcoin-cli` und die anderen Werkzeuge startbereit.

Für den Moment starten wir `bitcoind` und sehen etwas Log-Ausgabe. Bitcoin beginnt mit der Synchronisierung, und nun gibt es ein Verzeichnis mit der Blockchain und allen Konfigurationen unter `~/.bitcoin/`.

Von einem anderen Terminal aus können wir die Funktion von bitcoind mit dem Befehl `tail -f ~/.bitcoin/debug.log` kontrollieren.

### Schritt 1b - Bitcoin konfigurieren

Wie wir bereits gesehen haben, ist das Verzeichnis, in dem Bitcoin Core unter Linux die Konfigurationen und die Blockchain speichert, `~/.bitcoin/`. Falls man den Speicherort ändern möchte, gibt es verschiedene Ansätze:

- einen symbolischen Link des Verzeichnisses auf einen größeren Datenträger mit dem Befehl `ln -s` erstellen,
- über die Kommandozeile oder innerhalb von bitcoin.conf den Befehl `datadir` verwenden und das Zielverzeichnis angeben.

Bitcoin Core unterstützt drei verschiedene Arten von Netzwerken, mit denen man sich verbinden kann:
- `mainnet`, das klassische Netzwerk, an das wir alle gewöhnt sind, und der Standard für Core,
- `testnet`, ein Netzwerk ähnlich wie mainnet, aber die Token haben keinen Wert; Mining findet weiterhin statt, doch wenn 20 Minuten lang keine Blöcke vorhanden sind, fällt die Schwierigkeit stark ab; es leidet oft unter erheblichen Reorgs,
- `regtest`, in diesem Modus hat man eine kleine private Blockchain, die immer bei null beginnt und in der man mit minimaler Schwierigkeit minen kann; sie dient lokalen Tests.

Ein weiterer nützlicher Befehl ist `daemon`. Wenn er gesetzt ist, bleibt das Log von Bitcoin Core nicht mit der aktuellen Konsole verbunden. Um den Betrieb zu sehen, kann man weiterhin `tail -f ~/.bitcoin/debug.log` verwenden.

Alle Konfigurationen können über die Kommandozeile oder über die Datei `~/.bitcoin/bitcoin.conf` gestartet werden. Eine Datei, die zu einem Heim-Setup passt, bei dem der Ressourcenverbrauch minimal bleiben soll, könnte so aussehen.
Konfigurationsdatei

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

Dabei gilt:

- der Server wird mit `daemon=1` von der Konsole getrennt
- es werden nur Blöcke und nicht die Mempool heruntergeladen, `blocksonly=1`
- bis zu zwanzig Verbindungen sind erlaubt, `txindex=1`
- wir senden Informationen an andere Nodes im Internet bis zu höchstens 500 Megabyte pro Tag, `maxuploadtarget=500`
- ein Transaktionsindex wird geführt, `txindex=1`
- ein Blockfilter-Index wird geführt, `blockfilterindex=1`
- wir erlauben jedem, sich per rpc zu verbinden, `rpcallowip=0.0.0.0/0`
- wir binden rpc an alle Netzwerkkarten, `rpcallowip=0.0.0.0/0`
- wir setzen einen Benutzernamen für rpc, `rpcuser=username`, natürlich zu ersetzen
- wir setzen ein Passwort für rpc, `rpcpassword=password`, natürlich zu ersetzen

Die vollständige Liste der Funktionen findet man unter [https://jlopp.github.io/bitcoin-core-config-generator](https://jlopp.github.io/bitcoin-core-config-generator)

Man kann auch alles mit einem einzigen Terminalbefehl erledigen.

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

Falls ein anderer bereits synchronisierter Node verfügbar ist, kann man die Option `connect` verwenden, um sich NUR UND AUSSCHLIESSLICH mit diesem Node zu verbinden. Befindet sich dieser Node im lokalen Netzwerk, spart man mit dieser einfachen Konfiguration Zeit und Bandbreite.

Seit Release 26 unterstützt Core mit der Option `v2transport` die Verschlüsselung der Kommunikation zwischen Nodes.

Alle gezeigten Konfigurationen beziehen sich auf clearnet. Die Konfigurationen für tor werden Thema einer anderen Lektion sein.

### Schritt 1c - Bitcoin starten

Wir starten Bitcoin, indem wir eine Startdatei für systemd erstellen.

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
Hinweis: In diesem Fall verwenden wir den Benutzer `bitcoin`, um die Software zu starten.

Nun können wir das erstellte Skript registrieren und starten.

```
sudo systemctl enable bitcoind
sudo systemctl start bitcoind
```

Jedes Mal, wenn man den Status der Software kontrollieren möchte, kann man den folgenden Befehl verwenden.

```
systemctl status bitcoind
```

### Schritt 2 - Electrs installieren

Wir installieren `Electrs`, einen auf `Rust` basierenden Electrum-Server. Der erste Schritt ist daher die Installation dieser Sprache.

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Wir installieren außerdem clang und das Paket build-essential.

```
apt update
apt install clang cmake build-essential -y
```

Wir laden die neueste Version, derzeit 0.10.5, von Github herunter.

```
VERSION="0.10.5"
git clone --branch v$VERSION https://github.com/romanz/electrs.git
cd electrs
```

Wir importieren den Schlüssel des Entwicklers von `Electrs` und prüfen die Signatur der Github-Commits.

```
curl https://romanzey.de/pgp.txt | gpg --import
git verify-tag v$VERSION
```

Wenn die Signatur korrekt ist, können wir zur Kompilierung übergehen ...

```
cargo build --locked --release
```

und danach zur Installation.

```
sudo install -m 0755 -o root -g root -t /usr/local/bin ./target/release/electrs
```

### Schritt 2b - Electrs konfigurieren

Um `Electrs` zu konfigurieren, erstellen wir die Datei `config.toml` mit folgendem Inhalt.

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

Man kann auch alles mit einem einzigen Terminalbefehl erledigen.

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

Wir können Elects mit dem Befehl starten

```
electrs --conf config.toml
```

und warten, bis electrs alle Blöcke indexiert hat.

### Schritt 2c - Electrs starten

Wie bei Bitcoin können wir die Software starten, indem wir ein Skript für systemd erstellen.

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

Hinweis: In diesem Fall verwenden wir den Benutzer `bitcoin`, um die Software zu starten.

Nun können wir das erstellte Skript registrieren und starten.

```
sudo systemctl enable electrs
sudo systemctl start electrs
```

Jedes Mal, wenn man den Status der Software kontrollieren möchte, kann man den folgenden Befehl verwenden.

```
systemctl status electrs
```

### Schritt 3 - CLN installieren

Zu vervollständigen

### Schritt 3b - CLN konfigurieren

Zu vervollständigen

### Schritt 4 - Mempool.space installieren

Wir installieren `mariadb`.

```
sudo apt-get install mariadb-server mariadb-client
```

Und wir erstellen Datenbank und Benutzer.

```
sudo mysql -e "drop database mempool;"
sudo mysql -e "create database mempool;"
sudo mysql -e "grant all privileges on mempool.* to 'mempool'@'%' identified by 'mempool';"
sudo mysql -e "flush privileges;"
```

Wir klonen den Code

```
git clone https://github.com/mempool/mempool
cd mempool
latestrelease=$(curl -s https://api.github.com/repos/mempool/mempool/releases/latest|grep tag_name|head -1|cut -d '"' -f4)
git checkout $latestrelease

```

Wir stellen sicher, node 20.x und die neueste npm-Version zu verwenden.

```
sudo npm i -g npm
sudo npm i -g node@20
```

Wir kompilieren und testen das Backend

```
cd backend
npm install --no-install-links # npm@9.4.2 and later can omit the --no-install-links
npm run build

cp mempool-config.sample.json mempool-config.json
npm run start
```

Die Konfigurationen in `mempool-config.json` sorgfältig prüfen.

Wir wechseln zum Frontend.

```
cd ..

cd frontend
npm install
npm run serve:local-prod
```


### Schritt 4b - Mempool konfigurieren

Die Backend-Konfiguration befindet sich in der Datei `mempool-config.json`.

### Schritt 4c - Mempool starten

Wir können Mempool mit pm2 starten, das installiert werden muss.

```
sudo npm i -g pm2
pm2 startup 
```

Wir starten das Backend.

```
cd ..
cd backend 
pm2 start "npm run start"
```

Danach starten wir das Frontend.

```
cd ..
cd frontend
pm2 start "npm run serve:local-prod"
```

Wir speichern alles.

```
pm2 save
```

## Bitcoin mit Verbindung nur über tor
Wir beginnen mit der Installation von tor.


```
sudo apt install tor
```

und konfigurieren die tor-Konfigurationsdatei, um einen neuen hidden service zu erstellen, der Port 8333 des Nodes exportiert.


```
cat > /etc/tor/torrc <<EOL
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 8333 127.0.0.1:8333
EOL
```

Wir können tor neu starten, um die Änderungen anzuwenden. Dadurch können wir Port 8333 unseres Nodes exportieren, aber den Zugriff auf den Node noch nicht ausschließlich auf tor beschränken.

```
sudo systemctl restart tor
``` 

und die onion-Adresse des Nodes erhalten.

```
cat /var/lib/tor/hidden_service/hostname
```

Danach können wir den Zugriff auf den Node ausschließlich über tor beschränken, indem wir bitcoin.conf so ändern:

```
proxy=127.0.0.1:9050
listen=1
bind=127.0.0.1:8333=onion
externalip=tor_url.onion
onlynet=onion
```

Dabei ist `tor_url.onion` die zuvor erhaltene onion-Adresse des Nodes.


Nach dem Neustart des Nodes können wir prüfen, dass der Node ausschließlich über tor erreichbar ist.

```
sudo systemctl restart bitcoind

bitcoin-cli getnetworkinfo
```

Hier sollten wir sehen, dass der Node ausschließlich über tor erreichbar ist, also dass nur das Netzwerk `onion` `reachable` ist.

Außerdem werden alle unsere Peers durch onion-Adressen identifiziert.

```
bitcoin-cli getpeerinfo
```

Hinweis: tor ist extrem langsam. Berücksichtigt das, wenn ihr den Node von null an synchronisieren wollt.

## Testnet
Ein nützliches Netzwerk zum Üben ist `testnet`, das sich von `mainnet` dadurch unterscheidet, dass:

- die Token keinen Wert haben und es Websites gibt, die euch Testnet-Satoshi für Versuche anbieten,
- ihr immer mit minimalen Fees transagieren könnt,
- das Mining schwankt, auch weil man damit nichts verdient,
- falls ein Block 20 Minuten lang nicht gemined wird, fällt die Schwierigkeit stark ab,
- es oft erhebliche Reorgs gibt; aus dieser Sicht ist es schlechter als mainnet.

Viele Wallets wie green, electrum, specter, sparrow und andere unterstützen testnet und können verwendet werden, um:

- zu lernen, ohne die eigenen Gelder zu riskieren,
- für didaktische Zwecke,
- neue Dinge auszuprobieren.

Einige nützliche Tools für testnet, Eigenwerbung:

- [BTCBouncer](http://btcbouncer.com) ermöglicht Zahlungen an verschiedene Adressen und den Empfang der Gelder, abzüglich einer Fee, innerhalb von ein paar Blöcken,
- [BTCSigner](http://btcsigner.com) ermöglicht das Experimentieren mit Multisig mit einem Core-Node in testnet.

Es gibt viele weitere Tools und Websites, die testnet unterstützen, zusätzlich zu den wichtigsten Block-Explorern.

## Bitcoin-cli
Bitcoin-cli ist das Kommandozeilenwerkzeug zur Interaktion mit Bitcoin Core.

Die Befehle haben das Format:
```
bitcoin-cli [options] <command> [params]
```
und man kann immer `help` verwenden, um die Liste der Befehle oder Informationen zu einem bestimmten Befehl zu erhalten.

### Informationsbefehle zur Blockchain
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

### Steuerbefehle
- help ( "command" )
- stop
- uptime
- ...

### Mining-Befehle
- getblocktemplate ( "template_request" )
- submitblock "hexdata" ( "dummy" )
- ...

### Netzwerkbefehle
- addnode "node" "command"
- disconnectnode ( "address" nodeid )
- getnetworkinfo
- ...

### Verwaltung von Rawtransactions
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

### Werkzeuge
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

Einen vollständigen Kurs zur Nutzung von Bitcoin über die Kommandozeile findet man unter [Learning-Bitcoin-from-the-Command-Line](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line).

## Programm
Die Installation des Nodes ist auf mehrere Lektionen verteilt. Hier ist eine Liste der bereits gehaltenen:

| Datum       | Notizen                                        |
|-------------|------------------------------------------------|
| 240108-2100 | Auswahl der Hardware                           |
| 240115-2200 | Installation von core und Signaturprüfung      |
| 240122-2200 | Minimalkonfiguration                           |
