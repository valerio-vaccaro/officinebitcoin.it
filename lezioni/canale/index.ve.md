![cover](https://officinebitcoin.it/lezioni/canale/01cover.webp)

# Lightning Network non-custodial
Phoenix de Acinq xe un wallet nativo lightning network, non custodial, che ofre un wallet basà su standard BIP39 efficiente, ben connesso e che lassa el completo controllo ai utenti.

Te scoprirar tra poco che Phoenix vèrt un canale LN, del cui bilanciamento te xe responsabile al 100%.
Par lavorar ben co Phoenix, xe necessaria solo na minima attension e la conossenza base de la rede Lightning. Te impararà ad esempi a tègnar soto controllo la liquidità del to canale, a tègnarlo bilancià a seconda de le to necessità e a far in modo che Acinq te veda online, par tègnarlo verto e curar l'infrastruttura LN.

# Operassion base
Dopo aver [scaricà e verificà l'apk de Phoenix](https://officinebitcoin.it/lezioni/verifica/index.html), te pode installar l'app sul telefono.

Phoenix se vèrt domandandote se te vori crear un novo wallet o ripristinarn uno precedente. Se te xe a la toa prima esperienza co Phoenix scerni `Create new wallet`. Seguirà na serie de schermate de benvenù, che se conclud par scominsiar dove te premarar `Get started`.

![img](https://officinebitcoin.it/lezioni/canale/03.webp)

## Backup
Una volta verto Phoenix, **la prima operassion da far xe - come sempre - el backup del wallet**.

Phoenix adopra lo standard BIP39, derivation path m/84'/0'/0', fornendo na sequenza de 12 parole da trascriver su supporto cartaceo e conservar in un logo sicuro.

![img](https://officinebitcoin.it/lezioni/canale/04.webp)

Entra nei menu e domanda a Phoenix de mostrarte la *Recovery phrase*, clicando su `Display seed`.

![img](https://officinebitcoin.it/lezioni/canale/05.webp)

A la fin ricorda de scorrer la schermata fin in fondo, verso el basso, par confermar de aver eseguì el backup e no veder più la notifica e l'alert.

![img](https://officinebitcoin.it/lezioni/canale/06.webp)

Phoenix xe sostanzialmente pronto par esser doprà. El to novo wallet ga el saldo pari a zero e el pode esser configurà. In basso a manca te trovi el comando par entrar de novo nei settings e impostar voci utili par l'uso quotidiano.

![img](https://officinebitcoin.it/lezioni/canale/07.webp)

## Uso co Tor
Già da diverse version de Phoenix, Acinq ga disabilità la possibilità del motor Tor interno. Se te vori doprar Phoenix co la protezion Tor, i sarà necessari 2 accorgimenti:
- abilita Tor ne le impostassion de Phoenix
- dopra na app terza par instradar el traffico del wallet soto rede onion.

Accedi ai settings e scerni Tor, poe abilita `Enable Tor`, in fin instrada el traffico grazia a l'app che te dopre de solito (Orbot, Invizible Pro ecc). Sensa una de ste app terze, ma co Tor abilità nei settings de Phoenix, el wallet no riuscirà a conneterse a internet.

![img](https://officinebitcoin.it/lezioni/canale/09.webp)

## Altre impostassion
Te pode cambiar e/o impostar na serie de funzion:
- el nome del wallet, clicando su la parola `Wallet` in alto;
- la valuta de riferiment dal soto menu `Display`.
- impostar le fee in `Channel management`, impostassion importante perché un valor tropo basso de fee podarìa pregiudicar l'apertura del canale: de default xe impostà a 5.000 sats, portalo a 15.000, Phoenix doprarà comunque el valor adeguà al momento;
- te dovarìa impostar tute le precaussion de sicuresa che te te senti de poder gestir, nel soto menu `Access control`: PIN par spender, PIN o controllo biometrico par l'accesso a l'App;
- impostar un to `Electrum server` nel menu denominà come tale, prestando attension che Phoenix richiede un certificato SSL valido (Let's Encrypt, ad esempi);
- attivar le `Experimental features` par richieder un LN address Bolt12 riutilizzabile
- gestir eventual chiusure del canale o la creassion/cancellassion de più wallet.

![img](https://officinebitcoin.it/lezioni/canale/08.webp)

# Apertura canale LN ⚡️

De la schermata principal de Phoenix, scerni el comando `Receive`

![img](https://officinebitcoin.it/lezioni/canale/10.webp)

El wallet te propone do modalità de ricezion, tuti e do co QRcode: Lightning e Onchain.

## Pagamento de na invoice Lightning

![img](https://officinebitcoin.it/lezioni/canale/11.webp)

Un metodo veloce par vertir el to canale LN xe quelo de crear na invoice co Phoenix e pagarla co un altro wallet LN.

El primo pagamento in entrada determina l'apertura de un canale, la cui liquidità xe definida da l'importo stesso de l'invoice appena creada (escluse le fee par la transassion onchain de apertura del canale).

I fondi i podarìa esser immediatamente disponibili, nonostante sia visualizà un aviso temporaneo de attesa par le conferme onchain. Oppur te podarìa dover attendar par doprarlo.

## Transassion Onchain
L'apertura de un canale LN xe sempre na transassion onchain, multifirma 2di2: ti e la controparte (Acinq) stè stabilendo le condission, co fondi toi.

Se no te ghe la possibilità de pagar o far te pagar na invoice LN, ma te pode contar su fondi onchain, te pode doprar l'indirizzo onchain che Phoenix te fa visualizar.

Dopo la transassion, Phoenix el par così:

![img](https://officinebitcoin.it/lezioni/canale/12.webp)

L'app te avisa che xe necessario attendar 3 conferme in blockchain prima de poder doprar i fondi.

# Gestion de la liquidità del canale
Appena ricevude le 3 conferme, el to wallet LN xe pronto par esser doprà.

Inizialmente el ga tuta la liquidità in uscita e te pode solo spender; te pode constatarlo da `Settings -> Advanced -> Payment Channels`

![img](https://officinebitcoin.it/lezioni/canale/13.webp)

Te pode crear liquidità in entrada pagando una o più invoice Lightning Network.

# Uso del wallet

Doprar Phoenix wallet xe n'esperienza piacevole e molto sempliz.

Le uniche nozion da tègnar a mente xe:
1. el canale appena creà xe uno smart contract tra ti e Acinq, finanzià co i to fondi;
2. el gran lavoro de backup de i stati del canale e el so mantenimento infrastrutturale xe gestii da Acinq, che te domandarà qualche sat de fee ulteriore par le operassion de pagamento che te effettuarar;
3. accedi regolarmente al to wallet, vertendolo e facendo operassion ogni tanto perché, se la controparte se n'accorge de la toa assenza credendote uno "zombie", la podarìa decidar de serar el canale. Acinq serra i canali par no impiegar risorse e tempo a mantègnar attivi i backup e i canali dormienti;
4. anca ti te pode decidar de serar sto canale, qualora no gavessi più necessità de doprarlo.
5. in caso de chiusura del canale, la procedura de la `chiusura cooperativa` xe la mèjor, perché evita tante problematiche.

## Splicing
Una menzion particolar xe dedicada a la tecnica del `Splicing`, implementada da Acinq e che permete de aumentar o ridur la capacità total del canale.

Lo splicing xe interessante: se te ghe un canale de capacità `tot`, te pode ampliarlo o ridurlo. Podarìa sembrar che ste operassion dipenda da le necessità de ognidun, **ma no xe così semplistico**.

Xe necessario in fato sempre tègnar a mente che **Phoenix xe un wallet Lightning Network** e, anca se el ga el suporto par el Layer1 de Bitcoin, el va doprà par i piccoli pagamenti sul Layer2.

**Ogni operassion onchain, in fato, vegnarà interpretada da Acinq come motivo par modificar la capacità del canale**:
- ricezion de un importo pari a `xsats` su Phoenix da un wallet onchain : Acinq amplia el canale, portando la capacità da `tot` a `tot + xsats`
- pagamento de un importo pari a `ysats` da Phoenix verso un indirizzo onchain : Acinq ridu el canale, portando la capacità da `tot` a `tot - ysats`.

El `splicing` xe na transassion onchain (multifirma 2di2) che comporta de le fee. Sebèn ridotte rispeto a l'apertura/chiusura de canale, far ste operassion sora pensier o nel momento sbaglià, podarìa comportar dei costi inutilmente alti.

Par passar da LN a Onchain e viceversa, cerca de avvalerte dei adeguadi strumenti de `swap` e no doprar Phoenix Wallet par questo.

# Recupero de i fondi
Ultimo, ma più importante de tuto, ecco che entra in gioco l'importanza de aver in dotassion strumenti **non-custodial**.

Se e quando el canale vegnarà serà, te poderè recuperar i fondi onchain **importando le 12 parole del backup in un wallet che suporta lo standard BIP39**.

Electrum wallet, tra i altri, xe n'opzion che rende sta operassion sempliz e intuitiva.

Se el wallet xe invece *custodial* e no possedi le chiavi, te podarìa incontar problemi, che va da le dificoltà de interagir co un *impersonale servizio clienti*, sottoporto a un pesante `kyc` par riaverli indrio, **fin a l'impossibilità de recuperar i to fondi (qualsiasi sia l'importo total)**.

Ne val la pena?

# Suporto al studio
Se te xe partisipà a la presentassion in direta Telegram, te pode considerarla un ulterior passo verso la toa personal sovranità (no solo finanziaria).
Se te te la xe persa **no desperar**: sti apunti i serve appunto par recuperar e, in oltre, te devi saver che la riproporemo ancora su Officine.

Par no perder la prossima presentassion, unissite al [grupo Telegram](https://t.me/officinebitcoin), par restar in agiornamento costante.

![img](https://officinebitcoin.it/lezioni/canale/14.webp)

Te pode anca cercar el [Satoshi Spritz](https://satoshispritz.it/) più vesin a ti. Un Satoshi Spritz xe un meetup locale dove se parla solo de Bitcoin, dove te pode portar le to domande e far te risponder da altri bitcoiner esperti. Al link te trovarè la mapa de la penisola.

![img](https://officinebitcoin.it/lezioni/canale/15.webp)

In fin, se no te trovi el meetup vesin a ti, te pode aprofitar de le direte settimanai de [SatoshiSpritz Connect](https://t.me/SatoshiSpritzConnect), un meetup virtual creà par chi che no pode partisipar ai Satoshi Spritz, o par ajudar i meetup più picini a prender apunti e trovar ispirassion par le so presentassion.

![img](https://officinebitcoin.it/lezioni/canale/16.webp)
