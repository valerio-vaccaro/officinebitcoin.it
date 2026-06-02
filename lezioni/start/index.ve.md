---
layout: default
title: "Piccolo glossario inizial"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lezion Bitcoin-only</span> <span>Sto progetto xe mantegnuo da valerio-vaccaro</span></p>

## 🌍 Traduzion

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](assets/cover.webp)


Ecco un bel modo de iniziar a doprar Bitcoin in na maniera più corretta possibile.
Quel che segue xe el suggerimento par uno *starter kit* tanto snello e facile da implementare in autonomia.

Che te te sia un utente curioso, un professionista che desidera accettar Bitcoin come metodo de pagamento o un utente esperto a la ricerca de soluzioni par amici e parenti, sta guida te permetarà de:
- scaricar e installar un wallet mobile, par l'utilizzo de Bitcoin ad ogni livello (onchain par la conservazion a lungo termine; opure Liquid, e Lightning par i pagamenti istantanei);
- configurare un POS par generar richieste de pagamento partendo dal prezzo dei to beni/servizi in Euro;
- conosser le configurazion avanzate del wallet. Abbiamo lasciato sta parte a la fine de la guida, par semplificare l'approccio iniziale, ma ti dai sempre un occhio a sta parte, perché xe importante.
- 
Ciariemo prima de tuto cosa si intende all'inizio, parlando de doprar Bitcoin in *maniera corretta*.

# Piccolo glossario inizial
- `Not your keys, not your coins`
  Se te stai approcciando a Bitcoin par la prima volta, la frase `Not your keys, not your coins` par te xe nuova e el suo significato si riduce a la mera traduzione letterale.
  Bitcoin funziona sul principio de la crittografia asimmetrica, basato su na serie de coppie de ciavi publiche e private. Xe co el possesso **unico** e la gestion individuale de le ciavi private che te poi dire de disporre dei to Bitcoin.
  
  Pertanto, te devi essere solo ti a conosser le ciavi private, el segreto che te permetterà de possedere ed eventualmente spender i bitcoin associadi a ste ciavi.
  `Not your keys, not your coins` xe praticamente un _mantra_ par i bitcoiner de tutto el mondo e el diventerà anca par te.

- `Recovery phrase`
  Durante la so breve storia, el protocollo Bitcoin si xe evoluto in modo da rendere più semplice la gestion del segreto, ovvero le ciavi private. Ancuo ste vengono rappresentate sotto forma de na sequenza de 12 o 24 parole de la lingua inglese, un modo più semplice par trascriverle e verificarle.
  Le parole xe el segreto principale da conservar. Devono essere trascritte su un supporto cartaceo e custodite in un luogo tanto sicuro, ad esempio na cassaforte. No devono mai essere fotografate, trasferite su un computer e - tanto meno - condivise co altri.

- `Wallet`
  El wallet, portafoglio, xe el strumento che te permetterà de visualizzare el tuo saldo, nonché accettar o spender Bitcoin. Nel corso de sto tutorial ne scaricheremo uno sul to telefono.
  El wallet sul telefono si chiama `hot wallet`,  in quanto ospitato su un dispositivo sempre connesso a internet. Se sei all'inizio va più che ben, imparerai co el studio altri metodi par perfezionare l'uso dei wallet.

- `Non Custodial`
  De fondamenta importanza xe iniziar ad doprar Bitcoin tramite wallet `non-custodial`, ovvero che te **lasciano el completo controllo sulle ciavi private**. Diffida sempre de chi te spingerà ad doprar strumenti diversi, cosiddetti custodial, par approcciarti a Bitcoin. I wallet custodial xe strumenti dei quali no possiedi le ciavi.
    No xe questione de **se**, ma de **quando** te impediranno par sempre l'accesso ai to fondi.

# Blockstream App (ex Green Wallet)
Par el starter kit scaricheremo Blockstream App, un wallet `open source` de cui te poi verificar el codice. L'aplicazion ha na lunga tradizione de sviluppo e na discreta storia a le spalle, el wallet si xe rivelato affidabile in passato.

