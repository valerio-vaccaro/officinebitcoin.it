![cover](https://officinebitcoin.it/lezioni/canale/01cover.webp)

# Lightning Network non-custodial
Phoenix di Acinq è un wallet nativo lightning network, non custodial, che offre un wallet basato su standard BIP39 efficiente, ben connesso e che lascia il completo controllo agli utenti.

Scoprirai tra poco che  Phoenix apre un canale LN, del cui bilanciamento sei responsabile al 100%.
Per lavorare bene con Phoenix, è necessaria solo una minima attenzione e la conoscenza base della rete Lightning. Imparerai ad esempio a tenere sotto controllo la liquidità del tuo canale, a tenerlo bilanciato a seconda delle tue necessità e a fare in modo che Acinq ti veda online, per tenerlo aperto e curare l'infrastruttura LN.

# Operazioni base
Dopo aver [scaricato e verificato l'apk di Phoenix](https://officinebitcoin.it/lezioni/verifica/index.html), puoi installare l'app sul telefono.

Phoenix si apre chiedendoti se vuoi creare un nuovo wallet o ripristinarne uno precedente. Se sei alla tua prima esperienza con Phoenix scegli `Create new wallet`. Seguiranno una serie di schermate di benvenuto, che si concludono per iniziare dove premerai `Get started`.

![img](https://officinebitcoin.it/lezioni/canale/03.webp)

## Backup
Una volta aperto Phoenix, **la prima operazione da fare è - come sempre - il backup del wallet**.

Phoenix adotta lo standard BIP39, derivation path m/84'/0'/0', fornendo una sequenza di 12 parole da trascrivere su supporto cartaceo e conservare in un luogo sicuro.

![img](https://officinebitcoin.it/lezioni/canale/04.webp)

Entra nei menu e chiedi a Phoenix di mostrarti la  *Recovery phrase*, cliccando `Display seed`.

![img](https://officinebitcoin.it/lezioni/canale/05.webp)

Al termine ricorda di scorrere la schermata fino in fondo, verso il basso, per confermare di aver eseguito il backup e non vedere più la notifica e l'alert.

![img](https://officinebitcoin.it/lezioni/canale/06.webp)

Phoenix è sostanzialmente pronto per per essere utilizzato. Il tuo nuovo wallet ha il saldo pari a zero e può essere configurato. In basso a sinistra trovi il comando per entrare di nuovo nei settings e impostare voci utili per l'uso quotidiano.

![img](https://officinebitcoin.it/lezioni/canale/07.webp)

## Uso con Tor
Già da diverse versioni di Phoenix, Acinq ha disabilitato la possibilità del motore Tor interno. Se vuoi usare Phoenix con la protezione Tor, saranno necessari 2 accorgimenti:
- abilita Tor nelle impostazioni di Phoenix
- usa una app terza per instradare il traffico del wallet sotto rete onion.

Accedi ai settings e scegli Tor, poi abilita `Enable Tor`, infine instrada il traffico grazie alla app che usi di solito (Orbot, Invizible Pro ecc). Senza una di queste app terze, ma con Tor abilitato nei settings di Phoenix, il wallet non riuscirà a connettersi a internet.

![img](https://officinebitcoin.it/lezioni/canale/09.webp)

## Altre impostazioni
Puoi cambiare e/o impostare una serie di funzioni:
- il nome del wallet, cliccando sulla parola `Wallet` in alto;
- la valuta di riferimento dal sotto menu `Display`.
- impostare le fee in `Channel management`, impostazione importante perché un valore troppo basso di fee potrebbe pregiudicare l'apertura del canale: di default è impostato a 5.000 sats, portalo a 15.000, Phoenix userà comunque il valore adeguato al momento;
- dovresti impostare tutte le precauzioni di sicurezza che ti senti di poter gestire, nel sotto menu `Access control`: PIN per spendere, PIN o controllo biometrico per l'accesso alla App;
- impostare un tuo `Electrum server` nel menu denominato come tale, prestando attenzione che Phoenix richiede un certificato SSL valido (Let's Encrypt, ad esempio);
- attivare le `Experimental features` per richiedere un LN address Bolt12 riutilizzabile
- gestire eventuali chiusure del canale o la creazione/cancellazione di più wallet.

![img](https://officinebitcoin.it/lezioni/canale/08.webp)

# Apertura canale LN ⚡️

Dalla schermata principale di Phoenix, scegli il comando `Receive`

![img](https://officinebitcoin.it/lezioni/canale/10.webp)

Il wallet ti propone due modalità di ricezione, entrambi con QRcode: Lightning e Onchain.

## Pagamento di una invoice Lightning

![img](https://officinebitcoin.it/lezioni/canale/11.webp)

Un metodo veloce per aprire il tuo canale LN è è quella di creare una invoice con Phoenix e pagarla con un altro wallet LN.

Il primo pagamento in entrata determina l'apertura di un canale, la cui liquidità è definita dall'importo stesso dell'invoice appena creata (escluse le fee per la transazione onchain di apertura del canale).

I fondi potrebbero essere immediatamente disponibili, nonostante sia visualizzato un avviso temporaneo di attesa per le conferme onchain. Oppure potresti dovere attendere per utilizzarli.

## Transazione Onchain
L'apertura di un canale LN è sempre una transazione onchain, multifirma 2di2: tu e la controparte (Acinq) state stabilendo le condizioni, con fondi tuoi.

Se non hai a disposizione la possibilità di pagare o farti pagare una invoice LN, ma puoi contare su fondi onchain, puoi usare l'indirizzo onchain che Phoenix ti fa visualizzare.

Dopo la transazione, Phoenix appare così:

![img](https://officinebitcoin.it/lezioni/canale/12.webp)

L'app ti avvisa che è necessario attendere 3 conferme in blockchain prima di poter utilizzare i fondi.

# Gestione della liquidità del canale
Non appena ricevute le 3 conferme, il tuo wallet LN è pronto per essere utilizzato.

Inizialmente ha tutta la liquidità in uscita e puoi soltanto spendere, lo puoi constatare da `Settings -> Advanced -> Payment Channels`

![img](https://officinebitcoin.it/lezioni/canale/13.webp)

Puoi creare liquidità in ingresso  pagando una o più invoice Lightning Network.

# Uso del wallet

Usare Phoenix wallet è un'esperienza piacevole e molto semplice.

Le uniche nozioni da tenere a mente sono:
1. il canale appena creato è uno smart contract tra te e Acinq, finanziato con i tuoi fondi;
2. il grande lavoro di backup degli stati del canale e il suo mantenimento infrastrutturale sono gestiti a Acinq, che ti chiederà qualche sat di fee ulteriore per le operazioni di pagamento che effettuerai;
3. accedi regolarmente al tuo wallet, aprendolo e facendo operazioni ogni tanto perché, se la controparte si accorge della tua assenza credendoti uno "zombie", potrebbe decidere di chiudere il canale. Acinq chiude i canali per non impiegare risorse e tempo a mantenere attivi i backup e i canali dormienti;
4. anche tu puoi decidere di chiudere questo canale, qualora non avessi più necessità di usarlo.
5. in caso di chiusura del canale, la procedura della `chiusura cooperativa` è la migliore, perché evita tante problematiche.

## Splicing
Una menzione particolare è dedicata alla tecnica dello `Splicing`, implementata da Acinq e che permette di aumentare o ridurre la capacità totale del canale. 

Lo splicing è interessante: se hai un canale di capacità `tot`, puoi ampliarlo o ridurlo. Potrebbe sembrare che queste operazioni dipendano dalle necessità di ognuno, **ma non è così semplicistico**.

È necessario infatti sempre tenere a mente che **Phoenix è un wallet Lightning Network** e, anche se ha il supporto per il Layer1 di Bitcoin, va usato per i piccoli pagamenti sul Layer2.

**Ogni operazione onchain, infatti, verrà interpretata da Acinq come motivo per modificare la capacità del canale**:
- ricezione di un importo pari a `xsats` su Phoenix da un wallet onchain : Acinq amplia il canale, portando la capacità da `tot` a `tot + xsats`
-  pagamento di un importo pari a `ysats` da Phoenix verso un indirizzo onchain : Acinq riduce  il canale, portando la capacità da `tot` a `tot - ysats`.

Lo `splicing` è una transazione onchain (multifirma 2di2) che comporta delle fee. Sebbene ridotte rispetto all'apertura/chiusura di canale, fare queste operazioni sovra pensiero o nel momento sbagliato, potrebbe comportare dei costi inutilmente alti.

Per passare da LN a Onchain e viceversa, cerca di avvalerti degli adeguati strumenti di `swap` e non usare Phoenix Wallet per questo.

# Recupero dei fondi
Ultimo, ma più importante di tutto, ecco che entra in gioco l'importanza di avere in dotazione strumenti **non-custodial**.

Se e quando il canale verrà chiuso, potrai recuperare i fondi onchain **importando le 12 parole del backup in un wallet che supporta lo standard BIP39**. 

Electrum wallet, tra gli altri, è un'opzione che  rende questa operazione semplice ed intuitiva.

Se il wallet è invece *custodial* e non possiedi le chiavi, potresti incontrare problemi, che vanno dalle difficoltà di interagire con un *impersonale servizio clienti*, sottoporti ad un pesante `kyc` per riaverli indietro, **fino all'impossibilità di recuperare i tuoi fondi (qualsiasi sia l'importo totale)**.

Ne vale la pena?

# Supporto allo studio
Se hai partecipato alla presentazione in diretta Telegram, puoi considerarla un ulteriore passo verso la tua personale sovranità (non solo finanziaria).
Se te la sei persa **non disperare**: questi appunti servono appunto per recuperare e, inoltre, devi sapere che la riproporremo ancora su Officine.

Per non perdere la prossima presentazione, unisciti al [gruppo Telegram](https://t.me/officinebitcoin), così da rimanere in aggiornamento costante.

![img](https://officinebitcoin.it/lezioni/canale/14.webp)

Puoi inoltre cercare il [Satoshi Spritz](https://satoshispritz.it/) più vicino a te. Un Satoshi Spritz è un meetup locale dove si parla solo di Bitcoin, dove puoi portare le tue domande e farti rispondere da altri bitcoiner esperti. Al link troverai la mappa della penisola.

![img](https://officinebitcoin.it/lezioni/canale/15.webp)

Infine, se non trovi il meetup vicino a te, puoi approfittare delle dirette settimanali di [SatoshiSpritz Connect](https://t.me/SatoshiSpritzConnect), un meetup virtuale creato per chi non può partecipare ai Satoshi Spritz, o per aiutare i meetup più piccolini a prendere appunti e trovare ispirazione per le proprie presentazioni.

![img](https://officinebitcoin.it/lezioni/canale/16.webp)
