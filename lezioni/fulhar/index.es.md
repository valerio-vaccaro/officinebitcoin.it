---
layout: default
title: "Fullnode y hardware para un nodo"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lección Bitcoin-only</span> <span>Este proyecto es mantenido por valerio-vaccaro</span></p>

## 🌍 Traducciones

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Fullnode y hardware para un nodo

Tener un nodo Bitcoin es fundamental porque permite, con la máxima privacidad:

- validar toda la cadena de Bitcoin,
- comprobar el balance de nuestros wallet,
- transmitir nuestras nuevas transacciones,
- ...

## Selección del hardware

- mínimo 2GB de memoria RAM, recomendados 4GB,
- disco de al menos 1TB de almacenamiento, recomendados 2TB,
- cpu multi-core suficientemente potente, probablemente cualquier procesador desarrollado en la última década.

### Reutiliza un ordenador viejo

Un ordenador viejo puede reciclarse como nodo. En caso de usar un portátil, se recomienda retirar la batería, ya que mantenerla siempre cargando podría suponer un riesgo. La gran ventaja es el coste cero, o limitado solo al disco de mayor capacidad.

### Raspberry pi y otras placas

Raspberry pi es una placa ARM muy utilizada para crear sistemas IoT y nodos. Sin embargo, su coste excesivo y la necesidad de un disco por USB hacen que no sea la mejor elección posible en términos de rendimiento y estabilidad.

Odroid-M1 es una placa ARM potente y con una ranura interna para añadir almacenamiento adicional.

### Thin client

Con un presupuesto muy reducido, 30-100 euros, es posible comprar un Thin Client usado, en ebay, que combina bajo consumo con prestaciones suficientes para ejecutar el nodo.

Como ejemplos de Thin Client se han probado los siguientes modelos:

- Fujitsu Futro s920
- HP t620

## Selección del software

Instalar la menor cantidad posible de software en un nodo limita los posibles ataques y hace que el sistema sea más sencillo de mantener.

En línea se encuentran soluciones preempaquetadas, como Umbrel, Mynode y otras, que ocultan los controles de seguridad y añaden software y scripts, por ejemplo docker, difíciles de controlar. En estas lecciones pondremos la atención en crear un nodo a mano, es decir, instalando manualmente todo el software necesario.

### Paso 0 - El sistema operativo

La primera elección que hay que hacer es el sistema operativo. El consejo es utilizar Linux en una versión LTS, es decir, con soporte garantizado durante un número suficientemente largo de años. Mi elección personal es Debian 12.

El sistema operativo elegido debe instalarse en el ordenador y todos los paquetes deben actualizarse. La actualización será algo que nos acompañará durante toda la vida del nodo.

También se recomienda instalar tor, y/o otra VPN si es necesaria, y ssh, para permitir el mantenimiento remoto del nodo.

Por último, un SAI podría salvar el nodo de caídas bruscas de corriente, evitando dejar bitcoin y el resto del software en un estado inconsistente.

### Paso 1 - Instalamos Bitcoin

Descargamos core, los hashes y las firmas.

```
wget https://bitcoincore.org/bin/bitcoin-core-28.1/bitcoin-28.1-x86_64-linux-gnu.tar.gz
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS.asc
```

Si se utiliza una board con arquitectura arm, el paquete deberá cambiarse a `bitcoin-28.1-aarch64-linux-gnu.tar.gz`, es decir, el mismo paquete pero compilado para la arquitectura arm de 64 bits, aarch64, que es precisamente la utilizada por odroid.

En este punto podemos comprobar que uno de los hashes en SHA256SUMS corresponde al archivo descargado.

```
sha256sum --ignore-missing --check SHA256SUMS
```

El resultado nos indica que se ha encontrado una coincidencia para el archivo descargado.

```
bitcoin-28.1-x86_64-linux-gnu.tar.gz: OK
```

Ahora verificamos las firmas del archivo SHA256SUMS. Antes, si es necesario, obtenemos las claves y las importamos.

