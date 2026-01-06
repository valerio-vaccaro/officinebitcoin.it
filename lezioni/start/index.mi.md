---
name: Starter Kit Bitcoin
description: Starter kit sempliz e facil da implementà per doprà Bitcoin in manera corretta. Impara a scaricà e installà un wallet mobile, configurà un POS per richiest de pagament e scoprì le impostazion avanzad del wallet.
---
![cover](assets/cover.webp)


Ecco un bel mod de inizià a doprà Bitcoin in una manera pù corretta possibil.
Quell che segu l'è el suggeriment per un *starter kit* assai snell e facil da implementà in autonomia.

Che te siet un utent curios, un professionista che desidera accettà Bitcoin come metod de pagament o un utent espert in cerca de soluzion per amis e parent, questa guida te permetarà de:
- scaricà e installà un wallet mobile, per l'utilizz de Bitcoin a ogni livell (onchain per la conservazion a long termin; oppur Liquid, e Lightning per i pagament istantanee);
- configurà un POS per generà richiest de pagament partend dal prezz de i tò ben/servizzi in Euro;
- conoss le impostazion avanzad del wallet. Hoo lasciad questa part alla fin de la guida, per semplificà l'approcc inizial, ma te dai semper un occhi a questa part, poiché l'è important.

Chiariam prim de tut quell che se intend all'inizi, parland de doprà Bitcoin in *manera corretta*.

# Piccol glossari inizial
- `Not your keys, not your coins`
  Se te te stet approcciand a Bitcoin per la prima volta, la frase `Not your keys, not your coins` per te l'è noeva e el so significad se riduc a la mera traduzion literal.
  Bitcoin el funziona sul principi de la crittografia asimmetrica, basad su una serie de coppi de claav pubbliche e private. L'è con el possess **unic** e la gestion individual de le claav private che te pöet dir de dispone de i tò Bitcoin.
  
  Pertant, te devet esser sol te a conoss le claav private, el segret che te permetarà de possed e eventualment spend i bitcoin associad a queste claav.
  `Not your keys, not your coins` l'è praticament un _mantra_ per i bitcoiner de tut el mond e el diventerà anca per te.

- `Recovery phrase`
  Durant la soa breva storia, el protocoll Bitcoin l'è evolud in mod de rend pù sempliz la gestion del segret, ovver le claav private. Oggi queste vegnen rappresentad sota forma de una sequenza de 12 o 24 parol de la lengua inglesa, un mod pù sempliz per trascriverle e verificarle.
  Le parol hinn el segret principal da conservà. Devet esser trascritt su un support cartaceo e custodid in un loeugh assai segur, ad esempi una cassafort. Devet minga mai esser fotografad, trasferid su un computer e - tant men - condivis con alter.

- `Wallet`
  El wallet, portafogli, l'è l'strument che te permetarà de visualizzà el tò saldo, nonché accettà o spend Bitcoin. Nel cors de questo tutorial ne scaricarem un sul tò telefon.
  El wallet sul telefon l'è ciamad `hot wallet`, poiché ospitad su un dispositiv semper conness a internet. Se te set all'inizi va pù che ben, impararet con lo studi alter metod per perfezionà l'us de i wallet.

- `Non Custodial`
  De fondamental importanza l'è inizià a doprà Bitcoin tramit wallet `non-custodial`, ovver che te **lasen el complet controll su le claav private**. Diffida semper de chi te spingerà a doprà strument divers, ciamad custodial, per approccià a Bitcoin. I wallet custodial hinn strument de le quali te possedet minga le claav.
    L'è minga question de **se**, ma de **quand** te impedirann per semper l'access ai tò fond.

# Blockstream App (ex Green Wallet)
Per lo starter kit scaricarem Blockstream App, un wallet `open source` de cui te pöet verificà el codici. L'applicazion la gh'ha una longa tradizion de svilupp e una discreta storia alle spalle, el wallet l'è rivelad affidabil in passad.

