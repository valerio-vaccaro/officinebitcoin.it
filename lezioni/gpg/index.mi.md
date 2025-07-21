# Tutorial GPG:

Questa lezion te guida nell'usà Gnu Privacy Guard (GPG):
- per creà una noeuva coppia de claav,
- aggiung subclaav per firmà e criptà,
- fà backup de tutt le claav,
- trasferì subclaav a un YubiKey, e
- criptà/firmà un file doprand Yubikey.

L'è progettada per Linux con comand testaa su GPG 2.2.40/Debian 12. I stess comand poden funzionà similment su alter version de Linux e anca su MacOSX e Windows (eccett per filesystem criptaa).

El process seguiss le miglior pratiche de sicurezza, come la generazion de claav offline e backup sicur.

## Installazion
Installa gpg e i utilità necessari

```bash
sudo apt update
sudo apt install gnupg scdaemon pcscd yubikey-manager
```

Assicurass che la version sia 2.1.17 o pù recent (2.4.5 raccomandada).

```bash
gpg --version
```

Controlla la funzionalità de YubiKey

```bash
ykman info
```

Assicurass che l'applet OpenPGP sia abilità e el mode CCID sia attiv.

Dopra una macchina air-gapped (minga internet) per generà claav e evità fughe.

Ricorda che i PIN predefinii de YubiKey minga hinn sicur e hinn:
- PIN Utent predefinii: 123456
- PIN Admin predefinii: 12345678
Cambial prima de l'usà (vedi Pass 4).

## Pass 1
Genera una coppia de claav GPG primaria (pubblica e privada) per certificazion (C) domà; tutt le alter claav vegnarann derivada de questa.

Inizia la generazion de claav doprand --expert per opzion avanzaa.

```bash
gpg --expert --full-gen-key
```

Seleziona Tip de Claav:

```
Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
   (7) DSA (set your own capabilities)
   (8) RSA (set your own capabilities)
   (9) ECC and ECC
  (10) ECC (sign only)
  (11) ECC (set your own capabilities)
  (13) Existing key
  (14) Existing key from card
Your selection? 8
```

Scegli (8) RSA (set your own capabilities) per personalizzà el comportament de la claav.

Imposta le capacità:

```
Possible actions for a RSA key: Sign Certify Encrypt Authenticate
Current allowed actions: Sign Certify Encrypt

   (S) Toggle the sign capability
   (E) Toggle the encrypt capability
   (A) Toggle the authenticate capability
   (Q) Finished

Your selection? S
```

Disabilita Sign e Encrypt (premi S, E).

