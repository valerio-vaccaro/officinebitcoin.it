---
layout: default
title: "El ciclo de vita de na transazion Bitcoin"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lezion Bitcoin-only</span> <span>Sto progetto xe mantegnuo da valerio-vaccaro</span></p>

## 🌍 Traduzion

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# El ciclo de vita de na transazion Bitcoin

## Cos’xe na transazion Bitcoin
Na transazion Bitcoin xe un’azione registrata sulla blockchain che trasferisce valore da uno o più input (fondi ricevuti in precedenza, chiamati UTXO - Unspent Transaction Outputs) a uno o più output (nuovi destinatari). 
I input xe output de transazion passate no ancora spesi, mentre i output assegnano satoshi a indirizzi specifici. Un’eccezione xe la transazion "coinbase", la prima de ogni blocco, che genera nuovi bitcoin (ricompensa par i miner e fee) senza input. Se no tutti i fondi de un input vengono spesi, la differenza (change) torna al mittente tramite un output ulteriore o, se no gestita, xe persa par sempre.

## Fasi del ciclo de vita
Sto xe el ciclo de vita de na transazion:

- Creazione: El wallet costruisce la transazion sielziendo i UTXO da spender in base all’importo da inviare e a la strategia par minimizzare le fee. Se l’input supera l’output, si genera un output de "change" (resto) che torna al mittente, aumentando però la dimensione de la transazion e i costi. Alcuni wallet cercano de evitarlo.
- Firma: La transazion viene firmata co na o più firme digitali par ogni input, autenticandola. Sto passaggio xe cruciale par la validità e può coinvolgere più parti in caso de transazion multisig-.
- Diffusione: La transazion firmata viene trasmessa a la rete ("broadcast") e inserita nella mempool del nodo locale. La mempool valida la transazion secondo le regole de consenso (es. firme valide, fondi disponibili) e regole locali (es. dimensione massima de 400 KB par evitare spam). Poi, el nodo la propaga ai peer, che la validano e la inseriscono nelle loro mempool, creando na diffusione a cascata. Le mempool variano tra nodi par configurazion o connessioni diverse.
- Conferma: Un miner include la transazion in un blocco, confermandola sulla blockchain. Tuttavia, finché no ha più conferme (blocchi successivi), resta vulnerabile a sostituzioni o fork. Na transazion co fee basse può restare in mempool a lungo o essere scartata, ma potrebbe essere minata anca dopo mesi se i input restano no spesi.

## Gestione de problemi
- Transazione sparita dalla mempool: Se na transazion co fee basse viene rimossa (es. par picchi de traffico), si può ritrasmetterla manualmente (rebroadcast) usando el TXID, anca co script o explorer. Qualcuno potrebbe farlo par conto terzi.
- Replace-by-Fee (RBF): Se la fee xe insufficiente, si può sostituire la transazion co na che paga de più, purché marcata co el flag RBF. Na proposta suggerisce che tutte le transazion siano implicitamente sostituibili, poiché i miner preferiscono comunque fee più alte.
- Child Pays for Parent (CPFP): Se no si può doprar RBF (es. transazion no propria o fondi esauriti), si spende un output de la transazion bloccata co na nuova transazion che paga fee elevate, rendendo entrambe appetibili par i miner. Serve che la somma de le fee copra entrambe. Problemi sorgono se i nodi scartano la prima transazion, interrompendo la catena; un protocollo in sviluppo mira a trasmettere pacchetti de transazion par evitarlo.

## Conferma finale
Na transazion xe considerata definitiva solo co più conferme (blocchi sopra el suo). Na sola conferma no basta, poiché fork o doppie spese potrebbero invalidarla. El White Paper suggerisce 6 conferme (circa 60 minuti, co blocchi ogni 10 minuti in media), ma el numero varia in base all’importo e al rischio. La varianza nei tempi de blocco xe alta, ma la media si mantiene grazie a la difficoltà de mining.

## Conclusione
El ciclo si chiude co la transazion "scolpita" nella blockchain, registrando par sempre el spostamento de valore.

## Programma
Sta lezione xe stata realizzata par un Satoshi Spritz Connect.

