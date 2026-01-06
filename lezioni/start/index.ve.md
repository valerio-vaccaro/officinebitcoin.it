---
name: Starter Kit Bitcoin
description: Starter kit sempliz e facil da implementar par doprar Bitcoin in manera corretta. Impara a scaricar e installar un wallet mobile, configurar un POS par richieste de pagamento e scoprir le impostazion avanzade del wallet.
---
![cover](assets/cover.webp)


Ecco un bel modo de iniziare a doprar Bitcoin in na manera più corretta possibil.
Quello che segue xe el suggerimento par un *starter kit* molto snello e facil da implementar in autonomia.

Che te sii un utente curioso, un professionista che desidera accettar Bitcoin come metodo de pagamento o un utente esperto in cerca de soluzion par amici e parenti, sta guida te permetarà de:
- scaricar e installar un wallet mobile, par l'utilizzo de Bitcoin a ogni livello (onchain par la conservazion a longo termine; oppure Liquid, e Lightning par i pagamenti istantanei);
- configurar un POS par generar richieste de pagamento partendo dal prezzo de i to beni/servizi in Euro;
- conosser le impostazion avanzade del wallet. Ghemo lascià sta parte a la fin de la guida, par semplificar l'approccio inizial, ma te dai sempre un occhio a sta parte, perché xe importante.

Chiariemo prima de tut cosa se intende all'inizio, parlando de doprar Bitcoin in *manera corretta*.

# Piccolo glossario inizial
- `Not your keys, not your coins`
  Se te te stai approciando a Bitcoin par la prima volta, la frase `Not your keys, not your coins` par te xe nova e el so significato se riduce a la mera traduzion literal.
  Bitcoin funziona sul principio de la crittografia asimmetrica, basà su na serie de coppie de chiavi pubbliche e private. Xe col possesso **unico** e la gestión individuale de le chiavi private che te poi dir de disporre de i to Bitcoin.
  
  Pertanto, te devi esser solo ti a conosser le chiavi private, el segreto che te permetarà de posseder e eventualmente spender i bitcoin associà a ste chiavi.
  `Not your keys, not your coins` xe praticamente un _mantra_ par i bitcoiner de tuto el mondo e el diventerà anca par te.

- `Recovery phrase`
  Durante la so breve storia, el protocollo Bitcoin se ga evoludo in modo da render più semplice la gestión del segreto, ovvero le chiavi private. Oggi ste vien rappresentade soto forma de na sequenza de 12 o 24 parole de la lengua inglese, un modo più semplice par trascriverle e verificarle.
  Le parole xe el segreto principal da conservar. Le devi esser trascrite su un supporto cartaceo e custodie in un logo molto sicuro, ad esempio na cassaforte. Le no devi mai esser fotografade, trasferide su un computer e - tanto meno - condivise con altri.

- `Wallet`
  El wallet, portafoglio, xe lo strumento che te permetarà de visualizar el to saldo, nonché accettar o spender Bitcoin. Nel corso de sto tutorial ne scaricaremo un sul to telefono.
  El wallet sul telefono se ciama `hot wallet`, in quanto ospitado su un dispositivo sempre connesso a internet. Se te sii all'inizio va più che ben, impararai co lo studio altri metodi par perfezionar l'uso de i wallet.

- `Non Custodial`
  De fondamentale importanza xe iniziare a doprar Bitcoin tramite wallet `non-custodial`, ovvero che te **lassa el completo controllo su le chiavi private**. Diffida sempre de chi te spingerà a doprar strumenti diversi, ciamadi custodial, par approciarte a Bitcoin. I wallet custodial xe strumenti de le quali no possedi le chiavi.
    No xe question de **se**, ma de **quando** te impedirà par sempre l'accesso ai to fondi.

# Blockstream App (ex Green Wallet)
Par lo starter kit scaricaremo Blockstream App, un wallet `open source` de cui te poi verificar el codice. L'applicazion ga na longa tradizion de sviluppo e na discreta storia alle spalle, el wallet se ga rivelado affidabile in passado.