---
⚠️ Le istruzion che seguen hinn dedicad al download e installazion de l'app per Android. Per iOS dopra necessariament lo store ufficial.

---

Va al link https://github.com/Blockstream/green_android che l'è el repository Github ufficial del sviluppator.

![img](assets/01.webp)

A metà pagina, su la destra, seleziona `Latest` nello spazi dedicad a le *Releases*, per andà a scaricà la version pù aggiornada.

Te rivararà su una pagina che te mostrerà l'ultima release, 5.1.4 al moment de la stesura de questo tutorial a dicember 2025.
Nella stessa pagina seleziona quell che te pöet scaricà:

![img](assets/02.webp)

Scarica el file `.apk` senza dover passà dal Play Store e installal sul tò telefon Android.

![img](assets/03.webp)

---
⚠️ El tò telefon el pö richied permess particolar per scaricà app da font minga certificad. Concedi queste autorizzazion per continuà.

---
Quand Android te chied de installà Blockstream App, clicca su `Install`.

![img](assets/04.webp)

A la fin de l'installazion, scern `Open`.

![img](assets/05.webp)

Se apre Blockstream App e per inizià a doprà el wallet, scern `Get Started`.

![img](assets/07.webp)

Blockstream te chiederà se te voeuret partecipà ad una raccolta de dat, per aiutà i sviluppator a migliorà l'app. Declina l'invit.

![img](assets/08.webp)

# El tò prim wallet
Te pöet inizià a creà el tò prim wallet. Clicca su `Set Up Mobile Wallet`.

![img](assets/09.webp)

Inizia el process de creazion del tò wallet.

![img](assets/10.webp)

Che termina in pochi second. El tò wallet l'è pront e, per inizià a doprall, clicca su `Continue`.

![img](assets/11.webp)

El wallet se apre nella schermada ciamada `Home`. Per el moment dai un'occhiada, ma te dovriess concentrà subit sul menu in bass `Security`.

# Your Keys, your coins

![img](assets/12.webp)

In questo menu infatti te vegnarà propost de fà el backup del tò wallet. Alter minga che la visualizzazion de la sequenza de 12 parol che te servirann per ripristinall in futur. Queste 12 parol hinn el tò wallet: **assicurati pertant de esser in un ambient segur, lontan da oeucc indiscret, avè un'agendina o un quadern su cui trascriver le parol, prim de metterle al segur** (ad esempi in cassafort).
Clicca su `Back Up Now` e scopri le 12 parol.

**Riporta anca l'ordin esatt de le parol: 1, 2, 3 ecc: scrivi le parol in stampatell maiuscol, per una miglior visualizzazion futura ricordand però che, se te dovriess inserirle a man in futur, te dovriess doprà el stampatell minuscol**.

![img](assets/13.webp)

Dopo aver trascritt e mett le parol al segur, procedi con lo starter kit. Tutt le ulteriori configurazion le trovararà alla fin de la guida.

# Menu TRANSACT
L'utilizz del wallet l'è estremament semplificad:
- va nel menu `Transact`
- duu hinn i comand principal: `Send` e `Receive` (**ignora `Buy`**).

![img](assets/17.webp)

Quand te avararà de transazion, sarann visibil nella part sota ai comand.
Minga avend fond, per inizià a avènn te pöet selezionà `Receive`.

Te compaen una serie de *Asset*, ma concentrati sol su Bitcoin. Te pöet scern tra Bitcoin onchain (icona arancion) e Liquid (icona blu) che l'è quell che te permetarà de doprà pagament istantanee, come con Lightning Network, ma attravers un meccanism che vedarem in seguit.

Per inizià, scern Bitcoin Onchain, l'icona arancion.

![img](assets/18.webp)

