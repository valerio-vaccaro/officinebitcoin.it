---
layout: default
title: "Fullnode és hardver egy csomóponthoz"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only lecke</span> <span>Ezt a projektet valerio-vaccaro tartja karban</span></p>

## 🌍 Fordítások

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Fullnode és hardver egy csomóponthoz

Egy Bitcoin-csomópont üzemeltetése alapvető, mert maximális adatvédelem mellett lehetővé teszi:

- a teljes Bitcoin-lánc validálását,
- a walletjeink egyenlegének ellenőrzését,
- az új tranzakcióink továbbítását,
- ...

## Hardver kiválasztása

- legalább 2GB RAM, ajánlott 4GB,
- legalább 1TB tömegtár, ajánlott 2TB,
- kellően erős multi-core cpu, valószínűleg bármely, az elmúlt évtizedben fejlesztett processzor.

### Régi számítógép újrahasznosítása

Egy régi számítógép újrahasznosítható csomópontként. Laptop esetén ajánlott eltávolítani az akkumulátort, mert a folyamatos töltés alatt tartott akkumulátor kockázatot jelenthet. A nagy előny a nulla költség, vagy legfeljebb a nagyobb lemez ára.

### Raspberry pi és más kártyák

A Raspberry pi egy ARM-kártya, amelyet gyakran használnak IoT-rendszerek és csomópontok építésére. A magas ár és az USB-n csatlakozó lemez szükségessége miatt azonban teljesítmény és stabilitás szempontjából nem a legjobb választás.

Az Odroid-M1 egy erős ARM-kártya, belső slottal további tömegtár hozzáadásához.

### Thin client

Nagyon alacsony, 30-100 eurós költségvetéssel lehet használt Thin Clientet vásárolni, például ebayen, amely alacsony fogyasztást társít a csomópont futtatásához elégséges teljesítménnyel.

Thin Client példaként a következő modelleket tesztelték:

- Fujitsu Futro s920
- HP t620

## Szoftver kiválasztása

Minél kevesebb szoftver telepítése egy csomópontra csökkenti a lehetséges támadásokat, és egyszerűbbé teszi a rendszer karbantartását.

Online találhatók előre csomagolt megoldások, például Umbrel, Mynode és mások, amelyek elfedik a biztonsági ellenőrzéseket, és nehezen ellenőrizhető szoftvereket és szkripteket adnak hozzá, például dockert. Ezekben a leckékben a kézzel létrehozott csomópontra figyelünk, vagyis minden szükséges szoftvert manuálisan telepítünk.

### 0. lépés - Az operációs rendszer

Az első döntés az operációs rendszer kiválasztása. Az ajánlás egy LTS-verziójú Linux használata, vagyis olyan kiadásé, amelyhez kellően sok évig garantált a támogatás. Az én személyes választásom a Debian 12.

A kiválasztott operációs rendszert telepíteni kell a számítógépre, majd minden csomagot frissíteni kell. A frissítés a csomópont teljes élettartama alatt velünk marad.

Ajánlott telepíteni a tort, és/vagy szükség esetén más VPN-t, valamint az ssh-t, hogy lehetővé váljon a csomópont távoli karbantartása.

Végül egy szünetmentes tápegység megvédheti a csomópontot a hirtelen áramszünetektől, és elkerülheti, hogy a bitcoin és a többi szoftver inkonzisztens állapotban maradjon.

### 1. lépés - Telepítsük a Bitcoint

Letöltjük a core-t, a hasheket és az aláírásokat.

```
wget https://bitcoincore.org/bin/bitcoin-core-28.1/bitcoin-28.1-x86_64-linux-gnu.tar.gz
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS.asc
```

Ha arm architektúrájú boardot használunk, a csomagot `bitcoin-28.1-aarch64-linux-gnu.tar.gz` névre kell cserélni, vagyis ugyanarra a csomagra, de a 64 bites arm architektúrára, aarch64-re fordítva, amelyet az odroid is használ.

Ezen a ponton ellenőrizhetjük, hogy a SHA256SUMS egyik hash-e megfelel-e a letöltött archívumnak.

```
sha256sum --ignore-missing --check SHA256SUMS
```

Az eredmény jelzi, hogy egyezést talált a letöltött archívumhoz.

```
bitcoin-28.1-x86_64-linux-gnu.tar.gz: OK
```

Most ellenőrizzük a SHA256SUMS fájl aláírásait. Előtte, ha szükséges, szerezzük be és importáljuk a kulcsokat.

