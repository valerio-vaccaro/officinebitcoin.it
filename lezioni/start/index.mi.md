---
layout: default
title: "Piccol glossari inizial"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lezion Bitcoin-only</span> <span>Quest progett l'e mantegnuu da valerio-vaccaro</span></p>

## 🌍 Traduzion

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](assets/cover.webp)


Ecco on bell mod de inizià a doprà Bitcoin in ona maniera più corretta possibile.
Quell che seguita l'è el suggerimento per uno *starter kit* assai snello e facil da implementare in autonomia.

Che te te sia on utent curioso, on professionista che desidera accettà Bitcoin come metodo de pagament o on utent esperto a la ricerca de soluzion per amici e parenti, questa guida la te permetterà de:
- scaricà e installà on wallet mobile, per l'utilizzo de Bitcoin ad ogni livello (onchain per la conservazion a lungo termine; oppur Liquid, e Lightning per i pagament istantanei);
- configurare on POS per generà richieste de pagament partendo dal prezzo di tò beni/servizi in Euro;
- conoss i configurazion avanzate del wallet. Abbiamo lasciato questa parte a la fine de la guida, per semplificare l'approccio iniziale, ma ti dai semper on occhio a questa parte, perché l'è important.
- 
Ciariom prima de tutt cosa si intende all'inizio, parlando de doprà Bitcoin in *maniera corretta*.

# Piccol glossari inizial
- `Not your keys, not your coins`
  Se te stai approcciando a Bitcoin per la prima volta, la frase `Not your keys, not your coins` per te l'è nuova e el suo significato si riduce a la mera traduzion letterale.
  Bitcoin funziona sul principio de la crittografia asimmetrica, basato su ona serie de coppie de ciav pubbliche e private. L'è con el possesso **unico** e la gestion individuale di ciav private che te pödet dire de disporre di tò Bitcoin.
  
  Pertanto, te gh'heet de essere domà ti a conoss i ciav private, el segreto che te permetterà de possedere ed eventualmente spend i bitcoin associad a queste ciav.
  `Not your keys, not your coins` l'è praticamente on _mantra_ per i bitcoiner de tutto el mond e el diventerà anca per te.

- `Recovery phrase`
  Durant la soa breva storia, el protocollo Bitcoin si l'è evoluto in modo da rendere più sempliz la gestion del segreto, ovver i ciav private. Incoeu queste vengono rappresentate sotto forma de ona sequenza de 12 o 24 paroll de la lingua inglese, on modo più sempliz per trascriverle e verificarle.
  I paroll hinn el segreto principale da conservà. Devono essere trascritte su on supporto cartaceo e custodite in on luogo assai segur, ad esempio ona cassaforte. Minga devono mai essere fotografate, trasferite su on computer e - tanto meno - condivise con altri.

- `Wallet`
  El wallet, portafoglio, l'è el strument che te permetterà de visualizzare el tuo saldo, nonché accettà o spend Bitcoin. Nel corso de quest tutorial ne scaricheremo uno sul tò telefon.
  El wallet sul telefon si chiama `hot wallet`,  in quanto ospitato su on dispositivo semper connesso a internet. Se sei all'inizio va più che ben, imparerai con el studio altri metodi per perfezionare l'uso di wallet.

- `Non Custodial`
  De fondamental importanza l'è inizià ad doprà Bitcoin tramite wallet `non-custodial`, ovver che te **lasciano el completo controllo sulle ciav private**. Diffida semper de chi te spingerà ad doprà strument diversi, cosiddetti custodial, per approcciarti a Bitcoin. I wallet custodial hinn strument di quali minga possiedi i ciav.
    Minga l'è questione de **se**, ma de **quand** te impediranno per semper l'accesso ai tò fond.

# Blockstream App (ex Green Wallet)
Per el starter kit scaricheremo Blockstream App, on wallet `open source` de cui te pödet verificà el codis. L'applicazion ha ona lunga tradizion de sviluppo e ona discreta storia a le spalle, el wallet si l'è rivelato affidabile in passato.

