# Installare Debian
Prepariamo una chiavetta con l'immagine Debian scaricata dal sito ufficiale.

Colleghiamo tutti i cavi (display, tastiera, mouse e ethernet).

![alt text](https://officinebitcoin.it/lezioni/debian/1.jpg)

Colleghiamo la chiavetta USB di installazione.

![alt text](https://officinebitcoin.it/lezioni/debian/2.jpg)

Accendiamo il computer ed assicuriamoci che venga eseguita la nostra chiavetta con a bordo Debian.

![alt text](https://officinebitcoin.it/lezioni/debian/3.jpg)

## Installazione
Se tutto ha funzionato correttamente dovrebbe partire l'installer Debian e finiremo con il trovarci nella seguente schermata.

![alt text](https://officinebitcoin.it/lezioni/debian/4.jpg)

Scegliamo la prima riga e facciamo partire l'installazione grafica.

La prima cosa che ci verrà chiesta è la lingua, per questa installazione sceglierò "English" che risulta essere a mio avviso più comprensibile di ogni altra traduzione.

![alt text](https://officinebitcoin.it/lezioni/debian/5.jpg)

Ci verrà chiesto a questo punto la nostra posizione geografica, per trovare l'Italia dobbiamo selezionare OTHER->EUROPE->ITALY.

![alt text](https://officinebitcoin.it/lezioni/debian/6.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/7.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/8.jpg)

Come localizzazione anche qui io scelgo quella inglese.

![alt text](https://officinebitcoin.it/lezioni/debian/9.jpg)

E configuro la tastiera italiana visto che è quella che ho a disposizione.

![alt text](https://officinebitcoin.it/lezioni/debian/10.jpg)

Scegliamo poi un nome utente e lasciamo vuoto il dominio.

![alt text](https://officinebitcoin.it/lezioni/debian/11.jpg)

A questo punto Debian chi chiederà di selezionare una password per l'utente di root ...

![alt text](https://officinebitcoin.it/lezioni/debian/12.jpg)

e di creare un utente con al relativa password.

![alt text](https://officinebitcoin.it/lezioni/debian/13.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/14.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/15.jpg)

Occorre ora scegliere il disco di installazione, useremo l'intero disco e occorre selezionare il disco su cui effettuare l'installazione.

![alt text](https://officinebitcoin.it/lezioni/debian/16.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/17.jpg)

Occorre poi selezionare la struttura delle partizioni, per ora lasceremo tutto in una singola partizione.

![alt text](https://officinebitcoin.it/lezioni/debian/18.jpg)

Debian ci propone una tabella della partizione ma ... ha aggiunto lo swap che non vogliamo, quindi selezioniamolo e rimuoviamolo dalla lista.

![alt text](https://officinebitcoin.it/lezioni/debian/19.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/20.jpg)

Ora che lo abbiamo rimosso possiamo finalmente scrivere la lostra tabella.

![alt text](https://officinebitcoin.it/lezioni/debian/21.jpg)

Debian vorrebbe ritornare alla configurazione della tabella delle partizioni ma decliniamo l'invito.

![alt text](https://officinebitcoin.it/lezioni/debian/22.jpg)

E confermiamo la volotà di voler scrivere la tabella aggiornata.

![alt text](https://officinebitcoin.it/lezioni/debian/23.jpg)

Ci viene ora chiesto se vogliamo usare un mirror di debian, scegliamo di usarlo.

![alt text](https://officinebitcoin.it/lezioni/debian/24.jpg)

Scegliamo il nostro paese.

![alt text](https://officinebitcoin.it/lezioni/debian/25.jpg)

Solitamente il mirror del garr è veloce e affidabile, usiamo quello.

![alt text](https://officinebitcoin.it/lezioni/debian/26.jpg)

Non ho alcun proxy quindi lascio vuoto il campo.

![alt text](https://officinebitcoin.it/lezioni/debian/27.jpg)

Ma che programmi installare? Visto che facciamo un server disabilitiamo l'ambiente grafico (togliendo le prime due spunte) e selezioniamo SSH che ci servirà per accedere da remoto.

![alt text](https://officinebitcoin.it/lezioni/debian/28.jpg)

Parte l'installazione.

Alla fine ci viene chiesto se vogliamo installare grub che ci permette di avviare Linux, rispondiamo affermativamente e scegliamo lo stesso disco su cui abbiamo installato il sistema operativo.

![alt text](https://officinebitcoin.it/lezioni/debian/29.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/30.jpg)

Yuhuuu abbiamo finito, è ora di togliere la chiavetta USB e proseguire per riavviare la macchina.

![alt text](https://officinebitcoin.it/lezioni/debian/31.jpg)

Se tutto ha funzionato correttamente dovremmo trovarci di fronte un terminale che ci chiede di loggarci con uno dei profili creati durante l'installazione.

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