Quell che te compaar l'è un QR code, che rappresenta un de i tò indirizz Bitcoin, che vedet anca in bass ciamad con `bc1q` seguit da alter carater.
Te pöet mostrà el QR code ad una persona che te dev pagà, per ricev i tò prim fond, ragionevolment piccol frazion de Bitcoin, ciamad anca `Satoshi`.

![img](assets/19.webp)


Se invece te tornet indree e scern Liquid, el menu te segnala ⚡️**Lightning Ready**. 

Te devi savè infatti che, sfruttand un servizi de `SWAP`, Blockstream App te permetarà de ricev pagament quasi istantanee, emett richiest de pagament Lightning Network o pagà invoice LN, depositand/prelevand però i fond da un account Liquid del tò stess wallet.

![img](assets/20.webp)

Nel menu che se apre dopo questa scelta, seleziona come te voeuret ricev i fond, scernend tra Liquid e Lightning.
Se te scern Liquid, te vegnarà mostrad un QR code similar a quell visualizad scernend Bitcoin Onchain, che rappresenta un indirizz riconoscibil con el prefiss `lq1q` seguit da alter carater.

Se invece te selezionet Lightning, te vegnarà chiest de inserì l'import che te voeuret ricev e confermà cliccand su `Confirm`.

![img](assets/21.webp)

Blockstream App te mostra un QR code che rappresenta l'invoice LN, che pö esser pagada con qualunque wallet Lightning Network.

![img](assets/22.webp)

---
⚠️ Nella nostra simulazion, hoo chiest de ricev 210 sats, ma el QR code risultant, avvisa che ricevararà 160 sats.
I swap hinn infatti con un cost, circa 50 satoshi per ogni pagament ricevud.
**L'è important tenì a ment questo aspett, specialment in cas de ricezion de micro pagament**.
Nient cambia per chi dev pagà, che infatti vedarà decurtada la somma de la richiesta fada in fase de impostazion: 210 satoshi.

---

# Te set un comerciant? Dopa el POS
Per fà de questa guida un **starter kit** che se rispetta, pöem abbinà i incass in Bitcoin su questo wallet, doprand un POS estern.

Te pöet configurall in pochi sempliz passagg direttament al link https://btcpos.cash/.

![img](assets/23.webp)

Te pöet così ricev pagament Lightning direttament sul tò wallet cread su Blockstream App, condivid el link con i collaborator e - per fàll - te basta seguì i prossim pass e creà un link da ten poi a portada de click su la home del tò cellulare. Quell che te serv, l'è copià el `Descriptor` del tò wallet e incollall nel grand spazi central che trovet al link.

# 1. Ricev i prim fond su la rete Liquid
L'è necessari abilità la visualizzazion de i *Asset* nella schermada home del tò wallet. Se questo l'è staa appena cread, te dev fart pagà una invoice LN o comunque ricev fond su un indirizz Liquid.

Dopo aver ricevud i fond, te pöet selezionà Liquid tra i `Assets` che vedet nel menu `Home`.

![img](assets/24.webp)

# 2. Accedi ai parametr necessari
Ora te gh'hee a disposizion quell che serv per acced ai parametr che te permetarann de "trasportà" el tò wallet sul POS. Tecnicament l'è ciamad *esportazion de la claav pubblica* e l'è un tecnicism che impararet con lo studi approfondid. 
Per ora savì che, per fàll, te basta selezionà el menu in alt a destra:

![img](assets/25.webp)

E scern `Watch-only` nel menu a tendina comparid.
![img](assets/26.webp)


Appare `Output Descriptors`, che l'è appunt el parametr che stamm cercand. Copial con el comand apposid e torna su la pagina web dove te set configurand el POS.

![img](assets/27.webp)

# 3. Configura el POS
Incolla el descriptor nello spazi apposid e clicca `GENERATE POS LINK`. El sistema creerà un URL unic, valid sol per te e per el tò wallet.

![img](assets/28.webp)

