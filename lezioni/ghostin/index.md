# Ghostinbox.it: Use email without having an email 
Ghostinbox è una piattaforma web che consente agli utenti di creare indirizzi email temporanei per ricevere messaggi senza rivelare il proprio indirizzo email reale. Il servizio è ideale per registrazioni rapide, verifiche di account, test di deliverability delle email o qualsiasi situazione in cui si desideri evitare spam o proteggere la propria identità.

A differenza dei servizi email tradizionali, Ghostinbox non richiede registrazione né memorizza dati personali, rendendolo una scelta eccellente per chi prioritizza la privacy. Inoltre, il supporto per la rete Tor consente di accedere al servizio in modo anonimo, nascondendo l’indirizzo IP dell’utente. La natura open-source del progetto garantisce trasparenza e permette agli sviluppatori di esaminare il codice per eventuali vulnerabilità o personalizzazioni.

## Come funziona Ghostinbox?
![alt text](https://officinebitcoin.it/lezioni/ghostin/front.png)

L’utilizzo di Ghostinbox è estremamente intuitivo e non richiede competenze tecniche:

1. **Accedi al sito**: Visita https://ghostinbox.it/ (o tramite Tor per maggiore anonimato).
2. **Genera un indirizzo email temporaneo**: Clicca sul pulsante per creare un nuovo indirizzo email temporaneo (es. random@ghostinbox.it). L’indirizzo è immediatamente attivo e pronto per l’uso.
3. **Ricevi messaggi**: Usa l’indirizzo generato per ricevere email, ad esempio per registrazioni a servizi online, verifiche di account o test. I messaggi appaiono in tempo reale nella casella di posta sul sito.
4. **Monitora i messaggi**: Accedi alla casella di posta temporanea direttamente su Ghostinbox per visualizzare i messaggi ricevuti. Non è necessario un client email esterno.

![alt text](https://officinebitcoin.it/lezioni/ghostin/email.png)

Il servizio è progettato per essere rapido e privo di frizioni: non serve creare un account, e l’interfaccia minimalista rende l’esperienza fluida anche per utenti non tecnici. La possibilità di accedere tramite Tor aggiunge un ulteriore livello di protezione per chi desidera mantenere l’anonimato completo.

## Da alias a email
Per usare il servizio è necessario scegliere un alias che va scelto abbastanza lungo e casuale in modo tale da non poter essere indovinato da altri utenti. Questo alias sarà come una password per poter accedere alla email e quindi non va dimenticato.

Da questo alias viene ricavato un indirizzo email HASH@ghostinbox.it dove HASH è pari a `sha256(alias)` ovvero l'hash dell'alias usando sha 256; un untente può quindi usare questa email (mostrata nella schemata di ricezione) al fine di ricevere email, la pagina di ricezione si aggiorna automaticamente mostrando le email ricevute. Un utente può creasti un indirizzo email senza accedere al servizio ed usare il sito web solo per la consultazione.

Cliccando sulla email è possibile leggerne il testo ed eventualmente copiare link da cliccare; il formato delle email è volutamnete solo testuale e quindi non mostrerà alcuna delle caratteristiche grafiche delle email html based.

## A chi serve Ghostinbox?
Ghostinbox risponde a diverse esigenze legate alla privacy e alla gestione delle email temporanee:

1. **Protezione dallo spam**: Utilizzando un indirizzo temporaneo, gli utenti possono evitare che il loro indirizzo email reale venga inondato di spam o newsletter indesiderate.
2. **Registrazioni sicure**: Perfetto per iscriversi a servizi online, forum o piattaforme che richiedono una verifica via email senza compromettere l’email personale.
3. **Test di deliverability**: Gli sviluppatori e i marketer possono utilizzare Ghostinbox per testare l’invio e la ricezione di email senza coinvolgere indirizzi reali.
4. **Privacy avanzata**: Grazie al supporto per Tor, il servizio è ideale per utenti che desiderano mantenere l’anonimato durante l’interazione con siti web o servizi online.
5. **Uso temporaneo**: Adatto per situazioni in cui è necessario un indirizzo email usa-e-getta, come per promozioni, prove gratuite o comunicazioni a breve termine.

![alt text](https://officinebitcoin.it/lezioni/ghostin/stats.png)

## Caratteristiche tecniche
Il repository GitHub di Ghostinbox (https://github.com/valerio-vaccaro/ghostinbox.it) rivela un’implementazione leggera, scritta principalmente in Python con il framework Flask, con le seguenti caratteristiche:

- **Approccio serverless**: non esiste un email server ma viene sfruttata una email gratuita ed un servizio di forwarding delle email rendendo estremamente semplice ed economica l'architettura del servizio.
- **Architettura**: Ghostinbox utilizza un’architettura client-server basata su Flask per gestire la generazione degli indirizzi email temporanei e la visualizzazione dei messaggi. La semplicità del design garantisce prestazioni elevate anche con un alto volume di richieste.
- **Generazione degli indirizzi**: Gli indirizzi email temporanei vengono generati dinamicamente in base all'alias inserito.
- **Supporto per Tor**: Il servizio è configurato per essere accessibile tramite onion routing, garantendo che l’indirizzo IP dell’utente non venga tracciato durante l’interazione con il sito.
- **Gestione dei messaggi**: I messaggi ricevuti vengono eliminato dopo 30 giorni.
- **Sicurezza**: Nessun dato personale o messaggio viene memorizzato permanentemente. Il design del servizio riduce al minimo i rischi di violazioni, e l’assenza di registrazione elimina la necessità di fornire informazioni sensibili.
- **Open-source**: Il codice pubblico consente agli sviluppatori di verificare l’integrità del sistema, contribuire con miglioramenti o ospitare un’istanza personalizzata.

Punti di forza tecnici:
- **Privacy assoluta**: La cancellazione delle email dopo 3 giorni ed il supporto per Tor garantiscono un’esperienza anonima e sicura.
- **Leggerezza**: L’implementazione in Flask è ottimizzata per basse risorse, rendendo il servizio scalabile e veloce.
- **Trasparenza**: La licenza open-source permette audit del codice e personalizzazioni, aumentando la fiducia degli utenti.

## Conclusione
Ghostinbox è una soluzione elegante e funzionale per chi cerca un servizio di email temporanee rapido, sicuro e orientato alla privacy. Con la sua interfaccia intuitiva, il supporto per Tor e la trasparenza del codice open-source, si rivolge sia agli utenti comuni che desiderano proteggere la propria inbox dallo spam, sia agli sviluppatori che necessitano di un sistema affidabile per test o registrazioni temporanee. Per provare Ghostinbox, visita https://ghostinbox.it/. Per esplorare il codice o contribuire al progetto, consulta il repository su https://github.com/valerio-vaccaro/ghostinbox.it.