---
⚠️ Le istruzion che segue xe dedicate al download e installazione dell'app par Android. Par iOS dopra necessariamente el store ufficiale.

---

Vai al link https://github.com/Blockstream/green_android che xe el repository Github ufficiale dello sviluppatore.

![img](assets/01.webp)

A metà pagina, su la destra, seleziona `Latest` nello spazio dedicato a le  *Releases*, par andar a scaricar la version più aggiornada.

Arriverai su na pagina che te mostrerà l'ultima release, 5.1.4 al momento de la stesura de sto tutorial a dicembre 2025.
Nella stessa pagina seleziona cosa te poi scaricar:

![img](assets/02.webp)

Scarica pure el file `.apk` senza dover passare dal Play Store e installalo sul to telefono Android.

![img](assets/03.webp)

---
⚠️ El to telefono potrebbe richiedere permessi particolari par scaricar app da fonti no certificate. Concedi ste autorizzazioni par continuare.

---
Quando Android te chiede de installar Blockstream App, clicca su `Install`.

![img](assets/04.webp)

A la fin dell'installazione, sielzi `Open`.

![img](assets/05.webp)

Si apre Blockstream App e par iniziar ad doprar el wallet, sielzi `Get Started`.

![img](assets/07.webp)

Blockstream te chiederà se vuoi partecipare ad na raccolta dati, par aiutare i sviluppatori a migliorare l'app. Declina l'invito.

![img](assets/08.webp)

# El to primo wallet
Puoi iniziar a creare el tuo primo wallet. Clicca su `Set Up Mobile Wallet`.

![img](assets/09.webp)

Inizia el processo de creazione del to wallet.

![img](assets/10.webp)

Che termina nel giro de pochi secondi. El tuo wallet xe pronto e, par iniziar ad usarlo, clicca su `Continue`.

![img](assets/11.webp)

El wallet si apre nella schermata denominata `Home`. Par el momento dai pure un'occhiata, ma dovresti concentrarti subito sul menu in basso `Security`.

# Your Keys, your coins

![img](assets/12.webp)

In sto menu infati te verrà proposto de fare el backup del to wallet. Altro no xe che la visualizzazione de la sequenza de 12 parole che te serviranno par ripristinarlo in futuro. Ste 12 parole xe el to wallet: **assicurati pertanto de essere in un ambiente sicuro, lontano da occhi indiscreti, avere un'agendina o un quaderno su cui trascriver le parole, prima de metterle al sicuro** (ad esempio in cassaforte).
Clicca su `Back Up Now` e scopri le 12 parole.

**Riporta anca l'ordine esatto de le parole: 1, 2, 3 ecc: scrivi pure le parole in stampatello maiuscolo, par na migliore visualizzazione futura ricordando però che, se dovrai inserirle a mano in futuro, dovrai doprar el stampatello minuscolo**.

![img](assets/13.webp)

Dopo aver trascritto e messo le parole al sicuro, procedi co el starter kit. Tute le altre configurazion le troverai a la fine de la guida.

