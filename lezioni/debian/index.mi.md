---
layout: default
title: "Installà Debian"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lezion Bitcoin-only</span> <span>Quest progett l'e mantegnuu da valerio-vaccaro</span></p>

## 🌍 Traduzion

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Installà Debian
Prepariamo ona chiavetta con l'immagine Debian scaricata dal sito ufficial.

Colleghiamo tutti i cavi (display, tastiera, mouse e ethernet).

![alt text](https://officinebitcoin.it/lezioni/debian/1.jpg)

Colleghiamo la chiavetta USB de installazion.

![alt text](https://officinebitcoin.it/lezioni/debian/2.jpg)

Accendiamo el computer ed assicuriamoci che venga eseguita la nostra chiavetta con a bordo Debian.

![alt text](https://officinebitcoin.it/lezioni/debian/3.jpg)

## Installazion
Se tutto ha funzionato correttamente dovrebbe partire l'installer Debian e finiremo con el trovarci nella seguente schermata.

![alt text](https://officinebitcoin.it/lezioni/debian/4.jpg)

Scegliamo la prima riga e facciamo partire l'installazion grafica.

La prima cosa che ci verrà chiesta l'è la lingua, per questa installazion sernisserò "English" che risulta essere a mio avviso più comprensibile de ogni altra traduzion.

![alt text](https://officinebitcoin.it/lezioni/debian/5.jpg)

Ci verrà chiesto a quest punto la nostra posizion geografica, per trovare l'Italia dobbiamo selezionare OTHER->EUROPE->ITALY.

![alt text](https://officinebitcoin.it/lezioni/debian/6.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/7.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/8.jpg)

Come localizzazion anca qui io scelgo quella inglese.

![alt text](https://officinebitcoin.it/lezioni/debian/9.jpg)

E configuro la tastiera italiana visto che l'è quella che ho a disposizion.

![alt text](https://officinebitcoin.it/lezioni/debian/10.jpg)

Scegliamo poi on nome utent e lasciamo vuoto el dominio.

![alt text](https://officinebitcoin.it/lezioni/debian/11.jpg)

A quest punto Debian chi chiederà de selezionare ona password per l'utent de root ...

![alt text](https://officinebitcoin.it/lezioni/debian/12.jpg)

e de creare on utent con al relativa password.

![alt text](https://officinebitcoin.it/lezioni/debian/13.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/14.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/15.jpg)

Occorre ora sernissere el disco de installazion, useremo l'intero disco e occorre selezionare el disco su cui effettuare l'installazion.

![alt text](https://officinebitcoin.it/lezioni/debian/16.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/17.jpg)

Occorre poi selezionare la struttura di partizion, per ora lasceremo tutto in ona singola partizion.

![alt text](https://officinebitcoin.it/lezioni/debian/18.jpg)

Debian ci propone ona tabella de la partizion ma ... ha aggiunto el swap che minga vogliamo, donca selezioniamolo e rimuoviamolo dalla lista.

![alt text](https://officinebitcoin.it/lezioni/debian/19.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/20.jpg)

Ora che el abbiamo rimosso possiamo finalmente scrivere la lostra tabella.

![alt text](https://officinebitcoin.it/lezioni/debian/21.jpg)

Debian vorrebbe ritornare a la configurazion de la tabella di partizion ma decliniamo l'invito.

![alt text](https://officinebitcoin.it/lezioni/debian/22.jpg)

E confermiamo la volotà de voler scrivere la tabella aggiornada.

![alt text](https://officinebitcoin.it/lezioni/debian/23.jpg)

Ci viene ora chiesto se vogliamo doprà on mirror de debian, sernissamo de usarlo.

![alt text](https://officinebitcoin.it/lezioni/debian/24.jpg)

Scegliamo el nostro paese.

![alt text](https://officinebitcoin.it/lezioni/debian/25.jpg)

Solitamente el mirror del garr l'è veloce e affidabile, usiamo quello.

![alt text](https://officinebitcoin.it/lezioni/debian/26.jpg)

Minga ho alcun proxy donca lascio vuoto el campo.

![alt text](https://officinebitcoin.it/lezioni/debian/27.jpg)

Ma che programmi installà? Visto che facciamo on server disabilitiamo l'ambiente grafico (togliendo i prime due spunte) e selezioniamo SSH che ci servirà per accedere da remoto.

![alt text](https://officinebitcoin.it/lezioni/debian/28.jpg)

Parte l'installazion.

A la fine ci viene chiesto se vogliamo installà grub che ci permette de avviare Linux, rispondiamo affermativamente e sernissamo el stesso disco su cui abbiamo installato el sistema operativo.

![alt text](https://officinebitcoin.it/lezioni/debian/29.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/30.jpg)

Yuhuuu abbiamo finito, l'è ora de togliere la chiavetta USB e proseguire per riavviare la macchina.

![alt text](https://officinebitcoin.it/lezioni/debian/31.jpg)

Se tutto ha funzionato correttamente dovremmo trovarci de fronte on terminale che ci chiede de loggarci con uno di profili creati durante l'installazion.

## Configurazion

### Colleghiamoci
Colleghiamoci al nostro server con `ssh username@ip` indoe username sarà el nome scelto in fase de installazion ed ip l'indirizzo ip del computer su cui abbiamo installato. 

Ovviamente quest passo può essere saltato se si installa con on monitor ed ona tastiera invece che connettendosi via rete.

Attenzion che Debian vi PROIBISCE de connettervi via ssh usando i credenziali de superuser (cioè root).

### Repository
Aggiorniamo ora i repository.

Diventiamo superuser con el comando `su` e digitando la passoword de root.

Editiamo el file di repository con el comando `nano /etc/apt/sources.list` e togliamo tutte i linee presenti.

Aggiungiamo i seguenti linee.

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

El comando `apt udate` ci consente de controllare che tutto sia filato liscio e de aggiornare l'elenco di pacchetti.

### Aggiorniamo el sistema
Per aggiornare el sistema basta eseguire i seguenti comandi:

- `apt update` per aggiornare l'elenco di pacchetti,
- `apt upgrade` per aggiornare i pacchetti installati de cui esista ona nuova version.

### Installiamo tor e usiamolo con ssh
Per installà tor basta el sempliz comando `apt install tor`.

Ona volta installato possiamo configurarlo con el seguente comando `nano /etc/tor/torrc`.

In fondo al file aggiungiamo i seguenti linee.

```
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 22 127.0.0.1:22
```

E riavviamo tor con `systemctl restart tor`, ora possiamo trovare el nostro indirizzo onion con `cat /var/lib/tor/hidden_service/hostname`.

Sfruttando tor possiamo connetterci ora a la nostra macchina da ogni parte del mond con `torify ssh username@indirizzoonion.onion`.

## Programma
L'installazion de Debian l'è ona lezion ripetitiva, qui on elenco de quelle già tenute:

| Data        | Note                                           |
|-------------|------------------------------------------------|
| 240415-2200 | Prima lezion                                  |