---
⚠️ Le istruzion che segue xe dedicate al download e installazion de l'app par Android. Par iOS dopra necessariamente lo store ufficiale.

---

Va al link https://github.com/Blockstream/green_android che xe el repository Github ufficiale del sviluppatore.

![img](assets/01.webp)

A metà pagina, su la destra, seleziona `Latest` nello spazio dedicà a le *Releases*, par andar a scaricar la version più aggiornada.

Te rivararà su na pagina che te mostrerà l'ultima release, 5.1.4 al momento de la stesura de sto tutorial a dicember 2025.
Nella stessa pagina seleziona cosa te poi scaricar:

![img](assets/02.webp)

Scarica el file `.apk` senza dover passar dal Play Store e installalo sul to telefono Android.

![img](assets/03.webp)

---
⚠️ El to telefono podarìa richieder permessi particolari par scaricar app da fonti no certificate. Concedi ste autorizzazion par continuar.

---
Quando Android te chiede de installar Blockstream App, clicca su `Install`.

![img](assets/04.webp)

A la fin de l'installazion, scerni `Open`.

![img](assets/05.webp)

Se apre Blockstream App e par iniziare a doprar el wallet, scerni `Get Started`.

![img](assets/07.webp)

Blockstream te chiederà se te vori partecipar a na raccolta de dati, par aiutar i sviluppatori a migliorar l'app. Declina l'invito.

![img](assets/08.webp)

# El to primo wallet
Te poi iniziare a crear el to primo wallet. Clicca su `Set Up Mobile Wallet`.

![img](assets/09.webp)

Inizia el processo de creazion del to wallet.

![img](assets/10.webp)

Che termina in pochi secondi. El to wallet xe pronto e, par iniziare a doprarlo, clicca su `Continue`.

![img](assets/11.webp)

El wallet se apre nella schermada ciamada `Home`. Par el momento dai un'occhiada, ma te dovriessi concentrarte subito sul menu in basso `Security`.

# Your Keys, your coins

![img](assets/12.webp)

In sto menu infatti te vegnarà proposto de far el backup del to wallet. Altro no xe che la visualizazion de la sequenza de 12 parole che te servirà par ripristinarlo in futuro. Ste 12 parole xe el to wallet: **assicurati pertanto de esser in un ambiente sicuro, lontan da oci indiscreti, aver un'agendina o un quaderno su cui trascriver le parole, prima de metterle al sicuro** (ad esempio in cassaforte).
Clicca su `Back Up Now` e scopri le 12 parole.

**Riporta anca l'ordine esatto de le parole: 1, 2, 3 ecc: scrivi le parole in stampatello maiuscolo, par na migliore visualizazion futura ricordando però che, se te dovriessi inserirle a man in futuro, te dovriessi doprar lo stampatello minuscolo**.

![img](assets/13.webp)

Dopo aver trascrito e messo le parole al sicuro, procedi co lo starter kit. Tute le ulteriori configurazion le trovararà a la fin de la guida.

# Menu TRANSACT
L'utilizzo del wallet xe estremamente semplificado:
- va nel menu `Transact`
- do xe i comandi principali: `Send` e `Receive` (**ignora `Buy`**).

![img](assets/17.webp)

Quando te avarà de transazioni, le sarà visibili nella parte soto ai comandi.
No avendo fondi, par iniziare a averne te poi selezionar `Receive`.

Te compaiono na serie de *Asset*, ma concentrati solo su Bitcoin. Te poi scernir tra Bitcoin onchain (icona arancione) e Liquid (icona blu) che xe quello che te permetarà de doprar pagamenti istantanei, come co Lightning Network, ma attraverso un meccanismo che vedaremo in seguito.

Par iniziare, scerni Bitcoin Onchain, l'icona arancione.

![img](assets/18.webp)

