
# Setup Jade

![alt text](https://officinebitcoin.it/lezioni/jadeset/0_Cover.jpg)

Jade arriva nella confezione che si deve verificare essere integra, controllando i due adesivi ologramma anti-tamper apposti tra la scatola (inferiore) e il coperchio (superiore).

Nella confezione è presente un piccolo manuale utente, due template per il CompactSeedQR, nonché l’hardware wallet.

Il Jade si accende tenendo premuto il tasto inferiore e si presenta mostrando i 3 menu:

- Setup Jade
- Scan QR
- Options

Si possono impostare diversi parametri in Options, a seconda delle preferenze personali, ma è l’inizializzazione la prima parte da completare.

Agendo con il tasto scroll, si seleziona quindi il menu __Setup Jade__ e si conferma con il tasto frontale.

![alt text](https://officinebitcoin.it/lezioni/jadeset/1.jpg)

Compare l’avviso di controllare le istruzioni di setup dal sito https://blockstream.com/jade/

![alt text](https://officinebitcoin.it/lezioni/jadeset/2.jpg)

Per una corretta esecuzione, si consiglia di creare la mnemonica con il lancio dei dadi e utilizzare questa entropia per creare il wallet. Si scelga, quindi, __Advanced Setup__.

![alt text](https://officinebitcoin.it/lezioni/jadeset/3.jpg)

Jade avvisa che questo setup presenta alcune caratteristiche tecniche avanzate. È sufficiente prestare la massima attenzione e cliccare sul tasto di conferma

![alt text](https://officinebitcoin.it/lezioni/jadeset/4.jpg)

Nell’ottica di inserire la mnemonica generata con l’entropia dei dadi, scegliere __Restore Wallet__.

![alt text](https://officinebitcoin.it/lezioni/jadeset/5.jpg)

Si deve ora impostare la lunghezza della mnemonica, 12 o 24 parole. Il menu offre anche la possibilità di ripristinare il wallet scansionando un QR code: si tratta del SeedQr che verrà trattato in altra sede.

![alt text](https://officinebitcoin.it/lezioni/jadeset/6.jpg)

Per una questione prettamente didattica e di velocità, questo tutorial mostra il setup con una mnemonica da 12 parole.

Parte la procedura di inserimento della prima parola e Jade mostra la tastiera con cui immettere le relative lettere. Con il tasto scroll, posizionarsi ← → nella corretta posizione.

In questo esempio, la parola #1 è “below”.

![alt text](https://officinebitcoin.it/lezioni/jadeset/7.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/8.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/9.jpg)

Dopo l’inserimento delle prime 3-4 lettere, Jade pesca le parole dal dizionario BIP39 e inizia a fornire una serie di
suggerimenti. Con il tasto scroll andare avanti o indietro fino a trovare la parola corretta.

![alt text](https://officinebitcoin.it/lezioni/jadeset/10.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/11.jpg)

Continuare con l’inserimento delle parole, fino ad arrivare al momento dell’ultima parola: il checksum.

A questo punto Jade mostra due possibilità: inserire una parola esistente oppure offre la possibilità di calcolare un checksum valido con il proprio software.

![alt text](https://officinebitcoin.it/lezioni/jadeset/12.jpg)

N.B.

- Nel caso del setup da una mnemonica di 12 parole creata col lancio dei dadi, si consiglia di scegliere Existing e inserire le prime lettere della parola, scegliendole nel range proposto dal lancio dei dadi.
- Se il setup parte, invece, da una mnemonica di 24 parole generata col lancio dei dadi, si può far calcolare tutti i possibili checksum a Jade e poi sceglierne uno. È vero che si perde un po’ di entropia, ma solo nell’ultima parola. Quando si è deciso di affidare a Jade i propri fondi, è un trade-off accettabile.
- In caso di ripristino di un wallet già esistente: immettere il checksum corretto scegliendo Existing.

Portando avanti l’esempio di un setup da mnemonica generata con il lancio dei dadi, scegliamo Existing nel menu precedente, con l’intento di immettere le lettere e trovare il corrispondente checksum.

![alt text](https://officinebitcoin.it/lezioni/jadeset/13.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/14.jpg)

A questo punto Jade propone l’esportazione della recovery phrase sotto forma di _CompactSeedQR_.

Il _CompactSeedQR_ è una codifica che trasforma la frase mnemonica in QR code da scannerizzare per il ripristino del wallet su Jade.

Se si desidera provare a farlo, vedere la sezione in fondo a questo tutorial che spiega come fare.

![alt text](https://officinebitcoin.it/lezioni/jadeset/15.jpg)

Scegliendo “No” nel menu precedente, si può passare al termine del setup.

Il dispositivo è pronto per essere collegato al suo wallet di visualizzazione.

Il prossimo menu mostra le possibilità di connessione:

- USB
- QR code
- Bluetooth

![alt text](https://officinebitcoin.it/lezioni/jadeset/16.jpg)

Si scelga USB e confermare con il tasto di confermare

A questo punto Jade chiede di essere connesso ad una companion app.

Nell’esempio che segue si è scelto di connettere il dispositivo via USB a Blockstream Green; questo wallet, infatti, permette di controllare aggiornamenti firmware per Jade nonché, sentendo via USB il dispositivo, offre il setup auto-guidato.

Aprire quindi Green e controllare i settaggi di rete e di security.

Se c’è un aggiornamento firmware Green lo segnala subito ed è consigliato eseguire l’upgrade.

![alt text](https://officinebitcoin.it/lezioni/jadeset/17.jpg)

Terminato l’aggiornamento firmware, Green inizia ad interagire con Jade.

Il dispositivo di firma, a questo punto, chiede di impostare il duress PIN, che cripterà le chiavi private sul Jade, rendendole inaccessibili per chiunque, tranne per chi possiede il PIN a sei cifre.

![alt text](https://officinebitcoin.it/lezioni/jadeset/18.jpg)

Mentre Green attende con la schermata mostrata sopra, su Jade compare la possibilità di impostare il PIN a 6 cifre e confermarlo re-immettendolo correttamente.

![alt text](https://officinebitcoin.it/lezioni/jadeset/19.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/20.jpg)

Jade crea i dati persistenti criptandoli sul dispositivo.

![alt text](https://officinebitcoin.it/lezioni/jadeset/21.jpg)

Al termine dell’operazione, che può richiedere qualche istante, su Green si apre il wallet pronto all’uso.

Spegnendo Jade e riaccendendolo, il dispositivo si presenterà inizializzato, col firmware aggiornato e pronto per essere sbloccato (Unlock Jade) per l’utilizzo la sua companion app.

![alt text](https://officinebitcoin.it/lezioni/jadeset/22.jpg)

## Extra: creazione CompactSeedQR

Al termine dell’inserimento della mnemonica, abbiamo bypassato la parte di esportazione delle chiavi in formato QR code, per rimanere concentrati nella fase di setup. Questo tipo di esportazione si può fare sempre in seguito.

Si accende il Jade e dal menu Options → Temporary Signer → Continue → 12/24 Words si ritorna nel menu di inserimento della recovery phrase, al termine del quale viene proposta la schermata di scelta per l’esportazione in formato SeedQR.

![alt text](https://officinebitcoin.it/lezioni/jadeset/15.jpg)

Scegliendo Yes, si viene avvisati che si deve disegnare il QR code sul template fornito nella scatola.

![alt text](https://officinebitcoin.it/lezioni/jadeset/24.jpg)

La procedura inizia mostrando una visione di insieme di come sarà il QR code da disegnare (alcune parti sono cancellate per motivi di privacy)

![alt text](https://officinebitcoin.it/lezioni/jadeset/25.jpg)

In seguito verranno mostrate tutte le caselle della griglia, una per una, dalla A1 alla C3 o E5 a seconda della lunghezza della recovery phrase.

![alt text](https://officinebitcoin.it/lezioni/jadeset/26.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/27.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/28.jpg)

Dopo aver disegnato l’ultima casella della griglia, Jade mostra di nuovo la vista di insieme per una prima verifica. Proseguire confermando Done.

![alt text](https://officinebitcoin.it/lezioni/jadeset/29.jpg)

Si abilita la fotocamera incorporata di Jade, con la quale si deve inquadrare il SeedQR appena disegnato.

![alt text](https://officinebitcoin.it/lezioni/jadeset/30.jpg)

Se il disegno corrisponde a quanto proposto da Jade nella procedura appena compiuta, si visualizzerà un segnale di conferma.

![alt text](https://officinebitcoin.it/lezioni/jadeset/31.jpg)

Cliccando per confermare Continue, Jade si presenta funzionante dai menu principali.

Il CopactSeedQR è uno strumento per ripristinare il wallet su Jade.
