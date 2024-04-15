# Installare Debian
Prepariamo una chiavetta con l'immagine Debian scaricata dal sito ufficiale.

Colleghiamo tutti i cavi (display, tastiera, mouse e ethernet).

![alt text](https://officinebitcoin.it/lezioni/debian/1.jpg)

Colleghiamo la chiavetta USB di installazione.

![alt text](https://officinebitcoin.it/lezioni/debian/2.jpg)
<>
<img src="https://officinebitcoin.it/lezioni/debian/2.jpg" alt="drawing" width="50"/>

Accendiamo il computer ed assicuriamoci che venga eseguita la nostra chiavetta con a bordo Debian.


## Installazione
Se tutto ha funzionato correttamente dovrebbe partire l'installer Debian e finiremo con il trovarci nella seguente schermata.


## Configurazione

### Colleghiamoci
Colleghiamoci al nostro server con `ssh username@ip` dove username sarà il nome scelto in fase di installazione ed ip l'indirizzo ip del computer su cui abbiamo installato. 

Ovviamente questo passo può essere saltato se si installa con un monitor ed una tastiera invece che connettendosi via rete.

Attenzione che Debian vi PROIBISCE di connettervi via ssh usando le credenziali di superuser (cioè root).

### Repository
Aggiorniamo ora i repository.

Diventiamo superuser con il comando `su` e digitando la passoword di root.

Editiamo il file dei repository con il comando `nano /etc/apt/sources.list` e togliamo tutte le linee presenti.

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

Possiamo quindi salvare il file premoendo i tasti `CTRL+x` e poi `y`.

Il comando `apt udate` ci consente di controllare che tutto sia filato liscio e di aggiornare l'elenco dei pacchetti.

### Aggiorniamo il sistema
Per aggiornare il sistema basta eseguire i seguenti comandi:

- `apt update` per aggiornare l'elenco dei pacchetti,
- `apt upgrade` per aggiornare i pacchetti installati di cui esista una nuova versione.

### Installiamo tor e usiamolo con ssh
Per installare tor basta il semplice comando `apt install tor`.

Una volta installato possiamo configurarlo con il seguente comando `nano /etc/tor/torrc`.

In fondo al file aggiungiamo le seguenti linee.

```
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 22 127.0.0.1:22
```

E riavviamo tor con `systemctl restart tor`, ora possiamo trovare il nostro indirizzo onion con `cat /var/lib/tor/hidden_service/hostname`.

Sfruttando tor possiamo connetterci ora alla nostra macchina da ogni parte del mondo con `torify ssh username@indirizzoonion.onion`.

## Programma
L'installazione di Debian è una lezione ripetitiva, qui un elenco di quelle già tenute:

| Data        | Note                                           |
|-------------|------------------------------------------------|