Quello che te compaioni xe un QR code, che rappresenta uno de i to indirizzi Bitcoin, che vedi anca in basso ciamado co `bc1q` seguito da altri caratteri.
Te poi mostrar el QR code a na persona che te deve pagar, par ricever i to primi fondi, ragionevolmente piccole frazioni de Bitcoin, ciamade anca `Satoshi`.

![img](assets/19.webp)


Se invece te torni indrio e scerni Liquid, el menu te segnala ⚡️**Lightning Ready**. 

Te devi saver infatti che, sfruttando un servizio de `SWAP`, Blockstream App te permetarà de ricever pagamenti quasi istantanei, emetter richieste de pagamento Lightning Network o pagar invoice LN, depositando/prelevando però i fondi da un account Liquid del to stesso wallet.

![img](assets/20.webp)

Nel menu che se apre dopo sta scelta, seleziona come te vori ricever i fondi, scernendo tra Liquid e Lightning.
Se te scerni Liquid, te vegnarà mostrado un QR code simile a quello visualizado scernendo Bitcoin Onchain, che rappresenta un indirizzo riconoscibile co el prefisso `lq1q` seguito da altri caratteri.

Se invece te selezioni Lightning, te vegnarà chiesto de inserir l'importo che te vori ricever e confermar cliccando su `Confirm`.

![img](assets/21.webp)

Blockstream App te mostra un QR code che rappresenta l'invoice LN, che pode esser pagada co qualunque wallet Lightning Network.

![img](assets/22.webp)

---
⚠️ Nella nostra simulazion, ghemo chiesto de ricever 210 sats, ma el QR code risultante, avvisa che ricevararà 160 sats.
I swap ga infatti un costo, circa 50 satoshi par ogni pagamento ricevudo.
**Xe importante tener a mente sto aspetto, soprattutto in caso de ricezion de micro pagamenti**.
Niente cambia par chi deve pagar, che infatti vedarà decurtada la somma de la richiesta fada in fase de impostazion: 210 satoshi.

---

# Te sii un comerciante? Dopa el POS
Par far de sta guida un **starter kit** che se rispetta, podemo abbinar i incassi in Bitcoin su sto wallet, doprando un POS esterno.

Te poi configurarlo in pochi semplici passaggi direttamente al link https://btcpos.cash/.

![img](assets/23.webp)

Te poi così ricever pagamenti Lightning direttamente sul to wallet creà su Blockstream App, condividar el link co i collaboratori e - par farlo - te basta seguir i prossimi passi e crear un link da tener poi a portada de click su la home del to cellulare. Quello che te serve, xe copiar el `Descriptor` del to wallet e incollarlo nel grande spazio centrale che trovi al link.

# 1. Ricevi i primi fondi su la rete Liquid
Xe necessario abilitar la visualizazion de i *Asset* nella schermada home del to wallet. Se sto xe stà appena creà, te devi farti pagar na invoice LN o comunque ricever fondi su un indirizzo Liquid.

Dopo aver ricevudo i fondi, te poi selezionar Liquid tra i `Assets` che vedi nel menu `Home`.

![img](assets/24.webp)

# 2. Accedi ai parametri necessari
Ora te ghe a disposizion quanto serve par acceder ai parametri che te permetarà de "trasportar" el to wallet sul POS. Tecnicamente se ciama *esportazion de la chiave pubblica* e xe un tecnicismo che impararai co lo studio approfondido. 
Par ora sappi che, par farlo, te basta selezionar el menu in alto a destra:

![img](assets/25.webp)

E scernir `Watch-only` nel menu a tendina comparso.
![img](assets/26.webp)


Appare `Output Descriptors`, che xe appunto el parametro che stiamo cercando. Copialo co el comando apposito e torna su la pagina web dove te stai configurando el POS.

![img](assets/27.webp)

# 3. Configura el POS
Incolla el descriptor nello spazio apposito e clicca `GENERATE POS LINK`. El sistema creerà un URL unico, valido solo par te e par el to wallet.

![img](assets/28.webp)

