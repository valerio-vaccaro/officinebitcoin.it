# Tutorial GPG:

Questa lezione ti guida attraverso l'uso di Gnu Privacy Guard (GPG) per creare una nuova coppia di chiavi, aggiungere sottochiavi per firma e crittografia, fare il backup di tutte le chiavi, trasferire le sottochiavi su un YubiKey e crittografare/firmare un file usando Yubikey. 

È progettato per Linux, macOS o Windows (tramite Gpg4win o Git Bash), con comandi testati su GPG 2.4.5 (luglio 2025). 

Il processo segue le migliori pratiche di sicurezza, come la generazione delle chiavi offline e backup sicuri.

## Installazione
Installa gpg e le utilities necessarie

```bash
sudo apt update
sudo apt install gnupg scdaemon pcscd yubikey-manager
```

```bash
gpg --version
```

Assicurati che la versione sia 2.1.17 o successiva (2.4.5 consigliata).

Installa YubiKey Manager:

```bash
sudo apt install yubikey-manager
```

Verifica il funzionamento della YubiKey

```bash
ykman info
```

Assicurati che l'applet OpenPGP sia abilitata e la modalità CCID attiva.

Usa una macchina air-gapped (senza internet) per generare le chiavi e prevenire perdite.

PIN YubiKey
PIN Utente predefinito: 123456
PIN Admin predefinito: 12345678

Cambiali prima dell'uso (vedi Passo 4).

## Passo 1
Creare una Nuova Coppia di Chiavi GPGGenera una coppia di chiavi primaria (pubblica e privata) per certificazione (C) e firma (S).

Avvia la Generazione della Chiave:

```bash
gpg --expert --full-gen-key
```

Usa --expert per accedere alle opzioni avanzate.
Seleziona il Tipo di Chiave:

```
Per favore seleziona il tipo di chiave desiderato:
   (1) RSA e RSA
   (2) DSA e Elgamal
   (3) DSA (solo firma)
   (4) RSA (solo firma)
   (7) DSA (imposta le tue capacità)
   (8) RSA (imposta le tue capacità)
   (9) ECC (firma e crittografia)
  (10) ECC (solo firma)
  (11) ECC (imposta le tue capacità)
La tua selezione? 8
```

Scegli (8) RSA (imposta le tue capacità) per flessibilità.

Imposta le Capacità:

```
Azioni possibili per una chiave RSA: Sign Certify Encrypt Authenticate
Azioni attualmente consentite: Sign Certify Encrypt
   (S) Attiva/disattiva la capacità di firma
   (E) Attiva/disattiva la capacità di crittografia
   (A) Attiva/disattiva la capacità di autenticazione
   (Q) Finito
La tua selezione? S
```

Disattiva Sign e Encrypt (premi S, E).

Mantieni Certify (premi Q quando finito).

Come risultato tra le azioni attualmente consentite rimane solo Certify

Imposta la Dimensione della Chiave:

```
Le chiavi RSA possono essere tra 1024 e 4096 bit.
Che dimensione vuoi? (3072) 4096
```

Inserisci 4096 (massimo supportato da YubiKey 4/5).

Imposta la Scadenza:

```
Specifica per quanto tempo la chiave deve essere valida.
   0 = chiave non scade
   <n>  = chiave scade in n giorni
   <n>w = chiave scade in n settimane
   <n>m = chiave scade in n mesi
   <n>y = chiave scade in n anni
La chiave è valida per? (0) 2y
```

Inserisci 2y (2 anni) o la tua preferenza. Conferma la data.

Inserisci l'ID Utente:

```
GnuPG deve costruire un ID utente per identificare la tua chiave.
Nome reale: Alice Smith
Indirizzo email: alice@example.com
Commento:
Hai selezionato questo USER-ID:
   "Alice Smith <alice@example.com>"
Cambia (N)ome, (C)ommento, (E)mail o (O)k/(Q)uit? O
```

Fornisci nome ed email. Lascia il commento vuoto. Conferma con O.

Inserisci una passphrase forte (mescola lettere, numeri, simboli; evita parole comuni).

Esempio: Tr0ub4dor&3xplor3r!2025

La passphrase consente di protegge la tua chiave privata.

Genera entropia muovendo il mouse, digita casualmente o usa rng-tools (Linux):

```bash
sudo apt install rng-tools
sudo rngd -r /dev/urandom
```

Attendi il completamento della generazione della chiave. Annota l'ID della chiave (es. 3AA5C34371567BD2) dall'output:

```
gpg: chiave 3AA5C34371567BD2 marcata come fidata al massimo
```

Crea un certificato per revocare la chiave se compromessa:

```bash
gpg --output revoke.asc --gen-revoke 3AA5C34371567BD2
```

Scegli il motivo (es. 1 = chiave compromessa) e salva.

