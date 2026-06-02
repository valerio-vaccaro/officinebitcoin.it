---
layout: default
name: "Capì el Coin Control manual"
description: "Guida completa a la selezion manual de UTXO. Capì perchè l'è important e imparà come fàll con divers software wallet (desktop e mobile)"
title: "Capì el Coin Control manual"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lezion Bitcoin-only</span> <span>Quest progett l'e mantegnuu da valerio-vaccaro</span></p>

## 🌍 Traduzion

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](https://officinebitcoin.it/lezioni/coinco/cover.webp)

# Capì el Coin Control manual

## Introduzion

La solidità del protocollo Bitcoin l'è garantita da concetti cardine semplici. Tra questi, spicca la trasparenza: tutte i transazion Bitcoin hinn pubbliche e facilmente verificabili da chiunque. Sebbene questa caratteristica sia ona pietra miliare del protocollo, perché previene frodi e garantisce la genuinità di fond, può rappresentare anca ona sfida per la confidenzialità. **Te sei domandato se tanta trasparenza può inficiare la tua privacy?

Dovresti farlo. Se da ona parte accumulare satoshi minga-kyc l'è piuttosto sempliz, la tua privacy l'è maggiormente a rischio proprio nella fase si spesa.
## Cosa succede quand spendi on UTXO
Spendere Bitcoin minga l'è semplizmente el trasferimento de valore a qualcun altro. 

Consumando uno di tò UTXO, infatti, te gh'heet de soddisfare i condizion imposte per la trasparenza del protocollo, perché te gh'heet de dimostrare de essere el proprietario de quei fond. Devi pertanto:
- esporre la tua chiave pubblica;
- produrre ona firma digitale.

El momento de la spesa l'è dunque el più critico: **spend bitcoin l'è on atto da compiere in maniera consapevole e con el maggior controllo possibile**.

## Coin Control
Nel protocollo Bitcoin, elementi come "_conto_" o "_unità monetarie_" minga esistono. El concetto de UTXO minga fa parte di scopi de questa lezion, ma te invito a fare i domande relative al tuo satoshi spritz de fiducia, o a richiedere ona lezion qui su Officine Bitcoin.
Ciò che te gh'heet de sapere l'è che con Bitcoin ciò che accumuli e, in seguito spenderai, hinn piccole o grandi unità de conto misurate in satoshi, rappresentati da `output di transazione non spesi`, i **UTXO**, detti anca `coins`.
Quand si utilizzano UTXO per creare ona transazion, questi vengono completamente distrutti e si creano altri UTXO al loro posto.

I software wallet hinn sviluppati per fare questa scelta in maniera automatica, utilizzando coins selezionate in maniera "casuale" con l'unico criterio de coprire l'importo necessario a la spesa.

El `Coin Control`, che te pödet trovare anca denominato `Coin Selection`, l'è ona funzion caratteristica de alcuni software wallet, che te permette de **selezionare manualmente i UTXO da spend quand costruisci la tua transazion**.

Supponiamo de avere on wallet con 3 UTXO, rispettivamente da 21.000, 42.000 e 63.000 satoshi.

![img](https://officinebitcoin.it/lezioni/coinco/01.webp)

Se te gh'heet de spend 24.000 sats e lasci fare al software la selezion automatica, on buon wallet potrebbe sernissere de combinare l'UTXO1 + l'UTXO2 per pagare i 24k sats e i fee del miner, creando on resto che torna su on indirizzo interno del wallet de partenza.

![img](https://officinebitcoin.it/lezioni/coinco/02.webp)

Dopo la transazion la nuova situazion nel wallet, contando domà i UTXO, si può così riassumere.

![img](https://officinebitcoin.it/lezioni/coinco/03.webp)

Con el giusto software e la tua consapevolezza, invece, avresti potuto compiere ona scelta diversa e più corretta. Ad esempio selezionando domà l'UTXO2 (da 42.000 sats).

![img](https://officinebitcoin.it/lezioni/coinco/04.webp)

Con ona situazion finale, a livello de UTXO, nel tuo wallet che ha on aspetto differente.

![img](https://officinebitcoin.it/lezioni/coinco/05.webp)

## Perché selezionare manualmente i UTXO?
![img](https://officinebitcoin.it/lezioni/coinco/06.webp)

Nel nostro esempio, el saldo de fatto el stesso: `108.280 sats`. Dopo la spesa de 24.000 sats, senza coin control avremmo 2 UTXO nel wallet; con el coin control manuale ne abbiamo 3 totali.

**Perché fare tutto quest?**

Ci hinn, o potrebbero esserci, diversi motivi per cui minga abbiamo usato l'`UTXO1` **e hinn tutti a la base del perché - in fase de spesa - attivare el coin control manuale l'è ona di buone pratiche da seguire**.

## Privacy
El vantaggio principale, quand si parla de manual coin selection, l'è ona **maggiore privacy per chi spende**.

Prendiamo semper el nostro esempio: la spesa de 24.000 satoshi _senza coin control_. Essendo la blockchain de Bitcoin on registro pubblico, on osservatore esterno può dichiarare, senza ombra de dubbio, che i input `UTXO1 di 21.000 sats` e `UTXO2 di 42.000 sats`, nonché el resto, l'`UTXO5 da 38.280 sats` **appartengono tutti e tre allo stesso utent**.

Selezionando manualmente l'`UTXO2`, invece, rimane completamente riservato l'`UTXO1`, fermo nell'UTXO set in attesa de essere speso in on momento più appropriato.

L'`UTXO1` potrebbe provenire da ona fonte KYC, ad esempio on pagament ricevuto in cambio de beni e servizi, mentre i altri UTXO no.

**Se fosse el tò wallet, vorresti che on osservatore esterno possa risalire a la tua identità con ona certezza così assoluta?** I wallet che implementano la selezion manuale di UTXO, permettono ad esempio la **segregazion de uno o più UTXO**, ona funzion da doprà quand si presentano situazion de quest tipo.

Sebbene io sia convinta che fond KYC dovrebbero essere conservati in on wallet separato rispetto a bitcoin acquistati senza kyc, se quest l'è el tuo caso la segregazion de alcuni tò indirizzi l'è on aiuto fondamentale, che potresti ricevere imparando a selezionare manualmente i tò input de spesa.

## Risparmio sulle fee
Selezionare l'UTXO corretto per effettuare ona spesa consente de ottimizzare i fee. Semper partendo dal nostro esempio, el software wallet ha selezionato due UTXO per coprire la la spesa da fare. Due UTXO implicano due firme da mostrare a la rete, donca on peso maggiore de la transazion stessa in termini de vByte.

Usando el coin control manuale, invece, te pödet selezionarne uno domà che sia sufficiente a coprire l'importo, risparmiando fee perché diminuisce el "peso" de la transazion.

In periodi in cui i fee hinn alte, ma sei costretto a spend bitcoin on-chain (ad esempio per aprire on canale Lightning Network), ecco che el coin control si rivela el giusto incentivo economico a cui ricorrere.

## Aggregazion di resti
Quand si fa on pagament e si usano Bitcoin on-chain, la possibilità de ricevere on resto diventa quasi semper ona certezza. Ogni resto l'è de per sé ona piccola perdita de privacy, in quanto svela a la rete on tuo indirizzo che si può associare al tuo input de partenza.

Considerando che i migliori wallet HD generano di indirizzi appositi per i resti, te pödet riconoscerli facilmente e "segregare" tutti i resti di varie transazion effettuate; quand questi hanno raggiunto on certo importo te pödet selezionarli manualmente e consolidarli, o fare swap su Lightning Network (el mio metodo preferito) e trattarli così da riguadagnare la privacy perduta in fase de spesa.

## Spesa da on cold wallet
El cold wallet l'è uno strument con cui si può ragionevolmente ottenere on buon grado de sicurezza, per conservà ona qualsiasi quantità de fond da tenere da parte per on lungo periodo de tempo. Possono però capitare di imprevisti, in cui l'è necessario mettere mano ai risparmi e far fronte a qualche spesa inaspettata.

El mio consiglio l'è quello de **minga effettuare mai la spesa direttamente dal cold wallet, per evitare de ricevere el resto tra i indirizzi dello stesso**. Impara a selezionare manualmente i UTXO necessari a coprire la spesa, trasferiscili su on wallet hot e prepara la tua transazion da quest'ultimo. L'eventuale resto, poi, potrai rimandarlo su on indirizzo del cold wallet (se l'importo l'è adeguato), oppur utilizzarlo per altri scopi.

## Presentazion pratica
Dopo questa lunga introduzion, vediamo come mettere in pratica el coin control con diversi software desktop e mobile. Useremo semper el stesso wallet HD, importato in ognuno di strument scelti, in modo da mostrarti i piccole differenze che ci hinn tra de loro.

## Wallet Desktop

## Sparrow
Se usi Sparrow, apri el tò wallet e seleziona _UTXOs_ dal menu a sinistra. Te comparirà la lista di tutti i UTXO associad al tuo wallet.

Clicca semplizmente con el mouse su uno de loro e poi serniss _Send Selected_. Sparrow te mostra anca el totale selezionato per la spesa, accanto al comando.

![img](https://officinebitcoin.it/lezioni/coinco/07.webp)

Puoi anca selezionarne più de uno. Aiutati con el tasto _CTRL_ per selezionare UTXO minga adiacenti nella lista.

![img](https://officinebitcoin.it/lezioni/coinco/08.webp)

Dopo aver selezionato manualmente i UTXO, Sparrow te mostrerà ben, graficamente, come l'è costruita la tua transazion, che te pödet finalizzare e concludere.

![img](https://officinebitcoin.it/lezioni/coinco/09.webp)

### Segregazion dell'UTXO
Segregare di fond significa "bloccarli" all'interno del wallet, affinché minga possano essere usati come input de ona transazion. 

Sparrow permette questa funzionalità, cui si accede semper dal menu _UTXOs_. Si posiziona el mouse sull'UTXO da "bloccare" e si clicca el tasto destro del mouse. Tra i funzionalità de questa procedura comparirà el comando _Freeze_. L'è così che potrai segregare on UTXO con Sparrow Wallet.

![img](https://officinebitcoin.it/lezioni/coinco/29.webp)

## Electrum
Se el tò wallet desktop l'è Electrum, te gh'heet de sapere che te pödet selezionare manualmente i UTXO sia dal menu _Addresses_ sia dal menu _Coins_.
In entrambi i menu la selezion avviene puntando el mouse sull'UTXO da sernissere e sernissendo _Add to coin control_ dopo aver cliccato el tasto destro.

![img](https://officinebitcoin.it/lezioni/coinco/10.webp)

Anca con quest software te pödet selezionare più de on UTXO, aiutandoti con el tasto _CTRL_ de la tastiera se minga hinn adiacenti tra loro.

![img](https://officinebitcoin.it/lezioni/coinco/11.webp)

Graficamente Electrum te mostrerà la selezion evidenziando in verde i UTXO selezionati, mentre in basso te compare ona barra, evidenziata dello stesso colore, che mostra el saldo disponibile dopo el coin control.

![img](https://officinebitcoin.it/lezioni/coinco/12.webp)

Ona volta selezionato l'output o i output, te pödet costruire la tua transazion come semper, dal menu _Send_.

### Segregazion dell'UTXO
Electrum mette a disposizion questa possibilità, andando nel menu _Coins_ e selezionando on determinato UTXO e poi sernissendo _Freeze_ con el tasto destro del mouse. Si può "freezare" l'indirizzo anca senza fond dal menu _Addresses_, oppur la "coin" per minga spenderla.

![img](https://officinebitcoin.it/lezioni/coinco/28.webp)

## Nunchuk
Nunchuk permette de selezionare i UTXO dal menu principale, ona volta aperto.
Lancia Nunchuk e clicca _View coins_.

![img](https://officinebitcoin.it/lezioni/coinco/13.webp)

Si apre la finestra che contiene tutti i UTXO del tò wallet, indoe te pödet selezionarne uno o più, attivando la spunta accanto ad ogni importo. Dopo aver effettuato la selezion, continua con _Create transaction_.

![img](https://officinebitcoin.it/lezioni/coinco/14.webp)

Dopodiché potrai inserire l'indirizzo de destinazion e impostare l'importo e i fee.

![img](https://officinebitcoin.it/lezioni/coinco/15.webp)

## Blockstream App
Blockstream App desktop, già conossuto come Green, permette de fare coin selection quand si l'è già iniziata a costruire la transazion. Apri pertanto el tò wallet e clicca su _Send_.

![img](https://officinebitcoin.it/lezioni/coinco/16.webp)

Incolla l'indirizzo de destinazion nel campo apposito e poi seleziona _Manual coin selection_.
![img](https://officinebitcoin.it/lezioni/coinco/17.webp)
Si apre la finestra indoe te pödet selezionare uno o più UTXO. Nell'esempio che segue, abbiamo selezionato due coins. Dopodiché conferma la scelta cliccando su _Confirm Coin Selection_.

![img](https://officinebitcoin.it/lezioni/coinco/18.webp)

Imposta l'importo e i fee e poi procedi normalmente con la tua transazion.

![img](https://officinebitcoin.it/lezioni/coinco/19.webp)

⚠️ N.B. Nel menu _Coins_ de Green hinn presenti i voci _Lock_/_Unlock_ che prefigurano la possibilità de segregare UTXO. Questa possibilità l'è presente domà negli account cosiddetti multisig; inoltre la funzionalità si attiva domà selezionando UTXO de importo assai piccolo, vicino a la soglia del `Dust`.

## Wallet mobile

## Blue Wallet
Anca da mobile l'è possibile sernissere wallet che permettono de selezionare manualmente i UTXO. Vediamo per primo Blue Wallet.

Se sei on utent de quest software, apri el tò wallet e clicca per entrare nelle schermate di comandi relativi ad uno di tò wallet. Per accedere al coin control si deve entrare nella fase de spesa, donca clicca _Send_.

![img](https://officinebitcoin.it/lezioni/coinco/21.webp)

Nella successiva schermata serniss i menu segnalati dai tre pallini in alto a destra. Si apre ona finestra a tendina con ona serie de comandi. Scegli l'ultimo: _Coin Control_.

![img](https://officinebitcoin.it/lezioni/coinco/22.webp)

A quest punto Blue Wallet mostra tutti i tò UTXO. Oltre che dagli importi, hinn differenziati graficamente da colori diversi.

![img](https://officinebitcoin.it/lezioni/coinco/27.webp)

Scegli l'UTXO da selezionare dopodiché seleziona _Use Coin_.

![img](https://officinebitcoin.it/lezioni/coinco/23.webp)

Blue Wallet te riporta nella finestra de _Send_ per continuare a costruire la transazion. Aggiusta l'importo e i fee, dopodiché serniss _Next_.

![img](https://officinebitcoin.it/lezioni/coinco/24.webp)

A quest punto te pödet terminare la transazion, come fai de solito.

### Segregazion de on UTXO
Anca Blue Wallet permette de segregare i UTXO, rendendoli minga disponibili per la spesa, el che minga l'è male come funzion per on wallet da dispositivo mobile.

Si accede al coin control con la procedura appena spiegata e, dopo aver selezionato l'UTXO, serniss _Freeze_ al posto de _Use Coin_.

![img](https://officinebitcoin.it/lezioni/coinco/26.webp)

## Nunchuk
Anca la version mobile de Nunchuk prevede la possibilità per l'utent de effettuare el coin control. Se usi questa app da mobile, aprilo e vai nel menu _Wallet_. Da qui serniss _View coins_.

![img](https://officinebitcoin.it/lezioni/coinco/30.webp)

Nella finestra indoe compare la lista di UTXO clicca _Select_.

![img](https://officinebitcoin.it/lezioni/coinco/38.webp)

Accanto ad ogni UTXO appare la funzion de selezion. Come nella version desktop, anca su Nunchuk mobile la selezion manuale avviene spuntando el quadratino accanto all'importo. La schermata riporta el numero de UTXO selezionati e l'importo totale a disposizion. Ona volta finito, el simbolo ₿ in basso a sinistra, che l'è el comando per inizià a costruire la transazion.

![img](https://officinebitcoin.it/lezioni/coinco/31.webp)

Ora te pödet completare la transazion, sernissendo l'importo e cliccando su _Continue_.

![img](https://officinebitcoin.it/lezioni/coinco/32.webp)

Continua come fai semper, incollando on indirizzo de destinazion, ona descrizion e personalizzando i impostazion di fee.

## Bitcoin Keeper
Bitcoin Keeper l'è l'ultimo wallet che vedremo in questa guida. Vediamo la sua funzionalità applicata al coin control con on wallet single-sig, anca se on tale 'uso  minga l'è el scopo de questa app assai particolare.

Dopo aver impostato Keeper sul tò telefon, lancialo e apri on wallet contenente alcuni UTXO. Al centro de la schermata principale clicca _View All Coins_.

![img](https://officinebitcoin.it/lezioni/coinco/34.webp)

Keeper mostra ona panoramica di UTXO. Per accedere a la schermata de selezion clicca _Select To Control_.

![img](https://officinebitcoin.it/lezioni/coinco/35.webp)

Puoi selezionare i coins, spuntandole, cliccando sull'apposito comando. A la fin, clicca _Send_.

![img](https://officinebitcoin.it/lezioni/coinco/36.webp)

Bitcoin Keeper te porta direttamente al menu _Send_, indoe te pödet costruire la transazion con i UTXO selezionati.

![img](https://officinebitcoin.it/lezioni/coinco/37.webp)

## Hardware wallet
Ognuno di software wallet visti in questa guida può essere l'interfaccia watch-only de on tuo hardware wallet. Significa el coin control per dispositivo de firma offline si esegue con i passaggi visti fin qui.

## Raccomandazion generali
El coin control l'è ona pratica assai efficace per selezionare i input deli tò transazion. La selezion manuale l'è ancor più efficiente se, in fase de acquisto/ricezion di tò fond, hai etichettato ben la provenienza di tò satoshi. Se desideri imparare ben questa tecnica, te consiglio el tutorial:

https://planb.network/tutorials/privacy/on-chain/utxo-labelling-d997f80f-8a96-45b5-8a4e-a3e1b7788c52
