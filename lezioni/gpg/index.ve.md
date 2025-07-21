# GPG e Yubico: na guida pratica

## Introduzion
Gnu Privacy Guard (GPG) xe na implementazion open source del standard OpenPGP che permet de criptar, firmar e verificare messagi e file. In questa lezion impareremo come configurar e usar GPG con YubiKey par na gestione sicura de le chiavi.

## Installazion de GPG

### Su Debian/Ubuntu
```bash
sudo apt update
sudo apt install gnupg2
```

### Su macOS
```bash
brew install gnupg
```

### Su Windows
Scarica da: https://gnupg.org/download/

## Generazion de na coppia de chiavi

### Chiave primaria
```bash
gpg --full-generate-key
```

Scegli:
- Tipo: RSA
- Dimensione: 4096 bit
- Scadenza: 2y (2 anni)
- User ID: Nome Cognome <email@example.com>

### Chiavi secondarie
```bash
gpg --edit-key [ID_CHIAVE]
```

Nel prompt GPG:
```
addkey
```

Crea na chiave de firma:
- Tipo: RSA (firma)
- Dimensione: 4096 bit
- Scadenza: 2y

Crea na chiave de criptazion:
- Tipo: RSA (criptazion)
- Dimensione: 4096 bit
- Scadenza: 2y

Crea na chiave de autenticazion:
- Tipo: RSA (autenticazion)
- Dimensione: 4096 bit
- Scadenza: 2y

## Backup de le chiavi

### Esportazion de la chiave privada
```bash
gpg --export-secret-keys --armor [ID_CHIAVE] > chiave_privata.asc
```

### Esportazion de la chiave publica
```bash
gpg --export --armor [ID_CHIAVE] > chiave_publica.asc
```

### Backup del certificato de revoca
```bash
gpg --gen-revoke [ID_CHIAVE] > certificato_revoca.asc
```

## Configurazion de YubiKey

### Installazion de ykman
```bash
sudo apt install yubikey-manager
```

### Verifica de YubiKey
```bash
ykman info
```

### Cambio de PIN
```bash
ykman piv change-pin
```

### Cambio de PUK
```bash
ykman piv change-puk
```

## Trasferimento de chiavi su YubiKey

### Trasferimento de la chiave de firma
```bash
gpg --edit-key [ID_CHIAVE]
```

Nel prompt GPG:
```
key 1
keytocard
```

Scegli: Signature key

### Trasferimento de la chiave de criptazion
```bash
gpg --edit-key [ID_CHIAVE]
```

Nel prompt GPG:
```
key 2
keytocard
```

Scegli: Encryption key

### Trasferimento de la chiave de autenticazion
```bash
gpg --edit-key [ID_CHIAVE]
```

Nel prompt GPG:
```
key 3
keytocard
```

Scegli: Authentication key

## Uso de YubiKey

### Firma de na transazion
```bash
echo "Messagio da firmar" | gpg --clearsign
```

### Criptazion de un file
```bash
gpg --encrypt --recipient [ID_CHIAVE] file.txt
```

### Decriptazion de un file
```bash
gpg --decrypt file.txt.gpg
```

## Verifica de le chiavi

### Lista de le chiavi
```bash
gpg --list-keys
```

### Dettagli de na chiave
```bash
gpg --list-secret-keys --keyid-format LONG
```

### Verifica de la presenza su YubiKey
```bash
gpg --card-status
```

## Best practices

### Sicurezza
- Mantien le chiavi private offline
- Usa passphrase forti
- Fai backup regolari
- Testa le procedure de recovery

### Gestione
- Rota le chiavi regolarmente
- Mantien aggiornati i certificati de revoca
- Verifica periodicamente le chiavi pubbliche

## Troubleshooting

### Problemi comuni
- YubiKey non riconosciuto: verifica i driver
- PIN sbagliato: usa PUK par reset
- Chiave non trovada: verifica l'ID

### Comandi utili
```bash
gpg --version
gpg --list-keys
gpg --list-secret-keys
gpg --card-status
```

## Conclusione
GPG con YubiKey fornisce na soluzion robusta par la gestione sicura de le chiavi crittografiche. La combinazion de software open source e hardware dedicato garantisce na protezion affidabile dei dati sensibili. 