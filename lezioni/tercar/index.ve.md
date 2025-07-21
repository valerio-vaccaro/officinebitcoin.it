# El terminal a caratteri

## Introduzion
Linux (o mej un sistema GNU LInux in quanto linux xe solo el kernel che inizializza l'hardware e forniss le primitive par usarlo) usa el concetto del file par na vastità de attività. Xe file le sequenze de dati su de un hard disk, le configurazion ma no solo, esistono filesystem specific che crea file informativi con cui controllar el funzionamento del nostro computer ed anca molti device pò esser utilizzao come file, come dispositivi a caratter che processen in vari modi sequenze de byte.

El process de caricamento del sistema culmina con na interfaccia grafica o nel nostro caso con un prompt de na shell ovvero de l'interfaccia a caratter che utilizzaemo nelle nostre lezion.

Cognosser l'interfaccia permet de far molte operazion sulla maggior parte dei dispositivi linux, nel nostro corso consideremo `bash` (bourne again shell), la pù diffusa shell par linux; dopo el login se trovemo nella directory home del nostro computer ovvero in `/home/pippo` ipotizzando che el nostro nome utente sia pippo o in `/root` nel caso che fossimo entrai con l'account de superuser (root appunto).

NUN USAR MAI l'account de root come se fa in altri sistemi operativi.

Par spostarse tra le directory se pò usar el comando `cd` (change directory) ricordandose che l'accetta sia path assoluti iniziando con `/` che path relativi dalla directory corrente (indicabile con `.` o senza indicazion alcuna) o da altre directory come ad esempio la home (`~`); se se vol aver un elench de tuti i file present nella cartella se pò usar el comando `ls` (list) magari con l'argomento ll ovvero `ls -ll`

## Quaj comando util

Quaj comando util:

- `echo` stampa a video el contenuto de na stringa passada come argomento,
- `man` ciama el manual de un certo comando,
- `mc` filemanager da console,
- `nano` editor de testo minimal,
- `rm` rimove un file,
- `mkdir` crea na directory,
- `rmdir` rimove na directory (che dev esser voeida),
- `touch` crea un file voeo o cambia la data de un file esistente,
- `cat` stampa a video el contenuto de un file de testo,
- `ncdu` permet de navigar el filesystem ordinando in funzione de la dimensione dei file e delle directory,
- `wget` permet de scaricar un file dal web,
- `dd` permet de trasferir informazion tra file, dispositivi, ...
- `tail` stampa a video le ultime righe de un file (util par el log con l'opzion `-f` (follow))
- `chmod` cambia le proprietà de un file (par esempi l'argomento `+x` permet l'esecuzion de un file)

Eseguibili present nella cartella corrente pò esser esegui premendo `./` ovvero indicando che el path xe riferio alla directory corrente.

## Redirezion input/output
La redirezion de input ed output pò esser fada con i simboli `<` e `>`.

Par scriver su de un file pòmo eseguir

```
echo "pippo" > pippo.txt
```

Questo crearà un file de nome pippo.txt con contenuto pippo, se poeu digitemo 

```
echo "pluto" > pippo.txt
```

El contenuto del file vegnarà sostituio con pluto. Se volessimo mantegner el contenuto precedente e appendere in fondo el novo contenuto se dev usar `>>` inveci de `>`.

El simbolo `<` funziona in maniera analoga par i input.

## Pipe
El pipe `|` permet de concatenar l'output de un programma con l'input de un altro.

```
cowsay "buona sera" | lolcat
```

L'output de cowsay vegnarà dao in past al comando lolcat.

## Variabili
Le variabili xe nomi dao a spazi de memoria che pò contener stringhe, numeri e altro.

Par settar na variabile se usa el comando `=`, par usarla basta premess el carattere `$`. Par convenzion le variabili vegna scritte in maiuscolo.

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

Se pò anca lanciar un programma e salvar l'output in na variabile 

```
VARIABILE=$(ls)
```

L'output del comando ls xe salvà nella variabile de nome VARIABILE.

## Script 
I script xe liste de comandi esegui in sequenza.

El primo comando xe l'interprete utilizzao par lanciar el comando, normalmente `#!/bin/sh` ovvero l'eseguibile `/bin/sh` con el prefisso `#!`.

Prima de eseguili richiede i permessi de esecuzion con el comando `chmod +x nomefile`

## Ripetizion
Questa lezion xe ripetitiva e vegnarà repetuda ogni settimana. De seguito un elench de le ripetizion già fadde.

| Data        | Note                                           |
|-------------|------------------------------------------------|
| 240122-2230 | Prima lezion                                  |
| 240129-2230 | Script bash                                    |
| 240205-2230 | Script bash                                    | 