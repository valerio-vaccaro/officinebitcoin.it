---
layout: default
title: "Fullnode e hardware para um nó"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lição Bitcoin-only</span> <span>Este projeto é mantido por valerio-vaccaro</span></p>

## 🌍 Traduções

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Fullnode e hardware para um nó

Ter um nó Bitcoin é fundamental, pois permite, com a máxima privacidade:

- validar toda a cadeia do Bitcoin,
- verificar o saldo dos nossos wallets,
- transmitir as nossas novas transações,
- ...

## Seleção do hardware

- mínimo 2GB de memória RAM, recomendados 4GB,
- disco com pelo menos 1TB de armazenamento, recomendados 2TB,
- cpu multi-core suficientemente potente, provavelmente qualquer processador desenvolvido na última década.

### Reutiliza um computador antigo

Um computador antigo pode ser reciclado como nó. No caso de um laptop, recomenda-se remover a bateria, que, estando sempre em carga, poderia representar um risco. A grande vantagem é o custo igual a zero ou limitado apenas ao disco de maior capacidade.

### Raspberry pi e outras placas

Raspberry pi é uma placa ARM muito usada para criar sistemas IoT e nós. No entanto, o custo excessivo e a necessidade de um disco ligado por USB fazem com que não seja a melhor escolha possível em termos de desempenho e estabilidade.

Odroid-M1 é uma placa ARM potente e com um slot interno para adicionar armazenamento extra.

### Thin client

Com um orçamento muito reduzido, 30-100 euros, é possível comprar um Thin Client usado, no ebay, que combina baixo consumo com desempenho suficiente para executar o nó.

Como exemplos de Thin Client, foram testados os seguintes modelos:

- Fujitsu Futro s920
- HP t620

## Seleção do software

Instalar o mínimo possível de software num nó limita os possíveis ataques e torna o sistema mais simples de manter.

Online encontram-se soluções prontas, como Umbrel, Mynode e outras, que mascaram as verificações de segurança e acrescentam software e scripts, por exemplo docker, difíceis de controlar. Nestas lições vamos focar-nos na criação de um nó manualmente, ou seja, instalando manualmente todo o software necessário.

### Passo 0 - O sistema operativo

A primeira escolha a fazer é o sistema operativo. A recomendação é usar Linux numa versão LTS, ou seja, com suporte garantido por um número suficientemente longo de anos. A minha escolha pessoal recai sobre Debian 12.

O sistema operativo escolhido deve então ser instalado no computador e todos os pacotes devem ser atualizados. A atualização será algo que nos acompanhará durante toda a vida do nó.

Também se recomenda instalar tor, e/ou outra VPN se necessária, e ssh, para permitir a manutenção remota do nó.

Por fim, uma UPS poderia salvar o nó de quedas bruscas de corrente, evitando deixar bitcoin e os outros softwares num estado inconsistente.

### Passo 1 - Instalamos Bitcoin

Descarregamos core, os hashes e as assinaturas.

```
wget https://bitcoincore.org/bin/bitcoin-core-28.1/bitcoin-28.1-x86_64-linux-gnu.tar.gz
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS.asc
```

Caso se utilize uma board com arquitetura arm, o pacote deverá ser corrigido para `bitcoin-28.1-aarch64-linux-gnu.tar.gz`, isto é, o mesmo pacote mas compilado para a arquitetura arm de 64 bits, aarch64, que é precisamente a usada pela odroid.

Neste ponto podemos verificar se um dos hashes em SHA256SUMS corresponde ao arquivo descarregado.

```
sha256sum --ignore-missing --check SHA256SUMS
```

O resultado indica que foi encontrada uma correspondência para o arquivo descarregado.

```
bitcoin-28.1-x86_64-linux-gnu.tar.gz: OK
```

Agora verificamos as assinaturas do ficheiro SHA256SUMS. Antes, se necessário, obtemos as chaves e importamo-las.

```
git clone https://github.com/bitcoin-core/guix.sigs
gpg --import guix.sigs/builder-keys/*
```

