# Jade con Electrum Wallet

![alt text](https://officinebitcoin.it/lezioni/jadeele/0_cover.jpg)

Dopo aver inizializzato Jade, è possibile iniziare ad usarlo e – per farlo – bisogna scegliere un wallet di visualizzazione.

Jade è un dispositivo che può essere usato con diversi wallet, o companion app come le specifica Blockstream sul suo sito.

In questo tutorial si vedranno le fasi di utilizzo, via USB, con Electrum Wallet.

Si prenda il Jade inizializzato. Appena acceso si presenta così:


![alt text](https://officinebitcoin.it/lezioni/jadeele/001.jpg)

Selezionando Unlock Jade, compare il menu in cui si deve scegliere come connettere il dispositivo alla companion app.

Con Electrum è possibile connettere Jade solo via USB, che va quindi scelto.

Lanciare Electrum, che si aprirà proponendo come opzione di default l’apertura dell’ultimo wallet utilizzato.

Se è la prima volta che si connette Jade ad Electrum, selezionare Create New Wallet e poi Finish.

![alt text](https://officinebitcoin.it/lezioni/jadeele/1.jpg)

Dare un nome al wallet, ad es. Jade_Officine.

![alt text](https://officinebitcoin.it/lezioni/jadeele/3.jpg)

Selezionare Standard Wallet

![alt text](https://officinebitcoin.it/lezioni/jadeele/4.jpg)

Nella scelta del keystore è fondamentale selezionare Use a hardware device.

![alt text](https://officinebitcoin.it/lezioni/jadeele/5.jpg)

Electrum inizia la scansione alla ricerca del dispositivo hardware

![alt text](https://officinebitcoin.it/lezioni/jadeele/6.jpg)

Collegando l’USB al PC (già connesso dalla parte dell’USB C a Jade), l’hardware wallet mostra la schermata di blocco. Jade si sblocca mettendo il PIN a sei cifre impostato durante il setup


![alt text](https://officinebitcoin.it/lezioni/jadeele/7.jpg)

Sbloccato il dispositivo Hardware, Electrum rileva Jade. Proseguire cliccando Next.

![alt text](https://officinebitcoin.it/lezioni/jadeele/8.jpg)

A questo punto Electrum chiede di impostare lo script policy, si scelga Native Segwit.

![alt text](https://officinebitcoin.it/lezioni/jadeele/9.jpg)

Inizia la fase del trasferimento della chiave pubblica dal wallet su Jade a Electrum-visualizzazione.

![alt text](https://officinebitcoin.it/lezioni/jadeele/10.jpg)

al termine dell’esportazione della chiave pubblica, il procedimento è terminato.

Il watch-only è pronto ed Electrum avvisa del completamento con la schermata che segue.

![alt text](https://officinebitcoin.it/lezioni/jadeele/11.jpg)

Il wallet è effettivamente creato ed è possibile iniziare ad esplorarlo: si vedono gli addresses, le wallet information e – soprattutto – è possibile notare in basso a destra l’indicazione che si tratta di un wallet creato da Blockstream Jade. Il pallino verde accanto al logo Blockstream indica che il dispositivo è acceso e connesso correttamente.

![alt text](https://officinebitcoin.it/lezioni/jadeele/12.jpg)

Transazioni di ricezione e di spesa

Dal menu Receive di Electrum, generare uno scriptPubKey (indirizzo) per ricevere dei fondi. Iniziare sempre con un importo piccolo e fare un test di ricezione+spesa.

![alt text](https://officinebitcoin.it/lezioni/jadeele/13.jpg)

Ricevuti i sats se ne può controllare l’arrivo nel menu History.

![alt text](https://officinebitcoin.it/lezioni/jadeele/14.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeele/15.jpg)

Una volta confermata la transazione, si può spendere questo UTXO e terminare il test.

La spesa prevederà l’utilizzo di Jade per firmare.

Andare nel menu Send di Electrum, incollare uno scriptPubKey e controllarlo bene.

![alt text](https://officinebitcoin.it/lezioni/jadeele/16.jpg)

Una volta terminato premere Pay.

Si apre la finestra di transazione, nella quale è importante impostare le corrette fee di transazione. Finiti tutti i settaggi cliccare su Preview in basso a destra.

![alt text](https://officinebitcoin.it/lezioni/jadeele/17.jpg)

La finestra di transazione mostra alcuni dettagli importanti, primo fra tutti lo status: Unsigned.

In questa fase è possibile vedere anche il comando Sign, proprio per apporre la firma con Jade.

![alt text](https://officinebitcoin.it/lezioni/jadeele/18.jpg)

Electrum avvisa di seguire le istruzioni sul dispositivo hardware, il quale è pronto per firmare.

Prima, però, è meglio verificare cosa si sta firmando: tutti i parametri della transazione appena impostata, compaiono anche su Jade ed è possibile verificarli tutti.

![alt text](https://officinebitcoin.it/lezioni/jadeele/19.jpg)

Per proseguire accertarsi di posizionare il cursore sempre sulla freccina → che porta alle fasi successive e mai sulla “X” che cancella l’operazione.

La visualizzazione delle verifiche termina quando Jade mostra le fee. A questo punto la conferma equivale a mettere la firma.

![alt text](https://officinebitcoin.it/lezioni/jadeele/20.jpg)

Per un breve istante Jade processa la firma.

![alt text](https://officinebitcoin.it/lezioni/jadeele/21.jpg)

Mentre su Electrum è possibile constatare lo status della transazione, che da Unsigned è cambiato in Signed e adesso è possibile propagare la transazione cliccando Broadcast.

![alt text](https://officinebitcoin.it/lezioni/jadeele/22.jpg)

Il wallet, così testato, è utilizzabile per ricevere UTXO destinati ad essere conservati in modo sicuro.

![alt text](https://officinebitcoin.it/lezioni/jadeele/23.jpg)
