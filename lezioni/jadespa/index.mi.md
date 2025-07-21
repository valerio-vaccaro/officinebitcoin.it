# Jade airgapped con Sparrow Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/0.jpg)

Usà Jade per comunicazion completament airgapped l'è possibil, in virtù de le so caratteristich firmware e hardware.

La fotocamera e el display integrà, in fatti, svolg hinn propi la funzion de acquisì e invià messagg da e per el wallet de visualizzazion.

Quest tutorial mostra come usà Jade airgapped con Sparrow Wallet.

La procedura preved prima el setup, poeu l'esportazion de la chiav publica estesa da Jade a Sparrow-visualizzazion e, in fin, una transazion de spesa.

Per scelta didattica s'è scernuu de comincià mostrand la sequenza de operazion partend dal Jade.

## Advanced Setup

La scelta de usà el dispositiv airgapped comporta un ver e propri setup, ovvero va fada al moment de l'inizializzazion de Jade (1) che dev donca presentass minga inizializzaa.

![alt text](https://officinebitcoin.it/lezioni/jadespa/1.jpg)

Compar l'avvis de controllà le istruzion de setup dal sit https://blockstream.com/jade/.

![alt text](https://officinebitcoin.it/lezioni/jadespa/2.jpg)

La configurazion de Jade per l'utilizz airgapped se pö fà domà scernend Advanced Setup.

![alt text](https://officinebitcoin.it/lezioni/jadespa/3.jpg)

Jade avvisa che quest setup presenta quaj caratteristich tecnich avanzaa. L'è sufficient prestà la massima attenzion e cliccà sul tast de conferma

![alt text](https://officinebitcoin.it/lezioni/jadespa/4.jpg)

Nell'ottica de inserì la mnemonica generata con l'entropia de i dad, scernì Restore Wallet.

![alt text](https://officinebitcoin.it/lezioni/jadespa/5.jpg)

Se dev ora impostà la longhezza de la mnemonica, 12 o 24 paroll. El menu ofer anca la possibilitaa de ripristinà el wallet scansionand un QR code: se tratta del SeedQr che l'è staa tradaa nel tutorial dedicaa al Setup.

![alt text](https://officinebitcoin.it/lezioni/jadespa/6.jpg)

Per una question prettament didattica e de velocitaa, quest tutorial mostra el setup con una mnemonica de 12 paroll.

El passagg seguent l'è da seguì come descritt, per podè acced a la funzionalitaa airgapped. Se dev in fatti scernì de esportà la recovery phrase in format CompactSeedQR, scernend Yes.

![alt text](https://officinebitcoin.it/lezioni/jadespa/7.jpg)

Dopo la scelta se ven avvisaa che se dev disegnà el QR code sul template fornii nella scatola, come mostaa nella sezion "Extra" de la lezion dedicaa al Setup.

![alt text](https://officinebitcoin.it/lezioni/jadespa/8.jpg)

Al termen de la procedura se dev proced a la verific de la corrispondenza tra quant disegnaa e el CompactSeedQR mostaa dal dispositiv. In fatti, se abilita la fotocamera incorporata de Jade con la quala se dev inquadrà el SeedQR appena disegnaa.

![alt text](https://officinebitcoin.it/lezioni/jadespa/9.jpg)

Se el disegn corrispond a quant proponuu dal dispositiv nella procedura appena compia, ven visualizzaa el segnal de conferma.

![alt text](https://officinebitcoin.it/lezioni/jadespa/10.jpg)

Ecco che adess Jade mostra le opzion per la connession del dispositiv a una companion app: scernì QR.

![alt text](https://officinebitcoin.it/lezioni/jadespa/11.jpg)

Anca el pass seguent richied una scelta da part de l'utent: salvà le chiav criptaa sul dispositiv oppur cargàle a ogni session, scansionand el SeedQR appena disegnaa

![alt text](https://officinebitcoin.it/lezioni/jadespa/12.jpg)

N.B.

L'è util comprend quest duu opzion de access:

- QR PIN Unlock: Durant l'inizializzazion, Jade salvarà i dat del wallet criptandoli sul dispositiv; saran semper accessibil sbloccand Jade con la procedura del QR PIN.
- SeedQR: el SeedQR va scansionaa da Jade ogni volta che se desidera cargà le chiav sul dispositiv.

Per scelta didattica, nell'opzion precedenta s'è scernuu SeedQR, pertant el dispositiv vegnarà utilizzaa stateless: Jade avvisa che la session l'è temporanea e le chiav vegnarann "dimentegaa" dal dispositiv al spegniment del medem.

![alt text](https://officinebitcoin.it/lezioni/jadespa/13.jpg)

Esportazion de la chiav publica

Ora che Jade l'è configuraa appositament per lavorà fully airgapped, se passa a la delicada fase de l'esportazion de la chiav publica.
 
Partend semper da Jade, che l'è tornaa ai menu inizial, scernì Options.

![alt text](https://officinebitcoin.it/lezioni/jadespa/14.jpg)>

Nota: che Jade l'è in modalitaa Temporary Signer l'è visibil dall'icona che rappresenta un orolog accant a l'indicazion Active.

In Options, scernì Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/15.jpg)

Donca scernì Export Xpub

![alt text](https://officinebitcoin.it/lezioni/jadespa/16.jpg)

A quest punt el display de Jade mostra un QR code dinamic che rappresenta la chiav publica estesa. In Options de quest sot menu l'è possibil scernì l'esportazion de un multisig/singlesig ed el derivation path.

Per quest tutorial s'è scernuu de esportà un singlesig full segwit.

![alt text](https://officinebitcoin.it/lezioni/jadespa/17.jpg)

L'è in questa fase che entra in gioc Sparrow. Lancià el program e creà un noeuv wallet scernend New Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/18.jpg)

Dà un nom al wallet, donca cliccà su Create Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/19.jpg)

Nella schermada seguenta dei settings, cliccà su Airgapped Hardware Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/20.jpg)

Se ver una finestra de Sparrow che mostra i harware wallet implementaa. Scernì Jade

![alt text](https://officinebitcoin.it/lezioni/jadespa/21.jpg)

A quest punt se attiva la fotocamera del PC con el qual se sta operand.

![alt text](https://officinebitcoin.it/lezioni/jadespa/22.jpg)

Se se gh'ha a disposizion pù de una webcam, scernì quella mej dal menu a tendina ove compar Default Camera.

Riprend ora el Jade (che nel frattemp l'è continuand a mostrà el QR code dinamic rappresentant la Xpub) e piazzà el display davant a la camera del PC, tenend el QR code denter al spazi tratteggiaa.

![alt text](https://officinebitcoin.it/lezioni/jadespa/23.jpg)

Sott a l'imagin de la fotocamera se trova una barra de scorriment che se colora de blu.

L'avanzament de l'acquisizion Xpub in Sparrow l'è segnalaa in quel mod: da 0-100%

In questa fase pö vess necessari quaj aggiustament: aumentà/diminuì la luminositaa del display de Jade, inscì come la so illuminazion frontala, oppur scernì dal menu a tendina de Sparrow Use HD Capture o un abbassament de la risoluzion.

Se dev minga fass spaventà de quest dettagli, una volta mett a post el setup personal de l'ambient de lavor, queste fase procederann in completa comoditaa e scioltezza. (2)

In fatti l'esportazion l'è avvenuda quand se sara la finestra de la fotocamera e, tornand nei Settings de Sparrow, compar tutt i dat del wallet de visualizzazion.

![alt text](https://officinebitcoin.it/lezioni/jadespa/24.jpg)

Per la struttura de Sparrow l'è necessari ora aplicà lo script policy cliccand Apply.

La creazion del wallet proced con l'inseriment e la conferma de una password de cifratura del file del wallet.

![alt text](https://officinebitcoin.it/lezioni/jadespa/25.jpg)

E se conclud quand la barra de scorriment in bass a destra l'ha riempii el camp al 100%

![alt text](https://officinebitcoin.it/lezioni/jadespa/26.jpg)

## Transazion de spesa

Se, per ipotesi, Jade ricopr el rol de hardware wallet personal, se dev suppon che ghe n'abia de fond e che quest debbann vess spess in futur.

Dopo avè scernuu Sparrow come wallet de visualizzazion e Jade come dispositiv de firma, vedom come se costruiss, firma e propaga una transazion con quest duu strument.

![alt text](https://officinebitcoin.it/lezioni/jadespa/27.jpg)

Nell'esempi l'è disponibil un sald total pari a 56,598 sats.

Nel menu a sinistra de Sparrow scernì Send ed comincià a costruì la transazion de spesa. Dopo avè impostà tutt cliccà in bass a destra Create transaction.

![alt text](https://officinebitcoin.it/lezioni/jadespa/28.jpg)

Compar una finestra de transazion avanzaa, ove l'è visibil che Sparrow riconoss Jade come dispositiv de firma (Signing Wallet).

Se le impostazion hinn soddisfacent, cliccà su Finalize Transaction.

![alt text](https://officinebitcoin.it/lezioni/jadespa/29.jpg)

Compar la schermada de le firme. In un sistem airgapped l'esportazion del .psbt avven tramit QR code, pertant su Sparrow cliccà in bass a sinistra Show QR.

![alt text](https://officinebitcoin.it/lezioni/jadespa/30.jpg)

Compar una finestra che mostra un QR code dinamic, rappresentant la psbt, che dovarà poeu vess scansionaa con la fotocamera de Jade.

![alt text](https://officinebitcoin.it/lezioni/jadespa/31.jpg)

Prenì Jade e dai menu principal scernì Scan QR

![alt text](https://officinebitcoin.it/lezioni/jadespa/32.jpg)

Inquadrà el QR code dinamic che Sparrow l'è generand con la fotocamera de Jade che ora s'è attivada. Una barra de scorriment blu sul display de l'hardware wallet indica la percentual de completament de la lettura.

Una volta terminata l'importazion de la psbt, Jade mostra i dettagli de la transazion per la verific: indirizz de destinazion e import in una prima schermada

![alt text](https://officinebitcoin.it/lezioni/jadespa/33.jpg)

e le fee in una seconda schermada. Confermand in quest'ultima, se appon la firma con Jade.

![alt text](https://officinebitcoin.it/lezioni/jadespa/34.jpg)

Automaticament el display de Jade mostra un alter QR code dinamic: l'è la transazion firmaa.

Tra le opzion in questa schermada l'è possibil aumentà/abbassà la densitaa per una mej comunicazion con el wallet app.

![alt text](https://officinebitcoin.it/lezioni/jadespa/35.jpg)

Nel frattemp Sparrow – che hinn lassaa menter visualizzava un QR code dinamic – dev vess impostaa per ricev la transazion firmaa da propagà.

Se dev donca cliccà su Scan QR per riattivà la webcam del PC.

![alt text](https://officinebitcoin.it/lezioni/jadespa/36.jpg)

Posizionà el display de Jade davant a la webcam e lassà che Sparrow importi la transazion firmaa.

![alt text](https://officinebitcoin.it/lezioni/jadespa/37.jpg)

La barra de scorriment sott a l'imagin dev completass al 100% fin a avvenuda importazion, che Sparrow mostra come segu.

![alt text](https://officinebitcoin.it/lezioni/jadespa/38.jpg)

Ora se verifica de noeuv tutta la transazion e se va ben se pö propagà cliccand Broadcast Transaction.

Nel menu Transactions compar la transazion in uscita

![alt text](https://officinebitcoin.it/lezioni/jadespa/39.png)

Note

- (1) – Se Jade l'è già inizializzaa, basta andà nel menu Options → Settings → Factory reset
- (2) – Jade Original l'ha un display molt piccol e – per inquadrà el QR code dinamic nello spazi tratteggiaa che mostra Sparrow – l'è necessari avvicinà el display a poch centimetr. Poderess donca vess necessari dotass de una webcam ad altissima risoluzion e con una focala adatta, oppur affidass a app come Iriun, per "trasformà" un cellulaa nella camera del PC. I cellulaa, in fatti, hann una capacitaa superior de messa a fuoc a poca distanza. 