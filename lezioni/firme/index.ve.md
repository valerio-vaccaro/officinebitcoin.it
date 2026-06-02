---
layout: default
title: "Firme"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lezion Bitcoin-only</span> <span>Sto progetto xe mantegnuo da valerio-vaccaro</span></p>

## 🌍 Traduzion

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Firme
L'argomento de sta lezione saranno le firme digitali e come si applicano a Bitcoin.

## Cosa xe na firma?
Dobbiamo capire che cosa intendiamo par firma digitale. Quando pensiamo ad na normale firma pensiamo normalmente ad altro, siccome parliamo de documenti digitali la firma digitale lega sia l'identità dell'autore che el stato del documento firmato, donca sostanzialmente la firma dipende anca dal documento che andiamo a firmare.

Sto xe na differenza tanto grande co el mondo fisico, dove invece la firma noi la poniamo praticamente senza curarci del supporto su cui el facciamo. Certo che magari no andremo a firmare assegni o altri documenti senza preoccuparcene però sostanzialmente la firma che andiamo ad apporre no varia.

Le firme digitali invece xe xe na cosa un po' differente, le firme de digitali normalmente si basano su algoritmi a chiave pubblica e privato. Vuol dire che el nostro portafoglio da qualche parte nel mondo c'è na coppia de ciavi, pubblica e privata e la nostra (pseudo-)identità xe collegata a la chiave pubblica che tutti conoscono o che renderemo nota a tutti.

Noi utilizzeremo la nostra chiave privata, che xe un numero, e co qualche magia matematica produrremo na firma che xe un numero diverso e che dimostra che un certo stato de un certo documento appartiene o xe conossiuto da na certa identità connessa ad na chiave pubblica. Quello che vado a firmare xe l'impronta (o HASH) de un certo documento (o PAYLOAD).

Mi serve anca qualche un generatore de numeri casuali, butto tutti sti dati all'interno de uno "scatolone nero" che mi produce na firma, la firma donca xe un qualcosa che dimostra el possesso perché io sto firmando co el mio segreto ma dimostra anca che quello che io sto firmando no sia stato modificato.

Se modifico el PAYLOAD modifico l'HASH e ovviamente sto invalida la firma.

Donca sostanzialmente perché xe stata introdotta sta firma più complessa nel mondo digitale? Beh perché nel mondo digitale, a differenza de quello de quello fisico (e magari chi ha marinato a scuola se ne ricorda) copiare na firma xe tanto più semplice.

La firma digitale invece ha informazioni sul documento e donca cambia par ogni documento e no può essere incollata e riutilizzata su de un documento divergo.

La firma digitale serve donca a:
- dimostrare che io ho creato un certo messaggio o sto chiedendo na certa azione o sto dichiarando un certo stato de un sistema e
- dimostrare che quel messaggio o quel documento o quella stringa de dati no sia stata manipolata, ovvero che sia effettivamente quella che io volevo firmare.
- rendere irripudiabile na certa azione, se ho prodotto na firma xe stato proprio io a farla par quello specifico documento.

## Firme in Bitcoin
Sta tecnologia xe utilizzata in Bitcoin sotto l'acronimo ECDSA (Electronic Curve Digital Signature Algorithm) che xe un algoritmo par la produzione de firme digitali su curva ellittica, par ora no tratteremo altri schemi de firma.

Ricordiamo che in Bitcoin si possono produrre firme par:
- testo arbitrario, poco importante e usato
- nuove transazion, co el scopo de autorizzare la spesa de na certa UTXO

Ma ste firme come si legano a la transazion? Ogni indirizzo ha un meccanismo de spesa, dei script che devono essere eseguiti par sapere se na spesa può essere autorizzata. All'interno de sti script ci xe comandi (o OPCODE) destinati al controllo de le firme digitali quali OP_CHECKSIG, OP_CHECKSIGVERIFY, OP_CHECKMULTISIG, OP_CHECKMULTISIGVERIFY

