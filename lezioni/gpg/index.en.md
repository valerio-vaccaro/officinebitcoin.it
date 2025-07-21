# GPG Tutorial:

This lesson guides you through using Gnu Privacy Guard (GPG):
- to create a new key pair,
- add subkeys for signing and encryption,
- back up all keys,
- transfer subkeys to a YubiKey, and
- encrypt/sign a file using Yubikey.

It is designed for Linux with commands tested on GPG 2.2.40/Debian 12. The same commands may work similarly on other Linux versions and also on MacOSX and Windows (except for encrypted filesystems).

The process follows best security practices, such as offline key generation and secure backups.

## Installation
Install gpg and the necessary utilities

```bash
sudo apt update
sudo apt install gnupg scdaemon pcscd yubikey-manager
```

Make sure the version is 2.1.17 or later (2.4.5 recommended).

```bash
gpg --version
```

Check YubiKey functionality

```bash
ykman info
```

Ensure the OpenPGP applet is enabled and CCID mode is active.

Use an air-gapped machine (no internet) to generate keys and prevent leaks.

Remember that YubiKey default PINs are not secure and are:
- Default User PIN: 123456
- Default Admin PIN: 12345678
Change them before use (see Step 4).

## Step 1
Generate a primary GPG key pair (public and private) for certification (C) only; all other keys will derive from this.

Start key generation using --expert for advanced options.

```bash
gpg --expert --full-gen-key
```

Select Key Type:

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

Choose (8) RSA (set your own capabilities) to customize key behavior.

Set capabilities:

```
Possible actions for a RSA key: Sign Certify Encrypt Authenticate 
Current allowed actions: Sign Certify Encrypt 

   (S) Toggle the sign capability
   (E) Toggle the encrypt capability
   (A) Toggle the authenticate capability
   (Q) Finished

Your selection? S
```

Disable Sign and Encrypt (press S, E).

Keep Certify (press Q when done).

As a result, only Certify remains among the allowed actions.

Set Key Size:

```
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072) 4096
```

Enter 4096 (maximum supported by YubiKey 4/5).

Set Expiry:

```
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 
```

Enter 3y (3 years) or your preference. Confirm the date.

Enter User ID:

```
GnuPG needs to construct a user ID to identify your key.

Real name: Satoshi Spritz
Email address: info@satoshispritz.it
Comment: 
You selected this USER-ID:
    "Satoshi Spritz <info@satoshispritz.it>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? o
```

Provide name and email. Leave comment blank. Confirm with O.

Enter a strong passphrase (mix letters, numbers, symbols; avoid common words).

Example: Tr0ub4dor&3xplor3r!2025

The passphrase protects your private key.

Generate entropy by moving the mouse, typing randomly, or using rng-tools (Linux and only if you understand it well):

```bash
sudo apt install rng-tools
sudo rngd -r /dev/urandom
```

Wait for key generation to complete. Note the key ID (e.g. C2033656849FC82BA3C365E33C9BF8B9CB86875D) from the output:

```
gpublic and secret key created and signed.

pub   rsa2048 2025-07-20 [C]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid                      Satoshi Spritz <info@satoshispritz.it>

```

Create a revocation certificate in case the key is compromised (your client may have already created it):

```bash
gpg --output revoke_master_satoshispritz.asc --gen-revoke C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Choose the reason (e.g. 1 = key compromised) and save.

## Step 2
Create Signing and Encryption Subkeys. Two subkeys will be added for signing (S) and encryption (E).

The primary key remains for certification only.

Edit the key:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Enter passphrase if requested.

Add Signing Subkey:

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

Choose (4) RSA (sign only).

Set size: 4096.

Set expiry: 2y (2 years, subkeys can be rotated more frequently).

Confirm and enter passphrase.

Add Encryption Subkey:

```
gpg> addkey
```

Choose (6) RSA (encrypt only).

Set size: 4096.

Set expiry: 2y.

Confirm and enter passphrase.

Save Changes:

```
gpg> save
```

Check subkeys:

```bash
gpg --list-keys --with-subkey-fingerprints C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Example output:

```
pub   rsa4096 2025-07-20 [C] [expires: 2028-07-20]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid           [ultimate] Satoshi Spritz <info@satoshispritz.it>
sub   rsa4096 2025-07-20 [S] [expires: 2027-07-20]
      1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3
sub   rsa4096 2025-07-20 [E] [expires: 2027-07-20]
      94C11C615BE049B97899FA3C8DC3736F499D6C3E

```

Note the fingerprints of the signing (S) and encryption (E) subkeys.

## Step 3
Backup All Keys. Back up the primary key, subkeys, and public key to two encrypted USB drives for safety.

Prepare USB Drives: Insert two USB drives (e.g. /dev/sdb and /dev/sdc).

Create encrypted partitions (e.g. with LUKS):

```bash
sudo cryptsetup luksFormat /dev/sdb1
sudo cryptsetup luksOpen /dev/sdb1 backup1
sudo mkfs.ext4 /dev/mapper/backup1
sudo mount /dev/mapper/backup1 /mnt/backup1
```

Repeat for /dev/sdc1 (e.g. mount on /mnt/backup2).

Export Private Keys: Export the primary key and subkeys:

```bash
gpg --armor --export-secret-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/secret_master_satoshispritz.asc
gpg --armor --export-secret-keys 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/secret_sign_satoshispritz.asc
gpg --armor --export-secret-keys 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/secret_encrypt_satoshispritz.asc
```

Export public keys:

```bash
gpg --armor --export C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/public_master_satoshispritz.asc
gpg --armor --export 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/public_sign_satoshispritz.asc
gpg --armor --export 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/public_encrypt_satoshispritz.asc
```

Export the Revocation Certificate:

```bash
cp revoke_master_satoshispritz.asc /mnt/backup1/revoke_master_satoshispritz.asc
cp revoke_master_satoshispritz.asc /mnt/backup2/revoke_master_satoshispritz.asc
```

Unmount Safely:

```bash
sudo umount /mnt/backup1
sudo cryptsetup luksClose backup1
```

Repeat for backup2. Store the USB drives in separate, secure locations (e.g. safe).

Delete Local Keys (Optional): If using an air-gapped machine, delete the GPG directory:

```bash
rm -rf ~/.gnupg
```

Keys will then need to be imported on the machine where you will use them.

If not air-gapped, keep the keys until transfer to YubiKey.

## Step 4
Transfer signing and encryption subkeys to the YubiKey, keeping the primary key offline.

Insert Yubikey and check:

```bash
gpg --card-status
```

The output should show the OpenPGP applet (e.g. Version: 2.0).

Change default PINs:

```bash
gpg --change-pin
```

User PIN: Set a new 6-8 digit PIN (e.g. 654321).
Admin PIN: Set a new 8 digit PIN (e.g. 87654321).

Edit the Key for Transfer:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Select and Transfer Signing Subkey: List keys to identify subkey indices:

```
gpg> list
```

Example:

```
sec  rsa4096/3C9BF8B9CB86875D
     created: 2025-07-20  expires: 2028-07-20  usage: C   
     trust: ultimate      validity: ultimate
ssb  rsa4096/426E4AB8E6D72AC3
     created: 2025-07-20  expires: 2027-07-20  usage: S   
ssb  rsa4096/8DC3736F499D6C3E
     created: 2025-07-20  expires: 2027-07-20  usage: E
```

Select the signing subkey:

```
gpg> key 1
```

The signing subkey will have an asterisk (*).

Transfer to YubiKey:

```
gpg> keytocard
Please select where to store the key:
   (1) Signature key
   (3) Authentication key
Your selection?
```

Enter Admin PIN (e.g. 87654321). The signing private subkey is transferred to the YubiKey and replaced by a stub in the keyring.

Select and Transfer Encryption Subkey: Deselect the signing subkey:

```
gpg> key 1
```

Select the encryption subkey:

```
gpg> key 2
```

Transfer to YubiKey:

```
gpg> keytocard
Please select where to store the key:
   (2) Encryption key
Your selection? 2
```

Enter Admin PIN again.

Save Changes:

```
gpg> save
```

The private subkeys are now on the YubiKey, with local stubs.

Check YubiKey:

```bash
gpg --card-status
```

Check that the Signature key and Encryption key slots show the subkey fingerprints.

Export private subkeys (to verify backup):

```bash
gpg --armor --export-secret-subkeys C2033656849FC82BA3C365E33C9BF8B9CB86875D > secret-subkeys-satoshispritz.asc
```

Delete the local GPG directory:

```bash
rm -rf ~/.gnupg
```

Re-import the public key and stubs:

```bash
gpg --import public.asc
gpg --import secret-subkeys-satoshispritz.asc
```

The primary private key is no longer on the computer.

## Step 5
Use YubiKey to encrypt and sign a file for a recipient.

Prepare a Test File:

```bash
echo "This is a secret message." > test.txt
```

Get the recipient's public key (e.g. bob@example.com):

```bash
gpg --keyserver hkps://keys.openpgp.org --search-keys bob@example.com
```

Or import from a file:

```bash
gpg --import bob_public.asc
```

Encrypt and Sign: Encrypt for bob@example.com and sign with Yubikey:

```bash
gpg --encrypt --sign --recipient bob@example.com test.txt
```

Enter User PIN (e.g. 654321) when prompted.

If YubiKey requires touch confirmation (optional, set via ykman openpgp keys set-touch), touch the YubiKey.

The output will be test.txt.gpg

Decrypt the file (requires YubiKey):

```bash
gpg --decrypt test.txt.gpg > test_decrypted.txt
```

Enter User PIN and touch Yubikey if needed.

Check that test_decrypted.txt matches test.txt.

Bob can decrypt with his private key and verify your signature:

```bash
gpg --decrypt test.txt.gpg
```

If you only want to sign the file, you can use the following commands.

```bash
gpg --detach-sign test.txt
```

This will generate an output file called test.txt.sig

To verify it:

```bash
gpg --verify test.txt.sig test.txt
```

## Security Practices
- Always generate keys on an offline machine to avoid exposure.
- Store USB drives with private keys in separate, secure locations (e.g. safe or bank).
- Use strong, unique PINs. If PIN attempts are exceeded (3 for User, 3 for Admin), Yubikey locks and requires a reset, losing all keys.
- Keep revoke.asc accessible but secure to revoke the key if compromised.
- Create new subkeys before expiry (e.g. every year) as follows:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
gpg> addkey
```

Transfer new subkeys to the YubiKey and update the public key on servers:

```bash
gpg --keyserver hkps://keys.openpgp.org --send-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Use a second YubiKey for redundancy:

```bash
gpg --import secret.asc
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Repeat keytocard steps for the second YubiKey.

If you need to reset Yubikey:

```bash
ykman openpgp reset
```

To restore subkeys from backup:

```bash
gpg --import secret.asc
```

“Public Key Not Usable”: Ensure the recipient's public key is imported and trusted:

```bash
gpg --edit-key bob@example.com
gpg> trust
```
Set to 5 = Ultimate trust. 