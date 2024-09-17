# Firme
L'argomento di questa lezione saranno le firme digitali e come si applicano a Bitcoin.

## Cosa è una firma?
Dobbiamo capire che cosa intendiamo per firma digitale. Quando pensiamo ad una normale firma pensiamo normalmente ad altro, siccome parliamo di documenti digitali la firma digitale lega sia l'identità dell'autore che lo stato del documento firmato, quindi sostanzialmente la firma dipende anche dal documento che andiamo a firmare.

Questo è una differenza molto grande con il mondo fisico, dove invece la firma noi la poniamo praticamente senza curarci del supporto su cui lo facciamo. Certo che magari non andremo a firmare assegni o altri documenti senza preoccuparcene però sostanzialmente la firma che andiamo ad apporre non varia.

Le firme digitali invece sono sono una cosa un po' differente, le firme di digitali normalmente si basano su algoritmi a chiave pubblica e privato. Vuol dire che il nostro portafoglio da qualche parte nel mondo c'è una coppia di chiavi, pubblica e privata e la nostra (pseudo-)identità è collegata alla chiave pubblica che tutti conoscono o che renderemo nota a tutti.

Noi utilizzeremo la nostra chiave privata, che è un numero, e con qualche magia matematica produrremo una firma che è un numero diverso e che dimostra che un certo stato di un certo documento appartiene o è conosciuto da una certa identità connessa ad una chiave pubblica. Quello che vado a firmare è l'impronta (o HASH) di un certo documento (o PAYLOAD).

Mi serve anche qualche un generatore di numeri casuali, butto tutti questi dati all'interno di uno "scatolone nero" che mi produce una firma, la firma quindi è un qualcosa che dimostra il possesso perché io sto firmando con il mio segreto ma dimostra anche che quello che io sto firmando non sia stato modificato.

Se modifico il PAYLOAD modifico l'HASH e ovviamente questo invalida la firma.

Quindi sostanzialmente perché è stata introdotta questa firma più complessa nel mondo digitale? Beh perché nel mondo digitale, a differenza di quello di quello fisico (e magari chi ha marinato a scuola se ne ricorda) copiare una firma è molto più semplice.

La firma digitale invece ha informazioni sul documento e quindi cambia per ogni documento e non può essere incollata e riutilizzata su di un documento divergo.

La firma digitale serve quindi a:
- dimostrare che io ho creato un certo messaggio o sto chiedendo una certa azione o sto dichiarando un certo stato di un sistema e
- dimostrare che quel messaggio o quel documento o quella stringa di dati non sia stata manipolata, ovvero che sia effettivamente quella che io volevo firmare.
- rendere irripudiabile una certa azione, se ho prodotto una firma sono stato proprio io a farla per quello specifico documento.

## Firme in Bitcoin
Questa tecnologia è utilizzata in Bitcoin sotto l'acronimo ECDSA (Electronic Curve Digital Signature Algorithm) che è un algoritmo per la produzione di firme digitali su curva ellittica, per ora non tratteremo altri schemi di firma.

Ricordiamo che in Bitcoin si possono produrre firme per:
- testo arbitrario, poco importante e usato
- nuove transazioni, con lo scopo di autorizzare la spesa di una certa UTXO

Ma queste firme come si legano alla transazione? Ogni indirizzo ha un meccanismo di spesa, degli script che devono essere eseguiti per sapere se una spesa può essere autorizzata. All'interno di questi script ci sono comandi (o OPCODE) destinati al controllo delle firme digitali quali OP_CHECKSIG, OP_CHECKSIGVERIFY, OP_CHECKMULTISIG, OP_CHECKMULTISIGVERIFY