Ricordiamo che na transazion in Bitcoin xe costituita da:
- Input, ovvero i fondi che vado a spender e par cui devo produrre uno script de spesa
- Output, ovvero i nuovi indirizzi in cui andranno i fondi (e par ogni indirizzo xe connessa na modalità de spesa ben definita.

In sostanza, nella maggioranza dei casi dovrò donca produrre Par OGNI INPUT la/le firma/e necessarie a completare el script de spesa.

Ricordiamo che sta azione ci permette de dimostrare che quell'input xe nostro e che la vogliamo spender (vogliamo passare la proprietà in toto o vogliamo dividerlo o vogliamo unirlo co altri input).

Ovviamente la transazion xe valida se tutti i input xe correttamente firmati mentre se anca uno no dei input no xe firmato quella la transazion no può considerarsi valida.

La firma xe controllabile da tutti e no xe ripudiabile, ma par flessibilità Satoshi in maniera tanto tanto furba ha introdotto varie modalità de firma, cioè la firma xe sempre la stessa ma cambia el PAYLOAD cioè la porzione de transazion oggetto de la firma, sto consente ad esempio de generar schemi e protocolli complessi in cui pezzi de transazion possono essere combinate tra de loro, Satoshi ha chiamato ste modalità (veri e propri flag nel linguaggio de scripting) SIGHASH.

## SIGHASH
El più semplice SIGHASH xe SIGHASH_ALL che vuol dire de generar na firma co TUTTI i INPUT e TUTTI i OUTPUT, sta xe la modalità più semplice e più usata par fare na firma.

Na prima differenza si può avere co SIGHASH_NONE che firma TUTTI i INPUT, ma NESSUNO dei OUTPUT, consentendo de aggiungere output o modificare le fee a posteriori. ATTENZIONE che co sto schema, se no protetti da multisig o altre funzionalità, un miner o chiunque veda na transazion co sto schema de firma può sostituire i output redirigendo i fondi verso un proprio indirizzo.

Un flag più interessante xe SIGHASH_SINGLE in cui si firma na coppia de input ed output purché vengano inseriti in na transazion allo stesso livello (e.g. quinto input e quinto output), sto consentirebbe de comporre transazion più grandi basate su ste coppie ma no da na possibilità de introdurre un change ovvero richiede la spesa totale dell'input.

Parallelamente tutti sti SIGHASH possono essere combinati co el flag ANYONECANPAY che limita la firma solo all'input par cui si sta producendo firma dando donca possibilità a chiunque de aggiungere input a la transazion.

Ste firme xe tutte firme valide indipendentemente dal tipo de indirizzo e dagli script lasciando massima flessibilità de espressione al wallet, normalmente userà SIGHASH_ALL ma potrebbe pure seguire protocolli più complessi che richiedono schemi de firma differenti. In caso de multisig poi no c'è necessità de doprar el medesimo tipo de firma, un wallet 2di2 potrebbe firmare alcuni suoi UTXO co SIGHASH_NONE e ANYONECANPAY al fine de dare pieno controllo al secondo firmatario che potrà, ad esempio, raccogliere tutti sti input in na transazion da firmare co SIGHASH_ALL.

## Firme su testo arbitrario
Par par completezza le stesse firme che vengono utilizzate par i input de le transazion potete doprar anca par firmare del testo arbitrario.

Bitcoin propone uno schema in cui viene viene aggiunta del testo par evitare che sta funzionalità venga utilizzata par firmare a parte de transazion, donca se avete Bitcoin core o anca alcuni Wallet potete cercare na funzionalità de firma de messaggi de testo sulla base de un certo vostro indirizzo.

El wallet userà la chiave privata associata a la chiavetta pubblica che ha generato quell'indirizzo par fare de le firme de messaggi testuali 

All'atto de la verifica si ottiene la chiave pubblica che può essere può donca utilizzata par rigenerar l'indirizzo, donca se io ho el testo e la firma mi tiro fuori la chiave pubblica che ha firmato e dalla chiave pubblica posso ricalcolarmi l'indirizzo e controllarlo ad esempio co quello fornito.

## Programma
La lezione sulle firme può essere ripetuta, qui un elenco de quelle già tenute:

| Data        | Note                                           |
|-------------|------------------------------------------------|
|||
