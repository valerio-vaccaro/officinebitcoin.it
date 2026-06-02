---
layout: default
title: "Firme"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lezion Bitcoin-only</span> <span>Quest progett l'e mantegnuu da valerio-vaccaro</span></p>

## 🌍 Traduzion

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Firme
L'argomento de questa lezion saranno i firme digitali e come si applicano a Bitcoin.

## Cosa l'è ona firma?
Dobbiamo capire che cosa intendiamo per firma digitale. Quand pensiamo ad ona normale firma pensiamo normalmente ad altro, siccome parliamo de documenti digitali la firma digitale lega sia l'identità dell'autore che el stato del documento firmato, donca sostanzialmente la firma dipende anca dal documento che andiamo a firmare.

Quest l'è ona differenza assai grande con el mond fisico, indoe invece la firma noi la poniamo praticamente senza curarci del supporto su cui el facciamo. Certo che magari minga andremo a firmare assegni o altri documenti senza preoccuparcene però sostanzialmente la firma che andiamo ad apporre minga varia.

I firme digitali invece hinn hinn ona cosa on po' differente, i firme de digitali normalmente si basano su algoritmi a chiave pubblica e privato. Vuol dire che el nostro portafoglio da qualche parte nel mond c'è ona coppia de ciav, pubblica e privata e la nostra (pseudo-)identità l'è collegata a la chiave pubblica che tutti conoscono o che renderemo nota a tutti.

Noi utilizzeremo la nostra chiave privata, che l'è on numero, e con qualche magia matematica produrremo ona firma che l'è on numero diverso e che dimostra che on certo stato de on certo documento appartiene o l'è conossuto da ona certa identità connessa ad ona chiave pubblica. Quello che vado a firmare l'è l'impronta (o HASH) de on certo documento (o PAYLOAD).

Mi serve anca qualche on generatore de numeri casuali, butto tutti questi dati all'interno de uno "scatolone nero" che mi produce ona firma, la firma donca l'è on qualcosa che dimostra el possesso perché io sto firmando con el mio segreto ma dimostra anca che quello che io sto firmando minga sia stato modificato.

Se modifico el PAYLOAD modifico l'HASH e ovviamente quest invalida la firma.

Donca sostanzialmente perché l'è stata introdotta questa firma più complessa nel mond digitale? Beh perché nel mond digitale, a differenza de quello de quello fisico (e magari chi ha marinato a scuola se ne ricorda) copiare ona firma l'è assai più sempliz.

La firma digitale invece ha informazion sul documento e donca cambia per ogni documento e minga può essere incollata e riutilizzata su de on documento divergo.

La firma digitale serve donca a:
- dimostrare che io ho creato on certo messaggio o sto chiedendo ona certa azion o sto dichiarando on certo stato de on sistema e
- dimostrare che quel messaggio o quel documento o quella stringa de dati minga sia stata manipolata, ovver che sia effettivamente quella che io volevo firmare.
- rendere irripudiabile ona certa azion, se ho prodotto ona firma hinn stato proprio io a farla per quello specifico documento.

## Firme in Bitcoin
Questa tecnologia l'è utilizzata in Bitcoin sotto l'acronimo ECDSA (Electronic Curve Digital Signature Algorithm) che l'è on algoritmo per la produzion de firme digitali su curva ellittica, per ora minga tratteremo altri schemi de firma.

Ricordiamo che in Bitcoin si possono produrre firme per:
- testo arbitrario, poco important e usato
- nuove transazion, con el scopo de autorizzare la spesa de ona certa UTXO

Ma queste firme come si legano a la transazion? Ogni indirizzo ha on meccanismo de spesa, di script che devono essere eseguiti per sapere se ona spesa può essere autorizzata. All'interno de questi script ci hinn comandi (o OPCODE) destinati al controllo di firme digitali quali OP_CHECKSIG, OP_CHECKSIGVERIFY, OP_CHECKMULTISIG, OP_CHECKMULTISIGVERIFY

