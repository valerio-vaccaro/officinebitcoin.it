# Introduzion al Mining
El mining de Bitcoin l'è un process fondamental del protocoll che serv a proponì un ordin tra le transazion present nella mempool, scernendon un sotinsem per creà un noeuv blocc e aggiornà l'stat de la blockchain.

El mining l'è progettaa per vess decentralizzaa e casual (tra virgolett, poiché basaa su un puzzle crittografich), evitand inscì una gestion centralizzaa de le transazion.

## Scopo del Mining
El mining risolv problem legaa a la centralizzazion, come:

- Censura: un ent central podariss blocà quaj transazion, ma con miner decentralizzaa le transazion hann pù possibilitaa de vess incluse.
- Doppia spesa: senza un miner corrompibil, l'è difficil riscriv la storia o favorì una transazion a scapit de un'altra.
- Timestamping: forniss un ordin temporal segur e condivis, minga dipendent da un'autoritaa central, ma dal consens tra miner e nod.

# Come Funziona el Mining
El process de mining se pö spiegà pass per pass:

- Scelta de le transazion: el miner scern le transazion dalla mempool, spess privilegiand quelle con fee pù alt, ottimizzand el profit (un problem NP-complet simil al "riempiment del sacch").
- Costruzion de la Coinbase: el miner crea una transazion special (coinbase) che assegna a sé stess el prem del blocc (attualment 3,125 BTC, dimezzaa ogni quater ann) pù le commiss (fee) de le transazion scernide.
- Merkle Root: le transazion scernide vegnarann organizzaa in una struttura dat ad alber (Merkle Tree), che genera un Merkle Root, un hash che rappresenta tutt le transazion e el so ordin.
- Header del Blocc: el miner costruiss el prototip de l'header del blocc, includend:
1. El timestamp.
2. L'hash del blocc precedenta.
3. El Merkle Root.
4. La difficoltaa (target), che dipend dalla ret.
5. Un nonce (numer casual inizializzaa, per esempi, a zero).
- Puzzle Crittografich: El miner aplica duu volt l'algoritm SHA-256 all'header e verifica se el resultat l'ha un numer suficient de zero inizial (inferior a la soglia de difficoltaa). Se l'è minga, modifica el nonce o alter camp (es. timestamp o ordin de le transazion) e repeta el calcol. Quest l'è un lavor de forza bruta senza scorciatoi, grazi a le proprietaa de SHA-256.

## Ottimizzazion
Per velocizzà el process, i miner pö calculà el prim SHA-256 sui prim 64 byte de l'header (immutabil) e poeu iterà domà sul rest, cambiand el nonce. La specializzazion l'ha portaa a hardware (ASIC) che eseguiss miliard de tentativ al second.

# Process de Validazion
Quand un miner trova una soluzion, trasmet el blocc complet (header + transazion) alla ret. I nod validaa:
- l'hash de l'header (un sol SHA-256 per confermà).
- la correttezza de le informazion del blocc (timestamp, hash del blocc precedenta, Merkle Root e nonce).
- la riproducibilitaa del Merkle Root dopo avè controllaa la correttezza de tutt le transazion associade.

Se valid, el blocc ven aggiunt alla blockchain. El prem (coinbase + fee) l'è spendibil domà dopo 100 conferme (circa 16 ore), per garantì stabilitaa.

# Cost e Ricompens del Mining
Cost:

- Corrent elettrica: cost variabil principal.
- Hardware: ASIC costos e a vita breva, rapidament superaa da model pù efficient.
- Infrastruttur: raffreddament, installazion, manutenzion (es. pannell solar hinn minga "gratis").

Ricompens:

- Prem fiss (dimezzaa nel 2024 a 3,125 BTC).
- Fee variabil de le transazion.

El miner dev rispettà le regol del consens: un blocc minga valid ven scartaa, sprecand risors senza ricompensa. Anca un blocc valid pö vess "orfanaa" se un alter miner venc la gara, causand perdite.

## Strategia Economica
El mining l'è competitiv: i miner cercaa de massimizzà el temp de attivitaa per ammortizzà i cost fiss. Us spot (es. accend i miner domà con energia in eccess) hinn poch pratic, poiché i cost inizial richied continuitaa. El ritorn sull'investiment pö vess longh e incert.

# Mining in Solo e Pool

- Solo Mining: el miner lavora da sol, costruend el blocc con un full node o software personalizzaa. Se trova un blocc, pren tutt el prem, ma la probabilitaa l'è bassissima (poderess volè secol con un singol ASIC).
- Pool Mining: protocoll come Stratum permettaa ai miner de collaborà:
1. La pool forniss un template (coinbase, Merkle Root, ecc.).
2. I miner inviaa share (tentativ con un cert numer de zero, inferior a la difficoltaa del blocc) come prova de lavor.
3. Quand un miner de la pool trova un blocc, el prem ven divis proporzionalment a le share inviade.
- Stratum v2: Evoluzion che permettaa ai miner de scernì le transazion, riducend la centralizzazion de la pool, anca se richied controll per garantì la correttezza (es. fee per la pool).

# Stima de l'Hashrate
L'hashrate (potenz de calcol) se stima:
- In una Pool: Contand le share ricevude in un'unitaa de temp, moltiplicade per la difficoltaa de le share. L'è una stima perturbabil dalla fortuna.
- Global: Usand la difficoltaa de Bitcoin e el temp medi tra blocc (circa 10 minutt). Oscillazion hinn normal, ma la media l'è affidabil.

Hardware come Nerd Miner usa contator intern per dat precis, menter le pool se basaa su stime pù variabil, visibil nei grafic oscillant.

# Programma
Questa lezion l'è stada realizzaa per un Satoshi Spritz Connect. 