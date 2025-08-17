# Ghostinbox.it: Usar email sensa aver email 
Ghostinbox xe na piataforma web che permete ai utenti de crear indirisi email temporanei par ricever messagi sensa revelar el so indirisso email vero. El servisio xe ideale par registrazion rapidi, verifiche de account, test de deliverability de le email o qualsìa situasion in cui se vogia evitar spam o proteger la propria identità.

A diferensa dei servisi email tradisionali, Ghostinbox no richiede registrasion nì memoriza dati personali, rendendelo na scelta eccelente par chi prioritiza la privacy. Inoltre, el suporto par la re Tor permete de aceder al servisio in modo anonimo, nascondendo l'indirisso IP de l'utente. La natura open-source del progeto garantise trasparensa e permete ai svilupatori de esaminar el codice par eventual vulnerabilità o personalizasion.

## Come funsiona Ghostinbox?
![alt text](https://officinebitcoin.it/lezioni/ghostin/front.png)

L'utiliso de Ghostinbox xe estremamente intuitivo e no richiede competense tecniche:

1. **Vai sul sito**: Visita https://ghostinbox.it/ (o tramite Tor par magior anonimà).
2. **Genera un indirisso email temporaneo**: Clica sul pulsante par crear un novo indirisso email temporaneo (es. random@ghostinbox.it). L'indirisso xe imediatamente ativo e pronto par l'uso.
3. **Ricevi messagi**: Usa l'indirisso generà par ricever email, ad esempio par registrazion a servisi online, verifiche de account o test. I messagi apar in tempo real ne la casela de posta sul sito.
4. **Monitora i messagi**: Acedi a la casela de posta temporanea diretamente su Ghostinbox par visualizar i messagi ricevù. No xe necessario un client email esterno.

![alt text](https://officinebitcoin.it/lezioni/ghostin/email.png)

El servisio xe progetà par esser rapid e priv de fricion: no serve crear un account, e l'interfacia minimalista rende l'esperienza fluida anca par utenti no tecnici. La possibilità de aceder tramite Tor gionta un ulterior livel de protezion par chi desidera mantegner l'anonimà completo.

## Da alias a email
Par usar el servisio xe necessario scegier un alias che va scelto abastansa longo e casual in modo tale da no poder esser indovinà da altri utenti. Questo alias sarà come na password par poder aceder a la email e quindi no va dimenticà.

Da questo alias vien ricavà un indirisso email HASH@ghostinbox.it dove HASH xe pari a `sha256(alias)` ovvero l'hash de l'alias usando sha 256; un utente può quindi usar questa email (mostrada ne la schemata de ricezion) al fin de ricever email, la pagina de ricezion se agiorna automàticamente mostrando le email ricevude. Un utente può crearse un indirisso email sensa aceder al servisio ed usar el sito web solo par la consultasion.

Cliccando su la email xe possibile legerne el testo ed eventualmente copiar link da cliccar; el formato de le email xe volutamente solo testuale e quindi no mostrerà nissuna de le carateristiche grafiche de le email html based.

## A chi serve Ghostinbox?
Ghostinbox risponde a diverse esigenze legà a la privacy e a la gestión de le email temporanee:

1. **Protezion dal spam**: Usando un indirisso temporaneo, i utenti possono evitar che el so indirisso email vero venga inondà de spam o newsletter indesiderade.
2. **Registrazion sicure**: Perfeto par iscriversi a servisi online, forum o piataforme che richiede na verifica via email sensa comprometer l'email personal.
3. **Test de deliverability**: I svilupatori e i marketer possono usar Ghostinbox par testar l'invio e la ricezion de email sensa coinvolger indirisi veri.
4. **Privacy avansà**: Grazie al suporto par Tor, el servisio xe ideale par utenti che desidera mantegner l'anonimà durante l'interasion co siti web o servisi online.
5. **Uso temporaneo**: Adato par situasion in cui xe necessario un indirisso email usa-e-getta, come par promosion, prove gratuite o comunicasion a corto termine.

![alt text](https://officinebitcoin.it/lezioni/ghostin/stats.png)

## Carateristiche tecniche
El repository GitHub de Ghostinbox (https://github.com/valerio-vaccaro/ghostinbox.it) revela un'implementasion leggera, scrita principalmente in Python co el framework Flask, co le seguenti carateristiche:

- **Aprocio serverless**: no esiste un email server ma vien sfrutà na email gratuita ed un servisio de forwarding de le email rendendo estremamente sempia ed economica l'architettura del servisio.
- **Architettura**: Ghostinbox utilizza un'architettura client-server basà su Flask par gestir la generasion de i indirisi email temporanei e la visualisasion de i messagi. La semplicità del design garantise prestasion elevate anca co un alto volume de richieste.
- **Generasion de i indirisi**: I indirisi email temporanei vien generà dinamicamente in base a l'alias inserì.
- **Suporto par Tor**: El servisio xe configurà par esser acesibile tramite onion routing, garantendo che l'indirisso IP de l'utente no venga tracià durante l'interasion co el sito.
- **Gestión de i messagi**: I messagi ricevù vien eliminà dopo 30 dì.
- **Sicuresa**: Nissun dato personal o messagio vien memorizà permanentemente. El design del servisio riduse al minimo i rischi de violasion, e l'assenza de registrasion elimina la necessità de fornir informasion sensibili.
- **Open-source**: El codice pùblico permete ai svilupatori de verificar l'integrità del sistema, contribuir co miglioramenti o ospitar un'instansa personalizada.

Punti de forsa tecnici:
- **Privacy assoluta**: La cancelasion de le email dopo 30 dì ed el suporto par Tor garantise un'esperienza anonima e sicura.
- **Legerezza**: L'implementasion in Flask xe ottimizada par basse risorse, rendendo el servisio scalabile e veloce.
- **Trasparensa**: La licensa open-source permete audit del codice e personalizasion, aumentando la fiducia de i utenti.

## Conclusión
Ghostinbox xe na solusion elegante e funsionale par chi cerca un servisio de email temporanee rapid, sicuro e orientà a la privacy. Co la so trasparensa, suporto par la privacy e semplicità d'uso, rapresenta un'agiunta preziosa a l'ecosistema Bitcoin. Visita https://ghostinbox.it/ par provarlo o esplora el codice su https://github.com/valerio-vaccaro/ghostinbox.it.