---
⚠️ I istruzion che seguiten hinn dedicate al download e installazion dell'app per Android. Per iOS dopra necessariament el store ufficial.

---

Vai al link https://github.com/Blockstream/green_android che l'è el repository Github ufficial dello sviluppatore.

![img](assets/01.webp)

A metà pagina, su la drita, seleziona `Latest` nello spazio dedicato a le  *Releases*, per andà a scaricà la version più aggiornada.

Arriverai su ona pagina che te mostrerà l'ultima release, 5.1.4 al momento de la stesura de quest tutorial a dicembre 2025.
Nella stessa pagina seleziona cosa te pödet scaricà:

![img](assets/02.webp)

Scarica pure el file `.apk` senza dover passare dal Play Store e installalo sul tò telefon Android.

![img](assets/03.webp)

---
⚠️ El tò telefon potrebbe richiedere permessi particolari per scaricà app da fonti minga certificate. Concedi queste autorizzazion per continuare.

---
Quand Android te chiede de installà Blockstream App, clicca su `Install`.

![img](assets/04.webp)

A la fin dell'installazion, serniss `Open`.

![img](assets/05.webp)

Si apre Blockstream App e per inizià ad doprà el wallet, serniss `Get Started`.

![img](assets/07.webp)

Blockstream te chiederà se vuoi partecipare ad ona raccolta dati, per aiutare i sviluppatori a migliorare l'app. Declina l'invito.

![img](assets/08.webp)

# El tò prim wallet
Puoi inizià a creare el tuo primo wallet. Clicca su `Set Up Mobile Wallet`.

![img](assets/09.webp)

Inizia el processo de creazion del tò wallet.

![img](assets/10.webp)

Che termina nel giro de pochi secondi. El tuo wallet l'è pronto e, per inizià ad usarlo, clicca su `Continue`.

![img](assets/11.webp)

El wallet si apre nella schermata denominata `Home`. Per adess dai pure un'occhiata, ma dovresti concentrarti subito sul menu in basso `Security`.

# Your Keys, your coins

![img](assets/12.webp)

In quest menu infatti te verrà proposto de fare el backup del tò wallet. Altro minga l'è che la visualizzazion de la sequenza de 12 paroll che te serviranno per ripristinarlo in futuro. Queste 12 paroll hinn el tò wallet: **assegurati pertanto de essere in on ambiente segur, lontano da occhi indiscreti, avere un'agendina o on quaderno su cui trascriv i paroll, prima de metterle al segur** (ad esempio in cassaforte).
Clicca su `Back Up Now` e scopri i 12 paroll.

**Riporta anca l'ordine esatto di paroll: 1, 2, 3 ecc: scrivi pure i paroll in stampatello maiuscolo, per ona migliore visualizzazion futura ricordando però che, se dovrai inserirle a mano in futuro, dovrai doprà el stampatello minuscolo**.

![img](assets/13.webp)

Dopo aver trascritto e messo i paroll al segur, procedi con el starter kit. Tutt i alter configurazion i troverai a la fine de la guida.