Ricordiamo che ona transazion in Bitcoin l'è costituita da:
- Input, ovver i fond che vado a spend e per cui devo produrre uno script de spesa
- Output, ovver i nuovi indirizzi in cui andranno i fond (e per ogni indirizzo l'è connessa ona modalità de spesa ben definita.

In sostanza, nella maggioranza di casi dovrò donca produrre Per OGNI INPUT la/i firma/e necessarie a completare el script de spesa.

Ricordiamo che questa azion ci permette de dimostrare che quell'input l'è nostro e che la vogliamo spend (vogliamo passare la proprietà in toto o vogliamo dividerlo o vogliamo unirlo con altri input).

Ovviamente la transazion l'è valida se tutti i input hinn correttamente firmati mentre se anca uno no di input minga l'è firmato quella la transazion minga può considerarsi valida.

La firma l'è controllabile da tutti e minga l'è ripudiabile, ma per flessibilità Satoshi in maniera assai assai furba ha introdotto varie modalità de firma, cioè la firma l'è semper la stessa ma cambia el PAYLOAD cioè la porzion de transazion oggetto de la firma, quest consente ad esempio de generà schemi e protocolli complessi in cui pezzi de transazion possono essere combinate tra de loro, Satoshi ha chiamato queste modalità (veri e propri flag nel linguaggio de scripting) SIGHASH.

## SIGHASH
El più sempliz SIGHASH l'è SIGHASH_ALL che vuol dire de generà ona firma con TUTTI i INPUT e TUTTI i OUTPUT, questa l'è la modalità più sempliz e più usata per fare ona firma.

Ona prima differenza si può avere con SIGHASH_NONE che firma TUTTI i INPUT, ma NESSUNO di OUTPUT, consentendo de aggiungere output o modificare i fee a posteriori. ATTENZIONE che con quest schema, se minga protetti da multisig o altre funzionalità, on miner o chiunque veda ona transazion con quest schema de firma può sostituire i output redirigendo i fond verso on proprio indirizzo.

On flag più interessante l'è SIGHASH_SINGLE in cui si firma ona coppia de input ed output purché vengano inseriti in ona transazion allo stesso livello (e.g. quinto input e quinto output), quest consentirebbe de comporre transazion più grandi basate su queste coppie ma minga da ona possibilità de introdurre on change ovver richiede la spesa totale dell'input.

Parallelamente tutti questi SIGHASH possono essere combinati con el flag ANYONECANPAY che limita la firma domà all'input per cui si sta producendo firma dando donca possibilità a chiunque de aggiungere input a la transazion.

Queste firme hinn tutte firme valide indipendentemente dal tipo de indirizzo e dagli script lasciando massima flessibilità de espressione al wallet, normalmente userà SIGHASH_ALL ma potrebbe pure seguire protocolli più complessi che richiedono schemi de firma differenti. In caso de multisig poi minga c'è necessità de doprà el medesimo tipo de firma, on wallet 2di2 potrebbe firmare alcuni suoi UTXO con SIGHASH_NONE e ANYONECANPAY al fine de dare pieno controllo al secondo firmatario che potrà, ad esempio, raccogliere tutti questi input in ona transazion da firmare con SIGHASH_ALL.

## Firme su testo arbitrario
Per per completezza i stesse firme che vengono utilizzate per i input di transazion potete doprà anca per firmare del testo arbitrario.

Bitcoin propone uno schema in cui viene viene aggiunta del testo per evitare che questa funzionalità venga utilizzata per firmare a parte de transazion, donca se avete Bitcoin core o anca alcuni Wallet potete cercare ona funzionalità de firma de messaggi de testo sulla base de on certo vostro indirizzo.

El wallet userà la chiave privata associata a la chiavetta pubblica che ha generato quell'indirizzo per fare di firme de messaggi testuali 

All'atto de la verifica si ottiene la chiave pubblica che può essere può donca utilizzata per rigenerà l'indirizzo, donca se io ho el testo e la firma mi tiro fuori la chiave pubblica che ha firmato e dalla chiave pubblica posso ricalcolarmi l'indirizzo e controllarlo ad esempio con quello fornito.

## Programma
La lezion sulle firme può essere ripetuta, qui on elenco de quelle già tenute:

| Data        | Note                                           |
|-------------|------------------------------------------------|
|||
