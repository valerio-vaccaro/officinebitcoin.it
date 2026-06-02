---
layout: default
title: "用于节点的 Fullnode 与硬件"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only 课程</span> <span>本项目由 valerio-vaccaro 维护</span></p>

## 🌍 翻译

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# 用于节点的 Fullnode 与硬件

拥有一个 Bitcoin 节点非常重要，因为它可以在最大程度保护隐私的情况下：

- 验证整个 Bitcoin 链，
- 检查我们 wallet 的余额，
- 广播我们的新交易，
- ...

## 硬件选择

- 至少 2GB RAM，建议 4GB，
- 至少 1TB 存储盘，建议 2TB，
- 性能足够的 multi-core cpu，最近十年开发的处理器大概率都可以。

### 复用旧电脑

旧电脑可以回收用作节点。如果是 laptop，建议取出电池，因为电池长期处于充电状态可能带来风险。它最大的优势是成本为零，或只需要购买更大容量磁盘的成本。

### Raspberry pi 和其他开发板

Raspberry pi 是一块 ARM 板，常用于构建 IoT 系统和节点。不过，较高的成本以及必须通过 USB 接入磁盘，使它在性能和稳定性方面并不是最佳选择。

Odroid-M1 是一块性能较好的 ARM 板，并带有内部 slot，可用于添加额外的大容量存储。

### Thin client

预算很低时，30-100 欧元即可购买一台二手 Thin Client，例如在 ebay 上。它把低功耗和足以运行节点的性能结合在一起。

以下 Thin Client 型号已作为示例测试：

- Fujitsu Futro s920
- HP t620

## 软件选择

在节点上安装尽可能少的软件，可以限制可能的攻击面，也让系统更容易维护。

网上可以找到预打包方案，例如 Umbrel、Mynode 等。这些方案会掩盖安全检查，并加入难以控制的软件和脚本，例如 docker。在这些课程中，我们会关注手工创建节点，也就是手动安装所有必要软件。

### 步骤 0 - 操作系统

首先要选择操作系统。建议使用 LTS 版本的 Linux，也就是能保证足够多年支持的版本。我个人选择 Debian 12。

选定的操作系统需要安装到电脑上，并更新所有软件包。更新会贯穿节点的整个生命周期。

还建议安装 tor，和/或在需要时安装其他 VPN，以及 ssh，以便远程维护节点。

最后，不间断电源可以保护节点免受突然断电影响，避免 bitcoin 和其他软件停留在不一致状态。

### 步骤 1 - 安装 Bitcoin

下载 core、hash 和签名。

```
wget https://bitcoincore.org/bin/bitcoin-core-28.1/bitcoin-28.1-x86_64-linux-gnu.tar.gz
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS.asc
```

如果使用 arm 架构的 board，包名需要改为 `bitcoin-28.1-aarch64-linux-gnu.tar.gz`，也就是同一个包，但编译目标为 64 位 arm 架构 aarch64，而这正是 odroid 使用的架构。

此时可以检查 SHA256SUMS 中是否有一个 hash 与下载的归档文件匹配。

```
sha256sum --ignore-missing --check SHA256SUMS
```

结果会提示下载的归档文件找到了匹配项。

```
bitcoin-28.1-x86_64-linux-gnu.tar.gz: OK
```

现在验证 SHA256SUMS 文件的签名。必要时，先获取密钥并导入。

```
git clone https://github.com/bitcoin-core/guix.sigs
gpg --import guix.sigs/builder-keys/*
```

最后验证签名。

```
gpg --verify SHA256SUMS.asc
```

如果多次看到 `gpg: Good signature from ...`，就表示找到了有效签名。

继续解压和安装。

```
tar xzvf bitcoin-28.1-x86_64-linux-gnu.tar.gz 
sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-28.1/bin/*
```

完成后，我们已有 `bitcoind`、`bitcoin-cli` 和其他工具，可以直接运行。

现在先运行 `bitcoind`，会看到一些 log。Bitcoin 开始同步，此时 `~/.bitcoin/` 中会出现包含 blockchain 和所有配置的目录。

可以从另一个终端运行 `tail -f ~/.bitcoin/debug.log` 来检查 bitcoind 的运行情况。

### 步骤 1b - 配置 Bitcoin

如前所述，在 Linux 系统中，Bitcoin Core 保存配置和 blockchain 的目录是 `~/.bitcoin/`。如果想改变保存位置，可以使用不同方法：

- 使用 `ln -s` 命令，在更大的磁盘上创建该目录的符号链接，
- 从命令行或在 bitcoin.conf 内使用 `datadir` 命令，并指定目标目录。