```
git clone https://github.com/bitcoin-core/guix.sigs
gpg --import guix.sigs/builder-keys/*
```

Végül ellenőrizzük az aláírásokat.

```
gpg --verify SHA256SUMS.asc
```

Ha többször látjuk a `gpg: Good signature from ...` szöveget, az azt jelenti, hogy érvényes aláírásokat találtunk.

Folytassuk a kicsomagolással és a telepítéssel.

```
tar xzvf bitcoin-28.1-x86_64-linux-gnu.tar.gz 
sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-28.1/bin/*
```

Meg is vagyunk: most már a `bitcoind`, a `bitcoin-cli` és a többi segédprogram készen áll az indításra.

Egyelőre indítsuk el a `bitcoind`-t, és látni fogunk némi logot. A Bitcoin elkezd szinkronizálni, és megjelenik egy könyvtár a blockchainnel és az összes konfigurációval: `~/.bitcoin/`.

Egy másik terminálból a `tail -f ~/.bitcoin/debug.log` paranccsal ellenőrizhetjük a bitcoind működését.

### 1b. lépés - Bitcoin konfigurálása

Ahogy korábban láttuk, Linux alatt a Bitcoin Core a konfigurációkat és a blockchaint a `~/.bitcoin/` könyvtárba menti. Ha meg akarjuk változtatni a mentési helyet, több megközelítés használható:

- szimbolikus link létrehozása a könyvtárról egy nagyobb lemezre az `ln -s` paranccsal,
- parancssorból vagy a bitcoin.conf fájlban a `datadir` parancs használata, megadva a célkönyvtárat.

A Bitcoin Core három különböző hálózattípust támogat:
- `mainnet`, ez a klasszikus hálózat, amelyet mindannyian megszoktunk, és ez a core alapértelmezése,
- `testnet`, ez a mainnethez hasonló hálózat, de a tokeneknek nincs értékük; a mining ugyanúgy történik, de ha 20 percig nincs blokk, a nehézség lezuhan; gyakran jelentős reorgokat szenved el,
- `regtest`, ebben a módban egy kis privát blockchain van, amely mindig nulláról indul, és minimális nehézséggel lehet bányászni; helyi tesztekhez szolgál.

Egy másik hasznos parancs a `daemon`, amely beállítva nem tartja a Bitcoin Core logját az aktuális konzolhoz kötve. A működés megtekintéséhez továbbra is használható a `tail -f ~/.bitcoin/debug.log`.

Minden konfiguráció indítható parancssorból vagy a `~/.bitcoin/bitcoin.conf` fájlon keresztül. Egy otthoni setuphoz illő fájl, ahol a lehető legkisebb erőforrás-fogyasztást szeretném, a következő lehet.
konfigurációs fájl

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

Ahol:

- a szerver a `daemon=1` beállítással leválik a konzolról
- csak blokkok töltődnek le, nem a mempool, `blocksonly=1`
- legfeljebb húsz kapcsolat engedélyezett, `txindex=1`
- legfeljebb napi 500 megabyte információt küldünk más internetes csomópontoknak, `maxuploadtarget=500`
- tranzakciós indexet tartunk fenn, `txindex=1`
- blockfilter indexet tartunk fenn, `blockfilterindex=1`
- lehetőséget adunk bárkinek rpc-n keresztüli kapcsolódásra, `rpcallowip=0.0.0.0/0`
- az rpc-t minden hálózati kártyához kötjük, `rpcallowip=0.0.0.0/0`
- beállítunk egy username-et rpc-hez, `rpcuser=username`, természetesen cserélendő
- beállítunk egy passwordöt rpc-hez, `rpcpassword=password`, természetesen cserélendő