## Passo 2
Creare Sottochiavi per Firma e Crittografia, verrano quindi aggiunte due sottochiavi per firma (S) e crittografia (E). 

La chiave primaria resta solo per certificazione.

Modifichiamo la chiave:

```bash
gpg --expert --edit-key 3AA5C34371567BD2
```

Inserisci la passphrase se richiesto.

Aggiungi sottochiave per Firma:

```
gpg> addkey
Per favore seleziona il tipo di chiave desiderato:
   (3) DSA (solo firma)
   (4) RSA (solo firma)
   (5) Elgamal (solo crittografia)
   (6) RSA (solo crittografia)
   (7) DSA (imposta le tue capacità)
   (8) RSA (imposta le tue capacità)
La tua selezione? 4
```

Scegli (4) RSA (solo firma).

Imposta dimensione: 4096.

Imposta scadenza: 1y (1 anno, le sottochiavi possono essere ruotate più frequentemente).

Conferma e inserisci la passphrase.

Aggiungi s ottochiave per Crittografia:

```
gpg> addkey
```

Scegli (6) RSA (solo crittografia).

Imposta dimensione: 4096.

Imposta scadenza: 1y.

Conferma e inserisci la passphrase.

Salva le Modifiche:

```
gpg> save
```

Verifica le sottochiavi:

```bash
gpg --list-keys --with-subkey-fingerprints 3AA5C34371567BD2
```

Esempio di output:

```
pub   rsa4096/3AA5C34371567BD2 2025-07-18 [SC] [scade: 2027-07-18]
      1234567890ABCDEF1234567890ABCDEF12345678
uid                 Alice Smith <alice@example.com>
sub   rsa4096/4BB6D45482678BE3 2025-07-18 [S] [scade: 2026-07-18]
      2345678901BCDEF12345678901BCDEF123456789
sub   rsa4096/5CC7E56593789CF4 2025-07-18 [E] [scade: 2026-07-18]
      3456789012CDEF123456789012CDEF1234567890
```

Annota le impronte delle sottochiavi per firma (S) e crittografia (E).

## Passo 3
Backup di Tutte le ChiaviEsegui il backup della chiave primaria, delle sottochiavi e della chiave pubblica su due unità USB crittografate per sicurezza.

Prepara le Unità USB:Inserisci due unità USB (es. /dev/sdb e /dev/sdc).

Crea partizioni crittografate (es. con LUKS):

```bash
sudo cryptsetup luksFormat /dev/sdb1
sudo cryptsetup luksOpen /dev/sdb1 backup1
sudo mkfs.ext4 /dev/mapper/backup1
sudo mount /dev/mapper/backup1 /mnt/backup1
```

Ripeti per /dev/sdc1 (es. monta su /mnt/backup2).

Esporta le Chiavi Private:Esporta la chiave primaria e le sottochiavi:

```bash
gpg --armor --export-secret-keys 3AA5C34371567BD2 > /mnt/backup1/secret.asc
gpg --armor --export-secret-keys 3AA5C34371567BD2 > /mnt/backup2/secret.asc
```

Esporta la Chiave Pubblica:

```bash
gpg --armor --export 3AA5C34371567BD2 > /mnt/backup1/public.asc
gpg --armor --export 3AA5C34371567BD2 > /mnt/backup2/public.asc
```

Esporta il Certificato di Revoca:

```bash
cp revoke.asc /mnt/backup1/revoke.asc
cp revoke.asc /mnt/backup2/revoke.asc
```

Smonta in Modo Sicuro:

```bash
sudo umount /mnt/backup1
sudo cryptsetup luksClose backup1
```

Ripeti per backup2. Conserva le unità USB in luoghi separati e sicuri (es. cassaforte).

Elimina le Chiavi Locali (Facoltativo):Se usi una macchina air-gapped, elimina la directory GPG:

```bash
rm -rf ~/.gnupg
```

Se non air-gapped, mantieni le chiavi fino al trasferimento su YubiKey.

## Passo 4
Trasferisci le sottochiavi di firma e crittografia sul YubiKey, mantenendo la chiave primaria offline.

Inserisci Yubikey e verifica:

```bash
gpg --card-status
```

L'output dovrebbe mostrare l'applet OpenPGP (es. Version: 2.0).

Cambia i PIN predefiniti:

```bash
gpg --change-pin
```

PIN Utente: Imposta un nuovo PIN di 6-8 cifre (es. 654321).
PIN Admin: Imposta un nuovo PIN di 8 cifre (es. 87654321).

Modifica la Chiave per il Trasferimento:

```bash
gpg --expert --edit-key 3AA5C34371567BD2
```

Seleziona e Trasferisci la Sottochiave di Firma:Elenca le chiavi per identificare gli indici delle sottochiavi:

```
gpg> list
```

Esempio:

