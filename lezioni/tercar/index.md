# Il terminale a caratteri

## Introduzione
Linux (o meglio un sistema GNU LInux in quanto linux è solo il kernel che inizializza l'hardware e fornisce le primitive per usarlo) usa il concetto del file per uan vastità di attività. Sono file le sequenze di dati su di un hard disk, le configurazioni ma non solo, esistono filesystem specifici che creano file informativi con cui controllare il funzionamento del nostro computer ed anche molti device possono essere utilizzati come file, come dispositivi a caratteri che processano in vari modi sequenze di byte.

Il processo di caricamento del sistema culmina con una interfaccia grafica o nel nostro caso con un prompt di una shell ovvero dell'interfaccia a caratteri che utilizzeremo nelle nostre lezioni.

Conoscere l'interfaccia consente di effettuare molte operazioni sulla maggior parte dei dispositivi linux, nel nostro corso prenderemo in considerazione `bash` (bourne again shell), la più diffusa shell per linux; dopo il login ci troveremo nella directory home del nostro computer ovvero in `\home\pippo` ipotizzando che il nostro nome utente sia pippo o in `\root` nel caso che fossimo entrato con l'account di superuser (root appunto).

NON USARE MAI l'account di root come si è soliti fare in altri sistemi operativi.

Per spostarsi tra le directory si può usare il comando `cd` (change directory) ricordandosi che accetta sia path assoluti iniziando con `/` che path relativi dalla directory corrente (indicabile con `.` o senza indicazione alcuna) o da altre directory come ad esempio la home (`~`); qualora si voglia avere un elenco di tutti i file presenti nella cartella si può usare il comando `ls` (list) magary con l'argomento ll ovvero `ls -ll`

## Alcuni comandi utili

Alcuni comandi utili:

- `echo` stampa a video il contenuto di una stringa passata come argomento,
- `man` richiama il manuale di un certo comando,
- `mc` filemanager da console,
- `nano` edito di testo minimale,
- `rm` rimuove un file,
- `mkdir` creat una directory,
- `rmdir` rimuove una directory (che deve essere vuota),
- `touch` crea un file vuoto o cambia la data di un file esistente,
- `cat` stampa a video il contenuto di un file di testo,
- `ncdu` consente di navigare il filesystem ordinato in funzione della dimensione dei file e delle directory,
- `wget` consente di scaricare un file dal web,
- `dd` consente di traferire informazioni tra file, dispositivi, ...
- `tail` stampa a video le ultime riche di un file (utile per il log con l'opzione `-f` (follow))
- `chmod` cambia le prorietà di un file (ad esempio l'argomento `+x` consente l'esecuzione di un file)

Eseguibili presenti nella cartella corrente possono essere eseguiti premettendo `./` ovvero indicando che il path è riferito alla directory corrente.

## Redirezione input/output
La redirezione di input ed output puo essere fatta con i simboli `<` e `>`.

Per scrivere su di un file possiamo eseguire

```
echo "pippo" > pippo.txt
```

Questo creerà un file di nome pippo.txt con contenuto pippo, se poi digitiamo 

```
echo "pluto" > pippo.txt
```

Il contenuto del file verrà sostituito con pluto. Se volessimo mantenere il contenuto precedente e appendere in fondo il nuovo contenuto dobbiamo usare `>>` invece di `>`.

Il simbolo `<` funziona in maniera analoga per gli input.

## Pipe
Il pipe `|` consente di concatenare l'output di un programma con l'input di un altro.

```
cowsay "buona sera" | lolcat
```

L'output di cowsay viene dato in pasto al comando lolcat.

## Variabili
Le variabili sono nomi dati a spazi di memoria che possono contenere stringhe, numeri e altro.

Per settare una variabile si usa il comando `=`, per usarla basta premettere il carattere `$`. Per convenzione le variabili vengono scritte in maiuscolo.

```
VARIABILE="pippo"
echo $VARIABILE > pippo.txt
VARIABILE="pluto"
echo $VARIABILE >> pippo.txt
```

Crea un file con contenuto

```
pippo
pluto
```

Si può anche lanciare un programma e salvare l'output in una variabile 

```
VARIABILE=$(ls)
```

L'output del comando ls è salvato nella variabile di nome VARIABILE.

## Script 
Gli script sono liste di comandi eseguiti in sequenza.

Il primo comando è l'interprete utilizzato per lanciare il comando, normalmente `#!/bin/sh` ovvero l'eseguibile `/bin/sh` con il prefisso `#!`.

Prima di eseguirli richiedono i permessi di esecuzione con il comando `chmod +x nomefile`

## Ripetizioni
Questa lezione è ripetitiva e verrà ripetuta ogni settimana. Di seguito un elenco delle ripetizioni già effettuate.

| Data        | Note                                           |
|-------------|------------------------------------------------|
| 240122-2230 | Prima lezione                                  |
| 240129-2230 | Script bash                                    |
| 240205-2230 | Script bash                                    |