A funkciók teljes listája itt található: [https://jlopp.github.io/bitcoin-core-config-generator](https://jlopp.github.io/bitcoin-core-config-generator)

Mindez egyetlen terminálparanccsal is elvégezhető.

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

Ha rendelkezésre áll egy másik, már szinkronizált csomópont, a `connect` opcióval CSAK ÉS KIZÁRÓLAG ehhez a csomóponthoz lehet kapcsolódni. Ha ez a csomópont helyi hálózaton van, ezzel az egyszerű konfigurációval időt és sávszélességet nyerünk.

A 26-os release óta a core támogatja a csomópontok közötti kommunikáció titkosítását a `v2transport` opcióval.

Az összes bemutatott konfiguráció clearnetre vonatkozik; a tor konfigurációi egy másik lecke tárgyai lesznek.

### 1c. lépés - Bitcoin indítása

Indítsuk a Bitcoint egy systemd indítófájl létrehozásával.

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
Figyelem: ebben az esetben a `bitcoin` felhasználót használjuk a szoftver indításához.

Ezután regisztrálhatjuk a létrehozott scriptet és elindíthatjuk.

```
sudo systemctl enable bitcoind
sudo systemctl start bitcoind
```

Amikor ellenőrizni szeretnénk a szoftver állapotát, a következő parancs használható.

```
systemctl status bitcoind
```

### 2. lépés - Electrs telepítése

Telepítjük az `Electrs`-t, amely egy `Rust` alapú electrum server; az első lépés tehát ennek a nyelvnek a telepítése.

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Telepítjük a clangot és a build-essential csomagot is.

```
apt update
apt install clang cmake build-essential -y
```

Letöltjük a legújabb verziót, jelenleg a 0.10.5-öt, Githubról.

```
VERSION="0.10.5"
git clone --branch v$VERSION https://github.com/romanz/electrs.git
cd electrs
```

Importáljuk az `Electrs` fejlesztőjének kulcsát, és ellenőrizzük a Github commitok aláírását.

```
curl https://romanzey.de/pgp.txt | gpg --import
git verify-tag v$VERSION
```

Ha az aláírás helyes, továbbléphetünk a fordításra ...

```
cargo build --locked --release
```

majd a telepítésre.

```
sudo install -m 0755 -o root -g root -t /usr/local/bin ./target/release/electrs
```

### 2b. lépés - Electrs konfigurálása

Az `Electrs` konfigurálásához hozzuk létre a `config.toml` fájlt a következő tartalommal.

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

Mindez egyetlen terminálparanccsal is elvégezhető.

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

Az Elects a következő paranccsal indítható

```
electrs --conf config.toml
```

és meg kell várni, amíg az electrs befejezi az összes blokk indexelését.

### 2c. lépés - Electrs indítása

A Bitcoinhoz hasonlóan a szoftvert egy systemd script létrehozásával indíthatjuk.

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

Figyelem: ebben az esetben a `bitcoin` felhasználót használjuk a szoftver indításához.

Ezután regisztrálhatjuk a létrehozott scriptet és elindíthatjuk.

```
sudo systemctl enable electrs
sudo systemctl start electrs
```

Amikor ellenőrizni szeretnénk a szoftver állapotát, a következő parancs használható.

```
systemctl status electrs
```

### 3. lépés - CLN telepítése

Kiegészítendő

### 3b. lépés - CLN konfigurálása

Kiegészítendő

### 4. lépés - Mempool.space telepítése

Telepítjük a `mariadb`-t.

```
sudo apt-get install mariadb-server mariadb-client
```

Majd létrehozzuk az adatbázist és a felhasználót.

```
sudo mysql -e "drop database mempool;"
sudo mysql -e "create database mempool;"
sudo mysql -e "grant all privileges on mempool.* to 'mempool'@'%' identified by 'mempool';"
sudo mysql -e "flush privileges;"
```

Klónozzuk a kódot

```
git clone https://github.com/mempool/mempool
cd mempool
latestrelease=$(curl -s https://api.github.com/repos/mempool/mempool/releases/latest|grep tag_name|head -1|cut -d '"' -f4)
git checkout $latestrelease

```

Győződjünk meg róla, hogy node 20.x-et és az npm legfrissebb verzióját használjuk.

```
sudo npm i -g npm
sudo npm i -g node@20
```

Gondoskodjunk a backend fordításáról és teszteléséről

```
cd backend
npm install --no-install-links # npm@9.4.2 and later can omit the --no-install-links
npm run build

cp mempool-config.sample.json mempool-config.json
npm run start
```

Gondosan ellenőrizni kell a `mempool-config.json` konfigurációit.

Térjünk át a frontendre.

```
cd ..

cd frontend
npm install
npm run serve:local-prod
```


### 4b. lépés - Mempool konfigurálása

A backend konfigurációja a `mempool-config.json` fájlban található.

### 4c. lépés - Mempool indítása

A Mempool pm2-vel indítható, amelyet telepíteni kell.

```
sudo npm i -g pm2
pm2 startup 
```

Indítsuk a backendet.

```
cd ..
cd backend 
pm2 start "npm run start"
```

Ezután indítsuk a frontendet.

```
cd ..
cd frontend
pm2 start "npm run serve:local-prod"
```

Mentsünk el mindent.

```
pm2 save
```

## Bitcoin csak toron keresztüli kapcsolattal
Kezdjük a tor telepítésével.


```
sudo apt install tor
```

és állítsuk be a tor konfigurációs fájlját egy új hidden service létrehozásához, amely exportálja a csomópont 8333-as portját.


```
cat > /etc/tor/torrc <<EOL
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 8333 127.0.0.1:8333
EOL
```

Újraindíthatjuk a tort a módosítások alkalmazásához. Ez lehetővé teszi a csomópontunk 8333-as portjának exportálását, de még nem korlátozza a hozzáférést kizárólag torra.

```
sudo systemctl restart tor
``` 

és lekérhetjük a csomópont onion címét.

```
cat /var/lib/tor/hidden_service/hostname
```

Ezután a bitcoin.conf konfiguráció ilyen módosításával korlátozhatjuk a csomópont elérését csak és kizárólag torra:

```
proxy=127.0.0.1:9050
listen=1
bind=127.0.0.1:8333=onion
externalip=tor_url.onion
onlynet=onion
```

Ahol a `tor_url.onion` a csomópont korábban kapott onion címe.


A csomópont újraindításával ellenőrizhetjük, hogy a csomópont csak és kizárólag toron keresztül érhető el.

```
sudo systemctl restart bitcoind

bitcoin-cli getnetworkinfo
```

Itt azt kell látnunk, hogy a csomópont csak és kizárólag toron keresztül érhető el, vagyis csak az `onion` hálózat `reachable`.

Ezenkívül minden peerünk onion címekkel lesz azonosítva.

```
bitcoin-cli getpeerinfo
```

Figyelem: a tor rendkívül lassú; ezt vegyétek figyelembe, amikor nulláról szeretnétek szinkronizálni a csomópontot.

## Testnet
Gyakorláshoz hasznos hálózat a `testnet`, amely abban különbözik a `mainnet`-től, hogy:

- a tokeneknek nincs értékük, és vannak oldalak, amelyek testnet satoshikat adnak próbaképpen,
- mindig minimális fee mellett lehet tranzakciózni,
- a mining ingadozó, többek között azért, mert nem lehet vele keresni,
- ha 20 percig nem bányásznak blokkot, a nehézség lezuhan,
- gyakran vannak jelentős reorgok; ebből a szempontból rosszabb, mint a mainnet.

Sok wallet, például green, electrum, specter, sparrow és mások, támogatja a testnetet, és használhatók:

- tanulásra saját pénzek kockáztatása nélkül,
- oktatási célokra,
- új dolgok kipróbálására.

Néhány hasznos eszköz, önreklám, testnethez:

- [BTCBouncer](http://btcbouncer.com) lehetővé teszi fizetések küldését különböző címekre és a pénzek fogadását, egy fee levonásával, néhány blokkon belül,
- [BTCSigner](http://btcsigner.com) lehetővé teszi multisig kipróbálását egy core csomóponttal testneten.

Sok más tool és weboldal is támogatja a testnetet, a legfontosabb block explorerek mellett.

## Bitcoin-cli
A Bitcoin-cli a Bitcoin Core-ral való interakció parancssori segédprogramja.

A parancsok formátuma:
```
bitcoin-cli [options] <command> [params]
```
és mindig használható a `help` a parancsok listájához vagy egy konkrét parancs információihoz.

### Információs parancsok a blockchainről
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

### Vezérlő parancsok
- help ( "command" )
- stop
- uptime
- ...

### Mining parancsok
- getblocktemplate ( "template_request" )
- submitblock "hexdata" ( "dummy" )
- ...

### Hálózati parancsok
- addnode "node" "command"
- disconnectnode ( "address" nodeid )
- getnetworkinfo
- ...

### Rawtransactions kezelése
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

### Segédprogramok
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

Teljes kurzus a Bitcoin parancssori használatáról itt található: [Learning-Bitcoin-from-the-Command-Line](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line).

## Program
A csomópont telepítése több leckére van osztva; itt a már megtartottak listája:

| Dátum       | Megjegyzések                                   |
|-------------|------------------------------------------------|
| 240108-2100 | Hardver kiválasztása                           |
| 240115-2200 | Core telepítése és aláírások ellenőrzése       |
| 240122-2200 | Minimális konfiguráció                         |
