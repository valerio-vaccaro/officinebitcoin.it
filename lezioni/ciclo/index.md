# Il ciclo di vita di una transazione Bitcoin

## Cos’è una transazione Bitcoin
Una transazione Bitcoin è un’azione registrata sulla blockchain che trasferisce valore da uno o più input (fondi ricevuti in precedenza, chiamati UTXO - Unspent Transaction Outputs) a uno o più output (nuovi destinatari). 
Gli input sono output di transazioni passate non ancora spesi, mentre gli output assegnano satoshi a indirizzi specifici. Un’eccezione è la transazione "coinbase", la prima di ogni blocco, che genera nuovi bitcoin (ricompensa per i miner e fee) senza input. Se non tutti i fondi di un input vengono spesi, la differenza (change) torna al mittente tramite un output ulteriore o, se non gestita, è persa per sempre.

## Fasi del ciclo di vita
Questo è il ciclo di vita di una transazione:

- Creazione: Il wallet costruisce la transazione scegliendo gli UTXO da spendere in base all’importo da inviare e alla strategia per minimizzare le fee. Se l’input supera l’output, si genera un output di "change" (resto) che torna al mittente, aumentando però la dimensione della transazione e i costi. Alcuni wallet cercano di evitarlo.
- Firma: La transazione viene firmata con una o più firme digitali per ogni input, autenticandola. Questo passaggio è cruciale per la validità e può coinvolgere più parti in caso di transazioni multisig-.
- Diffusione: La transazione firmata viene trasmessa alla rete ("broadcast") e inserita nella mempool del nodo locale. La mempool valida la transazione secondo le regole di consenso (es. firme valide, fondi disponibili) e regole locali (es. dimensione massima di 400 KB per evitare spam). Poi, il nodo la propaga ai peer, che la validano e la inseriscono nelle loro mempool, creando una diffusione a cascata. Le mempool variano tra nodi per configurazioni o connessioni diverse.
- Conferma: Un miner include la transazione in un blocco, confermandola sulla blockchain. Tuttavia, finché non ha più conferme (blocchi successivi), resta vulnerabile a sostituzioni o fork. Una transazione con fee basse può restare in mempool a lungo o essere scartata, ma potrebbe essere minata anche dopo mesi se gli input restano non spesi.

## Gestione di problemi
- Transazione sparita dalla mempool: Se una transazione con fee basse viene rimossa (es. per picchi di traffico), si può ritrasmetterla manualmente (rebroadcast) usando il TXID, anche con script o explorer. Qualcuno potrebbe farlo per conto terzi.
- Replace-by-Fee (RBF): Se la fee è insufficiente, si può sostituire la transazione con una che paga di più, purché marcata con il flag RBF. Una proposta suggerisce che tutte le transazioni siano implicitamente sostituibili, poiché i miner preferiscono comunque fee più alte.
- Child Pays for Parent (CPFP): Se non si può usare RBF (es. transazione non propria o fondi esauriti), si spende un output della transazione bloccata con una nuova transazione che paga fee elevate, rendendo entrambe appetibili per i miner. Serve che la somma delle fee copra entrambe. Problemi sorgono se i nodi scartano la prima transazione, interrompendo la catena; un protocollo in sviluppo mira a trasmettere pacchetti di transazioni per evitarlo.

## Conferma finale
Una transazione è considerata definitiva solo con più conferme (blocchi sopra il suo). Una sola conferma non basta, poiché fork o doppie spese potrebbero invalidarla. Il White Paper suggerisce 6 conferme (circa 60 minuti, con blocchi ogni 10 minuti in media), ma il numero varia in base all’importo e al rischio. La varianza nei tempi di blocco è alta, ma la media si mantiene grazie alla difficoltà di mining.

## Conclusione
Il ciclo si chiude con la transazione "scolpita" nella blockchain, registrando per sempre lo spostamento di valore.

## Programma
Questa lezione è stata realizzata per un Satoshi Spritz Connect.

