# Jade airgapped con Sparrow Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/0.jpg)

Usar Jade par comunicazion completamente airgapped xe possibile, in virtù de le so caratteristiche firmware e hardware.

La fotocamera e el display integrà, in fatti, svolgen propi la funzion de acquisir e inviar messagi da e par el wallet de visualizazion.

Quest tutorial mostra come usar Jade airgapped con Sparrow Wallet.

La procedura preved prima el setup, poeu l'esportazion de la chiave publica estesa da Jade a Sparrow-visualizazion e, in fin, na transazion de spesa.

Par scelta didattica s'è scernuo de cominciar mostrando la sequenza de operazion partendo dal Jade.

## Advanced Setup

La scelta de usar el dispositiv airgapped comporta un ver e propri setup, ovvero va fado al moment de l'inizializazion de Jade (1) che dev donca presentarse minga inizializzao.

![alt text](https://officinebitcoin.it/lezioni/jadespa/1.jpg)

Compar l'avvis de controllar le istruzion de setup dal sito https://blockstream.com/jade/.

![alt text](https://officinebitcoin.it/lezioni/jadespa/2.jpg)

La configurazion de Jade par l'utilizz airgapped se pò far solo scernendo Advanced Setup.

![alt text](https://officinebitcoin.it/lezioni/jadespa/3.jpg)

Jade avvisa che quest setup presenta quaj caratteristiche tecniche avanzae. L'è sufficient prestar la massima atenzion e cliccar sul tast de conferma

![alt text](https://officinebitcoin.it/lezioni/jadespa/4.jpg)

Nell'ottica de inserir la mnemonica generata con l'entropia de i dadi, scerni Restore Wallet.

![alt text](https://officinebitcoin.it/lezioni/jadespa/5.jpg)

Se dev ora impostar la longhezza de la mnemonica, 12 o 24 parole. El menu ofer anca la possibilitaa de ripristinar el wallet scansionando un QR code: se tratta del SeedQr che xe stà tradao nel tutorial dedicao al Setup.

![alt text](https://officinebitcoin.it/lezioni/jadespa/6.jpg)

Par na question prettamente didattica e de velocitaa, quest tutorial mostra el setup con na mnemonica de 12 parole.

El passaggio seguente xe da seguir come descrito, par poder acceder a la funzionalitaa airgapped. Se dev in fatti scernir de esportar la recovery phrase in formato CompactSeedQR, scernendo Yes.

![alt text](https://officinebitcoin.it/lezioni/jadespa/7.jpg)

Dopo la scelta se ven avvisai che se dev disegnar el QR code sul template fornio nella scatola, come mostao nella sezion "Extra" de la lezion dedicao al Setup.

![alt text](https://officinebitcoin.it/lezioni/jadespa/8.jpg)

Al termen de la procedura se dev proceder a la verific de la corrispondenza tra quanto disegnao e el CompactSeedQR mostao dal dispositiv. In fatti, se abilita la fotocamera incorporata de Jade con la quala se dev inquadrar el SeedQR appena disegnao.

![alt text](https://officinebitcoin.it/lezioni/jadespa/9.jpg)

Se el disegno corrisponde a quanto proponuo dal dispositiv nella procedura appena compia, ven visualizao el segnal de conferma.

![alt text](https://officinebitcoin.it/lezioni/jadespa/10.jpg)

Ecco che adesso Jade mostra le opzion par la connession del dispositiv a na companion app: scerni QR.

![alt text](https://officinebitcoin.it/lezioni/jadespa/11.jpg)

Anca el passo seguente richiede na scelta da parte de l'utente: salvar le chiavi criptae sul dispositiv oppur cargarle a ogni session, scansionando el SeedQR appena disegnao

![alt text](https://officinebitcoin.it/lezioni/jadespa/12.jpg)

N.B.

L'è util comprendere queste do opzion de access:

- QR PIN Unlock: Durante l'inizializazion, Jade salvarà i dati del wallet criptandoli sul dispositiv; saran sempre accessibili sbloccando Jade con la procedura del QR PIN.
- SeedQR: el SeedQR va scansionao da Jade ogni volta che se desidera cargar le chiavi sul dispositiv.

Par scelta didattica, nell'opzion precedenta s'è scernuo SeedQR, pertanto el dispositiv vegnarà utilizzao stateless: Jade avvisa che la session xe temporanea e le chiavi vegnarà "dimentegae" dal dispositiv al spegnimento del medemo.

![alt text](https://officinebitcoin.it/lezioni/jadespa/13.jpg)

Esportazion de la chiave publica

Ora che Jade xe configurà appositamente par lavorar fully airgapped, se passa a la delicada fase de l'esportazion de la chiave publica.
 
Partendo sempre da Jade, che xe tornao ai menu inissiali, scerni Options.

![alt text](https://officinebitcoin.it/lezioni/jadespa/14.jpg)>

Nota: che Jade xe in modalitaa Temporary Signer xe visibile dall'icona che rappresenta un orologio accanto a l'indicazion Active.

In Options, scerni Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/15.jpg)

Donca scerni Export Xpub

![alt text](https://officinebitcoin.it/lezioni/jadespa/16.jpg)

A quest punt el display de Jade mostra un QR code dinamic che rappresenta la chiave publica estesa. In Options de quest sot menu xe possibil scernir l'esportazion de un multisig/singlesig ed el derivation path.

Par quest tutorial s'è scernuo de esportar un singlesig full segwit.

![alt text](https://officinebitcoin.it/lezioni/jadespa/17.jpg)

L'è in questa fase che entra in gioco Sparrow. Lancia el programma e crea un novo wallet scernendo New Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/18.jpg)

Dà un nome al wallet, donca clicca su Create Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/19.jpg)

Nella schermada seguenta dei settings, clicca su Airgapped Hardware Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/20.jpg)

Se ver na finestra de Sparrow che mostra i harware wallet implementai. Scerni Jade

![alt text](https://officinebitcoin.it/lezioni/jadespa/21.jpg)

A quest punt se attiva la fotocamera del PC con el qual se sta operando.

![alt text](https://officinebitcoin.it/lezioni/jadespa/22.jpg)

Se se ghe a disposizion pù de na webcam, scerni quella mej dal menu a tendina ove compar Default Camera.

Riprend ora el Jade (che nel frattempo xe continuando a mostrar el QR code dinamic rappresentante la Xpub) e piazza el display davanti a la camera del PC, tenendo el QR code denter al spazi tratteggiao.

![alt text](https://officinebitcoin.it/lezioni/jadespa/23.jpg)

Sotto a l'imagin de la fotocamera se trova na barra de scorrimento che se colora de blu.

L'avanzamento de l'acquisizion Xpub in Sparrow xe segnalao in quel modo: da 0-100%

In questa fase pò esser necessari quaj aggiustamento: aumentar/diminuir la luminositaa del display de Jade, inscì come la so illuminazion frontale, oppur scernir dal menu a tendina de Sparrow Use HD Capture o un abbassamento de la risoluzion.

Se dev minga fass spaventar de questi dettagli, na volta metto a posto el setup personal de l'ambient de lavor, queste fase procederà in completa comoditaa e scioltezza. (2)

In fatti l'esportazion xe avvenua quand se sara la finestra de la fotocamera e, tornando nei Settings de Sparrow, compar tuti i dati del wallet de visualizazion.

![alt text](https://officinebitcoin.it/lezioni/jadespa/24.jpg)

Par la struttura de Sparrow xe necessari ora aplicar lo script policy cliccando Apply.

La creazion del wallet proced con l'inserimento e la conferma de na password de cifratura del file del wallet.

![alt text](https://officinebitcoin.it/lezioni/jadespa/25.jpg)

E se conclud quand la barra de scorrimento in bass a destra xe riempia el camp al 100%

![alt text](https://officinebitcoin.it/lezioni/jadespa/26.jpg)

## Transazion de spesa

Se, par ipotesi, Jade ricopre el rol de hardware wallet personal, se dev suppon che ghe n'abbia de fondi e che questi debba esser spesi in futuro.

Dopo aver scernuo Sparrow come wallet de visualizazion e Jade come dispositiv de firma, vedemo come se costruisse, firma e propaga na transazion con questi do strumenti.

![alt text](https://officinebitcoin.it/lezioni/jadespa/27.jpg)

Nell'esempi xe disponibil un saldo total pari a 56,598 sats.

Nel menu a sinistra de Sparrow scerni Send ed cominciar a costruir la transazion de spesa. Dopo aver impostà tuto clicca in bass a destra Create transaction.

![alt text](https://officinebitcoin.it/lezioni/jadespa/28.jpg)

Compar na finestra de transazion avanzaa, dove xe visibile che Sparrow riconosse Jade come dispositiv de firma (Signing Wallet).

Se le impostazion xe soddisfacenti, clicca su Finalize Transaction.

![alt text](https://officinebitcoin.it/lezioni/jadespa/29.jpg)

Compar la schermada de le firme. In un sistema airgapped l'esportazion del .psbt avven tramite QR code, pertanto su Sparrow clicca in bass a sinistra Show QR.

![alt text](https://officinebitcoin.it/lezioni/jadespa/30.jpg)

Compar na finestra che mostra un QR code dinamic, rappresentante la psbt, che dovarà poeu esser scansionao con la fotocamera de Jade.

![alt text](https://officinebitcoin.it/lezioni/jadespa/31.jpg)

Preni Jade e dai menu principal scerni Scan QR

![alt text](https://officinebitcoin.it/lezioni/jadespa/32.jpg)

Inquadrar el QR code dinamic che Sparrow xe generando con la fotocamera de Jade che ora s'è attivada. Na barra de scorrimento blu sul display de l'hardware wallet indica la percentuale de completamento de la lettura.

Na volta terminada l'importazion de la psbt, Jade mostra i dettagli de la transazion par la verific: indiriso de destinazion e importo in na prima schermada

![alt text](https://officinebitcoin.it/lezioni/jadespa/33.jpg)

e le fee in na seconda schermada. Confermando in quest'ultima, se appone la firma con Jade.

![alt text](https://officinebitcoin.it/lezioni/jadespa/34.jpg)

Automaticamente el display de Jade mostra un altro QR code dinamic: xe la transazion firmata.

Tra le opzion in questa schermada xe possibil aumentar/abbassar la densitaa par na mej comunicazion con el wallet app.

![alt text](https://officinebitcoin.it/lezioni/jadespa/35.jpg)

Nel frattempo Sparrow – che avemo lassà mentre visualizzava un QR code dinamic – dev esser impostao par ricever la transazion firmada da propagar.

Se dev donca cliccar su Scan QR par riattivar la webcam del PC.

![alt text](https://officinebitcoin.it/lezioni/jadespa/36.jpg)

Posiziona el display de Jade davanti a la webcam e lassa che Sparrow importi la transazion firmada.

![alt text](https://officinebitcoin.it/lezioni/jadespa/37.jpg)

La barra de scorrimento sotto a l'imagin dev completarse al 100% fin a avvenuda importazion, che Sparrow mostra come segue.

![alt text](https://officinebitcoin.it/lezioni/jadespa/38.jpg)

Ora se verifica de novo tuta la transazion e se va ben se pò propagar cliccando Broadcast Transaction.

Nel menu Transactions compar la transazion in uscita

![alt text](https://officinebitcoin.it/lezioni/jadespa/39.png)

Note

- (1) – Se Jade xe già inizializzao, basta andar nel menu Options → Settings → Factory reset
- (2) – Jade Original xe un display molto piccol e – par inquadrar el QR code dinamic nello spazi tratteggiao che mostra Sparrow – xe necessario avvicinar el display a pochi centimetri. Poderà esser quindi necessario dotarse de na webcam ad altissima risoluzion e con na focale adatta, oppur affidarse a app come Iriun, par "trasformar" un cellulao nella camera del PC. I cellulaa, in fatti, ghe na capacità superiore de messa a fuoco a poca distanza. 