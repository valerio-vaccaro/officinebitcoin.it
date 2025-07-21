---
name: Capì el Controll Manual de le Moned
description: Guida completa a la selezion manual de UTXO. Capiss perchè l'è important e impara a fàll con vari wallet software (desktop e mobile)
---
![cover](https://officinebitcoin.it/lezioni/coinco/cover.webp)

# Introduzion
La robustezza del protocoll Bitcoin l'è garantita da concett core sempliz. Tra questi, la trasparenza se disting: tutt le transazion Bitcoin hinn pubbliche e facilment verificabil da chiunque. Menter questa caratteristica l'è una pietra angolar del protocoll, poiché previen frod e assicura l'autenticità de le fond, la pö anca presentà una sfida per la confidenzialità. **Te hè mai domandat se tanta trasparenza pö influenzà la tua privacy?**

Te dovriess. Menter accumulà satoshi non-KYC l'è assai sempliz, la tua privacy l'è pù a risch durant la fase de spesa.

## Cossa succed quand te spend un UTXO
Spend Bitcoin minga l'è semplizment trasferì valor a qualchun alter.

Consumand un de i tò UTXO, te devi soddisfà le condizion impost per la trasparenza del protocoll, poiché te devi provà la proprietà de quei fond. Te devi quindi:
- espon la tua claav pubblica;
- produc una firma digital.

El moment de la spesa l'è quindi el pù critic: **spend bitcoin l'è un att da fà consciament e con el massim controll possibil**.

# Coin Control
Nel protocoll Bitcoin, element come "account" o "unità monetaria" minga esist. El concett de UTXO minga l'è el focus de questa lezion, ma te inviti a fà domand al tuo Satoshi Spritz fidà o richied una lezion qui su Officine Bitcoin.
Quell che te devi savè l'è che con Bitcoin, quell che te accumul e poi spend hinn piccol o grand unità contabil misurad in satoshi, rappresentad da `unspent transaction outputs`, i **UTXO**, ciamad anca `moned`.
Quand te dopri UTXO per creà una transazion, vegnen completament distrutt e noeuv UTXO vegnen cread in la so posizion.

I wallet software hinn sviluppad per fà questa scelta automaticament, doprand moned selezionad "a cas" con l'unic criterio de coprì l'import de spesa richiest.

`Coin Control`, ciamad anca `Coin Selection`, l'è una funzionalità de qualch wallet software che te permet de **selezionà manualment i UTXO da spend quand costruiss la tua transazion**.

Suppon che te gh'hee un wallet con 3 UTXO, rispettivament 21,000, 42,000, e 63,000 satoshi.

![img](https://officinebitcoin.it/lezioni/coinco/01.webp)

Se te gh'hee besogn de spend 24,000 sats e lassi che el software selezioni automaticament, un bon wallet podaria scegli de combinà UTXO1 + UTXO2 per pagà i 24k sats e le fee de miner, creand un change che torna a un indirizz intern del wallet originari.

![img](https://officinebitcoin.it/lezioni/coinco/02.webp)

Dopo la transazion, la noeuva situazion nel wallet, contand domà i UTXO, pö vess riassunta come seguiss.

![img](https://officinebitcoin.it/lezioni/coinco/03.webp)

Con el software giust e la tua consapevolezza, però, te podariess avè fà una scelta diversa e pù corretta. Per esempi, selezionand domà UTXO2 (42,000 sats).

![img](https://officinebitcoin.it/lezioni/coinco/04.webp)

Con una situazion final de UTXO nel tuo wallet che la guarda diversa.

![img](https://officinebitcoin.it/lezioni/coinco/05.webp)

# Perchè selezionà manualment i UTXO?
![img](https://officinebitcoin.it/lezioni/coinco/06.webp)

Nel nost esempi, el saldo l'è in realtà el stess: `108,280 sats`. Dopo spend 24,000 sats, sensa coin control avriess 2 UTXO nel wallet; con controll manual de moned avess 3 in total.

**Perchè fà tutt quest?**

Hinn, o podarien vess, divers motiv per cui minga hann doprà `UTXO1` **e hinn tutt alla radice del perchè - quand spend - attivà el controll manual de moned l'è una bon pratica da seguì**.

## Privacy
El vantagg principal, quand se parla de selezion manual de moned, l'è **maggior privacy per chi spend**.

Pigliem el nost esempi de noeuv: spend 24,000 satoshi _sensa coin control_. Poiché la blockchain Bitcoin l'è un registro pubblic, un osservator estern pö affermà, sensa dubbi, che i input `UTXO1 de 21,000 sats` e `UTXO2 de 42,000 sats`, come anca el change, `UTXO5 de 38,280 sats` **tutt appartegnen al stess utent**.

Selezionand manualment `UTXO2`, invece, `UTXO1` resta completament privat, sedend nel set UTXO aspettand de vess spess a un temp pù approprià.

`UTXO1` podaria vegnì de una fonte KYC, per esempi un pagament ricevuu per beni e servizzi, menter i alter UTXO minga.

**Se l'è stada la tua wallet, te vorriess che un osservator estern pössa traccià la tua identità con tanta certezza?** I wallet che implementen selezion manual de UTXO permetten, per esempi, la **segregazion de un o pù UTXO**, una funzion da doprà quand situazion del genere sörgen.

Anche se credo che fond KYC dovriessen vess tenuu in un wallet separà da bitcoin non-KYC, se questa l'è la tua situazion, segregà qualch de i tò indirizz l'è un aiut fondamental, che te podariess otten imparand a selezionà manualment i tò input de spesa.

## Risparmi de fee
Selezionà l'UTXO corrett per una spesa te permet de ottimizzà le fee. De noeuv, nel nost esempi, el wallet software ha selezionà do UTXO per coprì la spesa. Do UTXO significan do firm per mostrà la ret, quindi un pes de transazion pù alt in termin de vBytes.

Doprand controll manual de moned, te pödet selezionà domà un che basta per coprì l'import, risparmiand fee poiché el "pes" de la transazion diminuiss.

Quand le fee hinn alt, ma te sei forzà a spend bitcoin on-chain (es. per aprì un canàl Lightning Network), el coin control deventa l'incentiv economic giust da doprà.

## Aggregazion de change
Quand fà un pagament e doprà Bitcoin on-chain, la possibilità de ricev change deventa quasi semper una certezza. Ogni change l'è de per sè una piccola perdita de privacy, poiché la rivela alla ret un de i tò indirizz che pö vess associà al tuo input originari.

Considerand che i miglior wallet HD generen indirizz special per change, te pödet facilment recognossli e "segregà" tutt el change de vari transazion; quand questi raggiungen un cert import te pödet selezionà manualment e consolidàli, o scambiàli sulla Lightning Network (el metòd che preferiss) per riguadagnà la privacy perduda durant la spesa.

## Spesa de un wallet fredd
Un wallet fredd l'è un strument con cui te pödet ragionevolment raggiung un bon gradi de sicurezza, per conservà qualsivoglia import de fond da tenì da part per un long temp. Tuttavia, event imprevist podarien succed, richiedend de acced ai tò risparmi e coprì spes imprevist.

El mio consigli l'è **mai spend direttament de un wallet fredd, per evità de ricev change tra i stess indirizz del wallet**. Impara a selezionà manualment i UTXO necessari per coprì la spesa, trasferissli a un wallet cald, e prepara la tua transazion de là. Qualsivoglia change, allora, te pödet invià de noeuv a un indirizz de wallet fredd (se l'import l'è approprià), o dopràll per alter scop.

# Dimostrazion pratica
Dopo questa longa introduzion, vedem come mett el coin control in pratica con vari software desktop e mobile. Doprarass semper el stess wallet HD, importà in ognun de i strument scelt, per mostrà le piccole differenz tra questi.

# Wallet Desktop

## Sparrow
Se te dopri Sparrow, vèrt el tuo wallet e seleziona _UTXOs_ dal menu de sinistra. Vedarass la lista de tutt i UTXO associad al tuo wallet.

Semplizment clicca su un e poi scegli _Send Selected_. Sparrow te mostra anca el total selezionà per spesa, accant al comand.

![img](https://officinebitcoin.it/lezioni/coinco/07.webp)

Te pödet anca selezionà pù de un. Dopera la claav _CTRL_ per selezionà UTXO non adiacend nella lista.

![img](https://officinebitcoin.it/lezioni/coinco/08.webp)

Dopo aver selezionà manualment i UTXO, Sparrow te mostrarà chiarament, graficament, come la tua transazion l'è costruida, che te pödet finalizzà e completà.

![img](https://officinebitcoin.it/lezioni/coinco/09.webp)

### Segregazion UTXO
Segregà fond significà "bloccàli" denter el wallet così che minga poden vess doprad come input de transazion.

Sparrow permet questa funzionalità, accessibil dal menu _UTXOs_. Passa sopra l'UTXO da "bloccà" e clicca de destra. Tra le opzion, trovarass _Freeze_. Quest l'è come te pödet segregà un UTXO con Sparrow Wallet.

![img](https://officinebitcoin.it/lezioni/coinco/29.webp)

## Electrum
Se el tuo wallet desktop l'è Electrum, te pödet selezionà manualment UTXO sia dal menu _Addresses_ che _Coins_.
In entramb i menu, la selezion se fà puntand el mouse sull'UTXO e scegliend _Add to coin control_ dopo aver cliccà de destra.

![img](https://officinebitcoin.it/lezioni/coinco/10.webp)

Te pödet anca selezionà pù de un UTXO, doprand la claav _CTRL_ se minga hinn adiacend.

![img](https://officinebitcoin.it/lezioni/coinco/11.webp)

Electrum evidenziarà graficament i UTXO selezionad in verd, e in bass, una barra evidenziada del stess color mostra el saldo disponibil dopo coin control.

![img](https://officinebitcoin.it/lezioni/coinco/12.webp)

Una volta che l'output (o i output) hinn selezionad, te pödet costruì la tua transazion come al solit dal menu _Send_.

### Segregazion UTXO
Electrum fornis questa opzion nel menu _Coins_ selezionand un UTXO specific e poi scegliend _Freeze_ con el botton de destra del mouse. Te pödet anca "bloccà" un indirizz sensa fond dal menu _Addresses_, o la "moneda" per evità spesa.

![img](https://officinebitcoin.it/lezioni/coinco/28.webp)

## Nunchuk
Nunchuk te permet de selezionà UTXO dal menu principal una volta vèrt.
Lancia Nunchuk e clicca _View coins_.

![img](https://officinebitcoin.it/lezioni/coinco/13.webp)

Se vèrt una finestra con tutt i UTXO del tuo wallet, dove te pödet selezionà un o pù spuntand la casella accant a ogni import. Dopo la selezion, continua con _Create transaction_.

![img](https://officinebitcoin.it/lezioni/coinco/14.webp)

Poi te pödet inserì l'indirizz de destinazion, impostà l'import e le fee.

![img](https://officinebitcoin.it/lezioni/coinco/15.webp)

## Blockstream App
Blockstream App desktop, precedentement ciamad Green, permet selezion de moned una volta che te hè iniziat a costruì la transazion. Vèrt el tuo wallet e clicca _Send_.

![img](https://officinebitcoin.it/lezioni/coinco/16.webp)

Incolla l'indirizz de destinazion nel camp approprià e poi seleziona _Manual coin selection_.
![img](https://officinebitcoin.it/lezioni/coinco/17.webp)
Se vèrt una finestra dove te pödet selezionà un o pù UTXO. Nel seguent esempi, hann selezionà do moned. Poi conferma la scelta cliccand _Confirm Coin Selection_.

![img](https://officinebitcoin.it/lezioni/coinco/18.webp)

Imposta l'import e le fee, poi procedi come al solit con la tua transazion.

![img](https://officinebitcoin.it/lezioni/coinco/19.webp)

⚠️ Nota: Nel menu _Coins_ de Green, hinn opzion _Lock_/_Unlock_ che suggerissen la possibilità de segregà UTXO. Quest l'è domà disponibil in cosiddett account multisig; la funzionalità l'è domà attivada per UTXO molt piccol, vicin al soglia `Dust`.

# Wallet Mobile

## Blue Wallet
Anca su mobile, te pödet scegli wallet che permeten selezion manual de UTXO. Guardem Blue Wallet prima.

Se te dopri questo software, vèrt el tuo wallet e clicca per entrà nelle schermate de comand per un de i tò wallet. Per acced al coin control, te devi entrà nella fase de spesa, quindi clicca _Send_.

![img](https://officinebitcoin.it/lezioni/coinco/21.webp)

Nella prossima schermata, scegli el menu indicà dai tre punt in alt a destra. Se vèrt una finestra a tendina con divers comand. Scegli l'ultim: _Coin Control_.

![img](https://officinebitcoin.it/lezioni/coinco/22.webp)

A quest punt, Blue Wallet mostra tutt i tò UTXO. Oltra agli import, vegnen differenzad graficament da color divers.

![img](https://officinebitcoin.it/lezioni/coinco/27.webp)

Seleziona l'UTXO, poi seleziona _Use Coin_.

![img](https://officinebitcoin.it/lezioni/coinco/23.webp)

Blue Wallet te porta de noeuv alla finestra _Send_ per continuà a costruì la transazion. Aggiusta l'import e le fee, poi scegli _Next_.

![img](https://officinebitcoin.it/lezioni/coinco/24.webp)

Ora te pödet completà la transazion come al solit.

### Segregazion UTXO
Blue Wallet permet anca de segregà UTXO, rendendli non disponibil per spesa, che l'è una bella funzionalità per un wallet mobile.

Acced al coin control come spiegà sopra e, dopo aver selezionà l'UTXO, scegli _Freeze_ invece de _Use Coin_.

![img](https://officinebitcoin.it/lezioni/coinco/26.webp)

## Nunchuk
La version mobile de Nunchuk permet anca agli utent de fà coin control. Se te dopri questa app su mobile, vèrtla e va al menu _Wallet_. De qui, scegli _View coins_.

![img](https://officinebitcoin.it/lezioni/coinco/30.webp)

Nella finestra con la lista de UTXO, clicca _Select_.

![img](https://officinebitcoin.it/lezioni/coinco/38.webp)

Accant a ogni UTXO, appare la funzion de selezion. Come nella version desktop, su Nunchuk mobile, la selezion manual se fà spuntand la casella accant all'import. La schermata mostra el numer de UTXO selezionad e l'import total disponibil. Una volta finida, el simbol ₿ in bass a sinistra l'è el comand per inizià a costruì la transazion.

![img](https://officinebitcoin.it/lezioni/coinco/31.webp)

Ora te pödet completà la transazion, scegliend l'import e cliccand _Continue_.

![img](https://officinebitcoin.it/lezioni/coinco/32.webp)

Continua come al solit, incolland un indirizz de destinazion, una descrizion, e personalizzand le impostazion de fee.

## Bitcoin Keeper
Bitcoin Keeper l'è l'ultim wallet che vedarass in questa guida. Vedem la so funzionalità de coin control con un wallet single-sig, anche se un us del genere minga l'è el scop principal de questa app particolar.

Dopo aver configurà Keeper sul tuo telefon, lancial e vèrt un wallet che contien qualch UTXO. Al center de la schermata principal, clicca _View All Coins_.

![img](https://officinebitcoin.it/lezioni/coinco/34.webp)

Keeper mostra una panoramica de le UTXO. Per acced alla schermata de selezion, clicca _Select To Control_.

![img](https://officinebitcoin.it/lezioni/coinco/35.webp)

Te pödet selezionà moned spuntandle, cliccand el comand approprià. Quand l'è fata, clicca _Send_.

![img](https://officinebitcoin.it/lezioni/coinco/36.webp)

Bitcoin Keeper te porta direttament al menu _Send_, dove te pödet costruì la transazion con i UTXO selezionad.

![img](https://officinebitcoin.it/lezioni/coinco/37.webp)

# Hardware wallet
Ognun de i wallet software vedud in questa guida pö vess l'interfaccia watch-only per el tuo hardware wallet. Quest significà che el coin control per un dispositiv de firm offline se fà con i pass vedud finora.

## Raccomandazion general
El coin control l'è una pratica molt efficace per selezionà i tò input de transazion. La selezion manual l'è anca pù efficient se, quand ricev i tò fond, te hè ben etichettà l'origin de i tò satoshi. Se te vöret padroneggià questa tecnica, raccomandi el tutorial:

https://planb.network/tutorials/privacy/on-chain/utxo-labelling-d997f80f-8a96-45b5-8a4e-a3e1b7788c52 