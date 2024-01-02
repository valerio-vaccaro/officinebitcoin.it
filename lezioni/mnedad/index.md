# Mnemoniche & Dadi: imapara a create la tua mnemonica 

## Introduzione
Creare la mnemonica sfruttando una propria fonte di entropia è ridurre la superficie di attacco di un wallet Bitcoin tuttavia occorre tenere conti di alcuni fattori:

- il processo deve risultare il più possibile semplice e veloce senza fronzoli o ripetizioni inutili,
- l'entropia non va copiata su device non necessari e va mantenuto al minimo la necessità di effettuare calcoli o elaborazioni,
- bisogna evitare l'uso di software/script/programmi a meno che non si abbia effettuato un accurato controllo del codice e di tutte le dipendenze,
- differenti setup possono richiedere processi leggermente differenti.

## Crezione delle parole
Il primo step è il calcolo delle 12 o 24 parole della mnemonica, 12 parole sono normalmente più che sufficienti per la sicurezza di un wallet Bitcoin.

Per la generazione delle parole si può usare il metodo descritto in [TRGM](https://github.com/valerio-vaccaro/TRMG) facente uso di 3 dadi di cui 1 a 8 facce e 2 a 16 facce. Ad OGNI lancio dei dadi corrisponde UNA ED UNA SOLA parola, per trovarla basta scorrere la tabella del sito cercado la corrispondenza dei dadi con il lancio effettuato (il primo dado è SEMPRE quello da 8 facce). La colonna word contiene la parola cercata. 

Il consiglio è di generare tutte le 12 o 24 parole ed eventualmente di correggere l'ultima o comunque di usare i dadi per generare l'entropia relativa all'ultima parola.

## Calcolo del checksum
L'ultima parola non è completamente decisa da noi ma contiene una parte di controllo ovvero non possiamo scegliere pienamente tutti gli 11 bit di entropia che la compongono, potremo invece scegliere i primi 7 nel caso di mnemonica di 12 parole o i primi 3 nel caso di menmonica a 24.

Mettiamo che la nostra ultima parola sia BACON corrispondente ai lanci 1, 9 e 11 (ricordiamo che il primo dado è SEMPRE quello da 8 facce), la tabella ci riporta anche Group 12 e Group 24 che ci permettono di raggruppare le parole considerando solo l'entropia dei primi due lanci (group 12) o sel solo primo lancio (group 24).

Ipotizziamo di voler costruire una mnemonica a 12 parole, ciò vuol dire che il checksum sarà una parola tra le 16 possibili avente come gruppo 12 lo stesso di bacon ovvero 0001000, le parole possibili sono:
|First|Second|Third|Index|Word	|Index in binary|Group 12	|Group 24|
|---|---|---|-------|-----------|---------------|-----------|---|
|1  |9	|1	|128	|avoid	    |00010000000	|0001000	|000|
|1  |9	|2	|129	|awake	    |00010000001	|0001000	|000|
|1  |9	|3	|130	|aware	    |00010000010	|0001000	|000|
|1  |9	|4	|131	|away	    |00010000011	|0001000	|000|
|1  |9	|5	|132	|awesome	|00010000100	|0001000	|000|
|1  |9	|6	|133	|awful	    |00010000101	|0001000	|000|
|1  |9	|7	|134	|awkward	|00010000110	|0001000	|000|
|1  |9	|8	|135	|axis	    |00010000111	|0001000	|000|
|1  |9	|9	|136	|baby	    |00010001000	|0001000	|000|
|1  |9	|10	|137	|bachelor	|00010001001	|0001000	|000|
|1  |9	|11	|138	|bacon	    |00010001010	|0001000	|000|
|1  |9	|12	|139	|badge	    |00010001011	|0001000	|000|
|1  |9	|13	|140	|bag    	|00010001100	|0001000	|000|
|1  |9	|14	|141	|balance	|00010001101	|0001000	|000|
|1  |9	|15	|142	|balcony	|00010001110	|0001000	|000|
|1  |9	|16	|143	|ball   	|00010001111	|0001000	|000|

Come trovare tra le varie parole l'unica corretta? Dipende dal tuo setup, vediamo alcuni esempi:

- bruteforce ovvero si provano tutte in sequenza fino a trovare quella corretta (molto arduo con menmoniche a 24 parole), questo è il metodo da usare con Ledger o con Electrum (assicurandosi di selezionare il flag BIP39),
- calcolare tutte le parole possibili con le prime 11 o 23 parole e ricercare l'unica che cade in questo insieme, questo metodo è quello utilizzabile con Jade e con altri hardware wallet capaci di calcolare tutte le possibili parole finali di una mnemonica,
- inserire la mnemonica completa e lasciare che l'hardware wallet la sistemi per noi, come ad esempio fa in maniera molto elegante Specter-DIY.

## Backup (argomento di un'altra lezione)
Fondamentale avere una buona politica di backup quindi:
- multipli backup,
- su multipli supporti e
- eventuamente crittati o splittati (ma bisogna saperlo fare bene).

## Bibliografia

- [TRMG](https://github.com/valerio-vaccaro/TRMG)

## Ripetizioni
Questa lezione è ripetitiva e verrà ripetuta ogni mese. Di seuito un elenco delle ripetizioni già effettuate.

| Data        | Note                                           |
|-------------|------------------------------------------------|
| 240102-2100 | Prima lezione                                  |