Prim te pöet anca impostà la valuta de riferiment, scernend tra USD, CHF e EUR nel menu a tendina dove appare `Currency`.
![img](assets/29.webp)

# 4. Incassa generand richiest de pagament col POS
Una volta cliccad su `GENERATE POS LINK`, la pagina mostra el risultad: **el link l'è staa cread con success**.
Te pöet copiàll poiché el link rimarrà semper accessibil **sol per el tò wallet** all'URL generad.

![img](assets/30.webp)

Te pöet anca aprì el POS e inizià a doprall:
![img](assets/31.webp)

Supponem, ad esempi de voer generà un'invoice da 3.351 sats, associand una descrizion. 

![img](assets/32.webp)

Cliccand su `CREATE INVOICE` el POS mostra el QR code o l'invoice testual da sottopor ad un eventual cliente.

![img](assets/33.webp)

Quand el cliente l'ha pagad l'invoice, su la quale leggerà correttament anca la *descrizion* (Coppa del Nonno in questo cas), el POS segnala el pagament ricevud.


![img](assets/34.webp)

Che l'è leggibil, correttament, anca sul wallet!
![img](assets/35.webp)

Ora te basta memorizzà e ten a portada de man el link del POS, per doprall al moment del besogn, anca sul cellulare dove te gh'hee installad el tò wallet.

![img](assets/36.webp)

Aggiungendol come link/app de la home

![img](assets/37.webp)

# ⚠️ NOTA IMPORTANT

Se te rileget ben i passagg appena compiud, relativament all'incass de l'invoice in quest'ultim esempi, notamm duu cos important:
1. al cliente l'è staa mostrada una invoice da 3.351 sats
2. el noster wallet l'ha incassad 3.293 sats.

Prim de gridà al scandal, l'è necessari tornà alla schermada inizial del POS, che mostra la dicitura che vedet nell'immagine sottostante: 

![img](assets/38.webp)

La differenza tra 3.351 (invoice sottoposta al cliente) e 3.293 (el tò incass) l'è esattament in questi termin:
- 50 sats per ogni invoice generada
- 0.25% come fee de servizi (8 sats = 0,25% de 3.351)
- Totale incassad: 3.293

#### Te set soltanto all'inizi e questo l'è un starter kit. Una piccola fee l'è el compromess per doprà Bitcoin in auto custodia, senza intermediari e doprà tutt le opportunità, anca i piccol pagament istantanee. 

#### Con lo studi impararet a doprà alter strument, che minga richiederann alter fee oltre a quelle previst anca per i utent espert.

---
# Alter impostazion

L'è arrivad el moment de conoss ben el tò prim wallet. Le impostazion hinn important, poiché te aiuterann nell'us quotidian.

## Menu
I menu de Blockstream App li trovet in bass e hinn:
- Home
- Transact
- Security
- Settings

Continua a configurà el tò wallet dal menu `Security`. Oltre alla possibilità de visualizzà e trascriver le parol de la `Recovery phrase`, questo menu te met a disposizion alter caratteristiche important.

Te pöet impostà, ad esempi, el login al tò wallet con el controll biometrico (se impostad sul tò telefon) o aggiung anca un PIN a ses cifre per acced al wallet.
Queste opzion hinn assai important, poiché impedissen a estranei de acced e visualizzà el tò wallet, qualora gh'abbien in man el tò cellulare.


![img](assets/14.webp)

in questo menu te pöet anca decid el temp de *Logout*, ovver quand el wallet se disconnet dopo qualch minut de inattività. De default l'è settad su *5 minut* e te pöet varià questo temp a seconda de le tò necessità, pù long o pù cort aggiustandol in base alla tua manualità.
![img](assets/15.webp)
# Menu SETTINGS
Menu assai important poiché contien tutt i settings del wallet.
Cliccand in questo menu te pöet ad esempi rinominà el wallet: nel noster esempi l'hoo ciamad *Starter Kit*. Rinominà i wallet, per distinguerli, l'è assai important quand se ne dopra pù de un sul stess dispositiv e se dev capì/scern qual doprà.