E por fim verificamos as assinaturas.

```
gpg --verify SHA256SUMS.asc
```

Se virmos várias vezes a mensagem `gpg: Good signature from ...`, significa que encontrámos assinaturas válidas.

Procedemos à descompactação e instalação.

```
tar xzvf bitcoin-28.1-x86_64-linux-gnu.tar.gz 
sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-28.1/bin/*
```

E pronto: agora temos `bitcoind`, `bitcoin-cli` e as outras utilidades prontas para serem lançadas.

Por agora lançamos `bitcoind` e veremos algum log. O Bitcoin começa a sincronizar-se e agora existirá um diretório com a blockchain e todas as configurações em `~/.bitcoin/`.

A partir de outro terminal podemos verificar o funcionamento do bitcoind executando o comando `tail -f ~/.bitcoin/debug.log`.

### Passo 1b - Configuramos Bitcoin

Como já vimos anteriormente, o diretório em que o Bitcoin Core guarda as configurações e a blockchain no Linux é `~/.bitcoin/`. Caso se queira alterar a localização de armazenamento, podem usar-se diferentes abordagens:

- criar um link simbólico do diretório para um disco maior com o comando `ln -s`,
- usar na linha de comando ou dentro de bitcoin.conf o comando `datadir`, especificando o diretório de destino.

O Bitcoin Core suporta três tipos diferentes de redes às quais se pode ligar:
- `mainnet`, a rede clássica a que todos estamos habituados e que é o padrão do core,
- `testnet`, uma rede análoga à mainnet, mas cujos tokens não têm valor; o mining continua a ser efetuado, mas se não houver blocos durante 20 minutos a dificuldade cai drasticamente; sofre frequentemente reorg importantes,
- `regtest`, neste modo tem-se uma pequena blockchain privada que começa sempre do zero e onde é possível minerar com dificuldade mínima; serve para testes locais.

Outro comando útil é `daemon`, que, se definido, não mantém o log do Bitcoin Core ligado à consola atual. Para ver o funcionamento, será sempre possível usar o comando `tail -f ~/.bitcoin/debug.log`.

Todas as configurações podem ser lançadas pela linha de comando ou através do ficheiro `~/.bitcoin/bitcoin.conf`. Um ficheiro compatível com uma configuração doméstica, isto é, em que quero manter o consumo de recursos no mínimo, poderia ser o seguinte.
ficheiro de configuração

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

Onde:

- o servidor é desligado da consola com `daemon=1`
- são descarregados apenas os blocos e não a mempool, `blocksonly=1`
- são permitidas até vinte ligações, `txindex=1`
- enviam-se informações aos outros nós na internet até ao máximo de 500 megabytes por dia, `maxuploadtarget=500`
- mantém-se um índice das transações, `txindex=1`
- mantém-se um índice dos blockfilter, `blockfilterindex=1`
- damos a qualquer pessoa a possibilidade de se ligar por rpc, `rpcallowip=0.0.0.0/0`
- ligamos rpc a todas as placas de rede, `rpcallowip=0.0.0.0/0`
- definimos um username para rpc, `rpcuser=username`, obviamente a substituir
- definimos uma password para rpc, `rpcpassword=password`, obviamente a substituir

