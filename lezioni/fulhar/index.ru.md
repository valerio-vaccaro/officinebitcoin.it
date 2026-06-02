---
layout: default
title: "Fullnode и аппаратное обеспечение для узла"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Урок Bitcoin-only</span> <span>Этот проект поддерживает valerio-vaccaro</span></p>

## 🌍 Переводы

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Fullnode и аппаратное обеспечение для узла

Иметь узел Bitcoin важно, потому что он позволяет с максимальной приватностью:

- проверять всю цепочку Bitcoin,
- контролировать баланс наших wallet,
- передавать наши новые транзакции,
- ...

## Выбор аппаратного обеспечения

- минимум 2GB оперативной памяти, рекомендуется 4GB,
- диск не менее 1TB массового хранилища, рекомендуется 2TB,
- достаточно производительный multi-core cpu, вероятно любой процессор, разработанный за последнее десятилетие.

### Повторно использовать старый компьютер

Старый компьютер можно использовать как узел. В случае laptop рекомендуется вынуть аккумулятор, потому что постоянное нахождение на зарядке может быть риском. Большое преимущество в том, что стоимость равна нулю или ограничена только более емким диском.

### Raspberry pi и другие платы

Raspberry pi — это ARM-плата, часто используемая для IoT-систем и узлов. Однако высокая стоимость и необходимость диска через USB делают ее не лучшим выбором по производительности и стабильности.

Odroid-M1 — производительная ARM-плата с внутренним слотом для добавления дополнительного хранилища.

### Thin client

С очень небольшим бюджетом, 30-100 евро, можно купить подержанный Thin Client, например на ebay, который сочетает низкое потребление с производительностью, достаточной для работы узла.

В качестве примеров Thin Client были протестированы следующие модели:

- Fujitsu Futro s920
- HP t620

## Выбор программного обеспечения

Установка минимально возможного количества программ на узел ограничивает возможные атаки и упрощает обслуживание системы.

В сети есть готовые решения, такие как Umbrel, Mynode и другие, которые скрывают проверки безопасности и добавляют программное обеспечение и скрипты, например docker, которые трудно контролировать. В этих уроках мы сосредоточимся на создании узла вручную, то есть на ручной установке всего необходимого ПО.

### Шаг 0 - Операционная система

Первый выбор — операционная система. Рекомендуется использовать Linux в версии LTS, то есть с гарантированной поддержкой на достаточно долгий срок. Мой личный выбор — Debian 12.

Выбранную операционную систему нужно установить на компьютер и обновить все пакеты. Обновления будут сопровождать нас в течение всей жизни узла.

Также рекомендуется установить tor, и/или другую VPN при необходимости, а также ssh, чтобы обеспечить удаленное обслуживание узла.

Наконец, источник бесперебойного питания может защитить узел от резких отключений электричества, не оставляя bitcoin и другое ПО в неконсистентном состоянии.

### Шаг 1 - Устанавливаем Bitcoin

Скачиваем core, хэши и подписи.

```
wget https://bitcoincore.org/bin/bitcoin-core-28.1/bitcoin-28.1-x86_64-linux-gnu.tar.gz
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS.asc
```

Если используется board с архитектурой arm, пакет нужно заменить на `bitcoin-28.1-aarch64-linux-gnu.tar.gz`, то есть на тот же пакет, но собранный для 64-битной arm-архитектуры aarch64, которая как раз используется odroid.

Теперь можно проверить, что один из хэшей в SHA256SUMS соответствует скачанному архиву.

```
sha256sum --ignore-missing --check SHA256SUMS
```

Результат сообщает, что для скачанного архива найдено совпадение.

```
bitcoin-28.1-x86_64-linux-gnu.tar.gz: OK
```

Теперь проверим подписи файла SHA256SUMS. Сначала, если нужно, получим ключи и импортируем их.

```
git clone https://github.com/bitcoin-core/guix.sigs
gpg --import guix.sigs/builder-keys/*
```

И наконец проверим подписи.

```
gpg --verify SHA256SUMS.asc
```

Если несколько раз видим строку `gpg: Good signature from ...`, значит мы нашли действительные подписи.

Переходим к распаковке и установке.

```
tar xzvf bitcoin-28.1-x86_64-linux-gnu.tar.gz 
sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-28.1/bin/*
```

Готово: теперь у нас есть `bitcoind`, `bitcoin-cli` и другие утилиты, готовые к запуску.

Пока запустим `bitcoind` и увидим немного логов. Bitcoin начнет синхронизацию, и появится каталог с blockchain и всеми конфигурациями в `~/.bitcoin/`.

Из другого терминала можно проверить работу bitcoind командой `tail -f ~/.bitcoin/debug.log`.

### Шаг 1b - Настраиваем Bitcoin

Как уже было видно, каталог, в котором Bitcoin Core сохраняет конфигурации и blockchain в Linux, — это `~/.bitcoin/`. Если нужно изменить место хранения, можно использовать разные подходы:

- создать символическую ссылку каталога на больший диск командой `ln -s`,
- использовать из командной строки или внутри bitcoin.conf команду `datadir`, указав целевой каталог.