![img](assets/39.webp)

Se invece te te spostet nel sotto-menu `Denomination`, te pöet trovà impostazion utilissim riguard la valuta.
![img](assets/40.webp)

Te consigli de doprà `satoshi/sats` come unità per i import in Bitcoin. El Satoshi l'è l'unità pù piccola del BTC, pari a un cento-milionesim de Bitcoin.
Inoltre apparirà la scelta de l'exchange de riferiment per la conversión. Dopera un che te permet de visualizzà e impostà i import in Eur.

![img](assets/41.webp)

Infine, nel menu `Settings` te pöet controllà la version attualment in us de Blockstream App e controllà se l'è da aggiornà, nonché gh'è i comand per chied support direttament *in-app*.
![img](assets/42.webp)


# Menu HOME
La `Home` de Blockstream App, l'è el menu dove se apre el tò wallet ad ogni noeuv access.
Scorrend vers el bass, trovararà l'opzion per acquistà Bitcoin tramit un exchange integrad. **Minga doprall**. 

![img](assets/16.webp)

# Ripristin del wallet

Se durant l'us te dovriess accorg che te dev cambià telefon, o che te gh'hee l'esigenza de doprà el wallet *Starter Kit* su pù de un dispositiv, con Blockstream App savì che te pöet fàll.

Per proced, te basta imparà la procedura de ripristin del wallet, come de seguit spiegada, che preved i pass da fà nel cas che te dovriess perd l'access al telefon dove te hoo iniziad a doprà el wallet.

i tò fond, infatti, hinn minga "sul dispositiv" cellulare, o "nel wallet". I fond hinn su la rete Bitcoin, sia essa Onchain, Lightning o Liquid. El wallet, per la precision: le claav pubbliche e private del tò wallet, hinn l'strument per acced ai indirizz doprad e - con essi - al saldo associad.

L'è per questa procedura che te hoo trascritt le 12 parol e le hoo mettud in un post segur... **Te l'hee fad vera?** Poiché senza quelle parol, minga te avararà pù access ai tò fond.

# a. Noeuv installazion de Blockstream App
Per prim, installa noeuvament Blockstream App con la procedura mostrada all'inizi. Pö esser che nel frattemp l'è arrivada una release noeuv, te proced con quella pù aggiornada.

Lancia Blockstream App nel noeuv dispositiv e proced sia cliccand `Get Started` che declinand l'offerta de la raccolta de dat.

# b. Restore from backup
Le similitudin con la prim installazion se fermen qui.
Quand arriva la schermada de creazion del wallet, invece de scern `Set Up Mobile Wallet` come te hoo fad la prim volta, scern `Restore from backup`.

![img](assets/43.webp)

Se te set doprand la rete principal de Bitcoin, ovver quella che dopra fond real, nella schermada successiva scern `Mainnet`.

![img](assets/43.webp)

Te compaar la schermada con le caselle dove inserì le parol de la `Recovery phrase`. Riscrivile in ordin e correttament, poi seleziona `Continue` per ricreà el wallet sul noeuv dispositiv.

![img](assets/45.webp)

La fase de ripristin del wallet pö durà qualch minut, aspetta con pazienza che se concluda con success. Alla fin del process, trovararà el tò wallet, con el saldo e la storia de le transazion.

![img](assets/46.webp)

---
⚠️ El wallet ricread sul noeuv dispositiv, l'è attiv al 100%.
Questo significa che possed anca le claav private per spend. Ricordall in cas te voeriess lasciall a qualch collaborator per la tua attività.

**Puttost dopra el link del POS per i collaborator, poiché l'è staa cread con la sola claav pubblica (el `descriptor`)**.

---

# Come continuà a imparà?

![img](assets/47.webp)
![img](assets/48.webp)