```
git clone https://github.com/bitcoin-core/guix.sigs
gpg --import guix.sigs/builder-keys/*
```

Y finalmente verificamos las firmas.

```
gpg --verify SHA256SUMS.asc
```

Si vemos muchas veces el texto `gpg: Good signature from ...`, significa que hemos encontrado firmas válidas.

Procedemos a descomprimir e instalar.

```
tar xzvf bitcoin-28.1-x86_64-linux-gnu.tar.gz 
sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-28.1/bin/*
```

Y ya está: ahora tenemos `bitcoind`, `bitcoin-cli` y las demás utilidades listas para ejecutarse.

Por ahora ejecutamos `bitcoind` y veremos algo de log. Bitcoin empieza a sincronizarse y ahora habrá un directorio con la blockchain y todas las configuraciones en `~/.bitcoin/`.

Desde otra terminal podemos comprobar el funcionamiento de bitcoind ejecutando el comando `tail -f ~/.bitcoin/debug.log`.

### Paso 1b - Configuramos Bitcoin

Como ya hemos visto anteriormente, el directorio en el que Bitcoin Core guarda las configuraciones y la blockchain en Linux es `~/.bitcoin/`. Si se quisiera cambiar la ubicación de guardado, se pueden usar distintos enfoques:

- crear un enlace simbólico del directorio en un disco más grande mediante el comando `ln -s`,
- usar desde la línea de comandos o dentro de bitcoin.conf el comando `datadir`, indicando el directorio de destino.

Bitcoin Core soporta tres tipos distintos de redes a las que conectarse:
- `mainnet`, la red clásica a la que todos estamos acostumbrados y la opción por defecto de core,
- `testnet`, una red análoga a mainnet pero cuyos tokens no tienen valor; el mining se realiza igualmente, pero si no hay bloques durante 20 minutos la dificultad cae en picado; suele sufrir reorg importantes,
- `regtest`, en esta modalidad se tiene una pequeña blockchain privada que siempre empieza desde cero y en la que se puede minar con dificultad mínima; sirve para pruebas locales.

Otro comando útil es `daemon`, que, si está configurado, no mantiene el log de Bitcoin Core unido a la consola actual. Para ver el funcionamiento siempre será posible usar el comando `tail -f ~/.bitcoin/debug.log`.

Todas las configuraciones pueden lanzarse desde la línea de comandos o mediante el archivo `~/.bitcoin/bitcoin.conf`. Un archivo compatible con un setup doméstico, es decir, en el que quiero mantener el consumo de recursos al mínimo, podría ser el siguiente.
archivo de configuración

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

Donde:

- el servidor se separa de la consola con `daemon=1`
- se descargan solo los bloques y no la mempool, `blocksonly=1`
- se permiten hasta veinte conexiones, `txindex=1`
- se envía información a otros nodos en internet hasta un máximo de 500 megabytes al día, `maxuploadtarget=500`
- se mantiene un índice de las transacciones, `txindex=1`
- se mantiene un índice de los blockfilter, `blockfilterindex=1`
- damos la posibilidad a cualquiera de conectarse mediante rpc, `rpcallowip=0.0.0.0/0`
- vinculamos rpc a todas las interfaces de red, `rpcallowip=0.0.0.0/0`
- configuramos un username para rpc, `rpcuser=username`, obviamente hay que sustituirlo
- configuramos una password para rpc, `rpcpassword=password`, obviamente hay que sustituirla