Bitcoin Core поддерживает три разных типа сетей для подключения:
- `mainnet`, классическая сеть, к которой мы все привыкли, и значение по умолчанию для core,
- `testnet`, сеть, аналогичная mainnet, но токены не имеют ценности; mining все равно выполняется, но при отсутствии блоков в течение 20 минут сложность резко падает; часто страдает от серьезных reorg,
- `regtest`, в этом режиме есть небольшая приватная blockchain, которая всегда начинается с нуля и где можно майнить с минимальной сложностью; нужна для локальных тестов.

Еще одна полезная команда — `daemon`: если она задана, лог Bitcoin Core не остается привязанным к текущей консоли. Для просмотра работы всегда можно использовать `tail -f ~/.bitcoin/debug.log`.

Все конфигурации можно запускать из командной строки или через файл `~/.bitcoin/bitcoin.conf`. Файл, подходящий для домашнего setup, где нужно держать потребление ресурсов минимальным, может выглядеть так.
файл конфигурации

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

Где:

- сервер отсоединяется от консоли с `daemon=1`
- скачиваются только блоки, а не mempool, `blocksonly=1`
- разрешено до двадцати соединений, `txindex=1`
- информация отправляется другим узлам в интернете максимум на 500 мегабайт в день, `maxuploadtarget=500`
- поддерживается индекс транзакций, `txindex=1`
- поддерживается индекс blockfilter, `blockfilterindex=1`
- мы даем возможность любому подключаться через rpc, `rpcallowip=0.0.0.0/0`
- привязываем rpc ко всем сетевым интерфейсам, `rpcallowip=0.0.0.0/0`
- задаем username для rpc, `rpcuser=username`, конечно, его нужно заменить
- задаем password для rpc, `rpcpassword=password`, конечно, его нужно заменить

