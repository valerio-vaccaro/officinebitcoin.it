![cover](assets/cover.webp)


Ecco un bel modo di iniziare a usare Bitcoin in una maniera più corretta possibile.
Quello che segue è il suggerimento per uno *starter kit* molto snello e facile da implementare in autonomia.

Che tu sia un utente curioso, un professionista che desidera accettare Bitcoin come metodo di pagamento o un utente esperto alla ricerca di soluzioni per amici e parenti, questa guida ti permetterà di:
- scaricare e installare un wallet mobile, per l'utilizzo di Bitcoin ad ogni livello (onchain per la conservazione a lungo termine; oppure Liquid, e Lightning per i pagamenti istantanei);
- configurare un POS per generare richieste di pagamento partendo dal prezzo dei tuoi beni/servizi in Euro;
- conoscere le configurazioni avanzate del wallet. Abbiamo lasciato questa parte alla fine della guida, per semplificare l'approccio iniziale, ma tu dai sempre un occhio a questa parte, perché è importante.
- 
Chiariamo innanzitutto cosa si intende all'inizio, parlando di usare Bitcoin in *maniera corretta*.

# Piccolo glossario iniziale
- `Not your keys, not your coins`
  Se ti stai approcciando a Bitcoin per la prima volta, la frase `Not your keys, not your coins` per te è nuova e il suo significato si riduce alla mera traduzione letterale.
  Bitcoin funziona sul principio della crittografia asimmetrica, basato su una serie di coppie di chiavi pubbliche e private. È con il possesso **unico** e la gestione individuale delle chiavi private che puoi dire di disporre dei tuoi Bitcoin.
  
  Pertanto, devi essere solo tu a conoscere le chiavi private, il segreto che ti permetterà di possedere ed eventualmente spendere i bitcoin associati a queste chiavi.
  `Not your keys, not your coins` è praticamente un _mantra_ per i bitcoiner di tutto il mondo e lo diventerà anche per te.

- `Recovery phrase`
  Durante la sua breve storia, il protocollo Bitcoin si è evoluto in modo da rendere più semplice la gestione del segreto, ovvero le chiavi private. Oggi queste vengono rappresentate sotto forma di una sequenza di 12 o 24 parole della lingua inglese, un modo più semplice per trascriverle e verificarle.
  Le parole sono il segreto principale da conservare. Devono essere trascritte su un supporto cartaceo e custodite in un luogo molto sicuro, ad esempio una cassaforte. Non devono mai essere fotografate, trasferite su un computer e - tanto meno - condivise con altri.

- `Wallet`
  Il wallet, portafoglio, è lo strumento che ti permetterà di visualizzare il tuo saldo, nonché accettare o spendere Bitcoin. Nel corso di questo tutorial ne scaricheremo uno sul tuo telefono.
  Il wallet sul telefono si chiama `hot wallet`,  in quanto ospitato su un dispositivo sempre connesso a internet. Se sei all'inizio va più che bene, imparerai con lo studio altri metodi per perfezionare l'uso dei wallet.

- `Non Custodial`
  Di fondamentale importanza è iniziare ad utilizzare Bitcoin tramite wallet `non-custodial`, ovvero che ti **lasciano il completo controllo sulle chiavi private**. Diffida sempre di chi ti spingerà ad usare strumenti diversi, cosiddetti custodial, per approcciarti a Bitcoin. I wallet custodial sono strumenti dei quali non possiedi le chiavi.
    Non è questione di **se**, ma di **quando** ti impediranno per sempre l'accesso ai tuoi fondi.

# Blockstream App (ex Green Wallet)
Per lo starter kit scaricheremo Blockstream App, un wallet `open source` di cui puoi verificare il codice. L'applicazione ha una lunga tradizione di sviluppo e una discreta storia alle spalle, il wallet si è rivelato affidabile in passato.

---
⚠️ Le istruzioni che seguono sono dedicate al download e installazione dell'app per Android. Per iOS usa necessariamente lo store ufficiale.

---

