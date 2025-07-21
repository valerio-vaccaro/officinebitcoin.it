# Installà Debian
Prepariam una chiavetta con l'imagine Debian scaricada dal sit ufficial.

Colleghiam tutt i cav (display, tastiera, mouse e ethernet).

![alt text](https://officinebitcoin.it/lezioni/debian/1.jpg)

Colleghiam la chiavetta USB de installazion.

![alt text](https://officinebitcoin.it/lezioni/debian/2.jpg)

Accendem el computer e assicurass che vegna eseguid la nostra chiavetta con a bord Debian.

![alt text](https://officinebitcoin.it/lezioni/debian/3.jpg)

## Installazion
Se tutt ha funzionà correttament dovria partì l'installer Debian e finirem con el trovass nella seguent schermata.

![alt text](https://officinebitcoin.it/lezioni/debian/4.jpg)

Scegliem la prima riga e fass partì l'installazion grafica.

La prima cosa che vegnarà chiesta l'è la lengua, per questa installazion sceglierò "English" che risulta vess a mio avvis pù comprensibil de ogni altera traduzion.

![alt text](https://officinebitcoin.it/lezioni/debian/5.jpg)

Vegnarà chiest a quest punt la nostra posizion geografica, per trovà l'Italia devem selezionà OTHER->EUROPE->ITALY.

![alt text](https://officinebitcoin.it/lezioni/debian/6.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/7.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/8.jpg)

Come localizzazion anca qui scegli quella inglesa.

![alt text](https://officinebitcoin.it/lezioni/debian/9.jpg)

E configur la tastiera italiana vist che l'è quella che gh'hee a disposizion.

![alt text](https://officinebitcoin.it/lezioni/debian/10.jpg)

Scegliem poi un nom utent e lassem vöid el domini.

![alt text](https://officinebitcoin.it/lezioni/debian/11.jpg)

A quest punt Debian te chiederà de selezionà una password per l'utent de root ...

![alt text](https://officinebitcoin.it/lezioni/debian/12.jpg)

e de creà un utent con la relativa password.

![alt text](https://officinebitcoin.it/lezioni/debian/13.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/14.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/15.jpg)

Occor ora scegli el disc de installazion, doprarem l'inter disc e occor selezionà el disc su cui fà l'installazion.

![alt text](https://officinebitcoin.it/lezioni/debian/16.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/17.jpg)

Occor poi selezionà la struttura de le partizion, per ora lassarem tutt in una singola partizion.

![alt text](https://officinebitcoin.it/lezioni/debian/18.jpg)

Debian te propone una tabella de la partizion ma ... ha aggiunt lo swap che minga volem, quindi selezionemlo e rimovemlo de la lista.

![alt text](https://officinebitcoin.it/lezioni/debian/19.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/20.jpg)

Ora che l'hem rimosso podem finalment scriv la nostra tabella.

![alt text](https://officinebitcoin.it/lezioni/debian/21.jpg)

Debian vorria tornà alla configurazion de la tabella de le partizion ma declinem l'invit.

![alt text](https://officinebitcoin.it/lezioni/debian/22.jpg)

E confermem la volontà de voler scriv la tabella aggiornad.

![alt text](https://officinebitcoin.it/lezioni/debian/23.jpg)

Vegn ora chiest se volem doprà un mirror de debian, scegliem de dopràll.

![alt text](https://officinebitcoin.it/lezioni/debian/24.jpg)

Scegliem el nostro paes.

![alt text](https://officinebitcoin.it/lezioni/debian/25.jpg)

Solitament el mirror del garr l'è veloce e affidabil, doprem quello.

![alt text](https://officinebitcoin.it/lezioni/debian/26.jpg)

Minga gh'hee alcun proxy quindi lass vöid el camp.

![alt text](https://officinebitcoin.it/lezioni/debian/27.jpg)

Ma che programm installà? Vist che fass un server disabilitem l'ambient grafic (togliend le prime do spunt) e selezionem SSH che servarà per acced da remoto.

![alt text](https://officinebitcoin.it/lezioni/debian/28.jpg)

Part l'installazion.

Alla fin vegn chiest se volem installà grub che permet de avvì Linux, rispondem affermativament e scegliem el stess disc su cui hem installà el sistema operativ.

![alt text](https://officinebitcoin.it/lezioni/debian/29.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/30.jpg)

Yuhuuu hem finì, l'è ora de togli la chiavetta USB e proseguì per riavvì la macchina.

![alt text](https://officinebitcoin.it/lezioni/debian/31.jpg)

Se tutt ha funzionà correttament dovriem trovass de front un terminal che chied de loggass con un de i profili cread durant l'installazion.

## Configurazion

### Colleghass
Colleghass al nostro server con `ssh username@ip` dove username sarà el nom scelt in fase de installazion e ip l'indirizz ip del computer su cui hem installà. 

Ovviament quest pass pö vess saltà se se installa con un monitor e una tastiera invece che connettendoss via ret.

Attenzion che Debian te PROIBISS de connettess via ssh doprand le credenzial de superuser (cioè root).

### Repository
Aggiornem ora i repository.

Deventem superuser con el comand `su` e digitand la password de root.

Editiem el file de i repository con el comand `nano /etc/apt/sources.list` e togliem tutt le linee present.

Aggiungem le seguent linee.

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

Podem quindi salvà el file premend i tast CTRL+x e poi y.

El comand `apt update` permet de controllà che tutt sia filà lisci e de aggiornà l'elenco de i pacchett.

### Aggiornem el sistema
Per aggiornà el sistema basta eseguì i seguent comand:

- `apt update` per aggiornà l'elenco de i pacchett,
- `apt upgrade` per aggiornà i pacchett installad de cui esista una noeuva version.

### Installem tor e dopremlo con ssh
Per installà tor basta el sempliz comand `apt install tor`.

Una volta installà podem configurall con el seguent comand `nano /etc/tor/torrc`.

In fond al file aggiungem le seguent linee.

```
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 22 127.0.0.1:22
```

E riavvì tor con `systemctl restart tor`, ora podem trovà el nostro indirizz onion con `cat /var/lib/tor/hidden_service/hostname`.

Sfruttand tor podem connettess ora alla nostra macchina de ogni part del mond con `torify ssh username@indirizzoonion.onion`.

## Program
L'installazion de Debian l'è una lezion ripetitiva, qui un elenco de quelle già tenuu:

| Data        | Note                                           |
|-------------|------------------------------------------------|
| 240415-2200 | Prima lezion                                  | 