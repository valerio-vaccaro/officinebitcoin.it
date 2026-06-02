---
layout: default
title: "Fullnode and hardware for a node"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only lesson</span> <span>This project is maintained by valerio-vaccaro</span></p>

## 🌍 Translations

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Fullnode and hardware for a node

Having a Bitcoin node is essential because, with maximum privacy, it lets you:

- validate the entire Bitcoin chain,
- check the balance of our wallets,
- transmit our new transactions
- ...

## Hardware selection

- minimum 2GB (4GB recommended) of RAM memory,
- disk with at least 1TB (2TB recommended) of mass storage,
- sufficiently high-performance multi-core CPU (probably any processor developed in the last decade).

### Reuse an old computer

An old computer can be recycled as a node, in the case of a laptop it is advisable to remove the battery which, if always placed on charge, could constitute a risk. The great advantage is given by the cost equal to zero or limited only to the largest disk.

### Raspberry Pi and other boards

Raspberry Pi is an ARM board widely used for the creation of IoT systems and nodes, however the excessive cost and the need for a disk on a USB port make it not the best possible choice in terms of performance and stability.

Odroid-M1 is a high-performance ARM board with an internal slot for adding additional storage.

### Thin clients

With a very small budget of 30-100 euros it is possible to purchase a used Thin Client (on ebay) which combines low consumption with sufficient performance to run the node.

The following models were tested as examples of Thin Client:

- Fujitsu Futro s920
- HP t620

## Software selection

Installing as little software as possible on a node limits possible attacks and makes the system easier to maintain.

Online you can find pre-packaged solutions (Umbrel, Mynode, ...) that mask the security checks and add software and scripts (for example docker) that are difficult to control. In these lessons we will focus on creating a node by hand or manually installing all the necessary software.

### Step 0 - The operating system

The first choice to make is the operating system, the advice is to use Linux in an LTS version or one in which support is guaranteed for a sufficiently long number of years. My personal choice is Debian 12.

The chosen operating system must then be installed on the computer and all packages must be updated (the update is something that will follow us throughout the life of the node).

It is also advisable to install Tor (and/or other VPN if necessary) and SSH to allow remote maintenance of the node.

Finally, an uninterruptible power supply could save the node from sudden power cuts, avoiding leaving bitcoin and other software in an inconsistent state.

### Step 1 - Let's install Bitcoin

Download Bitcoin Core, the hashes, and the signatures.

```
wget https://bitcoincore.org/bin/bitcoin-core-28.1/bitcoin-28.1-x86_64-linux-gnu.tar.gz
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS
wget https://bitcoincore.org/bin/bitcoin-core-28.1/SHA256SUMS.asc
```

If you use a board equipped with arm architecture, the package will have to be corrected in `bitcoin-28.1-aarch64-linux-gnu.tar.gz` or in the same package but compiled for the 64-bit arm architecture (aarch64) which is precisely the one used by odroid.

At this point we can check that one of the hashes in SHA256SUM matches the downloaded archive.

```
sha256sum --ignore-missing --check SHA256SUMS
```

The result tells us that a match has been found for the downloaded archive.

```
bitcoin-28.1-x86_64-linux-gnu.tar.gz: OK
```

Let's now verify the signatures of the SHA256SUM file, first, if necessary, obtain the keys and import them.

```
git clone https://github.com/bitcoin-core/guix.sigs
gpg --import guix.sigs/builder-keys/*
```

And finally we verify the signatures.

```
gpg --verify SHA256SUMS.asc
```

If we see the writing `gpg: Good signature from ...` several times it means that we have found valid signatures.

Let's proceed with unpacking and installation 

```
tar xzvf bitcoin-28.1-x86_64-linux-gnu.tar.gz 
sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-28.1/bin/*
```

And here we are, now we have `bitcoind`, `bitcoin-cli` and the other utilities ready to be launched.

For now let's launch `bitcoind` and we'll see some logs. Bitcoin starts to synchronize and now there will be a directory with the blockchain and all the configurations in `~/.bitcoin/`.

From another terminal we can check the operation of bitcoind by launching the command `tail -f ~/.bitcoin/debug.log`.

### Step 1b - Let's configure Bitcoin

As we have already seen previously, the directory in which Bitcoin core saves the configurations and the blockchain is the `~/.bitcoin/` directory as regards the Linux operating system, if you want to change the saving location you can use different approaches:

- create a symbolic link of the directory on a larger disk using the `ln -s` command,
- use the `datadir` command from the command line or within bitcoin.conf specifying the destination directory.

Bitcoin Core supports three different types of networks to connect to:
- `mainnet`, this is the classic network we are all used to and it is the default for core,
- `testnet`, this network is similar to mainnet but the tokens have no value, mining is always carried out but in case of absence of blocks for 20 minutes the difficulty is precipitated (it often suffers from significant reorgs),
- `regtest`, in this mode you have a small private blockchain that always starts from scratch and in which it is possible to mine at minimum difficulty (used for local tests).