Vai al link https://github.com/Blockstream/green_android che è il repository Github ufficiale dello sviluppatore.

![img](assets/01.webp)

A metà pagina, sulla destra, seleziona `Latest` nello spazio dedicato alle  *Releases*, per andare a scaricare la versione più aggiornata.

Arriverai su una pagina che ti mostrerà l'ultima release, 5.1.4 al momento della stesura di questo tutorial a dicembre 2025.
Nella stessa pagina seleziona cosa puoi scaricare:

![img](assets/02.webp)

Scarica pure il file `.apk` senza dover passare dal Play Store e installalo sul tuo telefono Android.

![img](assets/03.webp)

---
⚠️ Il tuo telefono potrebbe richiedere permessi particolari per scaricare app da fonti non certificate. Concedi queste autorizzazioni per continuare.

---
Quando Android ti chiede di installare Blockstream App, clicca su `Install`.

![img](assets/04.webp)

Al termine dell'installazione, scegli `Open`.

![img](assets/05.webp)

Si apre Blockstream App e per iniziare ad usare il wallet, scegli `Get Started`.

![img](assets/07.webp)

Blockstream ti chiederà se vuoi partecipare ad una raccolta dati, per aiutare gli sviluppatori a migliorare l'app. Declina l'invito.

![img](assets/08.webp)

# Il tuo primo wallet
Puoi iniziare a creare il tuo primo wallet. Clicca su `Set Up Mobile Wallet`.

![img](assets/09.webp)

Inizia il processo di creazione del tuo wallet.

![img](assets/10.webp)

Che termina nel giro di pochi secondi. Il tuo wallet è pronto e, per iniziare ad usarlo, clicca su `Continue`.

![img](assets/11.webp)

Il wallet si apre nella schermata denominata `Home`. Per il momento dai pure un'occhiata, ma dovresti concentrarti subito sul menu in basso `Security`.

# Your Keys, your coins

![img](assets/12.webp)

In questo menu infatti ti verrà proposto di fare il backup del tuo wallet. Altro non è che la visualizzazione della sequenza di 12 parole che ti serviranno per ripristinarlo in futuro. Queste 12 parole sono il tuo wallet: **assicurati pertanto di essere in un ambiente sicuro, lontano da occhi indiscreti, avere un'agendina o un quaderno su cui trascrivere le parole, prima di metterle al sicuro** (ad esempio in cassaforte).
Clicca su `Back Up Now` e scopri le 12 parole.

**Riporta anche l'ordine esatto delle parole: 1, 2, 3 ecc: scrivi pure le parole in stampatello maiuscolo, per una migliore visualizzazione futura ricordando però che, se dovrai inserirle a mano in futuro, dovrai usare lo stampatello minuscolo**.

![img](assets/13.webp)

Dopo aver trascritto e messo le parole al sicuro, procedi con lo starter kit. Tutte le ulteriori configurazioni le troverai alla fine della guida.

