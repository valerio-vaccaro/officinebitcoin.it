# Mnemonich & Dad: impara a creà la tua mnemonica 

## Introduzion
Creà la mnemonica sfruttand una propria font de entropia l'è riduv la superficie de attacc de un wallet Bitcoin tuttavia occor ten cont de quaj fattor:

- el process dev resultà el pù possibil sempliz e veloz senza fronzol o ripetizion inutil,
- l'entropia va minga copiada su device minga necessari e va mantegnua al minim la necessitaa de fà calcol o elaborazion,
- se dev evità l'us de software/script/program a men che minga se gh'abbia fada un accurat controll del cod e de tutt le dipendenze,
- different setup pö richied process leggerment different.

## Creazion de le paroll
El prim step l'è el calcol de le 12 o 24 paroll de la mnemonica, 12 paroll hinn normalment pù che sufficient per la segurezza de un wallet Bitcoin.

Per la generazion de le paroll se pö usà el metod descritt in [TRGM](https://github.com/valerio-vaccaro/TRMG) facent us de 3 dad de cui 1 a 8 facce e 2 a 16 facce. Ad OGNI lanci de i dad corrispond UNA ED UNA SOLA parolla, per trovalla basta scorr la tabella del sit cercand la corrispondenza de i dad con el lanci fada (el prim dad l'è SEMPRE quell de 8 facce). La colonna word cont la parolla cercada. 

El consigli l'è de generà tutt le 12 o 24 paroll ed eventualment de corregg l'ultima o comunque de usà i dad per generà l'entropia relativa all'ultima parolla.

## Calcol del checksum
L'ultima parolla l'è minga completament decisa da noeuv ma cont una part de controll ovvero pödom minga scernì pienament tutt i 11 bit de entropia che la compong, pödom invece scernì i prim 7 nel cas de mnemonica de 12 paroll o i prim 3 nel cas de mnemonica a 24.

Mettom che la nostra ultima parolla sia BACON corrispondent ai lanci 1, 9 e 11 (ricordom che el prim dad l'è SEMPRE quell de 8 facce), la tabella la riporta anca Group 12 e Group 24 che permettaa de raggruppà le paroll considerand domà l'entropia de i prim duu lanci (group 12) o domà prim lanci (group 24).

Ipotizzom de volè costruì una mnemonica a 12 paroll, quest völ dì che el checksum sarà una parolla tra le 16 possibil avend come grup 12 el medem de bacon ovvero 0001000, le paroll possibil hinn:

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

Come trovà tra le varie paroll l'unica corretta? Dipend dal to setup, vedom quaj esempi:

- bruteforce ovvero se provaa tutt in sequenza fin a trovà quella corretta (molt ardu con mnemonich a 24 paroll), quest l'è el metod da usà con Ledger o con Electrum (assicurandoss de scernì el flag BIP39),
- calculà tutt le paroll possibil con le prim 11 o 23 paroll e ricercà l'unica che casca in quest insem, quest metod l'è quell utilizzaa con Jade e con alter hardware wallet capac de calculà tutt le possibil paroll final de una mnemonica,
- inserì la mnemonica completa e lassà che l'hardware wallet la sistemi per noeuv, come per esempi fa in manera molt eleganta Specter-DIY.

## Backup (argoment de un'altra lezion)
Fondamental avè una bona politica de backup donca:
- multipl backup,
- su multipl support e
- eventualment criptaa o splittaa (ma se dev savell fà ben).

## Bibliografia

- [TRMG](https://github.com/valerio-vaccaro/TRMG)

## Ripetizion
Questa lezion l'è ripetitiva e vegnarà repetuda ogni mes. De segu un elench de le ripetizion già fadde.

| Data        | Note                                           |
|-------------|------------------------------------------------|
| 240102-2100 | Prima lezion                                  | 