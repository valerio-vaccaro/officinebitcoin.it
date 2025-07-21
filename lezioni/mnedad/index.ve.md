# Mnemoniche & Dadi: impara a crear la tua mnemonica 

## Introduzion
Crear la mnemonica sfruttando na propria fonte de entropia xe ridur la superficie de attacco de un wallet Bitcoin tuttavia occor ten cont de quaj fattori:

- el process dev resultar el pù possibil sempliz e veloz senza fronzoli o ripetizion inutili,
- l'entropia va minga copiada su device minga necessari e va mantegnua al minim la necessitaa de far calcoli o elaborazion,
- se dev evitar l'us de software/script/programmi a meno che minga se ghe abbia fado un accurato controll del codice e de tuti le dipendenze,
- differenti setup pò richieder process leggermente differenti.

## Creazion de le parole
El primo step xe el calcolo de le 12 o 24 parole de la mnemonica, 12 parole xe normalmente pù che sufficient par la sicurezza de un wallet Bitcoin.

Par la generazion de le parole se pò usar el metodo descrito in [TRGM](https://github.com/valerio-vaccaro/TRMG) facendo us de 3 dadi de cui 1 a 8 facce e 2 a 16 facce. Ad OGNI lancio de i dadi corrisponde UNA ED UNA SOLA parola, par trovarla basta scorrere la tabella del sito cercando la corrispondenza de i dadi con el lancio fado (el primo dado xe SEMPRE quelo de 8 facce). La colonna word contien la parola cercada. 

El consiglio xe de generar tuti le 12 o 24 parole ed eventualmente de corregger l'ultima o comunque de usar i dadi par generar l'entropia relativa all'ultima parola.

## Calcolo del checksum
L'ultima parola no xe completamente decisa da noaltri ma contien na parte de controll ovvero no pòmo scernir pienamente tuti i 11 bit de entropia che la compong, pòmo invece scernir i primi 7 nel caso de mnemonica de 12 parole o i primi 3 nel caso de mnemonica a 24.

Mettemo che la nostra ultima parola sia BACON corrispondente ai lanci 1, 9 e 11 (ricordemo che el primo dado xe SEMPRE quelo de 8 facce), la tabella la riporta anca Group 12 e Group 24 che permetta de raggruppar le parole considerando solo l'entropia de i primi do lanci (group 12) o solo primo lancio (group 24).

Ipotizzemo de voler costruir na mnemonica a 12 parole, questo vol dir che el checksum sarà na parola tra le 16 possibili avente come gruppo 12 lo stesso de bacon ovvero 0001000, le parole possibili xe:

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

Come trovar tra le varie parole l'unica corretta? Dipend dal to setup, vedemo quaj esempi:

- bruteforce ovvero se prova tuti in sequenza fin a trovar quella corretta (molto ardu con mnemoniche a 24 parole), questo xe el metodo da usar con Ledger o con Electrum (assicurandose de scernir el flag BIP39),
- calcular tuti le parole possibili con le prime 11 o 23 parole e ricercar l'unica che casca in questo insieme, questo metodo xe quelo utilizzabile con Jade e con altri hardware wallet capaci de calcular tuti le possibili parole final de na mnemonica,
- inserir la mnemonica completa e lassar che l'hardware wallet la sistemi par noaltri, come ad esempio fa in maniera molto elegante Specter-DIY.

## Backup (argomento de n'altra lezion)
Fondamental aver na bona politica de backup quindi:
- multipli backup,
- su multipli supporti e
- eventualmente criptai o splittai (ma se dev savelo far ben).

## Bibliografia

- [TRMG](https://github.com/valerio-vaccaro/TRMG)

## Ripetizion
Questa lezion xe ripetitiva e vegnarà repetuda ogni mese. De seguito un elench de le ripetizion già fadde.

| Data        | Note                                           |
|-------------|------------------------------------------------|
| 240102-2100 | Prima lezion                                  | 