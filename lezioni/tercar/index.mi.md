# El terminal a caratter

## Introduzion
Linux (o mej un sistem GNU Linux vist che linux l'è domà el kernel che inizializza l'hardware e forniss le primitive per duvral) l'us el concett del file per una vastitaa de attività. Hinn file le sequenze de dat su un hard disk, le configurazion ma minga domà, esisten filesystem specific che crean file informativ con cui controllà el funzionament del nost computer e anca tant device pöden vess duvaa come file, come dispositiv a caratter che processen in vari mod sequenze de byte.

El process de caricament del sistem el culmina con una interfaccia grafic o nel nost cas con un prompt de una shell ovvero de l'interfaccia a caratter che duvremm in del nost lezion.

Cognoss l'interfaccia permett de fà tant operazion sulla maggior part dei dispositiv linux, in del nost cors considerem `bash` (bourne again shell), la pù diffusa shell per linux; dopo el login se trovem nella directory home del nost computer ovvero in `/home/pippo` se el nost nom utent l'è pippo o in `/root` se semm dentraa con l'account de superuser (root appost).

NUN DUVRA MAI l'account de root come se fa in alter sistem operativ.

Per spostass tra le directory se pö duvrà el comand `cd` (change directory) ricordandoss che l'accetta sia path assolut che cumincien con `/` che path relativ dalla directory current (indicabil con `.` o senza indicazion) o da alter directory come la home (`~`); se se voeuv avè un elench de tutt i file present nella cartella se pö duvrà el comand `ls` (list) magari con l'argument ll ovvero `ls -ll`

## Quaj comand util

Quaj comand util:

- `echo` stampa a video el contnüü de una stringa passaa come argument,
- `man` ciamaa el manual de un cert comand,
- `mc` filemanager da console,
- `nano` editor de test minimal,
- `rm` rimov un file,
- `mkdir` crea una directory,
- `rmdir` rimov una directory (che dev vess voeuida),
- `touch` crea un file voeu o cambia la data de un file esistent,
- `cat` stampa a video el contnüü de un file de test,
- `ncdu` permett de navigà el filesystem ordinand in funzione de la dimension dei file e delle directory,
- `wget` permett de scaricà un file dal web,
- `dd` permett de trasferì informazion tra file, dispositiv, ...
- `tail` stampa a video le ultim righe de un file (util per el log con l'opzion `-f` (follow))
- `chmod` cambia le proprietaa de un file (per esempi l'argument `+x` permett l'esecuzion de un file)

Eseguibil present nella cartella current pöden vess eseguì premend `./` ovvero indicand che el path l'è riferii alla directory current.

## Redirezion input/output
La redirezion de input e output pö vess fada con i simbol `<` e `>`.

Per scriv su un file pödem eseguì

```
echo "pippo" > pippo.txt
```

Quest el crearà un file de nom pippo.txt con contnüü pippo, se poeu digitem

```
echo "pluto" > pippo.txt
```

El contnüü del file el vegnarà sostituì con pluto. Se se voeuv mantegnì el contnüü precedent e aggiung in fond el noeuv contnüü se dev duvrà `>>` inveci de `>`.

El simbol `<` el funziona in manera analoga per i input.

## Pipe
El pipe `|` permett de concatenà l'output de un program con l'input de un alter.

```
cowsay "buona sera" | lolcat
```

L'output de cowsay el vegnarà dà in past al comand lolcat.

## Variabil
Le variabil hinn nom daa a spazi de memoria che pöden contene stringhe, numer e alter robb.

Per settà una variabil se duvrà el comand `=`, per duvralla basta premess el caratter `$`. Per convenzion le variabil hinn scritt in maiuscol.

```
VARIABILE="pippo"
echo $VARIABILE > pippo.txt
VARIABILE="pluto"
echo $VARIABILE >> pippo.txt
```

Crea un file con contnüü

```
pippo
pluto
```

Se pö anca lancià un program e salvà l'output in una variabil

```
VARIABILE=$(ls)
```

L'output del comand ls l'è salvà nella variabil de nom VARIABILE.

## Script
I script hinn list de comand eseguì in sequenza.

El prim comand l'è l'interprete duvrà per lancià el comand, normalment `#!/bin/sh` ovvero l'eseguibil `/bin/sh` con el prefiss `#!`.

Prima de eseguilli hinn necessari i permess de esecuzion con el comand `chmod +x nomefile`

## Ripetizion
Questa lezion l'è ripetitiva e vegnarà repetuda ogni settimana. De segu un elench de le ripetizion già fadde.

| Data        | Note                                           |
|-------------|------------------------------------------------|
| 240122-2230 | Prima lezion                                  |
| 240129-2230 | Script bash                                    |
| 240205-2230 | Script bash                                    | 