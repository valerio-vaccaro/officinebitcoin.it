---
name: Comprendere il Coin Control manuale
description: Guida esaustiva alla selezione manuale degli UTXO. Capire perché è importante e imparare come puoi farlo con diversi software wallet (desktop e mobile)
---
![cover](assethttps://officinebitcoin.it/lezioni/coinco/cover.webp)


# Introduzione
La solidità del protocollo Bitcoin è garantita da concetti cardine semplici. Tra questi, spicca la trasparenza: tutte le transazioni Bitcoin sono pubbliche e facilmente verificabili da chiunque. Sebbene questa caratteristica sia una pietra miliare del protocollo, perché previene frodi e garantisce la genuinità dei fondi, può rappresentare anche una sfida per la confidenzialità. **Ti sei domandato se tanta trasparenza può inficiare la tua privacy?

Dovresti farlo. Se da una parte accumulare satoshi non-kyc è piuttosto semplice, la tua privacy è maggiormente a rischio proprio nella fase si spesa.
## Cosa succede quando spendi un UTXO
Spendere Bitcoin non è semplicemente il trasferimento di valore a qualcun altro. 

Consumando uno dei tuoi UTXO, infatti, devi soddisfare le condizioni imposte per la trasparenza del protocollo, perché devi dimostrare di essere il proprietario di quei fondi. Devi pertanto:
- esporre la tua chiave pubblica;
- produrre una firma digitale.

Il momento della spesa è dunque il più critico: **spendere bitcoin è un atto da compiere in maniera consapevole e con il maggior controllo possibile**.

# Coin Control
Nel protocollo Bitcoin, elementi come "_conto_" o "_unità monetarie_" non esistono. Il concetto di UTXO non fa parte degli scopi di questa lezione, ma ti invito a fare le domande relative al tuo satoshi spritz di fiducia, o a richiedere una lezione qui su Officine Bitcoin.
Ciò che devi sapere è che con Bitcoin ciò che accumuli e, in seguito spenderai, sono piccole o grandi unità di conto misurate in satoshi, rappresentati da `output di transazione non spesi`, gli **UTXO**, detti anche `coins`.
Quando si utilizzano UTXO per creare una transazione, questi vengono completamente distrutti e si creano altri UTXO al loro posto.

I software wallet sono sviluppati per fare questa scelta in maniera automatica, utilizzando coins selezionate in maniera "casuale" con l'unico criterio di coprire l'importo necessario alla spesa.

Il `Coin Control`, che puoi trovare anche denominato `Coin Selection`, è una funzione caratteristica di alcuni software wallet, che ti permette di **selezionare manualmente gli UTXO da spendere quando costruisci la tua transazione**.

Supponiamo di avere un wallet con 3 UTXO, rispettivamente da 21.000, 42.000 e 63.000 satoshi.

![img](assets/en/01.webp)

Se devi spendere 24.000 sats e lasci fare al software la selezione automatica, un buon wallet potrebbe scegliere di combinare l'UTXO1 + l'UTXO2 per pagare i 24k sats e le fee del miner, creando un resto che torna su un indirizzo interno del wallet di partenza.

![img](assets/en/02.webp)

Dopo la transazione la nuova situazione nel wallet, contando solo gli UTXO, si può così riassumere.

![img](assets/en/03.webp)

Con il giusto software e la tua consapevolezza, invece, avresti potuto compiere una scelta diversa e più corretta. Ad esempio selezionando solo l'UTXO2 (da 42.000 sats).

![img](assets/en/04.webp)

Con una situazione finale, a livello di UTXO, nel tuo wallet che ha un aspetto differente.

![img](assets/en/05.webp)

# Perché selezionare manualmente gli UTXO?
![img](assets/en/06.webp)

Nel nostro esempio, il saldo di fatto lo stesso: `108.280 sats`. Dopo la spesa di 24.000 sats, senza coin control avremmo 2 UTXO nel wallet; con il coin control manuale ne abbiamo 3 totali.

**Perché fare tutto questo?**

Ci sono, o potrebbero esserci, diversi motivi per cui non abbiamo usato l'`UTXO1` **e sono tutti alla base del perché - in fase di spesa - attivare il coin control manuale è una delle buone pratiche da seguire**.

## Privacy
Il vantaggio principale, quando si parla di manual coin selection, è una **maggiore privacy per chi spende**.

Prendiamo sempre il nostro esempio: la spesa di 24.000 satoshi _senza coin control_. Essendo la blockchain di Bitcoin un registro pubblico, un osservatore esterno può dichiarare, senza ombra di dubbio, che gli input `UTXO1 di 21.000 sats` e `UTXO2 di 42.000 sats`, nonché il resto, l'`UTXO5 da 38.280 sats` **appartengono tutti e tre allo stesso utente**.

Selezionando manualmente l'`UTXO2`, invece, rimane completamente riservato l'`UTXO1`, fermo nell'UTXO set in attesa di essere speso in un momento più appropriato.

L'`UTXO1` potrebbe provenire da una fonte KYC, ad esempio un pagamento ricevuto in cambio di beni e servizi, mentre gli altri UTXO no.

**Se fosse il tuo wallet, vorresti che un osservatore esterno possa risalire alla tua identità con una certezza così assoluta?** I wallet che implementano la selezione manuale degli UTXO, permettono ad esempio la **segregazione di uno o più UTXO**, una funzione da utilizzare quando si presentano situazioni di questo tipo.

Sebbene io sia convinta che fondi KYC dovrebbero essere conservati in un wallet separato rispetto a bitcoin acquistati senza kyc, se questo è il tuo caso la segregazione di alcuni tuoi indirizzi è un aiuto fondamentale, che potresti ricevere imparando a selezionare manualmente i tuoi input di spesa.

## Risparmio sulle fee
Selezionare l'UTXO corretto per effettuare una spesa consente di ottimizzare le fee. Sempre partendo dal nostro esempio, il software wallet ha selezionato due UTXO per coprire la la spesa da fare. Due UTXO implicano due firme da mostrare alla rete, quindi un peso maggiore della transazione stessa in termini di vByte.

Usando il coin control manuale, invece, puoi selezionarne uno solo che sia sufficiente a coprire l'importo, risparmiando fee perché diminuisce il "peso" della transazione.

In periodi in cui le fee sono alte, ma sei costretto a spendere bitcoin on-chain (ad esempio per aprire un canale Lightning Network), ecco che il coin control si rivela il giusto incentivo economico a cui ricorrere.

## Aggregazione dei resti
Quando si fa un pagamento e si usano Bitcoin on-chain, la possibilità di ricevere un resto diventa quasi sempre una certezza. Ogni resto è di per sé una piccola perdita di privacy, in quanto svela alla rete un tuo indirizzo che si può associare al tuo input di partenza.

Considerando che i migliori wallet HD generano degli indirizzi appositi per i resti, puoi riconoscerli facilmente e "segregare" tutti i resti delle varie transazioni effettuate; quando questi hanno raggiunto un certo importo puoi selezionarli manualmente e consolidarli, o fare swap su Lightning Network (il mio metodo preferito) e trattarli così da riguadagnare la privacy perduta in fase di spesa.

## Spesa da un cold wallet
Il cold wallet è uno strumento con cui si può ragionevolmente ottenere un buon grado di sicurezza, per conservare una qualsiasi quantità di fondi da tenere da parte per un lungo periodo di tempo. Possono però capitare degli imprevisti, in cui è necessario mettere mano ai risparmi e far fronte a qualche spesa inaspettata.

Il mio consiglio è quello di **non effettuare mai la spesa direttamente dal cold wallet, per evitare di ricevere il resto tra gli indirizzi dello stesso**. Impara a selezionare manualmente gli UTXO necessari a coprire la spesa, trasferiscili su un wallet hot e prepara la tua transazione da quest'ultimo. L'eventuale resto, poi, potrai rimandarlo su un indirizzo del cold wallet (se l'importo è adeguato), oppure utilizzarlo per altri scopi.

# Presentazione pratica
Dopo questa lunga introduzione, vediamo come mettere in pratica il coin control con diversi software desktop e mobile. Useremo sempre lo stesso wallet HD, importato in ognuno degli strumenti scelti, in modo da mostrarti le piccole differenze che ci sono tra di loro.

# Wallet Desktop

## Sparrow
Se usi Sparrow, apri il tuo wallet e seleziona _UTXOs_ dal menu a sinistra. Ti comparirà la lista dei tutti gli UTXO associati al tuo wallet.

Clicca semplicemente con il mouse su uno di loro e poi scegli _Send Selected_. Sparrow ti mostra anche il totale selezionato per la spesa, accanto al comando.

![img](assets/en/07.webp)

Puoi anche selezionarne più di uno. Aiutati con il tasto _CTRL_ per selezionare UTXO non adiacenti nella lista.

![img](assets/en/08.webp)

Dopo aver selezionato manualmente gli UTXO, Sparrow ti mostrerà bene, graficamente, come è costruita la tua transazione, che puoi finalizzare e concludere.

![img](assets/en/09.webp)

### Segregazione dell'UTXO
Segregare dei fondi significa "bloccarli" all'interno del wallet, affinché non possano essere usati come input di una transazione. 

Sparrow permette questa funzionalità, cui si accede sempre dal menu _UTXOs_. Si posiziona il mouse sull'UTXO da "bloccare" e si clicca il tasto destro del mouse. Tra le funzionalità di questa procedura comparirà il comando _Freeze_. È così che potrai segregare un UTXO con Sparrow Wallet.

![img](assets/en/29.webp)

## Electrum
Se il tuo wallet desktop è Electrum, devi sapere che puoi selezionare manualmente gli UTXO sia dal menu _Addresses_ sia dal menu _Coins_.
In entrambi i menu la selezione avviene puntando il mouse sull'UTXO da scegliere e scegliendo _Add to coin control_ dopo aver cliccato il tasto destro.

![img](assets/en/10.webp)

Anche con questo software puoi selezionare più di un UTXO, aiutandoti con il tasto _CTRL_ della tastiera se non sono adiacenti tra loro.

![img](assets/en/11.webp)

Graficamente Electrum ti mostrerà la selezione evidenziando in verde gli UTXO selezionati, mentre in basso ti compare una barra, evidenziata dello stesso colore, che mostra il saldo disponibile dopo il coin control.

![img](assets/en/12.webp)

Una volta selezionato l'output o gli output, puoi costruire la tua transazione come sempre, dal menu _Send_.

### Segregazione dell'UTXO
Electrum mette a disposizione questa possibilità, andando nel menu _Coins_ e selezionando un determinato UTXO e poi scegliendo _Freeze_ con il tasto destro del mouse. Si può "freezare" l'indirizzo anche senza fondi dal menu _Addresses_, oppure la "coin" per non spenderla.

![img](assets/en/28.webp)

## Nunchuk
Nunchuk permette di selezionare gli UTXO dal menu principale, una volta aperto.
Lancia Nunchuk e clicca _View coins_.

![img](assets/en/13.webp)

Si apre la finestra che contiene tutti gli UTXO del tuo wallet, dove puoi selezionarne uno o più, attivando la spunta accanto ad ogni importo. Dopo aver effettuato la selezione, continua con _Create transaction_.

![img](assets/en/14.webp)

Dopodiché potrai inserire l'indirizzo di destinazione e impostare l'importo e le fee.

![img](assets/en/15.webp)

## Blockstream App
Blockstream App desktop, già conosciuto come Green, permette di fare coin selection quando si è già iniziata a costruire la transazione. Apri pertanto il tuo wallet e clicca su _Send_.

![img](assets/en/16.webp)

Incolla l'indirizzo di destinazione nel campo apposito e poi seleziona _Manual coin selection_.
![img](assets/en/17.webp)
Si apre la finestra dove puoi selezionare uno o più UTXO. Nell'esempio che segue, abbiamo selezionato due coins. Dopodiché conferma la scelta cliccando su _Confirm Coin Selection_.

![img](assets/en/18.webp)

Imposta l'importo e le fee e poi procedi normalmente con la tua transazione.

![img](assets/en/19.webp)

⚠️ N.B. Nel menu _Coins_ di Green sono presenti le voci _Lock_/_Unlock_ che prefigurano la possibilità di segregare UTXO. Questa possibilità è presente solo negli account cosiddetti multisig; inoltre la funzionalità si attiva solo selezionando UTXO di importo molto piccolo, vicino alla soglia del `Dust`.

# Wallet mobile

## Blue Wallet
Anche da mobile è possibile scegliere wallet che permettono di selezionare manualmente gli UTXO. Vediamo per primo Blue Wallet.

Se sei un utente di questo software, apri il tuo wallet e clicca per entrare nelle schermate dei comandi relativi ad uno dei tuoi wallet. Per accedere al coin control si deve entrare nella fase di spesa, quindi clicca _Send_.

![img](assets/en/21.webp)

Nella successiva schermata scegli i menu segnalati dai tre pallini in alto a destra. Si apre una finestra a tendina con una serie di comandi. Scegli l'ultimo: _Coin Control_.

![img](assets/en/22.webp)

A questo punto Blue Wallet mostra tutti i tuoi UTXO. Oltre che dagli importi, sono differenziati graficamente da colori diversi.

![img](assets/en/27.webp)

Scegli l'UTXO da selezionare dopodiché seleziona _Use Coin_.

![img](assets/en/23.webp)

Blue Wallet ti riporta nella finestra di _Send_ per continuare a costruire la transazione. Aggiusta l'importo e le fee, dopodiché scegli _Next_.

![img](assets/en/24.webp)

A questo punto puoi terminare la transazione, come fai di solito.

### Segregazione di un UTXO
Anche Blue Wallet permette di segregare gli UTXO, rendendoli non disponibili per la spesa, il che non è male come funzione per un wallet da dispositivo mobile.

Si accede al coin control con la procedura appena spiegata e, dopo aver selezionato l'UTXO, scegli _Freeze_ al posto di _Use Coin_.

![img](assets/en/26.webp)

## Nunchuk
Anche la versione mobile di Nunchuk prevede la possibilità per l'utente di effettuare il coin control. Se usi questa app da mobile, aprilo e vai nel menu _Wallet_. Da qui scegli _View coins_.

![img](assets/en/30.webp)

Nella finestra dove compare la lista degli UTXO clicca _Select_.

![img](assets/en/38.webp)

Accanto ad ogni UTXO appare la funzione di selezione. Come nella versione desktop, anche su Nunchuk mobile la selezione manuale avviene spuntando il quadratino accanto all'importo. La schermata riporta il numero di UTXO selezionati e l'importo totale a disposizione. Una volta finito, il simbolo ₿ in basso a sinistra, che è il comando per iniziare a costruire la transazione.

![img](assets/en/31.webp)

Ora puoi completare la transazione, scegliendo l'importo e cliccando su _Continue_.

![img](assets/en/32.webp)

Continua come fai sempre, incollando un indirizzo di destinazione, una descrizione e personalizzando le impostazioni delle fee.

## Bitcoin Keeper
Bitcoin Keeper è l'ultimo wallet che vedremo in questa guida. Vediamo la sua funzionalità applicata al coin control con un wallet single-sig, anche se un tale 'uso  non è lo scopo di questa app molto particolare.

Dopo aver impostato Keeper sul tuo telefono, lancialo e apri un wallet contenente alcuni UTXO. Al centro della schermata principale clicca _View All Coins_.

![img](assets/en/34.webp)

Keeper mostra una panoramica degli UTXO. Per accedere alla schermata di selezione clicca _Select To Control_.

![img](assets/en/35.webp)

Puoi selezionare le coins, spuntandole, cliccando sull'apposito comando. Al termine, clicca _Send_.

![img](assets/en/36.webp)

Bitcoin Keeper ti porta direttamente al menu _Send_, dove puoi costruire la transazione con gli UTXO selezionati.

![img](assets/en/37.webp)

# Hardware wallet
Ognuno dei software wallet visti in questa guida può essere l'interfaccia watch-only di un tuo hardware wallet. Significa il coin control per dispositivo di firma offline si esegue con i passaggi visti fin qui.

## Raccomandazioni generali
Il coin control è una pratica molto efficace per selezionare gli input delle tue transazioni. La selezione manuale è ancor più efficiente se, in fase di acquisto/ricezione dei tuoi fondi, hai etichettato bene la provenienza dei tuoi satoshi. Se desideri imparare bene questa tecnica, ti consiglio il tutorial:

https://planb.network/tutorials/privacy/on-chain/utxo-labelling-d997f80f-8a96-45b5-8a4e-a3e1b7788c52