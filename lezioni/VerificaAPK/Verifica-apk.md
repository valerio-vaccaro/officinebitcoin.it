![cover](slide-verifica-apk/1cover.webp)
La verifica delle firme crittografiche è una pratica di sicurezza fondamentale che **ogni utente di software open-source dovrebbe inserire nelle routine delle buone pratiche**.

Open source è per sua natura modificabile e ciò significa che chiunque può, a livello teorico, introdurre backdoor, attacchi o codice malevolo nelle applicazioni che usi per esercitarti, intanto che impari il protocollo Bitcoin.

Come utente che sta approfondendo lo studio, hai la possibilità di verificare personalmente se il software scaricato è stato manomesso, e lo dovresti fare prima di installarlo e usarlo.

Prima di iniziare, portiamo anche in Officine Bitcoin un classico delle presentazioni: il meme. Non sarà una presentazione pesante, ma decomprimiamo l'atmosfera già da subito.

![meme](slide-verifica-apk/2meme.webp)

## Come fare?
Gli sviluppatori rilasciano le nuove versioni di software accompagnandole sempre con una firma crittografica.
Significa che - oltre ad aver aggiornato il software - lo rilasciano certificando di averlo vincolato con una specifica impronta digitale. Reminder: la firma digitale prodotta con la chiave privata, è unica e non modificabile.

Tutto ciò di cui hai bisogno è la suite GPG per procedere alla verifica della firma.

![img](slide-verifica-apk/3.webp)

# Pre requisiti per questa esercitazione
- Un breve ripasso sulla crittografia asimmetrica
- Gli elementi da verificare:
  - software (binario, apk ecc)
  - la firma digitale dello sviluppatore, normalmente un file `.asc`, `.sig` o un checksum.
- Gli strumenti per fare la verifica:
  - GPG suite
  - un terminale (vale sia per Linux sia per Win)
# Crittografia asimmetrica

![img](slide-verifica-apk/4.webp)

Qui ci sono due chiavi correlate tra loro: una chiave pubblica e una privata. Come suggeriscono i nomi:
- La chiave pubblica è disponibile liberamente e può essere condivisa con chiunque.
- La chiave privata è tenuta al sicuro dal suo proprietario.

I dati cifrati con la chiave pubblica possono essere decifrati solo dalla chiave privata corrispondente. Ciò consente a chiunque di inviare dati crittografati al proprietario della coppia di chiavi, senza previa condivisione della parte segreta.

La crittografia a chiave pubblica è più lenta della crittografia simmetrica e non è adatta a cifrare dati di grandi dimensioni. Tuttavia, consente la distribuzione sicura delle chiavi di crittografia.
Alcuni algoritmi comunemente utilizzati per la crittografia a chiave pubblica includono RSA, ECC, ElGamal e DSA.

## Lato sviluppatore: nuovo aggiornamento

Lo sviluppatore rilascia il codice open source, per sua natura non cifrato.
Ne fa un hash crittografico (e questo genera il `checksum`) e cifra il digest con la sua chiave privata: questo crea la firma, quel file `.sig` o `.asc` anticipato prima.

Dopo tale processo, lo sviluppatore carica sul sito o su un repository Github entrambi i file. È lì che inizia il tuo download.

![img](slide-verifica-apk/5.webp)

Poi ti servirà la chiave pubblica dello sviluppatore. A volte si trova nel repository Github, a volta su server pubblici (*keyserver*). Anche se la ricerca può richiedere sforzi, la chiave pubblica è un elemento indispensabile per verificare il software, quindi impegnati per ottenerla.

In caso di difficoltà, fai domande sul gruppo Telegram di Officine Bitcoin, dove troverai le indicazioni per ottenere una specifica chiave pubblica.

![img](slide-verifica-apk/6.webp)

Per verificare l'integrità dei dati, il destinatario decifra la firma utilizzando la chiave pubblica del mittente, ottenendo un risultato:

a. i dati sono considerati autentici e non modificati durante il transito.
b. i dati sono stati potenzialmente manomessi.

Crittografando il valore hash con la chiave privata, **le firme PGP garantiscono che il checksum stesso sia protetto e collegato all'identità del mittente. Ciò impedisce la falsificazione delle firme su dati alterati**.

Le firme possono essere utilizzate per verificare qualsiasi cosa: file, e-mail , documenti e download di software . Quando si controlla una firma PGP, si dimostra che i dati provengono realmente da una fonte affidabile e sono integri.

Ed è la verifica di un apk per cellulare che potrai verificare adesso.