# Menu TRANSACT
L'utilizzo del wallet è estremamente semplificato:
- vai nel menu `Transact`
- due sono i comandi principali: `Send` e `Receive` (**ignora `Buy)**.

![img](assets/17.webp)

Quando avrai delle transazioni, saranno visibili nella parte sotto ai comandi.
Non avendo fondi, per iniziare ad averne puoi selezionare `Receive`.

Ti compaiono una serie di *Asset*, ma concentrati solo su Bitcoin. Puoi scegliere tra Bitcoin onchain (icona arancione) e Liquid (icona blu) che è quello che ti permetterà di usufruire di pagamenti istantanei, come con Lightning Network, ma attraverso un meccanismo che vedremo in seguito.

Per iniziare, scegli Bitcoin Onchain, l'icona arancione.

![img](assets/18.webp)

Ciò che ti compare è un QR code, che rappresenta uno dei tuoi indirizzi Bitcoin, che vedi anche in basso denominato con `bc1q` seguito da altri caratteri.
Puoi mostrare il QR code ad una persona che ti deve pagare, per ricevere i tuoi primi fondi, ragionevolmente piccole frazioni di Bitcoin, dette anche `Satoshi`.

![img](assets/19.webp)


Se invece torni indietro e scegli Liquid, il menu ti segnala ⚡️**Lightning Ready**. 

Devi sapere infatti che, sfruttando un servizio di `SWAP`, Blockstream App ti permetterà di ricevere pagamenti quasi istantanei, emettere richieste di pagamento Lightning Network o pagare invoice LN, depositando/prelevando però i fondi da un account Liquid del tuo stesso wallet.

![img](assets/20.webp)

Nel menu che si apre dopo questa scelta, seleziona come vuoi ricevere i fondi, scegliendo tra Liquid e Lightning.
Se scegli Liquid, ti verrà mostrato un QR code simile a quello visualizzato scegliendo Bitcoin Onchain, che rappresenta un indirizzo riconoscibile con il prefisso `lq1q` seguito da altri caratteri.

Se invece selezioni Lightning, ti verrà chiesto di inserire l'importo che vuoi ricevere e confermare cliccando su `Confirm`.

![img](assets/21.webp)

Blockstream App ti mostra un QR code che rappresenta l'invoice LN, che può essere pagata con qualsiasi wallet Lightning Network.

![img](assets/22.webp)

---
⚠️ Nella nostra simulazione, abbiamo chiesto di ricevere 210 sats, ma il QR code risultante, avvisa che riceveremo 160 sats.
Gli swap hanno infatti un costo, circa 50 satoshi per ogni pagamento ricevuto.
**È importante tenere a mente questo aspetto, soprattutto in caso di ricezione di micro pagamenti**.
Nulla cambia per chi deve pagare, che infatti vedrà decurtata la somma della richiesta fatta in fase di impostazione: 210 satoshi.

---

# Sei un commerciante? Usa il POS
Per fare di questa guida uno uno **starter kit** che si rispetti, possiamo abbinare gli incassi in Bitcoin su questo wallet, utilizzando un POS esterno.

Puoi configurarlo in pochi semplici passaggi direttamente al link https://btcpos.cash/.

![img](assets/23.webp)

Potrai così ricevere pagamenti Lightning direttamente sul tuo wallet creato su Blockstream App, condividere il link con i collaboratori e - per farlo - ti basterà seguire i prossimi passi e creare un link da tenere poi a portata di click sulla home del tuo cellulare. Quello che ti serve, è copiare il `Descriptor` del tuo wallet e incollarlo nel grande spazio centrale che trovi al link.

# 1. Ricevi i primi fondi sulla rete Liquid
È necessario abilitare la visualizzazione degli *Asset* nella schermata home del tuo wallet. Se questo è stato appena creato, devi farti pagare una invoice LN o comunque ricevere fondi un su un indirizzo Liquid.

Dopo aver ricevuto i fondi, puoi selezionare Liquid tra gli `Assets` che vedi nel menu `Home`.

![img](assets/24.webp)

# 2. Accedi ai parametri necessari
Ora hai a disposizione quanto serve per accedere ai parametri che ti permetteranno di "trasportare" il tuo wallet sul POS. Tecnicamente si chiama *esportazione della chiave pubblica* ed è un tecnicismo che imparerai con lo studio approfondito. 
Per ora sappi che, per farlo, ti basta selezionare il menu in alto a destra:

![img](assets/25.webp)

E scegliere `Watch-only` nel menu a tendina comparso.
![img](assets/26.webp)


Appare `Output Descriptors`, che è appunto il parametro che stiamo cercando. Copialo con il comando apposito e torna sulla pagina web dove stai configurando il POS.

![img](assets/27.webp)

# 3. Configura il POS
Incolla il descriptor nello spazio apposito e clicca `GENERATE POS LINK`.  Verrà creato dal sistema un URL unico, valido solo per te e per il tuo wallet.

![img](assets/28.webp)

Prima puoi anche impostare la valuta di riferimento, scegliendo tra USD, CHF e EUR nel menu a tendina dove appare `Currency`.
![img](assets/29.webp)

# 4. Incassa generando richieste di pagamento col POS
Una volta cliccato su `GENERATE POS LINK`, la pagina mostra il risultato: **il link è stato creato con successo**.
Puoi copiarlo perché il link rimarrà sempre accessibile **solo per il tuo wallet** all'URL generato.

![img](assets/30.webp)

Puoi anche aprire il POS e iniziare ad usarlo:
![img](assets/31.webp)

Supponiamo, ad esempio di voler generare un'invoice da 3.351 sats, associando una descrizione. 

![img](assets/32.webp)

Cliccando su `CREATE INVOICE` il POS mostra il QR code o l'invoice testuale da sottoporre ad un eventuale cliente.

![img](assets/33.webp)

Quando il cliente ha pagato l'invoice, sulla quale leggerà correttamente anche la *descrizione* (Coppa del Nonno in questo caso), il POS segnala il pagamento ricevuto.


![img](assets/34.webp)

Che è leggibile, correttamente, anche sul wallet!
![img](assets/35.webp)

Ora ti basta memorizzare e tenere a portata di mano il link del POS, per utilizzarlo al momento del bisogno, anche sul cellulare dove hai installato il tuo wallet.

![img](assets/36.webp)

Aggiungendolo come link/app della home

![img](assets/37.webp)

# ⚠️ NOTA IMPORTANTE

Se rileggi bene i passaggi appena compiuti, relativamente all'incasso dell'invoice in quest'ultimo esempio, notiamo due cose importanti:
1. al cliente è stata mostrata una invoice da 3.351 sats
2. il nostro wallet ha incassato 3.293 sats.

Prima di gridare allo scandalo, è necessario tornare alla schermata iniziale del POS, che mostra la dicitura che vedi nell'immagine sottostante: 

![img](assets/38.webp)

La differenza tra 3.351 (invoice sottoposta al cliente) e 3.293 (il tuo incasso) è esattamente in questi termini:
- 50 sats per ogni invoice generata
- 0.25% come fee di servizio (8 sats = 0,25% di 3.351)
- Totale incassato: 3.293

#### Sei soltanto all'inizio e questo è uno starter kit. Una piccola fee è il compromesso per utilizzare Bitcoin in auto custodia, senza intermediari e usufruire di tutte le opportunità, anche i piccoli pagamenti istantanei. 

#### Con lo studio imparerai ad utilizzare altri strumenti, che non richiederanno altre fee oltre a quelle previste pure per gli utenti esperti.

---
# Altre impostazioni

È arrivato il momento di conoscere bene il tuo primo wallet. Le impostazioni sono importanti, perché ti aiuteranno nell'uso quotidiano.

## Menu
I menu di Blockstream App li trovi in basso e sono:
- Home
- Transact
- Security
- Settings

Continua a configurare il tuo wallet dal menu `Security`. Oltre alla possibilità di visualizzare e trascrivere le parole della `Recovery phrase`, questo menu ti  mette a disposizione altre caratteristiche importanti.

Puoi impostare, ad esempio, il login al tuo wallet con il controllo biometrico (se impostato sul tuo telefono) o aggiungere anche un PIN a sei cifre per accedere al wallet.
Queste opzioni sono molto importanti, perché impediscono ad estranei di accedere e visualizzare il tuo wallet, qualora abbiano in mano il tuo cellulare.


![img](assets/14.webp)

in questo menu puoi anche decidere il tempo di *Logout*, ovvero quando il wallet si disconnette dopo qualche minuto di inattività.  Di default è settato su *5 minuti* e puoi variare questo tempo a seconda delle tue necessità, più lungo o più corto aggiustandolo in base alla tua manualità.
![img](assets/15.webp)
# Menu SETTINGS
Menu molto importante perché contiene tutti i settings del wallet.
Cliccando in questo menu puoi ad esempio rinominare il wallet: nel nostro esempio lo abbiamo chiamato *Starter Kit*. Rinominare i wallet, per distinguerli, è molto importante quando se ne usa più di uno sullo stesso dispositivo e si deve capire/scegliere quale utilizzare.

![img](assets/39.webp)

Se invece ti sposti nel sotto-menu `Denomination`, puoi trovare impostazioni utilissime riguardo la valuta.
![img](assets/40.webp)

Ti consiglio di utilizzare `satoshi/sats` come unità per gli importi in Bitcoin. Il Satoshi è l'unità più piccola del BTC, pari a un cento-milionesimo di Bitcoin.
Inoltre apparirà la scelta dell'exchange di riferimento per la conversione. Utilizzane uno che ti permette di visualizzare e impostare gli importi in Eur.

![img](assets/41.webp)

Infine, nel menu `Settings` puoi controllare la versione attualmente in uso di Blockstream App e controllare se è da aggiornare, nonché ci sono i comandi per chiedere supporto direttamente *in-app*.
![img](assets/42.webp)


# Menu HOME
La `Home` di Blockstream App, è il menu dove si apre il tuo wallet ad ogni nuovo accesso.
Scorrendo verso il basso, troverai l'opzione per acquistare Bitcoin tramite un exchange integrato. **Non usarlo**. 

![img](assets/16.webp)

# Ripristino del wallet

Se durante l'uso ti dovessi accorgere che devi cambiare telefono, o che hai l'esigenza di utilizzare il wallet *Starter Kit* su più di un dispositivo, con Blockstream App sappi che puoi farlo.

Per procedere, ti basterà imparare la procedura di ripristino del wallet, come di seguito spiegata, che prevede i passi da compiere nel caso che dovessi perdere accesso al telefono dove hai iniziato ad usare il wallet.

i tuoi fondi, infatti, non sono "sul dispositivo" cellulare, o "nel wallet". I fondi sono nella rete Bitcoin, sia essa Onchain, Lightning o Liquid. Il wallet, per la precisione: le chiavi pubbliche e private del tuo wallet, sono lo strumento per accedere agli indirizzi utilizzati e - con essi - al saldo associato.

È per questa procedura che hai trascritto le 12 parole e le hai messe in un posto sicuro... **Lo hai fatto vero?** Perché senza quelle parole, non avrai più accesso ai tuoi fondi.

# a. Nuova installazione di Blockstream App
Per prima cosa, installa nuovamente Blockstream App con la procedura mostrata all'inizio. Potrebbe essere nel frattempo arrivata una release nuova, tu procedi con quella più aggiornata.

Lancia Blockstream App nel nuovo dispositivo e procedi sia cliccando `Get Started` che declinando l'offerta della raccolta dati.

# b. Restore from backup
Le similitudini con la prima installazione si fermano qui.
Quando arriva la schermata di creazione del wallet, anziché scegliere `Set Up Mobile Wallet` come hai fatto la prima volta, scegli `Restore from backup`.

![img](assets/43.webp)

Se stai usando la rete principale di Bitcoin, ovvero quella che utilizza fondi reali, nella schermata successiva scegli `Mainnet`.

![img](assets/43.webp)

Ti compare la schermata con le caselle dove immettere le parole della `Recovery phrase`. Riscrivile in ordine e correttamente, poi selezione `Continue` per ricreare il wallet sul nuovo dispositivo.

![img](assets/45.webp)

La fase di ripristino del wallet potrebbe durare alcuni minuti, aspetta con pazienza che si concluda con successo. Alla fine del processo, ritroverai il tuo wallet, con il saldo e la storia delle transazioni.

![img](assets/46.webp)

---
⚠️ Il wallet ricreato sul nuovo dispositivo, è attivo al 100%.
Significa che possiede anche le chiavi private per spendere. Ricordalo in caso volessi lasciarlo a qualche collaboratore per la tua attività.

**Piuttosto usa il link del POS per i collaboratori, perché è stato creato con la sola chiave pubblica (il `descriptor`)**.

---

# Come continuare a imparare?

![img](assets/47.webp)
![img](assets/48.webp)