Bitcoin Core 支持连接三种不同类型的网络：
- `mainnet`，这是我们熟悉的经典网络，也是 core 的默认网络，
- `testnet`，它类似 mainnet，但 token 没有价值；mining 仍会进行，但如果 20 分钟没有区块，难度会急剧下降；它经常遭遇严重 reorg，
- `regtest`，在这种模式下有一条小型私有 blockchain，总是从零开始，可以用最低难度挖矿；用于本地测试。

另一个有用命令是 `daemon`。如果设置它，Bitcoin Core 的 log 不会保持连接到当前 console。要查看运行情况，仍可使用 `tail -f ~/.bitcoin/debug.log`。

所有配置都可以从命令行启动，或通过 `~/.bitcoin/bitcoin.conf` 文件设置。适合家庭 setup，也就是希望资源消耗保持最低的文件，可以如下所示。
配置文件

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

其中：

- server 通过 `daemon=1` 与 console 分离
- 只下载区块，不下载 mempool，`blocksonly=1`
- 最多允许二十个连接，`txindex=1`
- 每天最多向互联网中的其他节点发送 500 megabyte 信息，`maxuploadtarget=500`
- 保留交易索引，`txindex=1`
- 保留 blockfilter 索引，`blockfilterindex=1`
- 允许任何人通过 rpc 连接，`rpcallowip=0.0.0.0/0`
- 将 rpc 绑定到所有网卡，`rpcallowip=0.0.0.0/0`
- 为 rpc 设置 username，`rpcuser=username`，显然需要替换
- 为 rpc 设置 password，`rpcpassword=password`，显然需要替换

