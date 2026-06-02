---
layout: default
name: "Capir el Coin Control manual"
description: "Guida completa a la selezion manuale dei UTXO. Capir parchè xe importante e imparar come te poi farlo co diversi software wallet (desktop e mobile)"
title: "Capir el Coin Control manual"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lezion Bitcoin-only</span> <span>Sto progetto xe mantegnuo da valerio-vaccaro</span></p>

## 🌍 Traduzion

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](https://officinebitcoin.it/lezioni/coinco/cover.webp)

# Capir el Coin Control manual

## Introduzione

La solidità del protocollo Bitcoin xe garantita da concetti cardine semplici. Tra sti, spicca la trasparenza: tutte le transazion Bitcoin xe pubbliche e facilmente verificabili da chiunque. Sebbene sta caratteristica sia na pietra miliare del protocollo, perché previene frodi e garantisce la genuinità dei fondi, può rappresentare anca na sfida par la confidenzialità. **Te sei domandato se tanta trasparenza può inficiare la tua privacy?

Dovresti farlo. Se da na parte accumulare satoshi no-kyc xe piuttosto semplice, la tua privacy xe maggiormente a rischio proprio nella fase si spesa.
## Cosa succede quando spendi un UTXO
Spendere Bitcoin no xe semplicemente el trasferimento de valore a qualcun altro. 

Consumando uno dei to UTXO, infati, te devi soddisfare le condizioni imposte par la trasparenza del protocollo, perché te devi dimostrare de essere el proprietario de quei fondi. Devi pertanto:
- esporre la tua chiave pubblica;
- produrre na firma digitale.

El momento de la spesa xe dunque el più critico: **spender bitcoin xe un atto da compiere in maniera consapevole e co el maggior controllo possibile**.

## Coin Control
Nel protocollo Bitcoin, elementi come "_conto_" o "_unità monetarie_" no esistono. El concetto de UTXO no fa parte dei scopi de sta lezione, ma te invito a fare le domande relative al tuo satoshi spritz de fiducia, o a richiedere na lezione qui su Officine Bitcoin.
Ciò che te devi sapere xe che co Bitcoin ciò che accumuli e, in seguito spenderai, xe piccole o grandi unità de conto misurate in satoshi, rappresentati da `output di transazione non spesi`, i **UTXO**, detti anca `coins`.
Quando si utilizzano UTXO par creare na transazion, sti vengono completamente distrutti e si creano altri UTXO al loro posto.

I software wallet xe sviluppati par fare sta scelta in maniera automatica, utilizzando coins selezionate in maniera "casuale" co l'unico criterio de coprire l'importo necessario a la spesa.

El `Coin Control`, che te poi trovare anca denominato `Coin Selection`, xe na funzione caratteristica de alcuni software wallet, che te permette de **selezionare manualmente i UTXO da spender quando costruisci la tua transazion**.

Supponiamo de avere un wallet co 3 UTXO, rispettivamente da 21.000, 42.000 e 63.000 satoshi.

![img](https://officinebitcoin.it/lezioni/coinco/01.webp)

Se te devi spender 24.000 sats e lasci fare al software la selezion automatica, un buon wallet potrebbe sielziere de combinare l'UTXO1 + l'UTXO2 par pagare i 24k sats e le fee del miner, creando un resto che torna su un indirizzo interno del wallet de partenza.

![img](https://officinebitcoin.it/lezioni/coinco/02.webp)

Dopo la transazion la nuova situazione nel wallet, contando solo i UTXO, si può così riassumere.

![img](https://officinebitcoin.it/lezioni/coinco/03.webp)

Co el giusto software e la tua consapevolezza, invece, avresti potuto compiere na scelta diversa e più corretta. Ad esempio selezionando solo l'UTXO2 (da 42.000 sats).

![img](https://officinebitcoin.it/lezioni/coinco/04.webp)

Co na situazione finale, a livello de UTXO, nel tuo wallet che ha un aspetto differente.

![img](https://officinebitcoin.it/lezioni/coinco/05.webp)

## Perché selezionare manualmente i UTXO?
![img](https://officinebitcoin.it/lezioni/coinco/06.webp)

Nel nostro esempio, el saldo de fatto el stesso: `108.280 sats`. Dopo la spesa de 24.000 sats, senza coin control avremmo 2 UTXO nel wallet; co el coin control manuale ne abbiamo 3 totali.

**Perché fare tutto sto?**

Ci xe, o potrebbero esserci, diversi motivi par cui no abbiamo usato l'`UTXO1` **e xe tutti a la base del perché - in fase de spesa - attivare el coin control manuale xe na de le buone pratiche da seguire**.

## Privacy
El vantaggio principale, quando si parla de manual coin selection, xe na **maggiore privacy par chi spende**.

Prendiamo sempre el nostro esempio: la spesa de 24.000 satoshi _senza coin control_. Essendo la blockchain de Bitcoin un registro pubblico, un osservatore esterno può dichiarare, senza ombra de dubbio, che i input `UTXO1 di 21.000 sats` e `UTXO2 di 42.000 sats`, nonché el resto, l'`UTXO5 da 38.280 sats` **appartengono tutti e tre allo stesso utente**.

Selezionando manualmente l'`UTXO2`, invece, rimane completamente riservato l'`UTXO1`, fermo nell'UTXO set in attesa de essere speso in un momento più appropriato.

L'`UTXO1` potrebbe provenire da na fonte KYC, ad esempio un pagamento ricevuto in cambio de beni e servizi, mentre i altri UTXO no.

**Se fosse el to wallet, vorresti che un osservatore esterno possa risalire a la tua identità co na certezza così assoluta?** I wallet che implementano la selezion manuale dei UTXO, permettono ad esempio la **segregazione de uno o più UTXO**, na funzione da doprar quando si presentano situazioni de sto tipo.

Sebbene io sia convinta che fondi KYC dovrebbero essere conservati in un wallet separato rispetto a bitcoin acquistati senza kyc, se sto xe el tuo caso la segregazione de alcuni to indirizzi xe un aiuto fondamentale, che potresti ricevere imparando a selezionare manualmente i to input de spesa.

## Risparmio sulle fee
Selezionare l'UTXO corretto par effettuare na spesa consente de ottimizzare le fee. Sempre partendo dal nostro esempio, el software wallet ha selezionato due UTXO par coprire la la spesa da fare. Due UTXO implicano due firme da mostrare a la rete, donca un peso maggiore de la transazion stessa in termini de vByte.

Usando el coin control manuale, invece, te poi selezionarne uno solo che sia sufficiente a coprire l'importo, risparmiando fee perché diminuisce el "peso" de la transazion.

In periodi in cui le fee xe alte, ma sei costretto a spender bitcoin on-chain (ad esempio par aprire un canale Lightning Network), ecco che el coin control si rivela el giusto incentivo economico a cui ricorrere.

## Aggregazione dei resti
Quando si fa un pagamento e si usano Bitcoin on-chain, la possibilità de ricevere un resto diventa quasi sempre na certezza. Ogni resto xe de par sé na piccola perdita de privacy, in quanto svela a la rete un tuo indirizzo che si può associare al tuo input de partenza.

Considerando che i migliori wallet HD generano dei indirizzi appositi par i resti, te poi riconoscerli facilmente e "segregare" tutti i resti de le varie transazion effettuate; quando sti hanno raggiunto un certo importo te poi selezionarli manualmente e consolidarli, o fare swap su Lightning Network (el mio metodo preferito) e trattarli così da riguadagnare la privacy perduta in fase de spesa.

## Spesa da un cold wallet
El cold wallet xe uno strumento co cui si può ragionevolmente ottenere un buon grado de sicurezza, par conservar na qualsiasi quantità de fondi da tenere da parte par un lungo periodo de tempo. Possono però capitare dei imprevisti, in cui xe necessario mettere mano ai risparmi e far fronte a qualche spesa inaspettata.

El mio consiglio xe quello de **no effettuare mai la spesa direttamente dal cold wallet, par evitare de ricevere el resto tra i indirizzi dello stesso**. Impara a selezionare manualmente i UTXO necessari a coprire la spesa, trasferiscili su un wallet hot e prepara la tua transazion da quest'ultimo. L'eventuale resto, poi, potrai rimandarlo su un indirizzo del cold wallet (se l'importo xe adeguato), opure utilizzarlo par altri scopi.

## Presentazione pratica
Dopo sta lunga introduzione, vediamo come mettere in pratica el coin control co diversi software desktop e mobile. Useremo sempre el stesso wallet HD, importato in ognuno dei strumenti scelti, in modo da mostrarti le piccole differenze che ci xe tra de loro.

## Wallet Desktop

## Sparrow
Se usi Sparrow, apri el to wallet e seleziona _UTXOs_ dal menu a sinistra. Te comparirà la lista dei tutti i UTXO associadi al tuo wallet.

Clicca semplicemente co el mouse su uno de loro e poi sielzi _Send Selected_. Sparrow te mostra anca el totale selezionato par la spesa, accanto al comando.

![img](https://officinebitcoin.it/lezioni/coinco/07.webp)

Puoi anca selezionarne più de uno. Aiutati co el tasto _CTRL_ par selezionare UTXO no adiacenti nella lista.

![img](https://officinebitcoin.it/lezioni/coinco/08.webp)

Dopo aver selezionato manualmente i UTXO, Sparrow te mostrerà ben, graficamente, come xe costruita la tua transazion, che te poi finalizzare e concludere.

![img](https://officinebitcoin.it/lezioni/coinco/09.webp)

### Segregazione dell'UTXO
Segregare dei fondi significa "bloccarli" all'interno del wallet, affinché no possano essere usati come input de na transazion. 

Sparrow permette sta funzionalità, cui si accede sempre dal menu _UTXOs_. Si posiziona el mouse sull'UTXO da "bloccare" e si clicca el tasto destro del mouse. Tra le funzionalità de sta procedura comparirà el comando _Freeze_. Xe così che potrai segregare un UTXO co Sparrow Wallet.

![img](https://officinebitcoin.it/lezioni/coinco/29.webp)

## Electrum
Se el to wallet desktop xe Electrum, te devi sapere che te poi selezionare manualmente i UTXO sia dal menu _Addresses_ sia dal menu _Coins_.
In entrambi i menu la selezion avviene puntando el mouse sull'UTXO da sielziere e sielziendo _Add to coin control_ dopo aver cliccato el tasto destro.

![img](https://officinebitcoin.it/lezioni/coinco/10.webp)

Anca co sto software te poi selezionare più de un UTXO, aiutandoti co el tasto _CTRL_ de la tastiera se no xe adiacenti tra loro.

![img](https://officinebitcoin.it/lezioni/coinco/11.webp)

Graficamente Electrum te mostrerà la selezion evidenziando in verde i UTXO selezionati, mentre in basso te compare na barra, evidenziata dello stesso colore, che mostra el saldo disponibile dopo el coin control.

![img](https://officinebitcoin.it/lezioni/coinco/12.webp)

Na volta selezionato l'output o i output, te poi costruire la tua transazion come sempre, dal menu _Send_.

### Segregazione dell'UTXO
Electrum mette a disposizione sta possibilità, andando nel menu _Coins_ e selezionando un determinato UTXO e poi sielziendo _Freeze_ co el tasto destro del mouse. Si può "freezare" l'indirizzo anca senza fondi dal menu _Addresses_, opure la "coin" par no spenderla.

![img](https://officinebitcoin.it/lezioni/coinco/28.webp)

## Nunchuk
Nunchuk permette de selezionare i UTXO dal menu principale, na volta aperto.
Lancia Nunchuk e clicca _View coins_.

![img](https://officinebitcoin.it/lezioni/coinco/13.webp)

Si apre la finestra che contiene tutti i UTXO del to wallet, dove te poi selezionarne uno o più, attivando la spunta accanto ad ogni importo. Dopo aver effettuato la selezion, continua co _Create transaction_.

![img](https://officinebitcoin.it/lezioni/coinco/14.webp)

Dopodiché potrai inserire l'indirizzo de destinazione e impostare l'importo e le fee.

![img](https://officinebitcoin.it/lezioni/coinco/15.webp)

## Blockstream App
Blockstream App desktop, già conossiuto come Green, permette de fare coin selection quando si xe già iniziata a costruire la transazion. Apri pertanto el to wallet e clicca su _Send_.

![img](https://officinebitcoin.it/lezioni/coinco/16.webp)

Incolla l'indirizzo de destinazione nel campo apposito e poi seleziona _Manual coin selection_.
![img](https://officinebitcoin.it/lezioni/coinco/17.webp)
Si apre la finestra dove te poi selezionare uno o più UTXO. Nell'esempio che segue, abbiamo selezionato due coins. Dopodiché conferma la scelta cliccando su _Confirm Coin Selection_.

![img](https://officinebitcoin.it/lezioni/coinco/18.webp)

Imposta l'importo e le fee e poi procedi normalmente co la tua transazion.

![img](https://officinebitcoin.it/lezioni/coinco/19.webp)

⚠️ N.B. Nel menu _Coins_ de Green xe presenti le voci _Lock_/_Unlock_ che prefigurano la possibilità de segregare UTXO. Sta possibilità xe presente solo negli account cosiddetti multisig; inoltre la funzionalità si attiva solo selezionando UTXO de importo tanto piccolo, vicino a la soglia del `Dust`.

## Wallet mobile

## Blue Wallet
Anca da mobile xe possibile sielziere wallet che permettono de selezionare manualmente i UTXO. Vediamo par primo Blue Wallet.

Se sei un utente de sto software, apri el to wallet e clicca par entrare nelle schermate dei comandi relativi ad uno dei to wallet. Par accedere al coin control si deve entrare nella fase de spesa, donca clicca _Send_.

![img](https://officinebitcoin.it/lezioni/coinco/21.webp)

Nella successiva schermata sielzi i menu segnalati dai tre pallini in alto a destra. Si apre na finestra a tendina co na serie de comandi. Scegli l'ultimo: _Coin Control_.

![img](https://officinebitcoin.it/lezioni/coinco/22.webp)

A sto punto Blue Wallet mostra tutti i to UTXO. Oltre che dagli importi, xe differenziati graficamente da colori diversi.

![img](https://officinebitcoin.it/lezioni/coinco/27.webp)

Scegli l'UTXO da selezionare dopodiché seleziona _Use Coin_.

![img](https://officinebitcoin.it/lezioni/coinco/23.webp)

Blue Wallet te riporta nella finestra de _Send_ par continuare a costruire la transazion. Aggiusta l'importo e le fee, dopodiché sielzi _Next_.

![img](https://officinebitcoin.it/lezioni/coinco/24.webp)

A sto punto te poi terminare la transazion, come fai de solito.

### Segregazione de un UTXO
Anca Blue Wallet permette de segregare i UTXO, rendendoli no disponibili par la spesa, el che no xe male come funzione par un wallet da dispositivo mobile.

Si accede al coin control co la procedura appena spiegata e, dopo aver selezionato l'UTXO, sielzi _Freeze_ al posto de _Use Coin_.

![img](https://officinebitcoin.it/lezioni/coinco/26.webp)

## Nunchuk
Anca la version mobile de Nunchuk prevede la possibilità par l'utente de effettuare el coin control. Se usi sta app da mobile, aprilo e vai nel menu _Wallet_. Da qui sielzi _View coins_.

![img](https://officinebitcoin.it/lezioni/coinco/30.webp)

Nella finestra dove compare la lista dei UTXO clicca _Select_.

![img](https://officinebitcoin.it/lezioni/coinco/38.webp)

Accanto ad ogni UTXO appare la funzione de selezion. Come nella version desktop, anca su Nunchuk mobile la selezion manuale avviene spuntando el quadratino accanto all'importo. La schermata riporta el numero de UTXO selezionati e l'importo totale a disposizione. Na volta finito, el simbolo ₿ in basso a sinistra, che xe el comando par iniziar a costruire la transazion.

![img](https://officinebitcoin.it/lezioni/coinco/31.webp)

Ora te poi completare la transazion, sielziendo l'importo e cliccando su _Continue_.

![img](https://officinebitcoin.it/lezioni/coinco/32.webp)

Continua come fai sempre, incollando un indirizzo de destinazione, na descrizione e personalizzando le impostazion de le fee.

## Bitcoin Keeper
Bitcoin Keeper xe l'ultimo wallet che vedremo in sta guida. Vediamo la sua funzionalità applicata al coin control co un wallet single-sig, anca se un tale 'uso  no xe el scopo de sta app tanto particolare.

Dopo aver impostato Keeper sul to telefono, lancialo e apri un wallet contenente alcuni UTXO. Al centro de la schermata principale clicca _View All Coins_.

![img](https://officinebitcoin.it/lezioni/coinco/34.webp)

Keeper mostra na panoramica dei UTXO. Par accedere a la schermata de selezion clicca _Select To Control_.

![img](https://officinebitcoin.it/lezioni/coinco/35.webp)

Puoi selezionare le coins, spuntandole, cliccando sull'apposito comando. A la fin, clicca _Send_.

![img](https://officinebitcoin.it/lezioni/coinco/36.webp)

Bitcoin Keeper te porta direttamente al menu _Send_, dove te poi costruire la transazion co i UTXO selezionati.

![img](https://officinebitcoin.it/lezioni/coinco/37.webp)

## Hardware wallet
Ognuno dei software wallet visti in sta guida può essere l'interfaccia watch-only de un tuo hardware wallet. Significa el coin control par dispositivo de firma offline si esegue co i passaggi visti fin qui.

## Raccomandazioni generali
El coin control xe na pratica tanto efficace par selezionare i input de le to transazion. La selezion manuale xe ancor più efficiente se, in fase de acquisto/ricezione dei to fondi, hai etichettato ben la provenienza dei to satoshi. Se desideri imparare ben sta tecnica, te consiglio el tutorial:

https://planb.network/tutorials/privacy/on-chain/utxo-labelling-d997f80f-8a96-45b5-8a4e-a3e1b7788c52
