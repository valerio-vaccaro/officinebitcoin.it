
# Jade airgapped con Sparrow Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/0.jpg)

Usare Jade per comunicazioni completamente airgapped è possibile, in virtù delle sue caratteristiche firmware e hardware.

La fotocamera e il display integrato, infatti, svolgono proprio la funzione di acquisire ed inviare messaggi da e per il wallet di visualizzazione.

Questo tutorial mostra come utilizzare Jade airgapped con Sparrow Wallet.

La procedura prevede prima il setup, poi l’esportazione della chiave pubblica estesa da Jade a Sparrow-visualizzazione e, infine, una transazione di spesa.

Per scelta didattica si è scelto di iniziare mostrando la sequenza di operazioni a partire dal Jade.

## Advanced Setup

La scelta di usare il dispositivo airgapped comporta un vero e proprio setup, ovvero va fatta al momento dell’inizializzazione di Jade (1) che deve quindi presentarsi non inizializzato.

![alt text](https://officinebitcoin.it/lezioni/jadespa/1.jpg)

Compare l’avviso di controllare le istruzioni di setup dal sito https://blockstream.com/jade/.

![alt text](https://officinebitcoin.it/lezioni/jadespa/2.jpg)

La configurazione di Jade per l’utilizzo airgapped si può fare solo scegliendo Advanced Setup.

![alt text](https://officinebitcoin.it/lezioni/jadespa/3.jpg)

Jade avvisa che questo setup presenta alcune caratteristiche tecniche avanzate. È sufficiente prestare la massima attenzione e cliccare sul tasto di conferma

![alt text](https://officinebitcoin.it/lezioni/jadespa/4.jpg)

Nell’ottica di inserire la mnemonica generata con l’entropia dei dadi, scegliere Restore Wallet.

![alt text](https://officinebitcoin.it/lezioni/jadespa/5.jpg)

Si deve ora impostare la lunghezza della mnemonica, 12 o 24 parole. Il menu offre anche la possibilità di ripristinare il wallet scansionando un QR code: si tratta del SeedQr che è stato trattato nel tutorial dedicato al Setup.

![alt text](https://officinebitcoin.it/lezioni/jadespa/6.jpg)

Per una questione prettamente didattica e di velocità, questo tutorial mostra il setup con una mnemonica da 12 parole.

Il passaggio successivo è da seguire come descritto, per poter accedere alla funzionalità airgapped. Si deve infatti scegliere di esportare la recovery phrase in formato CompactSeedQR, selezionando Yes.

![alt text](https://officinebitcoin.it/lezioni/jadespa/7.jpg)

Dopo la scelta si viene avvisati che si deve disegnare il QR code sul template fornito nella scatola, come mostrato nella sezione “Extra” della lezione dedicata al Setup.

![alt text](https://officinebitcoin.it/lezioni/jadespa/8.jpg)

Al termine della procedura si deve procedere alla verifica della corrispondenza tra quanto disegnato e il CompactSeedQR mostrato dal dispositivo. Infatti, si abilita la fotocamera incorporata di Jade con la quale si deve inquadrare il SeedQR appena disegnato.

![alt text](https://officinebitcoin.it/lezioni/jadespa/9.jpg)

Se il disegno corrisponde a quanto proposto dal dispositivo nella procedura appena compiuta, viene visualizzato il segnale di conferma.

![alt text](https://officinebitcoin.it/lezioni/jadespa/10.jpg)

Ecco che adesso Jade mostra le opzioni per la connessione del dispositivo ad una companion app: scegliere QR.

![alt text](https://officinebitcoin.it/lezioni/jadespa/11.jpg)

Anche il passo successivo richiede una scelta da parte dell’utente: salvare le chiavi criptate sul dispositivo oppure caricarle ad ogni sessione, scansionando il SeedQR appena disegnato

![alt text](https://officinebitcoin.it/lezioni/jadespa/12.jpg)

N.B.

È utile comprendere queste due opzione di accesso:

- QR PIN Unlock: Durante l'inizializzazione, Jade salverà i dati del wallet criptatandoli sul dispositivo; saranno sempre accessibili sbloccando Jade con la procedura del QR PIN.
- SeedQR: il SeedQR va scansionato da Jade ogni volta che si desidera caricare le chiavi sul dispositivo.

Per scelta didattica, nell’opzione precedente si è scelto SeedQR, pertanto il dispositivo verrà utilizzato stateless: Jade avvisa che la sessione è temporanea e le chiavi saranno “dimenticate” dal dispositivo allo spegnimento dello stesso.

![alt text](https://officinebitcoin.it/lezioni/jadespa/13.jpg)

Esportazione della chiave pubblica

Ora che Jade è configurato appositamente per lavorare fully airgapped, si passa alla delicata fase dell’esportazione della chiave pubblica.
 
Partendo sempre da Jade, che è tornato ai menu iniziali, scegliere Options.

![alt text](https://officinebitcoin.it/lezioni/jadespa/14.jpg)>

Nota: che Jade è in modalità Temporary Signer è visibile dall’icona che rappresenta un orologio accanto all’indicazione Active.

In Options, scegliere Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/15.jpg)

Quindi selezionare Export Xpub

![alt text](https://officinebitcoin.it/lezioni/jadespa/16.jpg)

A questo punto il display di Jade mostra un QR code dinamico che rappresenta la chiave pubblica estesa. In Options di questo sotto menu è possibile scegliere l’esportazione di un multisig/singlesig ed il derivation path.

Per questo tutorial si è scelto di esportare un singlesig full segwit.

![alt text](https://officinebitcoin.it/lezioni/jadespa/17.jpg)

È in questa fase che entra in gioco Sparrow. Lanciare il programma e creare un nuovo wallet scegliendo New Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/18.jpg)

Dare un nome al wallet, quindi cliccare su Create Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/19.jpg)

Nella schermata successiva dei settings, cliccare su Airgapped Hardware Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/20.jpg)

Si apre una finestra di Sparrow che mostra gli harware wallet implementati. Scegliere Jade

![alt text](https://officinebitcoin.it/lezioni/jadespa/21.jpg)

A questo punto si attiva la fotocamera del PC con il quale si sta operando.

![alt text](https://officinebitcoin.it/lezioni/jadespa/22.jpg)

Se si ha a disposizione più di una webcam, selezionare quella migliore dal menu a tendina ove compare Default Camera.

Riprendere ora il Jade (che nel frattempo sta continuando a mostrare il QR code dinamico rappresentante la Xpub) e piazzare il display davanti alla camera del PC, tenendo il QR code all’interno dello spazio tratteggiato.

![alt text](https://officinebitcoin.it/lezioni/jadespa/23.jpg)

Sotto all’immagine della fotocamera si trova una barra di scorrimento che si colora di blu.

L’avanzamento dell’acquisizione Xpub in Sparrow è segnalata in quel modo: da 0-100%

In questa fase possono essere necessari alcuni aggiustamenti: aumentare/diminuire la luminosità del display di Jade, così come la sua illuminazione frontale, oppure scegliere dal menu a tendina di Sparrow Use HD Capture o un abbassamento della risoluzione.

Non bisogna farsi spaventare da questi dettagli, una volta messo a posto il setup personale dell’ambiente di lavoro, queste fasi procederanno in completa comodità e scioltezza. (2)

Infatti l’esportazione è avvenuta quando si chiude la finestra della fotocamera e, tornando nei Settings di Sparrow, compaiono tutti i dati del wallet di visualizzazione.

![alt text](https://officinebitcoin.it/lezioni/jadespa/24.jpg)

Per la struttura di Sparrow è necessario ora applicare lo script policy cliccando Apply.

La creazione del wallet procede con l’inserimento e la conferma di una password di cifratura del file del wallet.

![alt text](https://officinebitcoin.it/lezioni/jadespa/25.jpg)

E si conclude quando la barra di scorrimento in basso a destra ha riempito il campo al 100%

![alt text](https://officinebitcoin.it/lezioni/jadespa/26.jpg)

## Transazione di spesa

Se, per ipotesi, Jade ricopre il ruolo di hardware wallet personale, si deve supporre che abbia dei fondi e che questi debbano essere spesi in futuro.

Dopo aver scelto Sparrow come wallet di visualizzazione e Jade come dispositivo di firma, vediamo come si costruisce, firma e propaga una transazione con questi due strumenti.

![alt text](https://officinebitcoin.it/lezioni/jadespa/27.jpg)

Nell’esempio è disponibile un saldo totale pari a 56,598 sats.

Nel menu a sinistra di Sparrow selezionare Send ed iniziare a costruire la transazione di spesa. Dopo avere impostato tutto cliccare in basso a destra Create transaction.

![alt text](https://officinebitcoin.it/lezioni/jadespa/28.jpg)

Compare una finestra di transazione avanzata, dove è visibile che Sparrow riconosce Jade come dispositivo di firma (Signing Wallet).

Se le impostazioni sono soddisfacenti, cliccare su Finalize Transaction.

![alt text](https://officinebitcoin.it/lezioni/jadespa/29.jpg)

Compare la schermata delle firme. In un sistema airgapped l’esportazione del .psbt avviene tramite QR code, pertanto su Sparrow cliccare in basso a sinistra Show QR.

![alt text](https://officinebitcoin.it/lezioni/jadespa/30.jpg)

Compare una finestra che mostra un QR code dinamico, rappresentante la psbt, che dovrà poi essere scansionato con la fotocamera di Jade.

![alt text](https://officinebitcoin.it/lezioni/jadespa/31.jpg)

Prendere Jade e dai menu principali selezionare Scan QR

![alt text](https://officinebitcoin.it/lezioni/jadespa/32.jpg)

Inquadrare il QR code dinamico che Sparrow sta generando con la fotocamera di Jade che ora si è attivata. Una barra di scorrimento blu sul display dell’hardware wallet indica la percentuale di completamento della lettura.

Una volta terminata l’importazione della psbt, Jade mostra i dettagli della transazione per la verifica: indirizzo di destinazione e importo in una prima schermata

![alt text](https://officinebitcoin.it/lezioni/jadespa/33.jpg)

e le fee in una seconda schermata. Confermando in quest’ultima, si appone la firma con Jade.

![alt text](https://officinebitcoin.it/lezioni/jadespa/34.jpg)

Automaticamente il display di Jade mostra un altro QR code dinamico: è la transazione firmata.

Tra le opzioni in questa schermata è possibile aumentare/abbassare la densità per una migliore comunicazione con il wallet app.

![alt text](https://officinebitcoin.it/lezioni/jadespa/35.jpg)

Nel frattempo Sparrow – che abbiamo lasciato mentre visualizzava un QR code dinamico – dev’essere impostato per ricevere la transazione firmata da propagare.

Si deve quindi cliccare su Scan QR per riattivare la webcam del PC.

![alt text](https://officinebitcoin.it/lezioni/jadespa/36.jpg)

Posizionare il display di Jade davanti alla webcam e lasciare che Sparrow importi la transazione firmata.

![alt text](https://officinebitcoin.it/lezioni/jadespa/37.jpg)

La barra di scorrimento sotto all’immagine deve completarsi al 100% fino ad avvenuta importazione, che Sparrow mostra come segue.

![alt text](https://officinebitcoin.it/lezioni/jadespa/38.jpg)

Ora si verifica di nuovo tutta la transazione e se va bene si può propagare cliccando Broadcast Transaction.

Nel menu Transactions compare la transazione in uscita

![alt text](https://officinebitcoin.it/lezioni/jadespa/39.png)

Note

- (1) – Se Jade è già inizializzato, basta andare nel menu Options → Settings → Factory reset
- (2) – Jade Original ha un display molto piccolo e – per inquadrare il QR code dinamico nello spazio tratteggiato che mostra Sparrow – è necessario avvicinare il display a pochi centimetri. Potrebbe quindi essere necessario dotarsi di una webcam ad altissima risoluzione e con una focale adatta, oppure affidarsi ad app come Iriun, per “trasformare” un cellulare nella camera del PC. I cellulari, infatti, hanno una capacità superiore di messa a fuoco a poca distanza.