Prima te poi anca impostar la valuta de riferiment, scernendo tra USD, CHF e EUR nel menu a tendina dove appare `Currency`.
![img](assets/29.webp)

# 4. Incassa generando richieste de pagamento col POS
Una volta clicado su `GENERATE POS LINK`, la pagina mostra el risultado: **el link xe stà creà co successo**.
Te poi copiarlo perché el link rimarrà sempre accessibile **solo par el to wallet** all'URL generado.

![img](assets/30.webp)

Te poi anca aprire el POS e iniziare a doprarlo:
![img](assets/31.webp)

Supponemo, ad esempio de voler generar na invoice da 3.351 sats, associando na descrizion. 

![img](assets/32.webp)

Cliccando su `CREATE INVOICE` el POS mostra el QR code o l'invoice testuale da sottopor a un eventuale cliente.

![img](assets/33.webp)

Quando el cliente ga pagà l'invoice, su la quale leggerà correttamente anca la *descrizion* (Coppa del Nonno in sto caso), el POS segnala el pagamento ricevudo.


![img](assets/34.webp)

Che xe leggibile, correttamente, anca sul wallet!
![img](assets/35.webp)

Ora te basta memorizar e tener a portada de man el link del POS, par doprarlo al momento del bisogno, anca sul cellulare dove te ghe installà el to wallet.

![img](assets/36.webp)

Aggiungendolo come link/app de la home

![img](assets/37.webp)

# ⚠️ NOTA IMPORTANTE

Se te rilezi ben i passaggi appena compiudi, relativamente all'incasso de l'invoice in quest'ultimo esempio, notemo do cose importanti:
1. al cliente xe stà mostrada na invoice da 3.351 sats
2. el nostro wallet ga incassà 3.293 sats.

Prima de gridar al scandalo, xe necessario tornar a la schermada inizial del POS, che mostra la dicitura che vedi nell'immagine sottostante: 

![img](assets/38.webp)

La differenza tra 3.351 (invoice sottoposta al cliente) e 3.293 (el to incasso) xe esattamente in sti termini:
- 50 sats par ogni invoice generada
- 0.25% come fee de servizio (8 sats = 0,25% de 3.351)
- Totale incassà: 3.293

#### Te sii soltanto all'inizio e sto xe un starter kit. Na piccola fee xe el compromesso par doprar Bitcoin in auto custodia, senza intermediari e doprar tute le opportunità, anca i piccoli pagamenti istantanei. 

#### Co lo studio impararai a doprar altri strumenti, che no richiederà altre fee oltre a quelle previste anca par i utenti esperti.

---
# Altre impostazion

Xe arrivà el momento de conosser ben el to primo wallet. Le impostazion xe importanti, perché te aiuterà nell'uso quotidiano.

## Menu
I menu de Blockstream App li trovi in basso e xe:
- Home
- Transact
- Security
- Settings

Continua a configurar el to wallet dal menu `Security`. Oltre a la possibilità de visualizar e trascriver le parole de la `Recovery phrase`, sto menu te mete a disposizion altre caratteristiche importanti.

Te poi impostar, ad esempio, el login al to wallet co el controllo biometrico (se impostà sul to telefono) o aggiunger anca un PIN a sei cifre par acceder al wallet.
Ste opzioni xe molto importanti, perché impedisce a estranei de acceder e visualizar el to wallet, qualora i ghe abbia in man el to cellulare.


![img](assets/14.webp)

in sto menu te poi anca decidar el tempo de *Logout*, ovvero quando el wallet se disconnete dopo qualche minuto de inattività. De default xe settà su *5 minuti* e te poi variar sto tempo a seconda de le to necessità, più longo o più corto aggiustandolo in base a la to manualità.
![img](assets/15.webp)
# Menu SETTINGS
Menu molto importante perché contien tute le settings del wallet.
Cliccando in sto menu te poi ad esempio rinominar el wallet: nel nostro esempio lo ghemo ciamà *Starter Kit*. Rinominar i wallet, par distinguerli, xe molto importante quando se ne dopra più de uno sul stesso dispositivo e se deve capir/scernir qual doprar.

