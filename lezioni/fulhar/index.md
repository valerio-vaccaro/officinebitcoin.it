# Fullnode ed hardware per un nodo
Avere un nodo Bitcoin è fondamentale in quanto consente con la massima privacy di:

- validare l'intera catena di Bitcoin,
- controllare il bilancio dei nostri wallet,
- trasmettere le nostre nuove transazioni
- ...

## Selezione dell'hardware

- minimo 2GB (consigliati 4GB) di memoria RAM,
- disco di almeno 1TB (consigliati 2TB) di memoria di massa,
- cpu multi-core sufficientemente performante (probabilmente qualsiasi processore sviluppato nell'ultimo decennio).

### Riutilizza un vecchio computer

Un vecchio computer può essere riciclato come nodo, in caso di laptop si consiglia di rimuovere la batteria che, posta sempre sotto carica, potrebbe costituire un rischio. Il grande vantaggio è dato dal costo pari a zero o limitato solo al disco più capiente.

### Raspberry pi ed altre schede

Raspberry pi è una scheda ARM molto utilizzata per la realizzazione di sistemi IoT e nodi, il costo eccessivo e la necessità di un disco su presa USB tuttavia la rendono non la migliore delle scelte possibili in termini di performance e di stabilità.

Odroid-M1 è una scheda ARM performante e con uno slot interno per l'aggiunta di memoria di massa aggiuntiva.

### Thin client

Con un budget molto ridotto 30-100 euro è possibile acquistare un Thin Client usato (su ebay) che associa bassi consumi a performance sufficienti a far girare il nodo.

Come esempi di Thin Client sono stati testati i seguenti modelli:

- Fujitsu Futro s920
- HP t620

## Selezione del software

Installare meno software possibile su di un nodo limita i possibili attacchi e rende il sistema più semplice da mantenere.

Online si trovano soluzioni preconfezionate (Umbrel, Mynode, ...) che mascherano i check di sicurezza ed aggiungono software e script (ad esempio docker) di difficile controllo. In queste lezioni porremo l'attenzione sulla creazione di un nodo a mano ovvero installando manualmente tutti i software necessari.

### Step 0 - Il sistema operativo

La prima scelta da fare è il sistema operativo, il consiglio è di utilizzare Linux in una versione LTS ovvero in cui sia garantito supporto per un numero sufficientemente lungo di anni. La mia personale scelta ricade su Debian 12.

Il sistema operativo scelto va quindi installato sul computer e vanno aggiornati tutti i pacchetti (l'aggiornamento è qualcosa che ci seguirà durante tutta la vita del nodo).

Si consiglia anche di installare tor ( e/o altra VPN se necessaria) ed ssh così da permettere la manutenzione remota del nodo.

Un gruppo di continuità infine potrebbe salvare il nodo da bruschi cali di corrente evitando di lasciare bitcoin e gli altri software in uno stato inconsistente.

### Step 1 - Installiamo Bitcoin
(ancora in sviluppo)

## Programma
L'installazione del nodo è divisa su più lezioni, qui un elenco di quelle già tenute:

| Data        | Note                                           |
|-------------|------------------------------------------------|
| 240108-2100 | Selezione dell'hardware                        |
