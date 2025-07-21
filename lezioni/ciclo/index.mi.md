# El cicl de vita de una transazion Bitcoin

## Cossa l'è una transazion Bitcoin
Una transazion Bitcoin l'è un'azion registrada sulla blockchain che trasferiss valor de un o pù input (fond ricevuu in precedenza, ciamaa UTXO - Unspent Transaction Outputs) a un o pù output (noeuv destinatari). 
I input hinn output de transazion passaa minga ancora spess, menter i output assegnen satoshi a indirizz specific. Un'eccezion l'è la transazion "coinbase", la prima de ogni blocch, che genera noeuv bitcoin (ricompensa per i miner e fee) sensa input. Se minga tutt i fond de un input vegnen spess, la differenza (change) torna al mittent tramit un output ulterior o, se minga gestida, l'è persa per semper.

## Fasi del cicl de vita
Quest l'è el cicl de vita de una transazion:

- Creazion: El wallet costruiss la transazion scegliend i UTXO de spende in bas all'import da invià e alla strategia per minimizzà i fee. Se l'input supera l'output, se genera un output de "change" (rest) che torna al mittent, aumentand però la dimensión de la transazion e i cost. Qualch wallet cerchèn de evitall.
- Firma: La transazion vegn firmada con una o pù firm digital per ogni input, autenticandla. Quest passagg l'è crucial per la validità e pö coinvolg pù part in cas de transazion multisig.
- Diffusion: La transazion firmada vegn trasmessa alla ret ("broadcast") e inserida nella mempool del nod local. La mempool valida la transazion segond i regol de consens (es. firm valid, fond disponibil) e regol local (es. dimensión massima de 400 KB per evità spam). Poi, el nod la propaga ai peer, che la validen e la inserissen nelle lor mempool, creand una diffusion a cascada. I mempool varien tra nod per configurazion o connession divers.
- Conferma: Un miner include la transazion in un blocch, confermandla sulla blockchain. Tuttavia, fin che la gh'ha minga pù conferm (blocch successiv), la resta vulnerabil a sostituzion o fork. Una transazion con fee bass pö restà in mempool a long o vess scartada, ma la pö vess minada anca dopo mes se i input resten minga spess.

## Gestion de problem
- Transazion sparida de la mempool: Se una transazion con fee bass vegn rimossa (es. per picch de traffic), se pö ritrasmetterla manualment (rebroadcast) doprand el TXID, anca con script o explorer. Qualchun la pö fà per cont terz.
- Replace-by-Fee (RBF): Se la fee l'è insufficent, se pö sostituì la transazion con una che paga de pù, purché marcada con el flag RBF. Una proposta suggeriss che tutt le transazion sien implicitament sostituibil, poiché i miner preferissen comunque fee pù alt.
- Child Pays for Parent (CPFP): Se se pö minga doprà RBF (es. transazion minga propria o fond esaurii), se spend un output de la transazion bloccada con una noeuva transazion che paga fee elevad, rendend entramb appetibil per i miner. Serv che la somma de le fee copra entramb. Problem sörgen se i nod scarten la prima transazion, interrompend la cadena; un protocoll in svilup mira a trasmetter pacchett de transazion per evitall.

## Conferma final
Una transazion l'è considerada definitiva domà con pù conferm (blocch sopra el so). Una sola conferma minga basta, poiché fork o doppi spess podarien invalidalla. El White Paper suggeriss 6 conferm (circa 60 minutt, con blocch ogni 10 minutt in media), ma el numer varia in bas all'import e al risch. La varianza nei temp de blocch l'è alta, ma la media se mantegn grazià alla difficoltà de mining.

## Conclusión
El cicl se sara con la transazion "scolpida" nella blockchain, registrand per semper el spostament de valor.

## Program
Questa lezion l'è stada realizzata per un Satoshi Spritz Connect. 