A lista completa das funcionalidades pode ser encontrada em [https://jlopp.github.io/bitcoin-core-config-generator](https://jlopp.github.io/bitcoin-core-config-generator)

Também se pode fazer tudo com um único comando de terminal.

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

Caso se tenha disponível outro nó já sincronizado, pode usar-se a opção `connect` para se ligar SÓ E EXCLUSIVAMENTE a esse nó. Se esse nó estiver na rede local, ganha-se tempo e largura de banda com esta configuração simples.

Desde a release 26, o core suporta cifragem das comunicações entre os nós com a opção `v2transport`.

Todas as configurações mostradas dizem respeito à clearnet; as configurações para tor serão objeto de outra lição.

### Passo 1c - Lançamos Bitcoin

Lançamos Bitcoin criando um ficheiro de arranque para systemd.

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
Atenção: neste caso estamos a usar o utilizador `bitcoin` para iniciar o software.

Podemos então registar o script criado e lançá-lo.

```
sudo systemctl enable bitcoind
sudo systemctl start bitcoind
```

Sempre que se quiser verificar o estado do software, pode usar-se o seguinte comando.

```
systemctl status bitcoind
```

### Passo 2 - Instalamos Electrs

Instalamos `Electrs`, que é um servidor electrum baseado em `Rust`; o primeiro passo é, portanto, instalar essa linguagem.

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Instalamos também clang e o pacote build-essential.

```
apt update
apt install clang cmake build-essential -y
```

Descarregamos a última versão, atualmente a 0.10.5, do Github.

```
VERSION="0.10.5"
git clone --branch v$VERSION https://github.com/romanz/electrs.git
cd electrs
```

Importamos a chave do programador de `Electrs` e verificamos a assinatura dos commits Github.

```
curl https://romanzey.de/pgp.txt | gpg --import
git verify-tag v$VERSION
```

Se a assinatura estiver correta, podemos passar à compilação ...

```
cargo build --locked --release
```

e depois à instalação.

```
sudo install -m 0755 -o root -g root -t /usr/local/bin ./target/release/electrs
```

### Passo 2b - Configuramos Electrs

Para configurar `Electrs`, criamos o ficheiro `config.toml` com o seguinte conteúdo.

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

Também se pode fazer tudo com um único comando de terminal.

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

Podemos lançar Elects com o comando

```
electrs --conf config.toml
```

e esperar que electrs termine de indexar todos os blocos.

### Passo 2c - Lançamos Electrs

Como no Bitcoin, podemos lançar o software criando um script para systemd.

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

Atenção: neste caso estamos a usar o utilizador `bitcoin` para iniciar o software.

Podemos então registar o script criado e lançá-lo.

```
sudo systemctl enable electrs
sudo systemctl start electrs
```

Sempre que se quiser verificar o estado do software, pode usar-se o seguinte comando.

```
systemctl status electrs
```

### Passo 3 - Instalamos CLN

A completar

### Passo 3b - Configuramos CLN

A completar

### Passo 4 - Instalamos Mempool.space

Instalamos `mariadb`.

```
sudo apt-get install mariadb-server mariadb-client
```

E criamos db e utilizador.

```
sudo mysql -e "drop database mempool;"
sudo mysql -e "create database mempool;"
sudo mysql -e "grant all privileges on mempool.* to 'mempool'@'%' identified by 'mempool';"
sudo mysql -e "flush privileges;"
```

Clonamos o código

```
git clone https://github.com/mempool/mempool
cd mempool
latestrelease=$(curl -s https://api.github.com/repos/mempool/mempool/releases/latest|grep tag_name|head -1|cut -d '"' -f4)
git checkout $latestrelease

```

Certifiquemo-nos de usar node 20.x e a última versão do npm.

```
sudo npm i -g npm
sudo npm i -g node@20
```

Tratamos de compilar e testar o backend

```
cd backend
npm install --no-install-links # npm@9.4.2 and later can omit the --no-install-links
npm run build

cp mempool-config.sample.json mempool-config.json
npm run start
```

Verificar atentamente as configurações de `mempool-config.json`.

Passamos ao frontend.

```
cd ..

cd frontend
npm install
npm run serve:local-prod
```


### Passo 4b - Configuramos Mempool

A configuração do backend encontra-se no ficheiro `mempool-config.json`.

### Passo 4c - Lançamos Mempool

Podemos lançar Mempool com pm2, que deve ser instalado.

```
sudo npm i -g pm2
pm2 startup 
```

Lançamos o backend.

```
cd ..
cd backend 
pm2 start "npm run start"
```

Depois lançamos o frontend.

```
cd ..
cd frontend
pm2 start "npm run serve:local-prod"
```

Guardamos tudo.

```
pm2 save
```

## Bitcoin com ligação apenas via tor
Começamos por instalar tor.


```
sudo apt install tor
```

e configuramos o ficheiro de configuração do tor para criar um novo hidden service exportando a porta 8333 do nó.


```
cat > /etc/tor/torrc <<EOL
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 8333 127.0.0.1:8333
EOL
```

Podemos reiniciar o tor para aplicar as alterações; isto permite exportar a porta 8333 do nosso nó, mas não limitar o acesso ao nó apenas e exclusivamente via tor.

```
sudo systemctl restart tor
``` 

e obter o endereço onion do nó.

```
cat /var/lib/tor/hidden_service/hostname
```

Feito isso, podemos limitar o acesso ao nó apenas e exclusivamente via tor, modificando a configuração de bitcoin.conf deste modo:

```
proxy=127.0.0.1:9050
listen=1
bind=127.0.0.1:8333=onion
externalip=tor_url.onion
onlynet=onion
```

Onde `tor_url.onion` é o endereço onion do nó obtido anteriormente.


Ao reiniciar o nó, podemos verificar que o nó é acessível apenas e exclusivamente via tor.

```
sudo systemctl restart bitcoind

bitcoin-cli getnetworkinfo
```

Aqui deveríamos ver que o nó é acessível apenas e exclusivamente via tor, ou seja, que só a rede `onion` está `reachable`.

Além disso, todos os nossos peer serão identificados por endereços onion.

```
bitcoin-cli getpeerinfo
```

Atenção: tor é extremamente lento; tenham isso em conta quando quiserem sincronizar o nó a partir do zero.

## Testnet
Uma rede útil para ganhar prática é `testnet`, que difere de `mainnet` porque:

- os tokens não têm valor e existem sites que vos oferecem satoshi de testnet para fazer testes,
- podem transacionar sempre com o mínimo de fees,
- o mining é flutuante, também porque não se ganha nada com ele,
- se um bloco não for minerado durante 20 minutos, a dificuldade cai drasticamente,
- frequentemente há reorg importantes; deste ponto de vista é pior do que mainnet.

Muitos wallets, green, electrum, specter, sparrow e outros, suportam testnet e podem ser usados para:

- aprender sem pôr em risco os próprios fundos,
- fins didáticos,
- experimentar coisas novas.

Algumas ferramentas úteis, autopromoção, para testnet:

- [BTCBouncer](http://btcbouncer.com) permite efetuar pagamentos para vários endereços e receber os fundos, menos uma fee, no espaço de alguns blocos,
- [BTCSigner](http://btcsigner.com) permite experimentar um multisig com um nó core em testnet.

Existem muitos outros tools e sites web que suportam testnet, além dos block explorer mais importantes.

## Bitcoin-cli
Bitcoin-cli é a utilidade de linha de comando para interagir com Bitcoin Core.

Os comandos têm o formato:
```
bitcoin-cli [options] <command> [params]
```
e pode-se sempre usar `help` para obter a lista dos comandos ou informações sobre um comando específico.

### Comandos informativos sobre a blockchain
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

### Comandos de controlo
- help ( "command" )
- stop
- uptime
- ...

### Comandos para mining
- getblocktemplate ( "template_request" )
- submitblock "hexdata" ( "dummy" )
- ...

### Comandos para a rede
- addnode "node" "command"
- disconnectnode ( "address" nodeid )
- getnetworkinfo
- ...

### Gestão de Rawtransactions
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

Um curso completo sobre o uso de Bitcoin pela linha de comando pode ser encontrado em [Learning-Bitcoin-from-the-Command-Line](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line).

## Programa
A instalação do nó está dividida em várias lições; aqui está uma lista das já realizadas:

| Data        | Notas                                          |
|-------------|------------------------------------------------|
| 240108-2100 | Seleção do hardware                            |
| 240115-2200 | Instalação do core e verificação das assinaturas |
| 240122-2200 | Configuração mínima                            |
