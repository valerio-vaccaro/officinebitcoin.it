---
layout: default
title: "Jade come chiave SSH"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lezione Bitcoin-only</span> <span>This project is maintained by valerio-vaccaro</span></p>

# Jade come chiave SSH

## Introduzione

Una chiave SSH consente di accedere a un server, GitHub o un repository senza consegnare una password. Con `jade-agent` la chiave privata non viene salvata nel computer: Jade la deriva dalla propria seed per una specifica identità e firma la richiesta solo dopo la conferma sul suo schermo.

Questa lezione usa una Jade aggiornata e il progetto [`jade-agent`](https://github.com/romanz/trezor-agent), parte della famiglia di strumenti nota storicamente come *Trezor Agent*. `trezor-agent` è il comando equivalente per un dispositivo Trezor; con Jade si usa `jade-agent`.

> **Separazione dei ruoli.** Non inserire mai la seed in un computer. Per l'uso più prudente, dedica una Jade e una seed al solo ruolo di identità SSH/GPG, distinta da quella che custodisce bitcoin. La stessa identità testuale genera sempre la stessa chiave: annotala con precisione.

## Occorrente e preparazione

- una Jade inizializzata, aggiornata e sbloccabile con PIN;
- un cavo USB dati;
- un computer Linux con OpenSSH e Python 3;
- un server o un servizio sul quale sia possibile registrare una chiave pubblica.

Completa prima il [setup di Jade](../jadeset/index.html). Per l'agente occorre un firmware Jade almeno `0.1.33`; aggiorna sempre da una fonte ufficiale e verifica di usare il dispositivo corretto.

Su Debian/Ubuntu installa i prerequisiti e l'agente in un ambiente Python isolato:

```bash
sudo apt update
sudo apt install openssh-client git python3-venv python3-dev libusb-1.0-0-dev libudev-dev
python3 -m venv ~/.local/opt/jade-agent
mkdir -p ~/.local/src
git clone https://github.com/romanz/trezor-agent.git ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install --upgrade pip
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent/agents/jade
```

`jade-agent` non è disponibile su PyPI: i due ultimi comandi installano il progetto base e poi il componente Jade direttamente dal suo repository. In seguito, per aggiornare il codice già scaricato, esegui `git -C ~/.local/src/trezor-agent pull` e ripeti i due comandi `pip install -e`.

Se Jade non viene vista dal computer, scollega e ricollega il cavo, controlla che sia un cavo dati e segui le [regole udev per Jade](https://github.com/bitcoin-core/HWI/blob/master/hwilib/udev/55-usb-jade.rules). In alcune distribuzioni l'utente deve appartenere al gruppo `dialout`; applica l'eventuale modifica con un nuovo login.

Per rendere più leggibili gli esempi, nella sessione corrente definiamo:

```bash
alias jade-agent="$HOME/.local/opt/jade-agent/bin/jade-agent"
```

Collega, sblocca Jade e mantienila nella schermata pronta a collegarsi a una companion app. Ogni esportazione di chiave o firma deve essere confermata sul dispositivo.

## Scegliere un'identità

L'identità è una stringa, di norma `utente@host`, usata dall'agente per derivare la chiave. Non è un indirizzo e-mail e non deve essere segreta. Usa una stringa distinta per ogni servizio, ad esempio:

```text
valerio@vps.example.org
git@github.com
```

Cambiare anche solo una lettera, l'algoritmo o l'indice produce un'altra chiave. Salva in un luogo sicuro un elenco di identità e destinazioni; non annotare la seed.

## Primo esempio: accesso a un server

Sul computer locale esporta la chiave pubblica. L'opzione `-e nist256p1` è importante: Jade supporta la curva NIST P-256 per queste identità.

```bash
mkdir -p ~/.ssh
jade-agent -e nist256p1 valerio@vps.example.org > ~/.ssh/jade-vps.pub
chmod 700 ~/.ssh
chmod 600 ~/.ssh/jade-vps.pub
cat ~/.ssh/jade-vps.pub
```

Controlla sullo schermo Jade l'operazione richiesta. Copia **solo** la riga pubblica risultante nel file `~/.ssh/authorized_keys` dell'utente `valerio` sul server. Se puoi ancora entrare con una password, un modo temporaneo è:

```bash
ssh-copy-id -i ~/.ssh/jade-vps.pub valerio@vps.example.org
```

Dal computer locale avvia quindi una singola connessione attraverso l'agente:

```bash
jade-agent -e nist256p1 valerio@vps.example.org -c
```

Jade mostrerà una richiesta di firma: verifica che l'identità e l'operazione corrispondano a ciò che intendi fare, quindi conferma. Per una shell in cui eseguire più comandi SSH, Git o `rsync`:

```bash
jade-agent -e nist256p1 valerio@vps.example.org --shell
ssh valerio@vps.example.org
rsync -av sito/ valerio@vps.example.org:/srv/sito/
exit
```

La chiave privata non compare in `~/.ssh`: il file `.pub` è pubblico e serve solo a far riconoscere Jade al server.

## Esempio: GitHub via SSH

Esporta una chiave diversa per GitHub e registrane il contenuto nelle impostazioni dell'account GitHub, nella sezione dedicata alle chiavi SSH.

```bash
jade-agent -e nist256p1 git@github.com > ~/.ssh/jade-github.pub
```

Aggiungi al file `~/.ssh/config`:

```sshconfig
Host github.com
    User git
    IdentityFile ~/.ssh/jade-github.pub
```

Apri una shell assistita, prova l'autenticazione e usa Git normalmente:

```bash
jade-agent -e nist256p1 git@github.com --shell
ssh -T git@github.com
git clone git@github.com:utente/progetto.git
cd progetto
git push
exit
```

## Verifiche e problemi comuni

- Non approvare una firma sul dispositivo se non hai appena avviato tu la connessione.
- Se SSH ignora l'agente, verifica che `~/.ssh/config` indichi il file `.pub`; un'impostazione `IdentitiesOnly yes` può richiedere esplicitamente `IdentityFile`.
- Se l'identità non coincide esattamente con quella usata per creare il file pubblico, il server rifiuterà l'accesso.
- Conserva un secondo metodo di accesso amministrativo finché non hai provato Jade su una nuova connessione. Solo dopo, se è appropriato al server, disabilita l'accesso a password.
- La seed ripristinata su un'altra Jade e la stessa identità ricreano la chiave; prova il ripristino solo con procedure che già conosci e senza esporre la seed.

Per tutte le opzioni disponibili, consulta la [guida SSH dell'agente](https://github.com/romanz/trezor-agent/blob/master/doc/README-SSH.md) e la [documentazione del firmware Jade](https://github.com/Blockstream/Jade/blob/master/docs/index.rst).