完整功能列表可在 [https://jlopp.github.io/bitcoin-core-config-generator](https://jlopp.github.io/bitcoin-core-config-generator) 找到。

也可以用一个终端命令完成全部操作。

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

如果有另一个已经同步好的节点，可以使用 `connect` 选项，只且仅连接到这个节点。如果该节点在本地网络中，这个简单配置可以节省时间和带宽。

从 release 26 开始，core 通过 `v2transport` 选项支持节点间通信加密。

这里展示的所有配置都针对 clearnet；tor 配置将是另一节课的主题。

### 步骤 1c - 启动 Bitcoin

通过为 systemd 创建启动文件来启动 Bitcoin。

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
注意：这里使用 `bitcoin` 用户来启动软件。

然后可以注册创建好的 script 并启动。

```
sudo systemctl enable bitcoind
sudo systemctl start bitcoind
```

每当想检查软件状态时，可以使用下面的命令。

```
systemctl status bitcoind
```

### 步骤 2 - 安装 Electrs

安装 `Electrs`，它是一个基于 `Rust` 的 electrum server，因此第一步是安装该语言。

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

同时安装 clang 和 build-essential 包。

```
apt update
apt install clang cmake build-essential -y
```

从 Github 下载最新版本，目前是 0.10.5。

```
VERSION="0.10.5"
git clone --branch v$VERSION https://github.com/romanz/electrs.git
cd electrs
```

导入 `Electrs` 开发者的密钥，并验证 Github commit 的签名。

```
curl https://romanzey.de/pgp.txt | gpg --import
git verify-tag v$VERSION
```

如果签名正确，就可以进入编译 ...

```
cargo build --locked --release
```

然后安装。

```
sudo install -m 0755 -o root -g root -t /usr/local/bin ./target/release/electrs
```

### 步骤 2b - 配置 Electrs

要配置 `Electrs`，创建 `config.toml` 文件，内容如下。

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

也可以用一个终端命令完成全部操作。

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

可以用下面的命令启动 Elects

```
electrs --conf config.toml
```

然后等待 electrs 完成所有区块的索引。

### 步骤 2c - 启动 Electrs

和 Bitcoin 一样，可以通过为 systemd 创建 script 来启动软件。

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

注意：这里使用 `bitcoin` 用户来启动软件。

然后可以注册创建好的 script 并启动。

```
sudo systemctl enable electrs
sudo systemctl start electrs
```

每当想检查软件状态时，可以使用下面的命令。

```
systemctl status electrs
```

### 步骤 3 - 安装 CLN

待补充

### 步骤 3b - 配置 CLN

待补充

### 步骤 4 - 安装 Mempool.space

安装 `mariadb`。

```
sudo apt-get install mariadb-server mariadb-client
```

然后创建 db 和用户。

```
sudo mysql -e "drop database mempool;"
sudo mysql -e "create database mempool;"
sudo mysql -e "grant all privileges on mempool.* to 'mempool'@'%' identified by 'mempool';"
sudo mysql -e "flush privileges;"
```

克隆代码

```
git clone https://github.com/mempool/mempool
cd mempool
latestrelease=$(curl -s https://api.github.com/repos/mempool/mempool/releases/latest|grep tag_name|head -1|cut -d '"' -f4)
git checkout $latestrelease

```

确保使用 node 20.x 和最新版本 npm。

```
sudo npm i -g npm
sudo npm i -g node@20
```

接着编译并测试 backend

```
cd backend
npm install --no-install-links # npm@9.4.2 and later can omit the --no-install-links
npm run build

cp mempool-config.sample.json mempool-config.json
npm run start
```

仔细检查 `mempool-config.json` 的配置。

转到 frontend。

```
cd ..

cd frontend
npm install
npm run serve:local-prod
```


### 步骤 4b - 配置 Mempool

backend 的配置位于 `mempool-config.json` 文件中。

### 步骤 4c - 启动 Mempool

可以用 pm2 启动 Mempool，但需要先安装 pm2。

```
sudo npm i -g pm2
pm2 startup 
```

启动 backend。

```
cd ..
cd backend 
pm2 start "npm run start"
```

然后启动 frontend。

```
cd ..
cd frontend
pm2 start "npm run serve:local-prod"
```

保存全部配置。

```
pm2 save
```

## 只通过 tor 连接的 Bitcoin
从安装 tor 开始。


```
sudo apt install tor
```

并设置 tor 配置文件，以创建新的 hidden service，导出节点的 8333 端口。


```
cat > /etc/tor/torrc <<EOL
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 8333 127.0.0.1:8333
EOL
```

可以重启 tor 来应用修改。这允许导出我们节点的 8333 端口，但还不能把节点访问限制为只且仅通过 tor。

```
sudo systemctl restart tor
``` 

并获得节点的 onion 地址。

```
cat /var/lib/tor/hidden_service/hostname
```

完成后，可以这样修改 bitcoin.conf 配置，把节点访问限制为只且仅通过 tor：

```
proxy=127.0.0.1:9050
listen=1
bind=127.0.0.1:8333=onion
externalip=tor_url.onion
onlynet=onion
```

其中 `tor_url.onion` 是此前获得的节点 onion 地址。


重启节点后，可以验证节点只且仅能通过 tor 访问。

```
sudo systemctl restart bitcoind

bitcoin-cli getnetworkinfo
```

这里应该看到节点只且仅能通过 tor 访问，也就是只有 `onion` 网络是 `reachable`。

此外，我们所有 peer 都会由 onion 地址标识。

```
bitcoin-cli getpeerinfo
```

注意：tor 非常慢；如果想从零开始同步节点，需要考虑这一点。

## Testnet
用于练习的一个有用网络是 `testnet`，它与 `mainnet` 的区别在于：

- token 没有价值，并且有网站会提供 testnet satoshi 供测试使用，
- 可以始终以最低 fee 进行交易，
- mining 是波动的，也因为没有收益，
- 如果一个区块 20 分钟未被挖出，难度会急剧下降，
- 经常会有重要 reorg；从这个角度看，它比 mainnet 更差。

许多 wallet，例如 green、electrum、specter、sparrow 等，都支持 testnet，可用于：

- 在不冒资金风险的情况下学习，
- 教学目的，
- 试验新东西。

一些有用的 testnet 工具，自我推广：

- [BTCBouncer](http://btcbouncer.com) 允许向多个地址付款，并在几个区块内收到资金，扣除一笔 fee，
- [BTCSigner](http://btcsigner.com) 允许用 testnet 上的 core 节点试验 multisig。

除了主要的 block explorer，还有许多其他 tools 和网站支持 testnet。

## Bitcoin-cli
Bitcoin-cli 是与 Bitcoin Core 交互的命令行工具。

命令格式为：
```
bitcoin-cli [options] <command> [params]
```
并且始终可以使用 `help` 获取命令列表或某个特定命令的信息。

### 关于 blockchain 的信息命令
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

### 控制命令
- help ( "command" )
- stop
- uptime
- ...

### mining 命令
- getblocktemplate ( "template_request" )
- submitblock "hexdata" ( "dummy" )
- ...

### 网络命令
- addnode "node" "command"
- disconnectnode ( "address" nodeid )
- getnetworkinfo
- ...

### Rawtransactions 管理
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

### 工具
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

关于从命令行使用 Bitcoin 的完整课程可在 [Learning-Bitcoin-from-the-Command-Line](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line) 找到。

## 课程安排
节点安装分为多节课程，这里列出已经进行的课程：

| 日期        | 备注                                           |
|-------------|------------------------------------------------|
| 240108-2100 | 硬件选择                                       |
| 240115-2200 | 安装 core 并验证签名                           |
| 240122-2200 | 最小配置                                       |
