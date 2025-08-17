# Ghostinbox.it: Usà l'email sensa avègh n'email 
Ghostinbox l'è una piattaforma web che permet a i utent de creà indirizz email temporanei per ricev i messagg sensa rivelà el sò indirizz email ver. El servisi l'è ideal per registrazion rapid, verifiche de account, test de deliverability de le email o qualsìa situaziù in cui se vogia evità el spam o protegg la propria identità.

A differenza de i servisi email tradiziunai, Ghostinbox l'è minga necessari registràss nì memorizzà dat personal, rendendel una scelta eccellent per chi prioritizza la privacy. Inoltre, el suport per la re Tor permet de acced al servisi in manera anonima, nascondend l'indirizz IP de l'utent. La natura open-source del progett garantiss trasparenza e permet a i svilupador de esaminà el còdegh per eventual vulnerabilità o personalizaziù.

## Come l'è che l'è funziona Ghostinbox?
![alt text](https://officinebitcoin.it/lezioni/ghostin/front.png)

L'utilizz de Ghostinbox l'è estremament intuitiv e l'è minga necessari competenze tecniche:

1. **Va sul sit**: Visita https://ghostinbox.it/ (o tramite Tor per magior anonimà).
2. **Genera un indirizz email temporaneu**: Clica sul pulsant per creà un noeuv indirizz email temporaneu (es. random@ghostinbox.it). L'indirizz l'è immediatament attiv e pront per l'uso.
3. **Ricev i messagg**: Usa l'indirizz generà per ricev email, ad esempi per registrazion a servisi online, verifiche de account o test. I messagg apparen in temp real in la casella de posta sul sit.
4. **Monitora i messagg**: Acced a la casella de posta temporanea direttament su Ghostinbox per visualizzà i messagg ricevù. L'è minga necessari un client email estern.

![alt text](https://officinebitcoin.it/lezioni/ghostin/email.png)

El servisi l'è progettà per ess rapid e priv de friziù: l'è minga necessari creà un account, e l'interfaccia minimalista rend l'esperienza fluida anca per utent minga tecnic. La possibilità de acced tramite Tor gionta un ulterior livell de proteziù per chi vogia mantegn l'anonimà complet.

## Da alias a email
Per usà el servisi l'è necessari sceglià un alias che va scelt abbastanza longh e casual in manera tale de minga podèss ess indovinà da alter utent. Quest alias sarà come una password per podè acced a l'email e donca minga va dimenticà.

Da quest alias ven ricavà un indirizz email HASH@ghostinbox.it dove HASH l'è pari a `sha256(alias)` ovver l'hash de l'alias usand sha 256; un utent può donca usà quest email (mostrada in la schemata de riceziù) al fin de ricev email, la pagina de riceziù se aggiorna automàticament mostrand le email ricevù. Un utent può creàss un indirizz email sensa acced al servisi ed usà el sit web solo per la consultaziù.

Cliccand su la email l'è possibil leggerne el test e eventualment copià link da cliccà; el format de le email l'è volutament solo testual e donca minga mostrerà nissuna de le carateristiche grafiche de le email html based.

## A chi l'è che serviss Ghostinbox?
Ghostinbox rispond a diverse esigenze legà a la privacy e a la gestiù de le email temporanee:

1. **Proteziù del spam**: Usand un indirizz temporaneu, i utent possono evità che el sò indirizz email ver venga inondà de spam o newsletter indesiderà.
2. **Registrazion sicur**: Perfett per iscrivess a servisi online, forum o piattaforme che richiedon una verificà via email sensa compromett l'email personal.
3. **Test de deliverability**: I svilupador e i marketer possono utilizzà Ghostinbox per testà l'invi e la riceziù de email sensa coinvolg indirizz ver.
4. **Privacy avansà**: Grazi al suport per Tor, el servisi l'è ideal per utent che vogion mantegn l'anonimà durante l'interaziù con sit web o servisi online.
5. **Us temporaneu**: Adatt per situaziù in cui l'è necessari un indirizz email usa-e-getta, come per promozion, prove gratuit o comunicaziù a curt termin.

![alt text](https://officinebitcoin.it/lezioni/ghostin/stats.png)

## Carateristiche tecniche
El repository GitHub de Ghostinbox (https://github.com/valerio-vaccaro/ghostinbox.it) revela un'implementaziù leggera, scritt principalment in Python con el framework Flask, con le seguent carateristiche:

- **Aprocci serverless**: l'è minga esist un email server ma ven sfruttà una email gratuit ed un servisi de forwarding de le email rendend estremament sempia ed economica l'architettura del servisi.
- **Architettura**: Ghostinbox utilizza un'architettura client-server basà su Flask per gestì la generaziù de i indirizz email temporanei e la visualizaziù de i messagg. La semplicitè del design garantiss prestaziù elevà anca con un alt volume de richieste.
- **Generaziù de i indirizz**: I indirizz email temporanei venn generà dinamicament in bas a l'alias inserì.
- **Suport per Tor**: El servisi l'è configurà per ess acesibil tramite onion routing, garantend che l'indirizz IP de l'utent minga venga traccià durante l'interaziù con el sit.
- **Gestiù de i messagg**: I messagg ricevù venn eliminà dopo 30 dì.
- **Sicurezza**: Nissun dat personal o messagg ven memorizà permanentement. El design del servisi riduiss al minim i risch de violaziù, e l'assenza de registraziù elimina la necessità de fornì informaziù sensibili.
- **Open-source**: El còdegh pùblic permet a i svilupador de verificar l'integrità del sistema, contribuì con migliorament o ospità un'instanza personalizada.

Punt de forsa tecnic:
- **Privacy assoluta**: La cancellaziù de le email dopo 30 dì ed el suport per Tor garantissen un'esperienza anonima e sicura.
- **Leggerezza**: L'implementaziù in Flask l'è ottimizzata per bass risors, rendend el servisi scalabil e velos.
- **Trasparenza**: La licensa open-source permet audit del còdegh e personalizaziù, aumentand la fiducia de i utent.

## Conclusiù
Ghostinbox l'è una soluziù eleganta e funziunala per chi cerca un servisi de email temporanee rapid, sicur e orientà a la privacy. Con la sò interfaccia intuitiva, el suport per Tor e la trasparenza del còdegh open-source, se rivolge sia a i utent comun che vogion protegg la propria inbox del spam, sia a i svilupador che necessitano de un sistema affidabil per test o registrazion temporanee. Per provà Ghostinbox, visita https://ghostinbox.it/. Per esplorà el còdegh o contribuì al progett, consulta el repository su https://github.com/valerio-vaccaro/ghostinbox.it.