# Menu TRANSACT
L'utilizzo del wallet xe estremamente semplificato:
- vai nel menu `Transact`
- due xe i comandi principali: `Send` e `Receive` (**ignora `Buy)**.

![img](assets/17.webp)

Quando avrai de le transazion, saranno visibili nella parte sotto ai comandi.
No avendo fondi, par iniziar ad averne te poi selezionare `Receive`.

Te compaiono na serie de *Asset*, ma concentrati solo su Bitcoin. Puoi sielziere tra Bitcoin onchain (icona arancione) e Liquid (icona blu) che xe quello che te permetterà de usufruire de pagamenti istantanei, come co Lightning Network, ma attraverso un meccanismo che vedremo in seguito.

Par iniziar, sielzi Bitcoin Onchain, l'icona arancione.

![img](assets/18.webp)

Ciò che te compare xe un QR code, che rappresenta uno dei to indirizzi Bitcoin, che vedi anca in basso denominato co `bc1q` seguito da altri caratteri.
Puoi mostrare el QR code ad na persona che te deve pagare, par ricevere i to primi fondi, ragionevolmente piccole frazioni de Bitcoin, dette anca `Satoshi`.

![img](assets/19.webp)


Se invece torni indietro e sielzi Liquid, el menu te segnala ⚡️**Lightning Ready**. 

Devi sapere infati che, sfruttando un servizio de `SWAP`, Blockstream App te permetterà de ricevere pagamenti quasi istantanei, emettere richieste de pagamento Lightning Network o pagare invoice LN, depositando/prelevando però i fondi da un account Liquid del tuo stesso wallet.

![img](assets/20.webp)

Nel menu che si apre dopo sta scelta, seleziona come vuoi ricevere i fondi, sielziendo tra Liquid e Lightning.
Se sielzi Liquid, te verrà mostrato un QR code simile a quello visualizzato sielziendo Bitcoin Onchain, che rappresenta un indirizzo riconossibile co el prefisso `lq1q` seguito da altri caratteri.

Se invece selezioni Lightning, te verrà chiesto de inserire l'importo che vuoi ricevere e confermare cliccando su `Confirm`.

![img](assets/21.webp)

Blockstream App te mostra un QR code che rappresenta l'invoice LN, che può essere pagata co qualsiasi wallet Lightning Network.

![img](assets/22.webp)

---
⚠️ Nella nostra simulazione, abbiamo chiesto de ricevere 210 sats, ma el QR code risultante, avvisa che riceveremo 160 sats.
I swap hanno infati un costo, circa 50 satoshi par ogni pagamento ricevuto.
**Xe importante tenere a mente sto aspetto, soprattutto in caso de ricezione de micro pagamenti**.
Nulla cambia par chi deve pagare, che infati vedrà decurtata la somma de la richiesta fatta in fase de impostazione: 210 satoshi.

---

# Sei un commerciante? Usa el POS
Par fare de sta guida uno uno **starter kit** che si rispetti, possiamo abbinare i incassi in Bitcoin su sto wallet, utilizzando un POS esterno.

Puoi configurarlo in pochi semplici passaggi direttamente al link https://btcpos.cash/.

![img](assets/23.webp)

Potrai così ricevere pagamenti Lightning direttamente sul tuo wallet creato su Blockstream App, condividere el link co i collaboratori e - par farlo - te basterà seguire i prossimi passi e creare un link da tenere poi a portata de click sulla home del tuo cellulare. Quello che te serve, xe copiare el `Descriptor` del to wallet e incollarlo nel grande spazio centrale che trovi al link.

# 1. Ricevi i primi fondi sulla rete Liquid
Xe necessario abilitare la visualizzazione dei *Asset* nella schermata home del to wallet. Se sto xe stato appena creato, te devi farti pagare na invoice LN o comunque ricevere fondi un su un indirizzo Liquid.

Dopo aver ricevuto i fondi, te poi selezionare Liquid tra i `Assets` che vedi nel menu `Home`.

![img](assets/24.webp)

# 2. Accedi ai parametri necessari
Ora hai a disposizione quanto serve par accedere ai parametri che te permetteranno de "trasportare" el to wallet sul POS. Tecnicamente si chiama *esportazione de la chiave pubblica* ed xe un tecnicismo che imparerai co el studio approfondito. 
Par ora sappi che, par farlo, te basta selezionare el menu in alto a destra:

![img](assets/25.webp)

E sielziere `Watch-only` nel menu a tendina comparso.
![img](assets/26.webp)


Appare `Output Descriptors`, che xe appunto el parametro che stiamo cercando. Copialo co el comando apposito e torna sulla pagina web dove stai configurando el POS.

![img](assets/27.webp)

# 3. Configura el POS
Incolla el descriptor nello spazio apposito e clicca `GENERATE POS LINK`.  Verrà creato dal sistema un URL unico, valido solo par te e par el to wallet.

![img](assets/28.webp)

Prima te poi anca impostare la valuta de riferimento, sielziendo tra USD, CHF e EUR nel menu a tendina dove appare `Currency`.
![img](assets/29.webp)

# 4. Incassa generando richieste de pagamento col POS
Na volta cliccato su `GENERATE POS LINK`, la pagina mostra el risultato: **el link xe stato creato co successo**.
Puoi copiarlo perché el link rimarrà sempre accessibile **solo par el to wallet** all'URL generato.

![img](assets/30.webp)

Puoi anca aprire el POS e iniziar ad usarlo:
![img](assets/31.webp)

Supponiamo, ad esempio de voler generar un'invoice da 3.351 sats, associando na descrizione. 

![img](assets/32.webp)

Cliccando su `CREATE INVOICE` el POS mostra el QR code o l'invoice testuale da sottoporre ad un eventuale cliente.

![img](assets/33.webp)

Quando el cliente ha pagato l'invoice, sulla quale leggerà correttamente anca la *descrizione* (Coppa del Nonno in sto caso), el POS segnala el pagamento ricevuto.


![img](assets/34.webp)

Che xe leggibile, correttamente, anca sul wallet!
![img](assets/35.webp)

Ora te basta memorizzare e tenere a portata de mano el link del POS, par utilizzarlo al momento del bisogno, anca sul cellulare dove hai installato el to wallet.

![img](assets/36.webp)

Aggiungendolo come link/app de la home

![img](assets/37.webp)

# ⚠️ NOTA IMPORTANTE

Se rileggi ben i passaggi appena compiuti, relativamente all'incasso dell'invoice in quest'ultimo esempio, notiamo due cose importanti:
1. al cliente xe stata mostrata na invoice da 3.351 sats
2. el nostro wallet ha incassato 3.293 sats.

Prima de gridare allo scandalo, xe necessario tornare a la schermata iniziale del POS, che mostra la dicitura che vedi nell'immagine sottostante: 

![img](assets/38.webp)

La differenza tra 3.351 (invoice sottoposta al cliente) e 3.293 (el tuo incasso) xe esattamente in sti termini:
- 50 sats par ogni invoice generata
- 0.25% come fee de servizio (8 sats = 0,25% de 3.351)
- Totale incassato: 3.293

#### Sei soltanto all'inizio e sto xe uno starter kit. Na piccola fee xe el compromesso par doprar Bitcoin in auto custodia, senza intermediari e usufruire de tutte le opportunità, anca i piccoli pagamenti istantanei. 

#### Co el studio imparerai ad doprar altri strumenti, che no richiederanno altre fee oltre a quelle previste pure par i utenti esperti.

---
# Altre impostazion

Xe arrivato el momento de conosser ben el tuo primo wallet. Le impostazion xe importanti, perché te aiuteranno nell'uso quotidiano.

## Menu
I menu de Blockstream App li trovi in basso e xe:
- Home
- Transact
- Security
- Settings

Continua a configurare el to wallet dal menu `Security`. Oltre a la possibilità de visualizzare e trascriver le parole de la `Recovery phrase`, sto menu te  mette a disposizione altre caratteristiche importanti.

Puoi impostare, ad esempio, el login al tuo wallet co el controllo biometrico (se impostato sul to telefono) o aggiungere anca un PIN a sei cifre par accedere al wallet.
Ste opzioni xe tanto importanti, perché impediscono ad estranei de accedere e visualizzare el to wallet, qualora abbiano in mano el tuo cellulare.


![img](assets/14.webp)

in sto menu te poi anca decidere el tempo de *Logout*, ovvero quando el wallet si disconnette dopo qualche minuto de inattività.  De default xe settato su *5 minuti* e te poi variare sto tempo a seconda de le to necessità, più lungo o più corto aggiustandolo in base a la tua manualità.
![img](assets/15.webp)
# Menu SETTINGS
Menu tanto importante perché contiene tutti i settings del wallet.
Cliccando in sto menu te poi ad esempio rinominare el wallet: nel nostro esempio el abbiamo chiamato *Starter Kit*. Rinominare i wallet, par distinguerli, xe tanto importante quando se ne usa più de uno sullo stesso dispositivo e si deve capire/sielziere quale doprar.

![img](assets/39.webp)

Se invece te sposti nel sotto-menu `Denomination`, te poi trovare impostazion utilissime riguardo la valuta.
![img](assets/40.webp)

Te consiglio de doprar `satoshi/sats` come unità par i importi in Bitcoin. El Satoshi xe l'unità più piccola del BTC, pari a un cento-milionesimo de Bitcoin.
Inoltre apparirà la scelta dell'exchange de riferimento par la conversion. Utilizzane uno che te permette de visualizzare e impostare i importi in Eur.

![img](assets/41.webp)

Infine, nel menu `Settings` te poi controllare la version attualmente in uso de Blockstream App e controllare se xe da aggiornare, nonché ci xe i comandi par chiedere supporto direttamente *in-app*.
![img](assets/42.webp)


# Menu HOME
La `Home` de Blockstream App, xe el menu dove si apre el to wallet ad ogni nuovo accesso.
Scorrendo verso el basso, troverai l'opzione par acquistare Bitcoin tramite un exchange integrato. **No usarlo**. 

![img](assets/16.webp)

# Ripristino del wallet

Se durante l'uso te dovessi accorgere che te devi cambiare telefono, o che hai l'esigenza de doprar el wallet *Starter Kit* su più de un dispositivo, co Blockstream App sappi che te poi farlo.

Par procedere, te basterà imparare la procedura de ripristino del wallet, come de seguito spiegata, che prevede i passi da compiere nel caso che dovessi perdere accesso al telefono dove hai iniziato ad doprar el wallet.

i to fondi, infati, no xe "sul dispositivo" cellulare, o "nel wallet". I fondi xe nella rete Bitcoin, sia essa Onchain, Lightning o Liquid. El wallet, par la precisione: le ciavi publiche e private del to wallet, xe el strumento par accedere agli indirizzi utilizzati e - co essi - al saldo associato.

Xe par sta procedura che hai trascritto le 12 parole e le hai messe in un posto sicuro... **El hai fatto vero?** Perché senza quelle parole, no avrai più accesso ai to fondi.

# a. Nuova installazione de Blockstream App
Par prima cosa, installa nuovamente Blockstream App co la procedura mostrata all'inizio. Potrebbe essere nel frattempo arrivata na release nuova, ti procedi co quella più aggiornada.

Lancia Blockstream App nel nuovo dispositivo e procedi sia cliccando `Get Started` che declinando l'offerta de la raccolta dati.

# b. Restore from backup
Le similitudini co la prima installazione si fermano qui.
Quando arriva la schermata de creazione del wallet, anziché sielziere `Set Up Mobile Wallet` come hai fatto la prima volta, sielzi `Restore from backup`.

![img](assets/43.webp)

Se stai usando la rete principale de Bitcoin, ovvero quella che utilizza fondi reali, nella schermata successiva sielzi `Mainnet`.

![img](assets/43.webp)

Te compare la schermata co le caselle dove immettere le parole de la `Recovery phrase`. Riscrivile in ordine e correttamente, poi selezion `Continue` par ricreare el wallet sul nuovo dispositivo.

![img](assets/45.webp)

La fase de ripristino del wallet potrebbe durare alcuni minuti, aspetta co pazienza che si concluda co successo. A la fine del processo, ritroverai el to wallet, co el saldo e la storia de le transazion.

![img](assets/46.webp)

---
⚠️ El wallet ricreato sul nuovo dispositivo, xe attivo al 100%.
Significa che possiede anca le ciavi private par spender. Ricordalo in caso volessi lasciarlo a qualche collaboratore par la tua attività.

**Piuttosto usa el link del POS par i collaboratori, perché xe stato creato co la sola chiave pubblica (el `descriptor`)**.

---

# Come continuare a imparare?

![img](assets/47.webp)
![img](assets/48.webp)
