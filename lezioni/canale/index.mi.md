![cover](https://officinebitcoin.it/lezioni/canale/01cover.webp)

# Lightning Network non-custodial
Phoenix de Acinq l'è un wallet nativ lightning network, non custodial, che el ofr un wallet basad su standard BIP39 efficient, ben conness e che el lassa el complet controll ai utent.

Te scoprirar tra poc che Phoenix el vèrt un canale LN, del cui bilanciament te see responsabil al 100%.
Par lavorà ben con Phoenix, l'è necessaria domà na minima attenziù e la conossenza base de la red Lightning. Te impararà ad esempi a tèg sota controll la liquidità del tò canale, a tègll bilanciad a seconda de le tò necessità e a fà in mod che Acinq te veda online, par tègll vert e curà l'infrastruttura LN.

# Operaziù base
Dopo avè [scaricà e verificà l'apk de Phoenix](https://officinebitcoin.it/lezioni/verifica/index.html), te pödet installà l'app sul telefon.

Phoenix el se vèrt domandandet se te voeuret creà un noeuv wallet o ripristinarn vun precedent. Se te see a la tua prima esperienza con Phoenix scern `Create new wallet`. Seguiran na serie de schermad de benvenù, che se concluden par scomenzà indove te premarar `Get started`.

![img](https://officinebitcoin.it/lezioni/canale/03.webp)

## Backup
Vuna volta vert Phoenix, **la prima operaziù da fà l'è - come semper - el backup del wallet**.

Phoenix el dopra lo standard BIP39, derivation path m/84'/0'/0', fornend una sequenza de 12 parol da trascriver su support cartacee e conservà in un loeugh sicur.

![img](https://officinebitcoin.it/lezioni/canale/04.webp)

Entra in del menu e domanda a Phoenix de mostrart la *Recovery phrase*, cliccand su `Display seed`.

![img](https://officinebitcoin.it/lezioni/canale/05.webp)

A la fin ricorda de scorrer la schermada fin in fond, vers el bass, par confermà de avè eseguì el backup e minga vedè pù la notifica e l'alert.

![img](https://officinebitcoin.it/lezioni/canale/06.webp)

Phoenix l'è sostanzialment pront par vess doprà. El tò noeuv wallet el gh'ha el saldo pari a zero e el pö vess configurad. In bass a manca te trovet el comand par entrar de noeuv in del settings e impostà voci utili par l'us quotidian.

![img](https://officinebitcoin.it/lezioni/canale/07.webp)

## Us con Tor
Già de diverse version de Phoenix, Acinq l'ha disabilità la possibilità del motor Tor intern. Se te voeuret doprà Phoenix con la proteziù Tor, saran necessari 2 accorgiment:
- abilita Tor in del impostaziù de Phoenix
- dopra na app terza par instradà el traffic del wallet sota red onion.

Acced ai settings e scern Tor, poeu abilita `Enable Tor`, in fin instrada el traffic grazia a l'app che te dopret de solit (Orbot, Invizible Pro ecc). Sensa vuna de quest app terz, ma con Tor abilitad in del settings de Phoenix, el wallet el riuscirà minga a connett a internet.

![img](https://officinebitcoin.it/lezioni/canale/09.webp)

## Alter impostaziù
Te pödet cambià e/o impostà na serie de funziù:
- el nom del wallet, cliccand su la parol `Wallet` in alt;
- la valuta de riferiment dal sot menu `Display`.
- impostà le fee in `Channel management`, impostaziù important perché un valor tròpp bass de fee el pö pregiudicà l'apertura del canale: de default l'è impostad a 5.000 sats, portall a 15.000, Phoenix el doprarà comunque el valor adeguad al moment;
- te dovress impostà tutt le precauziù de sicurezza che te te sentet de podè gestì, in del sot menu `Access control`: PIN par spend, PIN o controll biometric par l'access a l'App;
- impostà un tò `Electrum server` in del menu nominad come tal, prestand attenziù che Phoenix el richied un certificad SSL valid (Let's Encrypt, ad esempi);
- attivà le `Experimental features` par richied un LN address Bolt12 riutilizzabil
- gestì eventual chiusur del canale o la creaziù/cancellaziù de pù wallet.

![img](https://officinebitcoin.it/lezioni/canale/08.webp)

# Apertura canale LN ⚡️

De la schermada principal de Phoenix, scern el comand `Receive`

![img](https://officinebitcoin.it/lezioni/canale/10.webp)

El wallet te propòn dò modalità de riceziù, tutt e dò con QRcode: Lightning e Onchain.

## Pagament de na invoice Lightning

![img](https://officinebitcoin.it/lezioni/canale/11.webp)

Un metood veloce par vèrt el tò canale LN l'è quell de creà na invoice con Phoenix e pagàlla con un alter wallet LN.

El prim pagament in entrada el determina l'apertura de un canale, la cui liquidità l'è definida de l'import medesim de l'invoice appena creada (escluse le fee par la transaziù onchain de apertura del canale).

I fond pöden vess immediatament disponibil, nonostant sia visualizad un avvis temporanee de attesa par le conferme onchain. Oppur te pödarè dover attend par dopràll.

## Transaziù Onchain
L'apertura de un canale LN l'è semper na transaziù onchain, multifirma 2di2: ti e la contropart (Acinq) stee stabilend le condiziù, con fond tuoi.

Se te gh'heet minga a disposiziù la possibilità de pagà o fàtt pagà na invoice LN, ma te pödet contà su fond onchain, te pödet doprà l'indirizz onchain che Phoenix te fa visualizzà.

Dopo la transaziù, Phoenix el compar inscì:

![img](https://officinebitcoin.it/lezioni/canale/12.webp)

L'app te avvisa che l'è necessari attend 3 conferme in blockchain prima de podè doprà i fond.

# Gestion de la liquidità del canale
Appena ricevude le 3 conferme, el tò wallet LN l'è pront par vess doprà.

Inizialment el gh'ha tutta la liquidità in uscita e te pödet domà spend, te pödet constatàll de `Settings -> Advanced -> Payment Channels`

![img](https://officinebitcoin.it/lezioni/canale/13.webp)

Te pödet creà liquidità in entrada pagand na o pù invoice Lightning Network.

# Us del wallet

Doprà Phoenix wallet l'è n'esperienza piacevol e assai sempliz.

Le uniche noziù da tèg a ment hinn:
1. el canale appena cread l'è vun smart contract tra ti e Acinq, finanziad con i tò fond;
2. el grand lavor de backup de i stat del canale e el sò manteniment infrastruttural hinn gestii a Acinq, che te domandarà quaj sat de fee ulteriur par le operaziù de pagament che te effettuarar;
3. acced regolarment al tò wallet, vertendoll e fànd operaziù ogni tant perché, se la contropart la se n'accorg de la tua assenza credendet vun "zombie", la pö decid de serà el canale. Acinq el serra i canali par minga impiegà risors e temp a mantegn attiv i backup e i canali dormient;
4. anca ti te pödet decid de serà quest canale, qualora te gh'avess minga pù necessità de dopràll.
5. in cas de chiusura del canale, la procedura de la `chiusura cooperativa` l'è la mèjor, perché la evita tante problematiche.

## Splicing
Na menziù particolar l'è dedicada a la tecnica del `Splicing`, implementada de Acinq e che la permet de aumentà o ridù la capacità total del canale.

Lo splicing l'è interessant: se te gh'heet un canale de capacità `tot`, te pödet ampliàll o ridùll. El pö sembrà che quest operaziù dipenden de le necessità de ognidun, **ma l'è minga inscì semplistic**.

L'è necessari in fatti semper tèg a ment che **Phoenix l'è un wallet Lightning Network** e, anca se el gh'ha el support par el Layer1 de Bitcoin, el va doprà par i piccol pagament sul Layer2.

**Ogni operaziù onchain, in fatti, vegnarà interpretada de Acinq come motiv par modificà la capacità del canale**:
- riceziù de un import pari a `xsats` su Phoenix de un wallet onchain : Acinq el amplia el canale, portand la capacità de `tot` a `tot + xsats`
- pagament de un import pari a `ysats` de Phoenix vers un indirizz onchain : Acinq el ridu el canale, portand la capacità de `tot` a `tot - ysats`.

El `splicing` l'è na transaziù onchain (multifirma 2di2) che la comport di fee. Sebben ridotte rispett a l'apertura/chiusura de canale, fà quest operaziù sora pensier o in del moment sbagliad, el pö comportà di cost inutilment alt.

Par passà de LN a Onchain e viceversa, cerca de avvalett di adeguad strument de `swap` e minga doprà Phoenix Wallet par quest.

# Recuper de i fond
Ultim, ma pù important de tutt, ecco che entra in gioc l'importanza de avè in dotaziù strument **non-custodial**.

Se e quand el canale vegnarà serad, te pödarar recuperà i fond onchain **importand le 12 parol del backup in un wallet che el supporta lo standard BIP39**.

Electrum wallet, tra i alter, l'è n'opziù che la rend quest operaziù sempliz e intuitiva.

Se el wallet l'è invece *custodial* e te possedet minga le ciave, te pödarar incontà problem, che van de le difficoltà de interagì con un *impersonale servizzi client*, sottoport a un pesant `kyc` par riaverll indree, **fin a l'impossibilità de recuperà i tò fond (qualsiasi sia l'import total)**.

Ne val la pena?

# Support al studi
Se te gh'heet partecipà a la presentaziù in diretta Telegram, te pödet consideràlla un ulterior pass vers la tua personal sovranità (minga solo finanziaria).
Se te te la see persa **minga desperà**: quest appunt serven appunt par recuperà e, in oltre, te dev savè che la riproporremm anmò su Officine.

Par minga perd la prossima presentaziù, uniscet al [grupp Telegram](https://t.me/officinebitcoin), par restà in agiornament costant.

![img](https://officinebitcoin.it/lezioni/canale/14.webp)

Te pödet anca cerca el [Satoshi Spritz](https://satoshispritz.it/) pù vesin a te. Un Satoshi Spritz l'è un meetup local indove se parla domà de Bitcoin, indove te pödet portà le tò domand e fàtt rispond de alter bitcoiner espert. Al link te trovarè la mapa de la penisola.

![img](https://officinebitcoin.it/lezioni/canale/15.webp)

In fin, se te trovet minga el meetup vesin a te, te pödet approfittà de le dirette settimanai de [SatoshiSpritz Connect](https://t.me/SatoshiSpritzConnect), un meetup virtual creà par chi che pö minga partecipà ai Satoshi Spritz, o par aiutà i meetup pù picinin a prend appunt e trovar ispiraziù par le sò presentaziù.

![img](https://officinebitcoin.it/lezioni/canale/16.webp)
