---
layout: default
title: "El cicl de vita de ona transazion Bitcoin"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lezion Bitcoin-only</span> <span>Quest progett l'e mantegnuu da valerio-vaccaro</span></p>

## 🌍 Traduzion

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# El cicl de vita de ona transazion Bitcoin

## Cos’l'è ona transazion Bitcoin
Ona transazion Bitcoin l'è on’azion registrata sulla blockchain che trasferisce valore da uno o più input (fond ricevuti in precedenza, chiamati UTXO - Unspent Transaction Outputs) a uno o più output (nuovi destinatari). 
I input hinn output de transazion passate minga ancora spesi, mentre i output assegnano satoshi a indirizzi specifici. On’eccezion l'è la transazion "coinbase", la prima de ogni blocco, che genera nuovi bitcoin (ricompensa per i miner e fee) senza input. Se minga tutti i fond de on input vengono spesi, la differenza (change) torna al mittente tramite on output ulteriore o, se minga gestita, l'è persa per semper.

## Fasi del ciclo de vita
Quest l'è el ciclo de vita de ona transazion:

- Creazion: El wallet costruisce la transazion sernissendo i UTXO da spend in base all’importo da inviare e a la strategia per minimizzare i fee. Se l’input supera l’output, si genera on output de "change" (resto) che torna al mittente, aumentando però la dimensione de la transazion e i costi. Alcuni wallet cercano de evitarlo.
- Firma: La transazion viene firmata con ona o più firme digitali per ogni input, autentcandola. Quest passaggio l'è cruciale per la validità e può coinvolgere più parti in caso de transazion multisig-.
- Diffusione: La transazion firmata viene trasmessa a la rete ("broadcast") e inserita nella mempool del nodo locale. La mempool valida la transazion secondo i regole de consenso (es. firme valide, fond disponibili) e regole locali (es. dimensione massima de 400 KB per evitare spam). Poi, el nodo la propaga ai peer, che la validano e la inseriscono nelle loro mempool, creando ona diffusione a cascata. I mempool variano tra nodi per configurazion o connessioni diverse.
- Conferma: On miner include la transazion in on blocco, confermandola sulla blockchain. Tuttavia, finché minga ha più conferme (blocchi successivi), resta vulnerabile a sostituzion o fork. Ona transazion con fee basse può restare in mempool a lungo o essere scartata, ma potrebbe essere minata anca dopo mesi se i input restano minga spesi.

## Gestione de problemi
- Transazion sparita dalla mempool: Se ona transazion con fee basse viene rimossa (es. per picchi de traffico), si può ritrasmetterla manualmente (rebroadcast) usando el TXID, anca con script o explorer. Qualcuno potrebbe farlo per conto terzi.
- Replace-by-Fee (RBF): Se la fee l'è insufficiente, si può sostituire la transazion con ona che paga de più, purché marcata con el flag RBF. Ona proposta suggerisce che tutte i transazion siano implicitamente sostituibili, poiché i miner preferiscono comunque fee più alte.
- Child Pays for Parent (CPFP): Se minga si può doprà RBF (es. transazion minga propria o fond esauriti), si spende on output de la transazion bloccata con ona nuova transazion che paga fee elevate, rendendo entrambe appetibili per i miner. Serve che la somma di fee copra entrambe. Problemi sorgono se i nodi scartano la prima transazion, interrompendo la catena; on protocollo in sviluppo mira a trasmettere pacchetti de transazion per evitarlo.

## Conferma finale
Ona transazion l'è considerata definitiva domà con più conferme (blocchi sopra el suo). Ona sola conferma minga basta, poiché fork o doppie spese potrebbero invalidarla. El White Paper suggerisce 6 conferme (circa 60 minuti, con blocchi ogni 10 minuti in media), ma el numero varia in base all’importo e al rischio. La varianza nei tempi de blocco l'è alta, ma la media si mantiene grazie a la difficoltà de mining.

## Conclusione
El ciclo si chiude con la transazion "scolpita" nella blockchain, registrando per semper el spostamento de valore.

## Programma
Questa lezion l'è stata realizzata per on Satoshi Spritz Connect.