La lista completa de funcionalidades se puede encontrar en [https://jlopp.github.io/bitcoin-core-config-generator](https://jlopp.github.io/bitcoin-core-config-generator)

También se puede hacer todo con un único comando de terminal.

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

Si se dispone de otro nodo ya sincronizado, se puede usar la opción `connect` para conectarse SOLO Y EXCLUSIVAMENTE a ese nodo. Si ese nodo está en la red local, se gana tiempo y ancho de banda con esta configuración sencilla.

Desde la release 26, core soporta cifrado de las comunicaciones entre nodos con la opción `v2transport`.

Todas las configuraciones mostradas son relativas a clearnet; las configuraciones para tor serán objeto de otra lección.

### Paso 1c - Lanzamos Bitcoin

Lanzamos Bitcoin creando un archivo de arranque para systemd.

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
Atención: en este caso estamos utilizando el usuario `bitcoin` para iniciar el software.

Podemos registrar el script creado y lanzarlo.

```
sudo systemctl enable bitcoind
sudo systemctl start bitcoind
```

Cada vez que se quiera comprobar el estado del software se puede usar el siguiente comando.

```
systemctl status bitcoind
```

### Paso 2 - Instalamos Electrs

Instalamos `Electrs`, que es un servidor electrum basado en `Rust`; el primer paso es, por tanto, instalar ese lenguaje.

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Instalamos también clang y el paquete build-essential.

```
apt update
apt install clang cmake build-essential -y
```

Descargamos la última versión, actualmente la 0.10.5, desde Github.

```
VERSION="0.10.5"
git clone --branch v$VERSION https://github.com/romanz/electrs.git
cd electrs
```

Importamos la clave del desarrollador de `Electrs` y verificamos la firma de los commit de Github.

```
curl https://romanzey.de/pgp.txt | gpg --import
git verify-tag v$VERSION
```

Si la firma es correcta podemos pasar a la compilación ...

```
cargo build --locked --release
```

y luego a la instalación.

```
sudo install -m 0755 -o root -g root -t /usr/local/bin ./target/release/electrs
```

### Paso 2b - Configuramos Electrs

Para configurar `Electrs` creamos el archivo `config.toml` con el siguiente contenido.

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

También se puede hacer todo con un único comando de terminal.

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

Podemos lanzar Elects con el comando

```
electrs --conf config.toml
```

y esperar a que electrs termine de indexar todos los bloques.

### Paso 2c - Lanzamos Electrs

Como con Bitcoin, podemos lanzar el software creando un script para systemd.

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

Atención: en este caso estamos utilizando el usuario `bitcoin` para iniciar el software.

Podemos registrar el script creado y lanzarlo.

```
sudo systemctl enable electrs
sudo systemctl start electrs
```

Cada vez que se quiera comprobar el estado del software se puede usar el siguiente comando.

```
systemctl status electrs
```

### Paso 3 - Instalamos CLN

Por completar

### Paso 3b - Configuramos CLN

Por completar

### Paso 4 - Instalamos Mempool.space

Instalamos `mariadb`.

```
sudo apt-get install mariadb-server mariadb-client
```

Y creamos db y usuario.

```
sudo mysql -e "drop database mempool;"
sudo mysql -e "create database mempool;"
sudo mysql -e "grant all privileges on mempool.* to 'mempool'@'%' identified by 'mempool';"
sudo mysql -e "flush privileges;"
```

Clonamos el código

```
git clone https://github.com/mempool/mempool
cd mempool
latestrelease=$(curl -s https://api.github.com/repos/mempool/mempool/releases/latest|grep tag_name|head -1|cut -d '"' -f4)
git checkout $latestrelease

```

Asegurémonos de usar node 20.x y la última versión de npm.

```
sudo npm i -g npm
sudo npm i -g node@20
```

Procedemos a compilar y probar el backend

```
cd backend
npm install --no-install-links # npm@9.4.2 and later can omit the --no-install-links
npm run build

cp mempool-config.sample.json mempool-config.json
npm run start
```

Comprobar atentamente las configuraciones de `mempool-config.json`.

Pasamos al frontend.

```
cd ..

cd frontend
npm install
npm run serve:local-prod
```


### Paso 4b - Configuramos Mempool

La configuración del backend se encuentra en el archivo `mempool-config.json`.

### Paso 4c - Lanzamos Mempool

Podemos lanzar Mempool con pm2, que debe instalarse.

```
sudo npm i -g pm2
pm2 startup 
```

Lanzamos el backend.

```
cd ..
cd backend 
pm2 start "npm run start"
```

Luego lanzamos el frontend.

```
cd ..
cd frontend
pm2 start "npm run serve:local-prod"
```

Guardamos todo.

```
pm2 save
```

## Bitcoin con conexión solo mediante tor
Empezamos instalando tor.


```
sudo apt install tor
```

y configuramos el archivo de configuración de tor para crear un nuevo hidden service exportando el puerto 8333 del nodo.


```
cat > /etc/tor/torrc <<EOL
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 8333 127.0.0.1:8333
EOL
```

Podemos reiniciar tor para aplicar los cambios. Esto nos permite exportar el puerto 8333 de nuestro nodo, pero no limitar el acceso al nodo solo y exclusivamente mediante tor.

```
sudo systemctl restart tor
``` 

y obtener la dirección onion del nodo.

```
cat /var/lib/tor/hidden_service/hostname
```

Hecho esto, podemos limitar el acceso al nodo solo y exclusivamente mediante tor modificando la configuración de bitcoin.conf de este modo:

```
proxy=127.0.0.1:9050
listen=1
bind=127.0.0.1:8333=onion
externalip=tor_url.onion
onlynet=onion
```

Donde `tor_url.onion` es la dirección onion del nodo obtenida anteriormente.


Al reiniciar el nodo podemos verificar que el nodo es accesible solo y exclusivamente mediante tor.

```
sudo systemctl restart bitcoind

bitcoin-cli getnetworkinfo
```

Aquí deberíamos ver que el nodo es accesible solo y exclusivamente mediante tor, es decir, que solo la red `onion` está `reachable`.

Además, todos nuestros peer estarán identificados por direcciones onion.

```
bitcoin-cli getpeerinfo
```

Atención: tor es extremadamente lento; tenedlo en cuenta cuando queráis sincronizar el nodo desde cero.

## Testnet
Una red útil para practicar es `testnet`, que difiere de `mainnet` en que:

- los tokens no tienen valor y hay sitios que os ofrecen satoshi de testnet para hacer pruebas,
- podéis transaccionar siempre con el mínimo de fees,
- el mining es fluctuante, también porque no se gana nada con ello,
- si un bloque no se mina durante 20 minutos, la dificultad cae en picado,
- a menudo hay reorg importantes; desde este punto de vista es peor que mainnet.

Muchos wallet, green, electrum, specter, sparrow y otros, soportan testnet y pueden usarse para:

- aprender sin poner en riesgo los propios fondos,
- con fines didácticos,
- experimentar cosas nuevas.

Algunas herramientas útiles, autopromoción, para testnet:

- [BTCBouncer](http://btcbouncer.com) permite efectuar pagos a varias direcciones y recibir los fondos, menos una fee, en el plazo de un par de bloques,
- [BTCSigner](http://btcsigner.com) permite experimentar un multisig con un nodo core en testnet.

Hay muchas otras herramientas y sitios web que soportan testnet, además de los block explorer más importantes.

## Bitcoin-cli
Bitcoin-cli es la utilidad de línea de comandos para interactuar con Bitcoin Core.

Los comandos tienen el formato:
```
bitcoin-cli [options] <command> [params]
```
y siempre se puede usar `help` para obtener la lista de comandos o información sobre un comando específico.

### Comandos informativos sobre la blockchain
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

### Comandos de control
- help ( "command" )
- stop
- uptime
- ...

### Comandos para el mining
- getblocktemplate ( "template_request" )
- submitblock "hexdata" ( "dummy" )
- ...

### Comandos para la red
- addnode "node" "command"
- disconnectnode ( "address" nodeid )
- getnetworkinfo
- ...

### Gestión de Rawtransactions
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

### Utilidades
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

Un curso completo sobre el uso de Bitcoin desde la línea de comandos se puede encontrar en [Learning-Bitcoin-from-the-Command-Line](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line).

## Programa
La instalación del nodo está dividida en varias lecciones; aquí hay una lista de las ya impartidas:

| Fecha       | Notas                                          |
|-------------|------------------------------------------------|
| 240108-2100 | Selección del hardware                         |
| 240115-2200 | Instalación de core y verificación de firmas   |
| 240122-2200 | Configuración mínima                           |