Ricordiamo che una transazione in Bitcoin è costituita da:
- Input, ovvero i fondi che vado a spendere e per cui devo produrre uno script di spesa
- Output, ovvero i nuovi indirizzi in cui andranno i fondi (e per ogni indirizzo è connessa una modalità di spesa ben definita.

In sostanza, nella maggioranza dei casi dovrò quindi produrre PER OGNI INPUT la/le firma/e necessarie a completare lo script di spesa.

Ricordiamo che questa azione ci permette di dimostrare che quell'input è nostro e che la vogliamo spendere (vogliamo passare la proprietà in toto o vogliamo dividerlo o vogliamo unirlo con altri input).

Ovviamente la transazione è valida se tutti gli input sono correttamente firmati mentre se anche uno no degli input non è firmato quella la transazione non può considerarsi valida.

La firma è controllabile da tutti e non è ripudiabile, ma per flessibilità Satoshi in maniera molto molto furba ha introdotto varie modalità di firma, cioè la firma è sempre la stessa ma cambia il PAYLOAD cioè la porzione di transazione oggetto della firma, questo consente ad esempio di generare schemi e protocolli complessi in cui pezzi di transazioni possono essere combinate tra di loro, Satoshi ha chiamato queste modalità (veri e propri flag nel linguaggio di scripting) SIGHASH.

## SIGHASH
Il più semplice SIGHASH è SIGHASH_ALL che vuol dire di generare una firma con TUTTI gli INPUT e TUTTI gli OUTPUT, questa è la modalità più semplice e più usata per fare una firma.

Una prima differenza si può avere con SIGHASH_NONE che firma TUTTI gli INPUT, ma NESSUNO degli OUTPUT, consentendo di aggiungere output o modificare le fee a posteriori. ATTENZIONE che con questo schema, se non protetti da multisig o altre funzionalità, un miner o chiunque veda una transazione con questo schema di firma può sostituire gli output redirigendo i fondi verso un proprio indirizzo.

Un flag più interessante è SIGHASH_SINGLE in cui si firma una coppia di input ed output purché vengano inseriti in una transazione allo stesso livello (e.g. quinto input e quinto output), questo consentirebbe di comporre transazioni più grandi basate su queste coppie ma non da una possibilità di introdurre un change ovvero richiede la spesa totale dell'input.

Parallelamente tutti questi SIGHASH possono essere combinati con il flag ANYONECANPAY che limita la firma solo all'input per cui si sta producendo firma dando quindi possibilità a chiunque di aggiungere input alla transazione.

Queste firme sono tutte firme valide indipendentemente dal tipo di indirizzo e dagli script lasciando massima flessibilità di espressione al wallet, normalmente userà SIGHASH_ALL ma potrebbe pure seguire protocolli più complessi che richiedono schemi di firma differenti. In caso di multisig poi non c'è necessità di usare il medesimo tipo di firma, un wallet 2di2 potrebbe firmare alcuni suoi UTXO con SIGHASH_NONE e ANYONECANPAY al fine di dare pieno controllo al secondo firmatario che potrà, ad esempio, raccogliere tutti questi input in una transazione da firmare con SIGHASH_ALL.

## Firme su testo arbitrario
Per per completezza le stesse firme che vengono utilizzate per gli input delle transazioni potete utilizzare anche per firmare del testo arbitrario.

Bitcoin propone uno schema in cui viene viene aggiunta del testo per evitare che questa funzionalità venga utilizzata per firmare a parte di transazioni, quindi se avete Bitcoin core o anche alcuni Wallet potete cercare una funzionalità di firma di messaggi di testo sulla base di un certo vostro indirizzo.

Il wallet userà la chiave privata associata alla chiavetta pubblica che ha generato quell'indirizzo per fare delle firme di messaggi testuali 

All'atto della verifica si ottiene la chiave pubblica che può essere può quindi utilizzata per rigenerare l'indirizzo, quindi se io ho il testo e la firma mi tiro fuori la chiave pubblica che ha firmato e dalla chiave pubblica posso ricalcolarmi l'indirizzo e controllarlo ad esempio con quello fornito.

## Programma
La lezione sulle firme può essere ripetuta, qui un elenco di quelle già tenute:

| Data        | Note                                           |
|-------------|------------------------------------------------|
|||