Mantegn Certify (premi Q quand l'è fata).

Come risultat, domà Certify resta tra le azion permess.

Imposta la Grandezza de la Claav:

```
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072) 4096
```

Inseriss 4096 (massima supportada da YubiKey 4/5).

Imposta la Scadenza:

```
Please specify how long the key should be valid.
             0 = key does not expire
          <n>  = key expires in n days
          <n>w = key expires in n weeks
          <n>m = key expires in n months
          <n>y = key expires in n years
Key is valid for? (0)
```

Inseriss 3y (3 agn) o la tua preferenza. Conferma la data.

Inseriss l'ID Utent:

```
GnuPG needs to construct a user ID to identify your key.

Real name: Satoshi Spritz
Email address: info@satoshispritz.it
Comment:
You selected this USER-ID:
    "Satoshi Spritz <info@satoshispritz.it>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? o
```

Forniss nom e email. Lassa el comment vöid. Conferma con O.

Inseriss una passphrase fort (miscia letter, numer, simbol; evità parol comun).

Esempi: Tr0ub4dor&3xplor3r!2025

La passphrase protegg la tua claav privada.

Genera entropia movend el mouse, scrivend a cas, o doprand rng-tools (Linux e domà se te la capiss ben):

```bash
sudo apt install rng-tools
sudo rngd -r /dev/urandom
```

Aspetta che la generazion de claav se completa. Nota l'ID de la claav (es. C2033656849FC82BA3C365E33C9BF8B9CB86875D) de l'output:

```
gpublic and secret key created and signed.

pub   rsa2048 2025-07-20 [C]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid                      Satoshi Spritz <info@satoshispritz.it>

```

Crea un certificat de revoca in cas che la claav sia compromessa (el tuo client l'ha già creada):

```bash
gpg --output revoke_master_satoshispritz.asc --gen-revoke C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Scegli el motiv (es. 1 = claav compromessa) e salva.

## Pass 2
Crea Subclaav de Firm e Criptazion. Do subclaav vegnarann aggiunt per firmà (S) e criptà (E).

La claav primaria resta per certificazion domà.

Edita la claav:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Inseriss la passphrase se richiesta.

Aggiung Subclaav de Firm:

```
gpg> addkey
Please select what kind of key you want:
   (3) DSA (sign only)
   (4) RSA (sign only)
   (5) Elgamal (encrypt only)
   (6) RSA (encrypt only)
   (7) DSA (set your own capabilities)
   (8) RSA (set your own capabilities)
  (10) ECC (sign only)
  (11) ECC (set your own capabilities)
  (12) ECC (encrypt only)
  (13) Existing key
  (14) Existing key from card
Your selection? 4
```

Scegli (4) RSA (sign only).

Imposta grandezza: 4096.

Imposta scadenza: 2y (2 agn, le subclaav poden vess rotata pù frequentement).

Conferma e inseriss la passphrase.

Aggiung Subclaav de Criptazion:

```
gpg> addkey
```

Scegli (6) RSA (encrypt only).

Imposta grandezza: 4096.

Imposta scadenza: 2y.

Conferma e inseriss la passphrase.

Salva i Cambiament:

```
gpg> save
```

Controlla le subclaav:

```bash
gpg --list-keys --with-subkey-fingerprints C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Esempi de output:

```
pub   rsa4096 2025-07-20 [C] [expires: 2028-07-20]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid           [ultimate] Satoshi Spritz <info@satoshispritz.it>
sub   rsa4096 2025-07-20 [S] [expires: 2027-07-20]
      1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3
sub   rsa4096 2025-07-20 [E] [expires: 2027-07-20]
      94C11C615BE049B97899FA3C8DC3736F499D6C3E

```

Nota le impront digital de le subclaav de firm (S) e criptazion (E).

## Pass 3
Backup de Tutt le Claav. Fà backup de la claav primaria, subclaav, e claav pubblica a do drive USB criptaa per sicurezza.

Prepara Drive USB: Inseriss do drive USB (es. /dev/sdb e /dev/sdc).

Crea partizion criptaa (es. con LUKS):

```bash
sudo cryptsetup luksFormat /dev/sdb1
sudo cryptsetup luksOpen /dev/sdb1 backup1
sudo mkfs.ext4 /dev/mapper/backup1
sudo mount /dev/mapper/backup1 /mnt/backup1
```

Ripeti per /dev/sdc1 (es. monta su /mnt/backup2).

Esporta Claav Privad: Esporta la claav primaria e le subclaav:

```bash
gpg --armor --export-secret-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/secret_master_satoshispritz.asc
gpg --armor --export-secret-keys 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/secret_sign_satoshispritz.asc
gpg --armor --export-secret-keys 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/secret_encrypt_satoshispritz.asc
```

Esporta claav pubbliche:

```bash
gpg --armor --export C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/public_master_satoshispritz.asc
gpg --armor --export 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/public_sign_satoshispritz.asc
gpg --armor --export 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/public_encrypt_satoshispritz.asc
```

Esporta el Certificat de Revoca:

```bash
cp revoke_master_satoshispritz.asc /mnt/backup1/revoke_master_satoshispritz.asc
cp revoke_master_satoshispritz.asc /mnt/backup2/revoke_master_satoshispritz.asc
```

Smonta Sicurament:

```bash
sudo umount /mnt/backup1
sudo cryptsetup luksClose backup1
```

Ripeti per backup2. Conserva i drive USB in locazion separad e sicur (es. cassafort).

Cancella Claav Local (Opzional): Se dopri una macchina air-gapped, cancella la directory GPG:

```bash
rm -rf ~/.gnupg
```

Le claav vegnarann poi importada sulla macchina dove le doprarass.

Se minga air-gapped, mantegn le claav fin al trasferiment a YubiKey.

## Pass 4
Trasferiss subclaav de firm e criptazion al YubiKey, mantegnend la claav primaria offline.

Inseriss Yubikey e controlla:

```bash
gpg --card-status
```

L'output dovria mostrà l'applet OpenPGP (es. Version: 2.0).

Cambia i PIN predefinii:

```bash
gpg --change-pin
```

PIN Utent: Imposta un noeuv PIN de 6-8 cifr (es. 654321).
PIN Admin: Imposta un noeuv PIN de 8 cifr (es. 87654321).

Edita la Claav per el Trasferiment:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Seleziona e Trasferiss Subclaav de Firm: Lista le claav per identificà i indici de le subclaav:

```
gpg> list
```

Esempi:

```
sec  rsa4096/3C9BF8B9CB86875D
     created: 2025-07-20  expires: 2028-07-20  usage: C
     trust: ultimate      validity: ultimate
ssb  rsa4096/426E4AB8E6D72AC3
     created: 2025-07-20  expires: 2027-07-20  usage: S
ssb  rsa4096/8DC3736F499D6C3E
     created: 2025-07-20  expires: 2027-07-20  usage: E
```

Seleziona la subclaav de firm:

```
gpg> key 1
```

La subclaav de firm gh'avarà un asterisc (*).

Trasferiss al YubiKey:

```
gpg> keytocard
Please select where to store the key:
   (1) Signature key
   (3) Authentication key
Your selection?
```

Inseriss el PIN Admin (es. 87654321). La subclaav privada de firm vegn trasferida al YubiKey e sostituida da un stub nel keyring.

Seleziona e Trasferiss Subclaav de Criptazion: Deseleziona la subclaav de firm:

```
gpg> key 1
```

Seleziona la subclaav de criptazion:

```
gpg> key 2
```

Trasferiss al YubiKey:

```
gpg> keytocard
Please select where to store the key:
   (2) Encryption key
Your selection? 2
```

Inseriss el PIN Admin de noeuv.

Salva i Cambiament:

```
gpg> save
```

Le subclaav privad hinn ora sul YubiKey, con stub local.

Controlla YubiKey:

```bash
gpg --card-status
```

Controlla che i slot Signature key e Encryption key mostren le impront digital de le subclaav.

Esporta subclaav privad (per verificà el backup):

```bash
gpg --armor --export-secret-subkeys C2033656849FC82BA3C365E33C9BF8B9CB86875D > secret-subkeys-satoshispritz.asc
```

Cancella la directory GPG local:

```bash
rm -rf ~/.gnupg
```

Re-importa la claav pubblica e i stub:

```bash
gpg --import public.asc
gpg --import secret-subkeys-satoshispritz.asc
```

La claav privada primaria minga l'è pù sul computer.

## Pass 5
Dopra YubiKey per criptà e firmà un file per un destinatari.

Prepara un File de Test:

```bash
echo "This is a secret message." > test.txt
```

Oten la claav pubblica del destinatari (es. bob@example.com):

```bash
gpg --keyserver hkps://keys.openpgp.org --search-keys bob@example.com
```

O importa de un file:

```bash
gpg --import bob_public.asc
```

Cripta e Firma: Cripta per bob@example.com e firma con Yubikey:

```bash
gpg --encrypt --sign --recipient bob@example.com test.txt
```

Inseriss el PIN Utent (es. 654321) quand richiest.

Se YubiKey richied conferma touch (opzional, impostada via ykman openpgp keys set-touch), tocca el YubiKey.

L'output sarà test.txt.gpg

Decripta el file (richied YubiKey):

```bash
gpg --decrypt test.txt.gpg > test_decrypted.txt
```

Inseriss el PIN Utent e tocca Yubikey se necessari.

Controlla che test_decrypted.txt corrisponda a test.txt.

Bob pö decriptà con la so claav privada e verificà la tua firma:

```bash
gpg --decrypt test.txt.gpg
```

Se te vöret domà firmà el file, te pödet doprà i comand seguent.

```bash
gpg --detach-sign test.txt
```

Quest generarà un file de output ciamaa test.txt.sig

Per verificall:

```bash
gpg --verify test.txt.sig test.txt
```

## Pratiche de Sicurezza
- Semper genera claav su una macchina offline per evità esposizion.
- Conserva i drive USB con claav privad in locazion separad e sicur (es. cassafort o banca).
- Dopera PIN fort e unic. Se i tentativ de PIN vegnen superaa (3 per Utent, 3 per Admin), Yubikey se blocca e richied un reset, perdend tutt le claav.
- Mantegn revoke.asc accessibil ma sicur per revocà la claav se compromessa.
- Crea noeuv subclaav prima de la scadenza (es. ogni agn) come seguiss:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
gpg> addkey
```

Trasferiss noeuv subclaav al YubiKey e aggiorna la claav pubblica sui server:

```bash
gpg --keyserver hkps://keys.openpgp.org --send-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Dopera un segond YubiKey per ridondanza:

```bash
gpg --import secret.asc
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Ripeti i pass de keytocard per el segond YubiKey.

Se te gh'hee besogn de resettà Yubikey:

```bash
ykman openpgp reset
```

Per restaurà subclaav de backup:

```bash
gpg --import secret.asc
```

"Public Key Not Usable": Assicurass che la claav pubblica del destinatari sia importada e fidada:

```bash
gpg --edit-key bob@example.com
gpg> trust
```
Imposta a 5 = Ultimate trust. 