Usiamo ad esempio il download di Phoenix, wallet LN non-custodial, così da trattarlo nello specifico in una prossima serata di Officine Bitcoin.

# Download e verifica Phoenix Wallet (Acinq)
Se sei già stato sul sito di [Acinq](https://phoenix.acinq.co/), lo sviluppatore di Phoenix, sai già che il download è disponibile sugli store ufficiali per Android ed iOS.
Magari non ci hai mai fatto caso, ma per Android è disponibile anche il file apk.

![img](slide-verifica-apk/8.webp)

[Andiamoci!](https://github.com/ACINQ/phoenix/releases) per trovare file `apk` e `Signature` che scaricherai con `wget`.
Nel caso di Phoenix il file che contiene la firma per la verifica è denominato **`SHA256SUMS.ASC`**.

![img](slide-verifica-apk/9.webp)

Nello stesso repository ci sono anche le indicazioni per scaricare la chiave pubblica corrispondente alla *signing key E04E48E72C205463* (impronta digitale unica delle chiavi di Drouinf).
Copia il link e scaricala con `wget`, oppure segui le istruzioni suggerite nell'apposita sezione del repo.
**La chiave pubblica deve essere importata, oltre che scaricata**.

![img](slide-verifica-apk/10.webp)

---
⚠️ Il download dei file deve avvenire nella stessa directory.

---
# Apri il terminale
Con il terminale, posizionati nella directory dove sono stati scaricati l'apk e il file `SHA256SUMS.ASC` ed esegui i comandi nell'ordine.

![img](slide-verifica-apk/11.webp)

![img](slide-verifica-apk/12.webp)

Quando la verifica ha restituito esito positivo, potrai trasferire l'apk sul cellulare e installare l'app.

---
# Verifica difficoltosa
Ci possono essere diversi motivi per cui la verifica delle firme non è agevole, e sono quasi sempre da imputare al disordine o all'esperienza:
1. i file apk e/o .asc sono stati scaricati più volte, quindi nella directory risultano - ad esempio nomi strani tipo **nomefile-1** o **nomefile(1)**
2. apk e .asc non risiedono nella stessa directory
3. la chiave pubblica è stata scaricata ma non importata nel keyring gpg.

Possono invece capitare altre situazioni, per le quali - anche operando correttamente - la verifica non riesce.
È importante verificare l'errore che compare a terminale, copiarlo e iniziare una ricerca su internet per la soluzione.

# Verifica con Sparrow Wallet
Se invece utilizzi già Sparrow Wallet, puoi procedere a verificare i download con questo software, **il cui download e installazione devono essere preceduti da un'attenta e rigorosa verifica con GPG**.

Lancia Sparrow wallet e cerca nel menu `Tools` -> `Verify Downloads`.

![img](slide-verifica-apk/13.webp)

Si apre un'interfaccia che chiede di inserire i file appena scaricati. Cliccando su `Browse` si apre il file manager, per caricare ogni file nel campo richiesto.

![img](slide-verifica-apk/14.webp)

A volte il form dell'interfaccia si completa da solo. Se non lo fa, riempi tutti i campi con i file appropriati.

![img](slide-verifica-apk/15.webp)

L'esito, positivo, è mostrato graficamente dalle spunte verdi e dalla conferma *`Ready to install`* +  < nome file >.

# Supporto allo studio
Se hai partecipato alla presentazione in diretta Telegram, puoi considerarla un ulteriore passo verso la tua personale sovranità (non solo finanziaria).
Se te la sei persa **non disperare**: questi appunti servono appunto per recuperare e, inoltre, devi sapere che la riproporremo ancora su Officine.

Per non perdere la prossima presentazione, unisciti al [gruppo Telegram](https://t.me/officinebitcoin), così da rimanere in aggiornamento costante.

![img](slide-verifica-apk/17.webp)

Puoi inoltre cercare il [Satoshi Spritz](https://satoshispritz.it/) più vicino a te. Un Satoshi Spritz è un meetup locale dove si parla solo di Bitcoin, dove puoi portare le tue domande e farti rispondere da altri bitcoiner esperti. Al link troverai la mappa della penisola.

![img](slide-verifica-apk/16.webp)

Infine, se non trovi il meetup vicino a te, puoi approfittare delle dirette settimanali di [SatoshiSpritz Connect](https://t.me/SatoshiSpritzConnect), un meetup virtuale creato per chi non può partecipare ai Satoshi Spritz, o per aiutare i meetup più piccolini a prendere appunti e trovare ispirazione per le proprie presentazioni.

![img](slide-verifica-apk/18.webp)
