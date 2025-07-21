# Jade con Electrum Wallet: Configurazion e uso

## Introduzion
Jade può esser usato con Electrum Wallet par offrire na combinazion potente de sicurezza hardware e flessibilità software. In questa lezion impareremo come configurar e usar Jade con Electrum.

## Requisiti

### Software
- **Electrum**: Ultima versione
- **Jade**: Firmware aggiornato
- **Driver**: USB o HID

### Hardware
- **Jade**: Hardware wallet
- **Computer**: Windows, macOS, Linux
- **Cavo**: USB-C

## Installazion

### Electrum
1. **Download**: https://electrum.org
2. **Verifica**: PGP signature
3. **Installa**: Segui le istruzion

### Driver Jade
- **Linux**: Automatico
- **Windows**: HID standard
- **macOS**: Automatico

## Configurazion

### Primo avvio
1. **Avvia Electrum**
2. **Crea nuovo wallet**
3. **Scegli hardware wallet**
4. **Seleziona Jade**

### Connession
1. **Connessi Jade via USB**
2. **Sblocca Jade con PIN**
3. **Conferma connession in Electrum**

### Configurazion wallet
1. **Nome**: Scegli un nome
2. **Tipo**: Standard wallet
3. **Script**: Native SegWit (raccomandato)
4. **Conferma**: Impostazioni

## Funzionalità

### Ricevimento
1. **Tab Receive**
2. **Genera nuovo indiriso**
3. **Mostra QR code**
4. **Condividi indiriso**

### Invio
1. **Tab Send**
2. **Inserisci destinazion**
3. **Specifica importo**
4. **Conferma su Jade**

### Firma
1. **Verifica transazion su Jade**
2. **Conferma dettagli**
3. **Inserisci PIN**
4. **Firma completata**

## Configurazion avanzata

### Multi-sig
1. **Crea multi-sig wallet**
2. **Aggiungi Jade come cosigner**
3. **Configura altri cosigner**
4. **Testa configurazion**

### Coin Control
1. **Abilita Coin Control**
2. **Seleziona UTXO manualmente**
3. **Ottimizza fee**
4. **Migliora privacy**

### Time-locks
1. **Configura time-lock**
2. **Specifica condizion**
3. **Testa funzionalità**
4. **Verifica sicurezza**

## Sicurezza

### Best practices
- **PIN**: Complesso e sicuro
- **Seed**: Backup multipli
- **Firmware**: Aggiornato
- **Electrum**: Verificato

### Verifica
- **Indirisi**: Controlla su Jade
- **Transazioni**: Verifica dettagli
- **Firme**: Conferma su hardware
- **Backup**: Testa ripristino

### Privacy
- **Coin Control**: Usa sempre
- **Indirisi**: Non riutilizzare
- **Tor**: Configura opzional
- **Log**: Pulisci regolarmente

## Troubleshooting

### Problemi comuni
- **Jade non riconosciuto**: Verifica cavo
- **PIN sbagliato**: Reset PIN
- **Firma fallita**: Verifica transazion
- **Connession persa**: Riconnessi

### Debug
```bash
# Log Electrum
tail -f ~/.electrum/logs/electrum.log

# Log Jade
# Verifica display Jade
```

### Recovery
- **Seed**: 12/24 parole
- **Electrum**: Backup wallet
- **Jade**: Factory reset
- **Configurazion**: Ripristina

## Esempi pratici

### Transazion semplice
1. **Ricevi**: 0.001 BTC
2. **Invia**: 0.0005 BTC
3. **Fee**: 0.0001 BTC
4. **Change**: 0.0004 BTC

### Multi-sig setup
1. **2-of-3**: Jade + 2 software
2. **Configurazion**: Electrum
3. **Test**: Transazion di prova
4. **Backup**: Tutte le chiavi

### CoinJoin
1. **Configura**: JoinMarket
2. **Connessi**: Jade
3. **Partecipa**: CoinJoin
4. **Verifica**: Privacy migliorata

## Configurazion server

### Electrum Personal Server
1. **Installa EPS**
2. **Configura Jade**
3. **Connessi server**
4. **Testa funzionalità**

### Tor
1. **Installa Tor**
2. **Configura Electrum**
3. **Testa connession**
4. **Verifica privacy**

## Monitoraggio

### Statistiche
- **Balance**: In tempo reale
- **Transazioni**: Storico completo
- **Fee**: Ottimizzazion
- **Privacy**: Analisi UTXO

### Log
- **Electrum**: Log dettagliati
- **Jade**: Eventi hardware
- **Sistema**: Log sistema
- **Rete**: Connession

## Aggiornamenti

### Firmware Jade
1. **Download**: Nuova versione
2. **Verifica**: Hash SHA256
3. **Backup**: Wallet e seed
4. **Aggiorna**: Firmware

### Electrum
1. **Download**: Nuova versione
2. **Verifica**: PGP signature
3. **Backup**: Wallet
4. **Aggiorna**: Software

## Conclusione
Jade con Electrum offre na soluzion completa par la gestione sicura de Bitcoin. La combinazion de hardware wallet e software flessibile garantisce sicurezza, privacy e controllo completo sui propri fondi. 