![img](assets/39.webp)

Se invece te te sposti nel sotto-menu `Denomination`, te poi trovar impostazion utilissime riguardo la valuta.
![img](assets/40.webp)

Te consiglio de doprar `satoshi/sats` come unità par i importi in Bitcoin. El Satoshi xe l'unità più piccola del BTC, pari a un cento-milionesimo de Bitcoin.
Inoltre apparirà la scelta de l'exchange de riferiment par la conversión. Dopera uno che te permete de visualizar e impostar i importi in Eur.

![img](assets/41.webp)

Infine, nel menu `Settings` te poi controlar la version attualmente in uso de Blockstream App e controlar se xe da aggiornar, nonché ghe xe i comandi par chieder supporto direttamente *in-app*.
![img](assets/42.webp)


# Menu HOME
La `Home` de Blockstream App, xe el menu dove se apre el to wallet ad ogni novo accesso.
Scorrendo verso el basso, trovararà l'opzion par acquistar Bitcoin tramite un exchange integrà. **No doprarlo**. 

![img](assets/16.webp)

# Ripristino del wallet

Se durante l'uso te dovriessi accorger che devi cambiar telefono, o che te ghe l'esigenza de doprar el wallet *Starter Kit* su più de un dispositivo, co Blockstream App sappi che te poi farlo.

Par proceder, te basta imparar la procedura de ripristino del wallet, come de seguito spiegada, che prevede i passi da far nel caso che te dovriessi perder l'accesso al telefono dove te ghe inizià a doprar el wallet.

i to fondi, infatti, no xe "sul dispositivo" cellulare, o "nel wallet". I fondi xe su la rete Bitcoin, sia essa Onchain, Lightning o Liquid. El wallet, par la precision: le chiavi pubbliche e private del to wallet, xe lo strumento par acceder ai indirizzi dopradi e - co essi - al saldo associà.

Xe par sta procedura che te ghe trascrito le 12 parole e le ghe messe in un posto sicuro... **Te l'he fato vero?** Perché senza quelle parole, no te avarà più accesso ai to fondi.

# a. Nova installazion de Blockstream App
Par prima cosa, installa novamente Blockstream App co la procedura mostrada all'inizio. Podarìa esser che nel frattempo xe arrivà na release nova, te procedi co quella più aggiornada.

Lancia Blockstream App nel novo dispositivo e procedi sia cliccando `Get Started` che declinando l'offerta de la raccolta de dati.

# b. Restore from backup
Le similitudini co la prima installazion se ferma qui.
Quando arriva la schermada de creazion del wallet, invece de scernir `Set Up Mobile Wallet` come te ghe fato la prima volta, scerni `Restore from backup`.

![img](assets/43.webp)

Se te stai doprando la rete principale de Bitcoin, ovvero quella che dopra fondi reali, nella schermada successiva scerni `Mainnet`.

![img](assets/43.webp)

Te compaioni la schermada co le caselle dove inserir le parole de la `Recovery phrase`. Riscrivile in ordine e correttamente, poi seleziona `Continue` par ricrear el wallet sul novo dispositivo.

![img](assets/45.webp)

La fase de ripristino del wallet podarìa durar alcuni minuti, aspetta co pazienza che se concluda co successo. A la fin del processo, trovararà el to wallet, co el saldo e la storia de le transazioni.

![img](assets/46.webp)

---
⚠️ El wallet ricreà sul novo dispositivo, xe attivo al 100%.
Questo significa che possiede anca le chiavi private par spender. Ricordalo in caso te voriessi lasciarlo a qualche collaboratore par la to attività.

**Piuttosto dopra el link del POS par i collaboratori, perché xe stà creà co la sola chiave pubblica (el `descriptor`)**.

---

# Come continuar a imparar?

![img](assets/47.webp)
![img](assets/48.webp)