# Menu TRANSACT
L'utilizzo del wallet l'è estremamente semplificato:
- vai nel menu `Transact`
- due hinn i comandi principali: `Send` e `Receive` (**ignora `Buy)**.

![img](assets/17.webp)

Quand avrai di transazion, saranno visibili nella parte sotto ai comandi.
Minga avendo fond, per inizià ad averne te pödet selezionare `Receive`.

Te compaiono ona serie de *Asset*, ma concentrati domà su Bitcoin. Puoi sernissere tra Bitcoin onchain (icona arancione) e Liquid (icona blu) che l'è quello che te permetterà de usufruire de pagament istantanei, come con Lightning Network, ma attraverso on meccanismo che vedremo in seguito.

Per inizià, serniss Bitcoin Onchain, l'icona arancione.

![img](assets/18.webp)

Ciò che te compare l'è on QR code, che rappresenta uno di tò indirizzi Bitcoin, che vedi anca in basso denominato con `bc1q` seguito da altri caratteri.
Puoi mostrare el QR code ad ona persona che te deve pagare, per ricevere i tò primi fond, ragionevolmente piccole frazion de Bitcoin, dette anca `Satoshi`.

![img](assets/19.webp)


Se invece torni indietro e serniss Liquid, el menu te segnala ⚡️**Lightning Ready**. 

Devi sapere infatti che, sfruttando on servizio de `SWAP`, Blockstream App te permetterà de ricevere pagament quasi istantanei, emettere richieste de pagament Lightning Network o pagare invoice LN, depositando/prelevando però i fond da on account Liquid del tuo stesso wallet.

![img](assets/20.webp)

Nel menu che si apre dopo questa scelta, seleziona come vuoi ricevere i fond, sernissendo tra Liquid e Lightning.
Se serniss Liquid, te verrà mostrato on QR code simile a quello visualizzato sernissendo Bitcoin Onchain, che rappresenta on indirizzo riconossbile con el prefisso `lq1q` seguito da altri caratteri.

Se invece selezion Lightning, te verrà chiesto de inserire l'importo che vuoi ricevere e confermare cliccando su `Confirm`.

![img](assets/21.webp)

Blockstream App te mostra on QR code che rappresenta l'invoice LN, che può essere pagata con qualsiasi wallet Lightning Network.

![img](assets/22.webp)

---
⚠️ Nella nostra simulazion, abbiamo chiesto de ricevere 210 sats, ma el QR code risultante, avvisa che riceveremo 160 sats.
I swap hanno infatti on costo, circa 50 satoshi per ogni pagament ricevuto.
**L'è important tenere a mente quest aspetto, soprattutto in caso de ricezion de micro pagament**.
Nulla cambia per chi deve pagare, che infatti vedrà decurtata la somma de la richiesta fatta in fase de impostazion: 210 satoshi.

---

# Sei on commerciante? Usa el POS
Per fare de questa guida uno uno **starter kit** che si rispetti, possiamo abbinare i incassi in Bitcoin su quest wallet, utilizzando on POS esterno.

Puoi configurarlo in pochi semplici passaggi direttamente al link https://btcpos.cash/.

![img](assets/23.webp)

Potrai così ricevere pagament Lightning direttamente sul tuo wallet creato su Blockstream App, condividere el link con i collaboratori e - per farlo - te basterà seguire i prossimi passi e creare on link da tenere poi a portata de click sulla home del tuo cellulare. Quello che te serve, l'è copiare el `Descriptor` del tò wallet e incollarlo nel grande spazio centrale che trovi al link.

# 1. Ricevi i primi fond sulla rete Liquid
L'è necessario abilitare la visualizzazion di *Asset* nella schermata home del tò wallet. Se quest l'è stato appena creato, te gh'heet de farti pagare ona invoice LN o comunque ricevere fond on su on indirizzo Liquid.

Dopo aver ricevuto i fond, te pödet selezionare Liquid tra i `Assets` che vedi nel menu `Home`.

![img](assets/24.webp)

# 2. Accedi ai parametri necessari
Ora hai a disposizion quanto serve per accedere ai parametri che te permetteranno de "trasportare" el tò wallet sul POS. Tecnicamente si chiama *esportazion de la chiave pubblica* ed l'è on tecnicismo che imparerai con el studio approfondito. 
Per ora sappi che, per farlo, te basta selezionare el menu in alto a destra:

![img](assets/25.webp)

E sernissere `Watch-only` nel menu a tendina comparso.
![img](assets/26.webp)


Appare `Output Descriptors`, che l'è appunto el parametro che stiamo cercando. Copialo con el comando apposito e torna sulla pagina web indoe stai configurando el POS.

![img](assets/27.webp)

# 3. Configura el POS
Incolla el descriptor nello spazio apposito e clicca `GENERATE POS LINK`.  Verrà creato dal sistema on URL unico, valido domà per te e per el tò wallet.

![img](assets/28.webp)

Prima te pödet anca impostare la valuta de riferimento, sernissendo tra USD, CHF e EUR nel menu a tendina indoe appare `Currency`.
![img](assets/29.webp)

# 4. Incassa generando richieste de pagament col POS
Ona volta cliccato su `GENERATE POS LINK`, la pagina mostra el risultato: **el link l'è stato creato con successo**.
Puoi copiarlo perché el link rimarrà semper accessibile **domà per el tò wallet** all'URL generato.

![img](assets/30.webp)

Puoi anca aprire el POS e inizià ad usarlo:
![img](assets/31.webp)

Supponiamo, ad esempio de voler generà un'invoice da 3.351 sats, associando ona descrizion. 

![img](assets/32.webp)

Cliccando su `CREATE INVOICE` el POS mostra el QR code o l'invoice testuale da sottoporre ad on eventuale cliente.

![img](assets/33.webp)

Quand el cliente ha pagato l'invoice, sulla quale leggerà correttamente anca la *descrizion* (Coppa del Nonno in quest caso), el POS segnala el pagament ricevuto.


![img](assets/34.webp)

Che l'è leggibile, correttamente, anca sul wallet!
![img](assets/35.webp)

Ora te basta memorizzare e tenere a portata de mano el link del POS, per utilizzarlo al momento del bisogno, anca sul cellulare indoe hai installato el tò wallet.

![img](assets/36.webp)

Aggiungendolo come link/app de la home

![img](assets/37.webp)

# ⚠️ NOTA IMPORTANTE

Se rileggi ben i passaggi appena compiuti, relativamente all'incasso dell'invoice in quest'ultimo esempio, notiamo due cose importanti:
1. al cliente l'è stata mostrata ona invoice da 3.351 sats
2. el nostro wallet ha incassato 3.293 sats.

Prima de gridare allo scandalo, l'è necessario tornare a la schermata iniziale del POS, che mostra la dicitura che vedi nell'immagine sottostante: 

![img](assets/38.webp)

La differenza tra 3.351 (invoice sottoposta al cliente) e 3.293 (el tuo incasso) l'è esattamente in questi termini:
- 50 sats per ogni invoice generata
- 0.25% come fee de servizio (8 sats = 0,25% de 3.351)
- Totale incassato: 3.293

#### Sei soltanto all'inizio e quest l'è uno starter kit. Ona piccola fee l'è el compromesso per doprà Bitcoin in auto custodia, senza intermediari e usufruire de tutte i opportunità, anca i piccoli pagament istantanei. 

#### Con el studio imparerai ad doprà altri strument, che minga richiederanno altre fee oltre a quelle previste pure per i utent esperti.

---
# Altre impostazion

L'è arrivato el momento de conoss ben el tuo primo wallet. I impostazion hinn importanti, perché te aiuteranno nell'uso quotidiano.

## Menu
I menu de Blockstream App li trovi in basso e hinn:
- Home
- Transact
- Security
- Settings

Continua a configurare el tò wallet dal menu `Security`. Oltre a la possibilità de visualizzare e trascriv i paroll de la `Recovery phrase`, quest menu te  mette a disposizion altre caratteristiche importanti.

Puoi impostare, ad esempio, el login al tuo wallet con el controllo biometrico (se impostato sul tò telefon) o aggiungere anca on PIN a sei cifre per accedere al wallet.
Queste opzion hinn assai importanti, perché impediscono ad estranei de accedere e visualizzare el tò wallet, qualora abbiano in mano el tuo cellulare.


![img](assets/14.webp)

in quest menu te pödet anca decidere el tempo de *Logout*, ovver quand el wallet si disconnette dopo qualche minuto de inattività.  De default l'è settato su *5 minuti* e te pödet variare quest tempo a seconda deli tò necessità, più lungo o più corto aggiustandolo in base a la tua manualità.
![img](assets/15.webp)
# Menu SETTINGS
Menu assai important perché contiene tutti i settings del wallet.
Cliccando in quest menu te pödet ad esempio rinominare el wallet: nel nostro esempio el abbiamo chiamato *Starter Kit*. Rinominare i wallet, per distinguerli, l'è assai important quand se ne usa più de uno sullo stesso dispositivo e si deve capire/sernissere quale doprà.

![img](assets/39.webp)

Se invece te sposti nel sotto-menu `Denomination`, te pödet trovare impostazion utilissime riguardo la valuta.
![img](assets/40.webp)

Te consiglio de doprà `satoshi/sats` come unità per i importi in Bitcoin. El Satoshi l'è l'unità più piccola del BTC, pari a on cento-milionesimo de Bitcoin.
Inoltre apparirà la scelta dell'exchange de riferimento per la conversion. Utilizzane uno che te permette de visualizzare e impostare i importi in Eur.

![img](assets/41.webp)

Infine, nel menu `Settings` te pödet controllare la version attualmente in uso de Blockstream App e controllare se l'è da aggiornare, nonché ci hinn i comandi per chiedere supporto direttamente *in-app*.
![img](assets/42.webp)


# Menu HOME
La `Home` de Blockstream App, l'è el menu indoe si apre el tò wallet ad ogni nuovo accesso.
Scorrendo verso el basso, troverai l'opzion per acquistare Bitcoin tramite on exchange integrato. **Minga usarlo**. 

![img](assets/16.webp)

# Ripristino del wallet

Se durante l'uso te dovessi accorgere che te gh'heet de cambiare telefon, o che hai l'esigenza de doprà el wallet *Starter Kit* su più de on dispositivo, con Blockstream App sappi che te pödet farlo.

Per procedere, te basterà imparare la procedura de ripristino del wallet, come de seguito spiegata, che prevede i passi da compiere nel caso che dovessi perdere accesso al telefon indoe hai iniziato ad doprà el wallet.

i tò fond, infatti, minga hinn "sul dispositivo" cellulare, o "nel wallet". I fond hinn nella rete Bitcoin, sia essa Onchain, Lightning o Liquid. El wallet, per la precisione: i ciav pubbliche e private del tò wallet, hinn el strument per accedere agli indirizzi utilizzati e - con essi - al saldo associato.

L'è per questa procedura che hai trascritto i 12 paroll e i hai messe in on posto segur... **El hai fatto vero?** Perché senza quelle paroll, minga avrai più accesso ai tò fond.

# a. Nuova installazion de Blockstream App
Per prima cosa, installa nuovamente Blockstream App con la procedura mostrata all'inizio. Potrebbe essere nel frattempo arrivata ona release nuova, ti procedi con quella più aggiornada.

Lancia Blockstream App nel nuovo dispositivo e procedi sia cliccando `Get Started` che declinando l'offerta de la raccolta dati.

# b. Restore from backup
I similitudini con la prima installazion si fermano qui.
Quand arriva la schermata de creazion del wallet, anziché sernissere `Set Up Mobile Wallet` come hai fatto la prima volta, serniss `Restore from backup`.

![img](assets/43.webp)

Se stai usando la rete principale de Bitcoin, ovver quella che utilizza fond reali, nella schermata successiva serniss `Mainnet`.

![img](assets/43.webp)

Te compare la schermata con i caselle indoe immettere i paroll de la `Recovery phrase`. Riscrivile in ordine e correttamente, poi selezion `Continue` per ricreare el wallet sul nuovo dispositivo.

![img](assets/45.webp)

La fase de ripristino del wallet potrebbe durare alcuni minuti, aspetta con pazienza che si concluda con successo. A la fine del processo, ritroverai el tò wallet, con el saldo e la storia di transazion.

![img](assets/46.webp)

---
⚠️ El wallet ricreato sul nuovo dispositivo, l'è attivo al 100%.
Significa che possiede anca i ciav private per spend. Ricordalo in caso volessi lasciarlo a qualche collaboratore per la tua attività.

**Piuttosto usa el link del POS per i collaboratori, perché l'è stato creato con la sola chiave pubblica (el `descriptor`)**.

---

# Come continuare a imparare?

![img](assets/47.webp)
![img](assets/48.webp)