Another useful command is `daemon` which, if set, does not keep the bitcoin core log connected to the current console. To see how it works it will always be possible to use the `tail -f ~/.bitcoin/debug.log` command.

All configurations can be launched from the command line or via the `~/.bitcoin/bitcoin.conf` file, a file compatible with a home setup (i.e. where I want to keep resource consumption to a minimum) could be the following.
configuration file

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

In which the:

- server is disconnected from the console with `daemon=1`
- only the blocks are downloaded and not the mempool `blocksonly=1`
- up to twenty `txindex=1` connections are allowed
- information is sent to other nodes on the internet for a maximum of 500 megabytes per day `maxuploadtarget=500`
- an index of transactions is maintained `txindex=1`
- an index of blockfilters is maintained `blockfilterindex=1`
- we give anyone the opportunity to connect via rpc `rpcallowip=0.0.0.0/0`
- we connect rpc to all network cards `rpcallowip=0.0.0.0/0`
- seventh a username for rpc `rpcuser=username` (obviously to be replaced)
- we set a password for rpc `rpcpassword=password` (obviously to be replaced)

The full list of features can be found at [https://jlopp.github.io/bitcoin-core-config-generator](https://jlopp.github.io/bitcoin-core-config-generator)

You can even do it all with a single terminal command.

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

If you have another node already synchronized, you can use the `connect` option to connect ONLY AND EXCLUSIVELY to this node. If this node is in the local network you save time and bandwidth with this simple configuration.

Since release 26 core supports encryption of communications between nodes with the `v2transport` option.

All the configurations shown are related to clearnet, the configurations for tor will be the subject of another lesson.

### Step 1c - Let's launch Bitcoin

Let's launch Bitcoin by building a launch file for systemd.

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
Warning: in this case we are using the user `bitcoin` to start the software.

We can then register the created script and launch it.

```
sudo systemctl enable bitcoind
sudo systemctl start bitcoind
```

Whenever you want to check the status of the software you can use the following command.

```
systemctl status bitcoind
```

### Step 2 - Let's install Electrs

We install `Electrs` which is an electrum server based on `Rust`, the first step is therefore to install this language.

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

We also install clang and the build-essential package.

```
apt update
apt install clang cmake build-essential -y
```

We download the latest version (currently 0.10.5) from Github.

```
VERSION="0.10.5"
git clone --branch v$VERSION https://github.com/romanz/electrs.git
cd electrs
```

We import the developer key of `Electrs` and verify the signature of the Github commits.

```
curl https://romanzey.de/pgp.txt | gpg --import
git verify-tag v$VERSION
```

If the signature is correct we can move on to compiling...

```
cargo build --locked --release
```

and then to installation.

```
sudo install -m 0755 -o root -g root -t /usr/local/bin ./target/release/electrs
```

### Step 2b - Let's configure Electrs

To configure `Electrs` we create the file `config.toml` with the following content.

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

You can even do it all with a single terminal command.

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

We can launch Elects with the command

```
electrs --conf config.toml
```

and wait for electrs to finish indexing all the blocks.

### Step 2c - Let's launch Eletrs

As for Bitcoin we can launch the software by creating a script for systemd.

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

Warning: in this case we are using the user `bitcoin` to start the software.

We can then register the created script and launch it.

```
sudo systemctl enable electrs
sudo systemctl start electrs
```

Whenever you want to check the status of the software you can use the following command.

```
systemctl status electrs
```

### Step 3 - Let's install CLN

To be completed.

### Step 3b - Let's configure CLN

To be completed.

### Step 4 - Let's install Mempool.space

Let's install `mariadb`.

```
sudo apt-get install mariadb-server mariadb-client
```

And we create db and user.

```
sudo mysql -e "drop database mempool;"
sudo mysql -e "create database mempool;"
sudo mysql -e "grant all privileges on mempool.* to 'mempool'@'%' identified by 'mempool';"
sudo mysql -e "flush privileges;"
```

Let's clone the code

```
git clone https://github.com/mempool/mempool
cd mempool
latestrelease=$(curl -s https://api.github.com/repos/mempool/mempool/releases/latest|grep tag_name|head -1|cut -d '"' -f4)
git checkout $latestrelease

```

Let's make sure you're using node 20.x and the latest version of npm.

```
sudo npm i -g npm
sudo npm i -g node@20
```

Let's compile and test the backend

```
cd backend
npm install --no-install-links # npm@9.4.2 and later can omit the --no-install-links
npm run build

cp mempool-config.sample.json mempool-config.json
npm run start
```

Check your `mempool-config.json` configurations carefully.

Let's move on to the frontend.

```
cd ..

cd frontend
npm install
npm run serve:local-prod
```


### Step 4b - Let's configure Mempool

The backend configuration is found in the `mempool-config.json` file.

### Step 4c - Let's launch Mempool

We can launch Mempool with pm2, which must be installed.

```
sudo npm i -g pm2
pm2 startup 
```

Let's launch the backend.

```
cd ..
cd backend 
pm2 start "npm run start"
```

We then launch the frontend.

```
cd ..
cd frontend
pm2 start "npm run serve:local-prod"
```

Let's save everything.

```
pm2 save
```

## Bitcoin with connection only via tor
Let's start by installing Tor.


```
sudo apt install tor
```

and we set the Tor configuration file to create a new hidden service by exporting the node's port 8333.


```
cat > /etc/tor/torrc <<EOL
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 8333 127.0.0.1:8333
EOL
```

We can restart Tor to apply the changes, this allows us to export port 8333 of our node but does not limit access to the node only and exclusively via Tor.

```
sudo systemctl restart tor
``` 

and get the onion address of the node.

```
cat /var/lib/tor/hidden_service/hostname
```

Once this is done we can limit access to the node only and exclusively via Tor by modifying the configuration of bitcoin.conf in this way:

```
proxy=127.0.0.1:9050
listen=1
bind=127.0.0.1:8333=onion
externalip=tor_url.onion
onlynet=onion
```

Where `tor_url.onion` is the onion address of the node obtained previously.


By restarting the node we can verify that the node is accessible only and exclusively via Tor.

```
sudo systemctl restart bitcoind

bitcoin-cli getnetworkinfo
```

Here we should see that the node is accessible only and exclusively via Tor, that is, only the `onion` network is `reachable`.

Furthermore, our peers will all be identified by onion addresses.

```
bitcoin-cli getpeerinfo
```

Warning: Tor is extremely slow, take this into account when you want to synchronize the node from scratch.

## Testnet
A useful network to practice is `testnet` which differs from `mainnet` in that:

- tokens have no value and there are sites that offer you satoshi of testnet for testing,
- you can always transact at the minimum fee,
- mining is fluctuating (also because you don't earn anything from it),
- if a block is not mined for 20 minutes the difficulty worsens,
- often there are important reorgs (from this point of view it is worse than mainnet).

Many wallets (green, electrum, specter, sparrow, ...) support testnet and can be used for:

- learn without putting your funds at risk,
- for educational purposes,
- to experience new things.

Some useful tools (self-promotion) for testnet:

- [BTCBouncer](http://btcbouncer.com) allows you to make payments to various addresses and receive the funds (minus a fee) within a couple of blocks,
- [BTCSigner](http://btcsigner.com) allows you to experiment with a multisig with a core node in testnet.

There are many other tools and websites that support testnet in addition to the major block explorers.

## Bitcoin-cli
Bitcoin-cli is the command line utility for interacting with Bitcoin Core.

The commands have the format:
```
bitcoin-cli [options] <command> [params]
```
and you can always use `help` to get the list of commands or information about a specific command.

### Blockchain Information Commands Blockchain
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

### Control commands
- help ( "command" )
- stop
- uptime
- ...

### Commands for mining
- getblocktemplate ( "template_request" )
- submitblock "hexdata" ( "dummy" )
- ...

### Network commands
- addnode "node" "command"
- disconnectnode ( "address" nodeid )
- getnetworkinfo
- ...

### Rawtransactions management
- analyzepsbt "psbt"
- combinepsbt ["psbt",...]
- combinerawtransaction ["hexstring",...]
- createpsbt [{"txid":"hex","vout":n,"sequence":n},...] [{"address":amount,...},{"data":"hex"},...] ( locktime replaceable )
- createrawtransaction [{"txid":"hex","vout":n,"sequence":n},...] [{"address":amount,...},{"data":"hex"},...] ( locktime replaceable )
- decodepsbt "psbt"
- decodrawtransaction "hexstring" ( iswitness )
- finalizepsbt "psbt" ( extract )
- getrawtransaction "txid" ( verbose "blockhash" )
- sendrawtransaction "hexstring" ( maxfeerate )
- signrawtransactionwithkey "hexstring" ["privatekey",...] ( [{"txid":"hex","vout":n,"scriptPubKey":"hex","redeemScript":"hex","witnessScript":"hex","amount":amount},...] "sighashtype" )
- testmempoolaccept ["rawtx",...] ( maxfeerate )
- ...

### Utilities
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

A complete course on using Bitcoin from the command line can be found at [Learning-Bitcoin-from-the-Command-Line](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line).

## Program
The installation of the node is divided into several lessons, here is a list of those already held:

| Date | Notes |
|------------------------|------------------------------------------------|
| 240108-2100 | Hardware Selection |
| 240115-2200 | Core installation and signature verification |
| 240122-2200 | Minimal configuration |
| 240129-2200 | Testnet |
| 240205-2200 | bitcoind-cli |
| 240711-2200 | electrs |
