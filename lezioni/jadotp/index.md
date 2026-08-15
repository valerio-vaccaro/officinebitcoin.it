---
layout: default
title: "Jade come autenticatore OTP"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lezione Bitcoin-only</span> <span>This project is maintained by valerio-vaccaro</span></p>

# Jade come autenticatore OTP

## Introduzione

Molti siti usano un secondo fattore TOTP: un codice di sei o più cifre che cambia a intervalli regolari, normalmente ogni 30 secondi. Jade può conservare il segreto TOTP in un dispositivo protetto da PIN e generare il codice senza app di autenticazione sul telefono.

OTP migliora la protezione dell'account, ma non sostituisce una password unica e robusta, le passkey quando disponibili, né i codici di recupero. Un TOTP può essere richiesto da un sito di e-mail, un exchange, un account GitHub o un wallet: valuta con cura quali segreti vuoi associare allo stesso dispositivo.

## Preparare Jade e il computer

Aggiorna Jade con un firmware recente e completa il [setup iniziale](../jadeset/index.html), inclusa la scelta di un PIN. Per usare TOTP non serve installare alcun software sul computer: il computer o il telefono serve solo per aprire il sito che sta attivando il 2FA e per mostrare il QR di configurazione.

Prima di registrare un account:

- verifica data e ora corrette su Jade; il codice dipende dall'orologio;
- prepara un backup dei codici di recupero forniti dal servizio, su carta o in un archivio cifrato;
- aggiorna Jade prima di spostare più account: le funzioni di importazione/esportazione richiedono firmware recente;
- non fotografare né inoltrare il QR del segreto TOTP: chi lo possiede può generare i tuoi codici.

> **Attenzione al backup.** I record OTP non sono derivati dalla seed bitcoin. Ripristinare la seed su una Jade nuova non ripristina i codici TOTP. Esporta e verifica un backup prima di resettare, vendere o sostituire il dispositivo.

## Aggiungere un nuovo account

1. Sul sito o nell'app che vuoi proteggere, apri l'attivazione dell'autenticazione a due fattori e scegli un'app autenticatore/TOTP. Non confermare ancora la procedura finale.
2. Sblocca Jade. Dal menu scegli **Options → Authentication → OTP**.
3. Seleziona **New OTP Record** e poi la scansione del QR; in alternativa inserisci manualmente l'URI `otpauth://` fornito dal servizio.
4. Inquadra con Jade il QR visualizzato su computer o telefono. Dai al record un nome riconoscibile, per esempio `github-mario` o `mail-lavoro`.
5. Scegli **View OTP**, seleziona il record e digita sul sito il codice mostrato da Jade prima che scada. Solo dopo il servizio conferma l'attivazione.

Jade mostra una barra di avanzamento per il tempo residuo del codice. Se il sito rifiuta il codice, aspetta il successivo, controlla l'ora di Jade e ripeti con attenzione.

## Uso quotidiano: esempio GitHub

Quando GitHub richiede il secondo fattore dopo la password:

1. sblocca Jade e apri **Options → Authentication → OTP → View OTP**;
2. scegli il record `github-mario`;
3. inserisci il codice corrente nella pagina di login;
4. prima di approvare una richiesta inattesa, controlla l'indirizzo del sito nel browser: un codice TOTP digitato in una pagina di phishing può essere riutilizzato immediatamente dall'attaccante.

Il segreto non passa nel computer durante questo uso; il codice temporaneo, però, viene digitato nel browser e può essere sottratto da malware o phishing. Per gli account più importanti, preferisci passkey o chiavi FIDO2 se il servizio le offre e conserva i recovery code offline.

## Importare da un'app autenticatore

Jade può leggere il formato QR di esportazione di alcune app 2FA. Nell'app di origine crea l'export, poi su Jade scegli **Options → Authentication → OTP → New OTP → Scan QR** (oppure **Scan QR** dalla home) e inquadra il codice. Per una scansione più affidabile esporta un account alla volta e ingrandisci il QR sullo schermo.

Non eliminare il record dall'app originale finché non hai verificato su Jade almeno un accesso reale. Se il servizio lo permette, conserva per un breve periodo un secondo metodo di recupero indipendente.

## Esportare e verificare il backup

Per ogni record importante apri **View OTP**, seleziona il record, poi **Details → Export**. Jade può mostrare il segreto come QR da importare in un autenticatore secondario o come testo. Il segreto va trattato esattamente come una password:

- salva il QR/testo solo in una destinazione fidata e cifrata oppure su supporto offline controllato;
- verifica il backup generando un codice sul dispositivo secondario e confrontandolo con quello di Jade;
- conserva separatamente i recovery code del servizio;
- solo dopo una verifica riuscita, rimuovi una vecchia copia se desideri ridurre il numero di duplicati.

La [guida ufficiale Blockstream per OTP](https://help.blockstream.com/blockstream-jade/add-more-security-functionality/use-jade-as-a-2fa-authentication-device) descrive anche importazione, esportazione e le limitazioni della modalità QR.
