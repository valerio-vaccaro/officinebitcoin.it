---
layout: default
title: "Installar Debian"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lezion Bitcoin-only</span> <span>Sto progetto xe mantegnuo da valerio-vaccaro</span></p>

## 🌍 Traduzion

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Installar Debian
Prepariamo na chiavetta co l'immagine Debian scaricata dal sito ufficiale.

Colleghiamo tutti i cavi (display, tastiera, mouse e ethernet).

![alt text](https://officinebitcoin.it/lezioni/debian/1.jpg)

Colleghiamo la chiavetta USB de installazione.

![alt text](https://officinebitcoin.it/lezioni/debian/2.jpg)

Accendiamo el computer ed assicuriamoci che venga eseguita la nostra chiavetta co a bordo Debian.

![alt text](https://officinebitcoin.it/lezioni/debian/3.jpg)

## Installazione
Se tutto ha funzionato correttamente dovrebbe partire l'installer Debian e finiremo co el trovarci nella seguente schermata.

![alt text](https://officinebitcoin.it/lezioni/debian/4.jpg)

Scegliamo la prima riga e facciamo partire l'installazione grafica.

La prima cosa che ci verrà chiesta xe la lingua, par sta installazione sielzierò "English" che risulta essere a mio avviso più comprensibile de ogni altra traduzione.

![alt text](https://officinebitcoin.it/lezioni/debian/5.jpg)

Ci verrà chiesto a sto punto la nostra posizione geografica, par trovare l'Italia dobbiamo selezionare OTHER->EUROPE->ITALY.

![alt text](https://officinebitcoin.it/lezioni/debian/6.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/7.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/8.jpg)

Come localizzazione anca qui io scelgo quella inglese.

![alt text](https://officinebitcoin.it/lezioni/debian/9.jpg)

E configuro la tastiera italiana visto che xe quella che ho a disposizione.

![alt text](https://officinebitcoin.it/lezioni/debian/10.jpg)

Scegliamo poi un nome utente e lasciamo vuoto el dominio.

![alt text](https://officinebitcoin.it/lezioni/debian/11.jpg)

A sto punto Debian chi chiederà de selezionare na password par l'utente de root ...

![alt text](https://officinebitcoin.it/lezioni/debian/12.jpg)

e de creare un utente co al relativa password.

![alt text](https://officinebitcoin.it/lezioni/debian/13.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/14.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/15.jpg)

Occorre ora sielziere el disco de installazione, useremo l'intero disco e occorre selezionare el disco su cui effettuare l'installazione.

![alt text](https://officinebitcoin.it/lezioni/debian/16.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/17.jpg)

Occorre poi selezionare la struttura de le partizioni, par ora lasceremo tutto in na singola partizione.

![alt text](https://officinebitcoin.it/lezioni/debian/18.jpg)

Debian ci propone na tabella de la partizione ma ... ha aggiunto el swap che no vogliamo, donca selezioniamolo e rimuoviamolo dalla lista.

![alt text](https://officinebitcoin.it/lezioni/debian/19.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/20.jpg)

Ora che el abbiamo rimosso possiamo finalmente scrivere la lostra tabella.

![alt text](https://officinebitcoin.it/lezioni/debian/21.jpg)

Debian vorrebbe ritornare a la configurazione de la tabella de le partizioni ma decliniamo l'invito.

![alt text](https://officinebitcoin.it/lezioni/debian/22.jpg)

E confermiamo la volotà de voler scrivere la tabella aggiornada.

![alt text](https://officinebitcoin.it/lezioni/debian/23.jpg)

Ci viene ora chiesto se vogliamo doprar un mirror de debian, sielziamo de usarlo.

![alt text](https://officinebitcoin.it/lezioni/debian/24.jpg)

Scegliamo el nostro paese.

![alt text](https://officinebitcoin.it/lezioni/debian/25.jpg)

Solitamente el mirror del garr xe veloce e affidabile, usiamo quello.

![alt text](https://officinebitcoin.it/lezioni/debian/26.jpg)

No ho alcun proxy donca lascio vuoto el campo.

![alt text](https://officinebitcoin.it/lezioni/debian/27.jpg)

Ma che programmi installar? Visto che facciamo un server disabilitiamo l'ambiente grafico (togliendo le prime due spunte) e selezioniamo SSH che ci servirà par accedere da remoto.

![alt text](https://officinebitcoin.it/lezioni/debian/28.jpg)

Parte l'installazione.

A la fine ci viene chiesto se vogliamo installar grub che ci permette de avviare Linux, rispondiamo affermativamente e sielziamo el stesso disco su cui abbiamo installato el sistema operativo.

![alt text](https://officinebitcoin.it/lezioni/debian/29.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/30.jpg)

Yuhuuu abbiamo finito, xe ora de togliere la chiavetta USB e proseguire par riavviare la macchina.

![alt text](https://officinebitcoin.it/lezioni/debian/31.jpg)

Se tutto ha funzionato correttamente dovremmo trovarci de fronte un terminale che ci chiede de loggarci co uno dei profili creati durante l'installazione.

## Configurazione

### Colleghiamoci
Colleghiamoci al nostro server co `ssh username@ip` dove username sarà el nome scelto in fase de installazione ed ip l'indirizzo ip del computer su cui abbiamo installato. 

Ovviamente sto passo può essere saltato se si installa co un monitor ed na tastiera invece che connettendosi via rete.

Attenzione che Debian vi PROIBISCE de connettervi via ssh usando le credenziali de superuser (cioè root).

### Repository
Aggiorniamo ora i repository.

Diventiamo superuser co el comando `su` e digitando la passoword de root.

Editiamo el file dei repository co el comando `nano /etc/apt/sources.list` e togliamo tutte le linee presenti.

Aggiungiamo le seguenti linee.

```                                                                    
deb http://deb.debian.org/debian/ bookworm contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm contrib main non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-updates contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm-updates contrib main non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-proposed-updates contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm-proposed-updates contrib main non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-backports contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm-backports contrib main non-free non-free-firmware

deb http://deb.debian.org/debian-security/ bookworm-security contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian-security/ bookworm-security contrib main non-free non-free-firmware

```

Possiamo donca salvare el file premoendo i tasti `CTRL+x` e poi `y`.

El comando `apt udate` ci consente de controllare che tutto sia filato liscio e de aggiornare l'elenco dei pacchetti.

### Aggiorniamo el sistema
Par aggiornare el sistema basta eseguire i seguenti comandi:

- `apt update` par aggiornare l'elenco dei pacchetti,
- `apt upgrade` par aggiornare i pacchetti installati de cui esista na nuova version.

### Installiamo tor e usiamolo co ssh
Par installar tor basta el semplice comando `apt install tor`.

Na volta installato possiamo configurarlo co el seguente comando `nano /etc/tor/torrc`.

In fondo al file aggiungiamo le seguenti linee.

```
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 22 127.0.0.1:22
```

E riavviamo tor co `systemctl restart tor`, ora possiamo trovare el nostro indirizzo onion co `cat /var/lib/tor/hidden_service/hostname`.

Sfruttando tor possiamo connetterci ora a la nostra macchina da ogni parte del mondo co `torify ssh username@indirizzoonion.onion`.

## Programma
L'installazione de Debian xe na lezione ripetitiva, qui un elenco de quelle già tenute:

| Data        | Note                                           |
|-------------|------------------------------------------------|
| 240415-2200 | Prima lezione                                  |
