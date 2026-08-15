---
layout: default
title: "Jade con GPG"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lezione Bitcoin-only</span> <span>This project is maintained by valerio-vaccaro</span></p>

# Jade con GPG

## Introduzione

GnuPG (GPG) permette di firmare file e commit, verificare firme e cifrare dati per uno o più destinatari. `jade-gpg` usa Jade per generare e custodire il materiale crittografico: il computer conserva il portachiavi pubblico e inoltra a Jade le richieste da approvare, ma non riceve la chiave privata.

Jade supporta le identità GPG tramite `jade-agent`, la variante per Jade del progetto comunemente chiamato *Trezor Agent*. Non è necessario, né corretto, eseguire `trezor-agent` con una Jade: installa e usa `jade-agent`/`jade-gpg`.

> **Prima di iniziare:** una firma GPG collega stabilmente una chiave alla tua identità pubblica. Usa un nome e un indirizzo e-mail che desideri pubblicare. Per una migliore compartimentazione, usa una Jade dedicata alle identità digitali e non quella che contiene fondi importanti.

## Preparare Jade e il computer

Inizializza, aggiorna e sblocca Jade seguendo il [setup di Jade](../jadeset/index.html). Serve firmware `0.1.33` o successivo per il supporto di identità SSH/GPG.

Su Debian/Ubuntu installa GnuPG e i prerequisiti, poi l'agente in un ambiente isolato:

```bash
sudo apt update
sudo apt install gnupg git python3-venv python3-dev libusb-1.0-0-dev libudev-dev
python3 -m venv ~/.local/opt/jade-agent
mkdir -p ~/.local/src
git clone https://github.com/romanz/trezor-agent.git ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install --upgrade pip
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent
~/.local/opt/jade-agent/bin/pip install -e ~/.local/src/trezor-agent/agents/jade
```

Il pacchetto `jade-agent` non è pubblicato su PyPI: per questo viene installato dal repository sorgente insieme alla libreria condivisa. Per aggiornarlo in futuro: `git -C ~/.local/src/trezor-agent pull`, quindi ripeti i due comandi `pip install -e`.

Per gli esempi seguenti rendi disponibili i programmi appena installati:

```bash
export PATH="$HOME/.local/opt/jade-agent/bin:$PATH"
```

Se Jade non viene riconosciuta, controlla cavo dati, permessi USB e [regole udev](https://github.com/bitcoin-core/HWI/blob/master/hwilib/udev/55-usb-jade.rules). Non usare `sudo` per lanciare GPG o l'agente: creeresti file e socket appartenenti a root.

## Creare l'identità GPG su Jade

Mantieni separato questo portachiavi da eventuali chiavi GPG software già presenti. Il comando iniziale crea la configurazione dedicata e chiede conferme su Jade:

```bash
jade-gpg init "Mario Rossi <mario@example.org>"
export GNUPGHOME="$HOME/.gnupg/jade"
gpg --list-secret-keys --keyid-format long
```

`GNUPGHOME` deve restare impostata in ogni terminale che usa questa identità; puoi aggiungere l'export al file di configurazione della shell. Non mescolare in `~/.gnupg/jade` chiavi software ordinarie: l'agente presume che le chiavi segrete del portachiavi siano hardware-backed.

Esporta subito la chiave pubblica, che puoi condividere o pubblicare:

```bash
gpg --armor --export mario@example.org > mario-example-org.asc
gpg --fingerprint mario@example.org
```

Confronta l'impronta attraverso un canale indipendente prima di fidarti di una chiave altrui o prima di comunicare la tua. La chiave pubblica e la sua impronta non sono segreti.

## Esempio: firmare e verificare un file

Crea un file di prova e produci una firma separata ASCII-armored:

```bash
printf 'Officine Bitcoin: prova firma GPG\n' > messaggio.txt
gpg --armor --detach-sign --local-user mario@example.org messaggio.txt
gpg --verify messaggio.txt.asc messaggio.txt
```

Durante la firma Jade chiede di autorizzare l'operazione. La verifica usa soltanto dati pubblici, quindi non richiede Jade. Prima di firmare un file reale, leggi sempre il nome e l'azione mostrati sia nel terminale sia sul dispositivo.

## Esempio: cifrare un file per te stesso

È utile per archiviare un documento che vuoi poter aprire solo con Jade. Cifra per il tuo identificativo, quindi decritta in un nuovo file:

```bash
printf 'dato riservato\n' > segreto.txt
gpg --armor --encrypt --recipient mario@example.org --output segreto.txt.asc segreto.txt
gpg --decrypt --output segreto-ripristinato.txt segreto.txt.asc
cmp segreto.txt segreto-ripristinato.txt
```

Il file `segreto.txt.asc` può essere conservato o inviato; non è segreto. Il file in chiaro, invece, richiede una gestione sicura. Per cifrare a un'altra persona sostituisci il destinatario con la sua impronta completa, dopo averla verificata.

## Esempio: firmare commit Git

Con Jade collegata e `GNUPGHOME` impostata, configura solo il repository corrente:

```bash
git config --local user.signingkey "mario@example.org"
git config --local commit.gpgsign true
git config --local gpg.program gpg
git commit -S -m "Documenta la configurazione"
git log --show-signature -1
```

Il provider Git remoto potrebbe richiedere l'importazione della chiave pubblica per mostrare la firma come verificata. La firma locale rimane comunque verificabile con `gpg --verify` o `git log --show-signature` da chi possiede la tua chiave pubblica.

## Backup e recupero

Non esiste un file di chiave privata da copiare: la capacità di firmare o decifrare dipende da Jade e dalla sua mnemonica. Conserva la mnemonica offline come già richiesto per il wallet e conserva anche:

- il nome esatto dell'identità GPG;
- l'impronta pubblica e una copia della chiave pubblica;
- una copia dei dati cifrati;
- istruzioni verificate per reinstallare `jade-agent`.

La mnemonica da sola non rende pratico il recupero se hai perso il nome/parametri dell'identità. Non pubblicare mai la mnemonica, né inserirla in una pagina web o nel computer. Per altre opzioni e casi d'uso, vedi la [guida GPG dell'agente](https://github.com/romanz/trezor-agent/blob/master/doc/README-GPG.md).