```
sec  rsa4096/3AA5C34371567BD2 2025-07-18 [C]
ssb  rsa4096/4BB6D45482678BE3 2025-07-18 [S]
ssb  rsa4096/5CC7E56593789CF4 2025-07-18 [E]
```

Seleziona la sottochiave di firma:

```
gpg> key 1
```

La sottochiave di firma ([S]) avrà un asterisco (*).

Trasferisci su YubiKey:

```
gpg> keytocard
Seleziona dove memorizzare la chiave:
  (1) Chiave di firma
  (2) Chiave di crittografia
  (3) Chiave di autenticazione
La tua selezione? 1
```

Inserisci il PIN Admin (87654321). La sottochiave privata di firma viene trasferita sul YubiKey e sostituita da uno stub nel portachiavi.

Seleziona e Trasferisci la Sottochiave di Crittografia:Deseleziona la sottochiave di firma:

```
gpg> key 1
```

Seleziona la sottochiave di crittografia:

```
gpg> key 2
```

Trasferisci su YubiKey:

```
gpg> keytocard
La tua selezione? 2
```

Inserisci di nuovo il PIN Admin.

Salva le Modifiche:

```
gpg> save
```

Le sottochiavi private sono ora sul YubiKey, con stub locali.

Verifica YubiKey:

```bash
gpg --card-status
```

Controlla che gli slot Signature key e Encryption key mostrino le impronte digitali delle sottochiavi.

Esporta le sottochiavi private (per verifica del backup):

```bash
gpg --armor --export-secret-subkeys 3AA5C34371567BD2 > secret-subkeys.asc
```

Elimina la directory GPG locale:

```bash
rm -rf ~/.gnupg
```

Reimporta la chiave pubblica e gli stub:

```bash
gpg --import public.asc
gpg --import secret-subkeys.asc
```

La chiave primaria privata non è più sul computer.

## Passo 5
Usa YubiKey per crittografare e firmare un file per un destinatario.

Prepara un File di Prova:

```bash
echo "Questo è un messaggio segreto." > test.txt
```

Ottieni la chiave pubblica del destinatario (es. bob@example.com):

```bash
gpg --keyserver hkps://keys.openpgp.org --search-keys bob@example.com
```

Oppure importa da un file:

```bash
gpg --import bob_public.asc
```

Crittografa e Firma:Crittografa per bob@example.com e firma con Yubikey:

```bash
gpg --encrypt --sign --recipient bob@example.com test.txt
```

Inserisci il PIN Utente (654321) quando richiesto. 

Se YubiKey richiede la conferma tattile (opzionale, impostata tramite ykman openpgp keys set-touch), tocca YubiKey.

L'output generato sarà test.txt.gpg

Decrittografa il file (richiede YubiKey):

```bash
gpg --decrypt test.txt.gpg > test_decrypted.txt
```

Inserisci il PIN Utente e tocca Yubikey se necessario. 

Verifica che test_decrypted.txt corrisponda a test.txt.

Bob può decriptare con la sua chiave privata e verificare la tua firma:

```bash
gpg --decrypt test.txt.gpg
``

Se inece vuoi solo fimrare il file

```bash
gpg --detach-sign test.txt
```

Verrà generato un file di output chiamato test.txt.sig

Per verificarlo:

```bash
gpg --verify test.txt.sig test.txt
```

## Pratiche di sicurezza
- Genera sempre le chiavi su una macchina offline per evitare esposizioni.
- Conserva le unità USB con le chiavi private in luoghi separati e sicuri (es. cassaforte o banca).
- Usa PIN forti e unici. Se i tentativi di PIN sono superati (3 per Utente, 3 per Admin), Yubikey si blocca e richiede un reset, perdendo tutte le chiavi.
- Mantieni revoke.asc accessibile ma sicuro per revocare la chiave se compromessa.
- Crea nuove sottochiavi prima della scadenza (es. ogni anno) in queta maniera:

```bash
gpg --expert --edit-key 3AA5C34371567BD2
gpg> addkey
```

Trasferisci le nuove sottochiavi sul YubiKey e aggiorna la chiave pubblica sui server:

```bash
gpg --keyserver hkps://keys.openpgp.org --send-keys 3AA5C34371567BD2
```

Usa un secondo YubiKey per ridondanza:

```bash
gpg --import secret.asc
gpg --expert --edit-key 3AA5C34371567BD2
```

Ripeti i passaggi keytocard per il secondo YubiKey.

Se fosse necessario resettare Yubikey:

```bash
ykman openpgp reset
```

Mentre per ripristina le sottochiavi dal backup:

```bash
gpg --import secret.asc
```

“Chiave Pubblica Non Utilizzabile”:Assicurati che la chiave pubblica del destinatario sia importata e fidata:

```bash
gpg --edit-key bob@example.com
gpg> trust
```
Imposta a 5 = Fiducia massima.
