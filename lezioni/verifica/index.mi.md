![cover](https://officinebitcoin.it/lezioni/verifica/1cover.webp)
La verifica de le firm crittografich l'è una pratica de sicurezza fondamental che **ogni utent de software open-source el dovress inserì in la routine de le bon abitudin**.

Open source l'è per la sò natura modificabil e quell chì el vol dì che chiunque el pö, a livell teoregh, introdü backdoor, attacch o còdegh malevol in le applicaziù che te dopret per esercitàtt, intant che te impar el protocoll Bitcoin.

Come utent che l'è in del profondì el studi, te gh'hee la possibilità de verificar personalment se el software scaricà l'è staa manomess, e te el dovress fà prima de installàll e dopràll.

Prima de scomenzà, portemm anca in Officine Bitcoin un classic de le presentaziù: el meme. El sarà minga una presentaziù pesanta, ma decomprimemm l'atmosfera già de subit.

![meme](https://officinebitcoin.it/lezioni/verifica/2meme.webp)

## Come fàll?
I svilupador rilasenn le noeuv version de software accompagnandole semper con una firm crittografica.
El vol dì che - oltre ad avè agiornà el software - el rilasenn certificand de avèll vincolà con una specifica impronta digital. Reminder: la firm digital produuda con la ciave privada, l'è unica e minga modificabil.

Tutt quell de cui te gh'heet besogn l'è la suite GPG per proced a la verifica de la firm.

![img](https://officinebitcoin.it/lezioni/verifica/3.webp)

# Pre requisit per quest esercitaziù
- Un bref ripass su la crittografia asimetrica
- I element da verificar:
  - software (binari, apk ecc)
  - la firm digital de l'svilupador, normalment un file `.asc`, `.sig` o un checksum.
- I strument per fà la verifica:
  - GPG suite
  - un terminal (el val sia per Linux sia per Win)
# Crittografia asimetrica

![img](https://officinebitcoin.it/lezioni/verifica/4.webp)

Qui gh'è dò ciave correlate tra lor: una ciave pùblica e una privada. Come suggerissen i nom:
- La ciave pùblica l'è disponibil liberament e la pö vess condividuda con chiunque.
- La ciave privada l'è tenuda al sicur dal sò proprietari.

I dat cifrà con la ciave pùblica pöden vess decifrà domà de la ciave privada corrispondent. Quell chì el permet a chiunque de mandà dat crittografà al proprietari de la coppia de ciave, sensa previa condivid de la part segreta.

La crittografia a ciave pùblica l'è pù lenta de la crittografia simetrica e l'è minga adatta a cifrà dat de grand dimension. Però, la permet la distribuziù sicura de le ciave de crittografia.
Quaj algoritm doprà comunement per la crittografia a ciave pùblica includen RSA, ECC, ElGamal e DSA.

## Part svilupador: noeuv agiornament

L'svilupador el rilasc el còdegh open source, per la sò natura minga cifrà.
El ne fa un hash crittografich (e quest chì el genera el `checksum`) e el cifra el digest con la sò ciave privada: quest chì el crea la firm, quell file `.sig` o `.asc` anticipà prima.

Dopo quell process, l'svilupador el carica sul sit o su un repository Github tutt e dò i file. L'è lì che scomenza el tò download.

![img](https://officinebitcoin.it/lezioni/verifica/5.webp)

Poi te servirà la ciave pùblica de l'svilupador. A volt la se troeuva in del repository Github, a volt su server pùblich (*keyserver*). Anca se la ricerca la pö richied sforz, la ciave pùblica l'è un element indispensabil per verificar el software, donca impegnett per ottegnilla.

In cas de difficoltà, fa domand sul grupp Telegram de Officine Bitcoin, indove te trovarè i indicaziù per ottegnì una specifica ciave pùblica.

![img](https://officinebitcoin.it/lezioni/verifica/6.webp)

Per verificar l'integrità de i dat, el destinatari el decifra la firm doprand la ciave pùblica del mittent, ottegnend un risultà:

a. i dat hinn consideraa autentich e minga modificaa durante el transit.
b. i dat hinn staa potenzialment manomess.

Crittografand el valor hash con la ciave privada, **le firm PGP garanteen che el checksum medesim el sia protett e collegà a l'identità del mittent. Quell chì el impediss la falsificaziù de le firm su dat alteraa**.

Le firm pöden vess doprade per verificar quajvuna: file, e-mail, document e download de software. Quand se controlla una firm PGP, se dimostra che i dat provenen de fatti de na font affidabil e hinn integri.

E l'è la verifica de un apk per cellulare che te poderè verificar adess.

Doprom come esempi el download de Phoenix, wallet LN non-custodial, per trattàll in del specific in una prossima serada de Officine Bitcoin.

# Download e verifica Phoenix Wallet (Acinq)
Se te see già staa sul sit de [Acinq](https://phoenix.acinq.co/), l'svilupador de Phoenix, te see già che el download l'è disponibil su i store ufficial per Android e iOS.
Magari te gh'hee minga mai faa cas, ma per Android l'è disponibil anca el file apk.

![img](https://officinebitcoin.it/lezioni/verifica/8.webp)

[Andemm-gh!](https://github.com/ACINQ/phoenix/releases) per trovar i file `apk` e `Signature` che te scaricarè con `wget`.
In del cas de Phoenix el file che el cont la firm per la verifica l'è nominà **`SHA256SUMS.ASC`**.

![img](https://officinebitcoin.it/lezioni/verifica/9.webp)

In del medem repository gh'è anca i indicaziù per scaricà la ciave pùblica corrispondent a la *signing key E04E48E72C205463* (impronta digital unica de le ciave de Drouinf).
Copia el link e scaricalla con `wget`, oppur seguì i istruzion suggeride in la seziù apposita del repo.

![img](https://officinebitcoin.it/lezioni/verifica/10.webp)

---
⚠️**La ciave pùblica la dev vess importada, oltre che scaricada**.
⚠️ El download de i file el dev succed in la medema directory.

---
# Vèrt el terminal
Con el terminal, posizionett in la directory indove hinn staa scaricaa l'apk e el file `SHA256SUMS.ASC` ed eseguì i comand in l'ordin.

![img](https://officinebitcoin.it/lezioni/verifica/11.webp)

![img](https://officinebitcoin.it/lezioni/verifica/12.webp)

Quand la verifica l'ha restituì esit positiv, te poderè trasferì l'apk sul cellulare e installà l'app.

---
# Verifica difficoltosa
Gh'è pöden vess diverse reson per cui la verifica de le firm l'è minga agevola, e hinn quasi semper da imputà al disordin o a l'esperienza:
1. i file apk e/o .asc hinn staa scaricaa pù volt, donca in la directory resulten - per esempi nom strani tipo **nomefile-1** o **nomefile(1)**
2. apk e .asc stann minga in la medema directory
3. la ciave pùblica l'è stada scaricada ma minga importada in del keyring gpg.

Pöden invece capitar alter situaziù, per le quali - anca operand corettament - la verifica la ries minga.
L'è important verificar l'eror che compar a terminal, copiàll e scomenzà una ricerca su internet per la soluziù.

# Verifica con Sparrow Wallet
Se invece te dopret già Sparrow Wallet, te pödet proced a verificar i download con quest software, **el cui download e installaziù deven vess precedude de un'attenta e rigorosa verifica con GPG**.

Lancia Sparrow wallet e cerca in del menu `Tools` -> `Verify Downloads`.

![img](https://officinebitcoin.it/lezioni/verifica/13.webp)

Se vèrt un'interfaccia che la domanda de inserì i file appena scaricaa. Cliccand su `Browse` se vèrt el file manager, per caricar ogni file in del camp richiest.

![img](https://officinebitcoin.it/lezioni/verifica/14.webp)

A volt el form de l'interfaccia el se completa da sol. Se el fa minga, riempi tutt i camp con i file appropriaa.

![img](https://officinebitcoin.it/lezioni/verifica/15.webp)

L'esit, positiv, l'è mostrà graficament de le spunt verd e de la conferma *`Ready to install`* + < nome file >.

# Support al studi
Se te gh'heet partecipà a la presentaziù in diretta Telegram, te pödet consideràlla un ulterior pass vers la tua personal sovranità (minga solo finanziaria).
Se te te la see persa **minga desperà**: quest appunt serven appunt per recuperà e, in oltre, te dev savè che la riproporremm anmò su Officine.

Per minga perd la prossima presentaziù, uniscet al [grupp Telegram](https://t.me/officinebitcoin), per restà in agiornament costant.

![img](https://officinebitcoin.it/lezioni/verifica/17.webp)

Te pödet anca cerca el [Satoshi Spritz](https://satoshispritz.it/) pù vesin a te. Un Satoshi Spritz l'è un meetup local indove se parla domà de Bitcoin, indove te pödet portà le tò domand e fàtt rispond de alter bitcoiner espert. Al link te trovarè la mapa de la penisola.

![img](https://officinebitcoin.it/lezioni/verifica/16.webp)

In fin, se te trovet minga el meetup vesin a te, te pödet approfittà de le dirette settimanai de [SatoshiSpritz Connect](https://t.me/SatoshiSpritzConnect), un meetup virtual creà per chi che pö minga partecipà ai Satoshi Spritz, o per aiutà i meetup pù picinin a prend appunt e trovar ispiraziù per le sò presentaziù.

![img](https://officinebitcoin.it/lezioni/verifica/18.webp)