Полный список функций можно найти на [https://jlopp.github.io/bitcoin-core-config-generator](https://jlopp.github.io/bitcoin-core-config-generator)

Все это можно сделать одной командой в терминале.

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

Если есть другой уже синхронизированный узел, можно использовать опцию `connect`, чтобы подключаться ТОЛЬКО И ИСКЛЮЧИТЕЛЬНО к этому узлу. Если он находится в локальной сети, эта простая конфигурация экономит время и пропускную способность.

Начиная с release 26, core поддерживает шифрование коммуникаций между узлами с опцией `v2transport`.

Все показанные конфигурации относятся к clearnet; конфигурации для tor будут темой другого урока.

### Шаг 1c - Запускаем Bitcoin

Запускаем Bitcoin, создав файл запуска для systemd.

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
Внимание: в этом случае мы используем пользователя `bitcoin` для запуска software.

Теперь можно зарегистрировать созданный скрипт и запустить его.

```
sudo systemctl enable bitcoind
sudo systemctl start bitcoind
```

Каждый раз, когда нужно проверить состояние software, можно использовать следующую команду.

```
systemctl status bitcoind
```

### Шаг 2 - Устанавливаем Electrs

Устанавливаем `Electrs`, electrum server на основе `Rust`; первый шаг — установить этот язык.

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Также устанавливаем clang и пакет build-essential.

```
apt update
apt install clang cmake build-essential -y
```

Скачиваем последнюю версию, сейчас 0.10.5, с Github.

```
VERSION="0.10.5"
git clone --branch v$VERSION https://github.com/romanz/electrs.git
cd electrs
```

Импортируем ключ разработчика `Electrs` и проверяем подпись commit Github.

```
curl https://romanzey.de/pgp.txt | gpg --import
git verify-tag v$VERSION
```

Если подпись корректна, можно переходить к компиляции ...

```
cargo build --locked --release
```

а затем к установке.

```
sudo install -m 0755 -o root -g root -t /usr/local/bin ./target/release/electrs
```

### Шаг 2b - Настраиваем Electrs

Чтобы настроить `Electrs`, создаем файл `config.toml` со следующим содержимым.

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

Все это можно сделать одной командой в терминале.

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

Можно запустить Elects командой

```
electrs --conf config.toml
```

и дождаться, пока electrs закончит индексировать все блоки.

### Шаг 2c - Запускаем Electrs

Как и для Bitcoin, можно запустить software, создав скрипт для systemd.

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

Внимание: в этом случае мы используем пользователя `bitcoin` для запуска software.

Теперь можно зарегистрировать созданный скрипт и запустить его.

```
sudo systemctl enable electrs
sudo systemctl start electrs
```

Каждый раз, когда нужно проверить состояние software, можно использовать следующую команду.

```
systemctl status electrs
```

### Шаг 3 - Устанавливаем CLN

Требует дополнения

### Шаг 3b - Настраиваем CLN

Требует дополнения

### Шаг 4 - Устанавливаем Mempool.space

Устанавливаем `mariadb`.

```
sudo apt-get install mariadb-server mariadb-client
```

И создаем db и пользователя.

```
sudo mysql -e "drop database mempool;"
sudo mysql -e "create database mempool;"
sudo mysql -e "grant all privileges on mempool.* to 'mempool'@'%' identified by 'mempool';"
sudo mysql -e "flush privileges;"
```

Клонируем код

```
git clone https://github.com/mempool/mempool
cd mempool
latestrelease=$(curl -s https://api.github.com/repos/mempool/mempool/releases/latest|grep tag_name|head -1|cut -d '"' -f4)
git checkout $latestrelease

```

Убедимся, что используем node 20.x и последнюю версию npm.

```
sudo npm i -g npm
sudo npm i -g node@20
```

Компилируем и тестируем backend

```
cd backend
npm install --no-install-links # npm@9.4.2 and later can omit the --no-install-links
npm run build

cp mempool-config.sample.json mempool-config.json
npm run start
```

Внимательно проверить конфигурации в `mempool-config.json`.

Переходим к frontend.

```
cd ..

cd frontend
npm install
npm run serve:local-prod
```


### Шаг 4b - Настраиваем Mempool

Конфигурация backend находится в файле `mempool-config.json`.

### Шаг 4c - Запускаем Mempool

Mempool можно запустить через pm2, который нужно установить.

```
sudo npm i -g pm2
pm2 startup 
```

Запускаем backend.

```
cd ..
cd backend 
pm2 start "npm run start"
```

Затем запускаем frontend.

```
cd ..
cd frontend
pm2 start "npm run serve:local-prod"
```

Сохраняем все.

```
pm2 save
```

## Bitcoin с подключением только через tor
Начнем с установки tor.


```
sudo apt install tor
```

и настроим конфигурационный файл tor, чтобы создать новый hidden service, экспортирующий порт 8333 узла.


```
cat > /etc/tor/torrc <<EOL
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 8333 127.0.0.1:8333
EOL
```

Можно перезапустить tor, чтобы применить изменения. Это позволяет экспортировать порт 8333 нашего узла, но еще не ограничивает доступ к узлу только и исключительно через tor.

```
sudo systemctl restart tor
``` 

и получить onion-адрес узла.

```
cat /var/lib/tor/hidden_service/hostname
```

После этого можно ограничить доступ к узлу только и исключительно через tor, изменив конфигурацию bitcoin.conf так:

```
proxy=127.0.0.1:9050
listen=1
bind=127.0.0.1:8333=onion
externalip=tor_url.onion
onlynet=onion
```

Где `tor_url.onion` — onion-адрес узла, полученный ранее.


Перезапустив узел, можно проверить, что он доступен только и исключительно через tor.

```
sudo systemctl restart bitcoind

bitcoin-cli getnetworkinfo
```

Здесь мы должны увидеть, что узел доступен только и исключительно через tor, то есть что только сеть `onion` является `reachable`.

Кроме того, все наши peer будут идентифицированы onion-адресами.

```
bitcoin-cli getpeerinfo
```

Внимание: tor крайне медленный; учитывайте это, когда хотите синхронизировать узел с нуля.

## Testnet
Полезная сеть для практики — `testnet`, которая отличается от `mainnet` тем, что:

- токены не имеют ценности, и есть сайты, предлагающие satoshi testnet для проведения тестов,
- можно всегда проводить транзакции с минимальными fee,
- mining нестабилен, в том числе потому, что на нем ничего не зарабатывают,
- если блок не был добыт в течение 20 минут, сложность резко падает,
- часто бывают серьезные reorg; с этой точки зрения она хуже mainnet.

Многие wallet, green, electrum, specter, sparrow и другие, поддерживают testnet и могут использоваться для:

- обучения без риска для собственных средств,
- учебных целей,
- экспериментов с новыми вещами.

Некоторые полезные инструменты, самореклама, для testnet:

- [BTCBouncer](http://btcbouncer.com) позволяет выполнять платежи на разные адреса и получать средства, за вычетом fee, в течение пары блоков,
- [BTCSigner](http://btcsigner.com) позволяет экспериментировать с multisig с core-узлом в testnet.

Есть много других tools и сайтов, поддерживающих testnet, помимо самых важных block explorer.

## Bitcoin-cli
Bitcoin-cli — это утилита командной строки для взаимодействия с Bitcoin Core.

Команды имеют формат:
```
bitcoin-cli [options] <command> [params]
```
и всегда можно использовать `help`, чтобы получить список команд или информацию о конкретной команде.

### Информационные команды о blockchain
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

### Команды управления
- help ( "command" )
- stop
- uptime
- ...

### Команды для mining
- getblocktemplate ( "template_request" )
- submitblock "hexdata" ( "dummy" )
- ...

### Команды для сети
- addnode "node" "command"
- disconnectnode ( "address" nodeid )
- getnetworkinfo
- ...

### Управление Rawtransactions
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

### Утилиты
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

Полный курс по использованию Bitcoin из командной строки можно найти по адресу [Learning-Bitcoin-from-the-Command-Line](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line).

## Программа
Установка узла разделена на несколько уроков; вот список уже проведенных:

| Дата        | Примечания                                     |
|-------------|------------------------------------------------|
| 240108-2100 | Выбор аппаратного обеспечения                  |
| 240115-2200 | Установка core и проверка подписей             |
| 240122-2200 | Минимальная конфигурация                       |
