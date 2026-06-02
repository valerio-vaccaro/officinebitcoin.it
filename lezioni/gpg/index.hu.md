---
layout: default
title: "GPG és YubiKey útmutató"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only lecke</span> <span>Ezt a projektet valerio-vaccaro tartja karban</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# GPG és YubiKey útmutató

Ez a lecke végigvezet a Gnu Privacy Guard (GPG) használatán:
- új kulcspár létrehozásához,
- aláírási és titkosítási alkulcsok hozzáadásához,
- az összes kulcs biztonsági mentéséhez,
- alkulcsok YubiKey-re átviteléhez, és
- fájl titkosításához/aláírásához Yubikey használatával.

Linuxra készült, a parancsok GPG 2.2.40/Debian 12 rendszeren lettek tesztelve. Ugyanezek a parancsok hasonlóan működhetnek más Linux-verziókon, valamint MacOSX és Windows alatt is (a titkosított fájlrendszerek kivételével).

A folyamat bevált biztonsági gyakorlatokat követ, például az offline kulcsgenerálást és a biztonságos mentéseket.

## Telepítés
Telepítsd a gpg-t és a szükséges segédprogramokat

```bash
sudo apt update
sudo apt install gnupg scdaemon pcscd yubikey-manager
```

Győződj meg róla, hogy a verzió 2.1.17 vagy újabb (a 2.4.5 ajánlott).

```bash
gpg --version
```

Ellenőrizd a YubiKey működését

```bash
ykman info
```

Győződj meg róla, hogy az OpenPGP applet engedélyezve van, és a CCID mód aktív.

Használj hálózattól elszigetelt gépet (internet nélkül) a kulcsok létrehozásához és a szivárgások megelőzéséhez.

Ne feledd, hogy a YubiKey alapértelmezett PIN-jei nem biztonságosak, és ezek:
- Default User PIN: 123456
- Default Admin PIN: 12345678
Használat előtt változtasd meg őket (lásd a 4. lépést).

## 1. lépés
Hozz létre egy elsődleges GPG kulcspárt (nyilvános és privát) kizárólag tanúsításra (C); minden más kulcs ebből fog származni.

Indítsd el a kulcsgenerálást a --expert opcióval a haladó beállításokhoz.

```bash
gpg --expert --full-gen-key
```

Válaszd ki a kulcstípust:

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

Válaszd a (8) RSA (set your own capabilities) opciót a kulcs viselkedésének testreszabásához.

Állítsd be a képességeket:

```
Possible actions for a RSA key: Sign Certify Encrypt Authenticate 
Current allowed actions: Sign Certify Encrypt 

   (S) Toggle the sign capability
   (E) Toggle the encrypt capability
   (A) Toggle the authenticate capability
   (Q) Finished

Your selection? S
```

Kapcsold ki a Sign és Encrypt képességeket (nyomd meg az S, E billentyűket).

Hagyd meg a Certify képességet (ha kész vagy, nyomd meg a Q-t).

Ennek eredményeként az engedélyezett műveletek közül csak a Certify marad.

Állítsd be a kulcsméretet:

```
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072) 4096
```

Írd be: 4096 (a YubiKey 4/5 által támogatott maximum).

Állítsd be a lejáratot:

```
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 
```

Írd be: 3y (3 év), vagy amit szeretnél. Erősítsd meg a dátumot.

Add meg a User ID-t:

```
GnuPG needs to construct a user ID to identify your key.

Real name: Satoshi Spritz
Email address: info@satoshispritz.it
Comment: 
You selected this USER-ID:
    "Satoshi Spritz <info@satoshispritz.it>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? o
```

Add meg a nevet és az e-mail-címet. A megjegyzést hagyd üresen. Erősítsd meg O-val.

Adj meg erős passphrase-t (keverj betűket, számokat és szimbólumokat; kerüld a gyakori szavakat).

Példa: Tr0ub4dor&3xplor3r!2025

A passphrase védi a privát kulcsodat.

Generálj entrópiát az egér mozgatásával, véletlenszerű gépeléssel vagy rng-tools használatával (Linuxon, és csak akkor, ha jól érted):

```bash
sudo apt install rng-tools
sudo rngd -r /dev/urandom
```

Várd meg, amíg a kulcsgenerálás befejeződik. Jegyezd fel a key ID-t (például C2033656849FC82BA3C365E33C9BF8B9CB86875D) a kimenetből:

```
gpublic and secret key created and signed.

pub   rsa2048 2025-07-20 [C]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid                      Satoshi Spritz <info@satoshispritz.it>

```

Hozz létre visszavonási tanúsítványt arra az esetre, ha a kulcs kompromittálódna (lehet, hogy a kliensed már létrehozta):

```bash
gpg --output revoke_master_satoshispritz.asc --gen-revoke C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Válaszd ki az okot (például 1 = kulcs kompromittálódott), és mentsd el.

## 2. lépés
Hozz létre aláírási és titkosítási alkulcsokat. Két alkulcs kerül hozzáadásra aláíráshoz (S) és titkosításhoz (E).

Az elsődleges kulcs csak tanúsításra marad.

Szerkeszd a kulcsot:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Add meg a passphrase-t, ha kéri.

Add hozzá az aláírási alkulcsot:

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

Válaszd a (4) RSA (sign only) opciót.

Méret beállítása: 4096.

Lejárat beállítása: 2y (2 év, az alkulcsok gyakrabban rotálhatók).

Erősítsd meg, és add meg a passphrase-t.

Add hozzá a titkosítási alkulcsot:

```
gpg> addkey
```

Válaszd a (6) RSA (encrypt only) opciót.

Méret beállítása: 4096.

Lejárat beállítása: 2y.

Erősítsd meg, és add meg a passphrase-t.

Mentsd a módosításokat:

```
gpg> save
```

Ellenőrizd az alkulcsokat:

```bash
gpg --list-keys --with-subkey-fingerprints C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Példa kimenet:

```
pub   rsa4096 2025-07-20 [C] [expires: 2028-07-20]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid           [ultimate] Satoshi Spritz <info@satoshispritz.it>
sub   rsa4096 2025-07-20 [S] [expires: 2027-07-20]
      1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3
sub   rsa4096 2025-07-20 [E] [expires: 2027-07-20]
      94C11C615BE049B97899FA3C8DC3736F499D6C3E

```

Jegyezd fel az aláírási (S) és titkosítási (E) alkulcsok fingerprintjeit.

## 3. lépés
Az összes kulcs biztonsági mentése. Készíts mentést az elsődleges kulcsról, az alkulcsokról és a nyilvános kulcsról két titkosított USB-meghajtóra.

Készítsd elő az USB-meghajtókat: helyezz be két USB-meghajtót (például /dev/sdb és /dev/sdc).

Hozz létre titkosított partíciókat (például LUKS-szal):

```bash
sudo cryptsetup luksFormat /dev/sdb1
sudo cryptsetup luksOpen /dev/sdb1 backup1
sudo mkfs.ext4 /dev/mapper/backup1
sudo mount /dev/mapper/backup1 /mnt/backup1
```

Ismételd meg /dev/sdc1 esetén (például /mnt/backup2 alá csatolva).

Privát kulcsok exportálása: exportáld az elsődleges kulcsot és az alkulcsokat:

```bash
gpg --armor --export-secret-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/secret_master_satoshispritz.asc
gpg --armor --export-secret-keys 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/secret_sign_satoshispritz.asc
gpg --armor --export-secret-keys 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/secret_encrypt_satoshispritz.asc
```

Nyilvános kulcsok exportálása:

```bash
gpg --armor --export C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/public_master_satoshispritz.asc
gpg --armor --export 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/public_sign_satoshispritz.asc
gpg --armor --export 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/public_encrypt_satoshispritz.asc
```

A visszavonási tanúsítvány exportálása:

```bash
cp revoke_master_satoshispritz.asc /mnt/backup1/revoke_master_satoshispritz.asc
cp revoke_master_satoshispritz.asc /mnt/backup2/revoke_master_satoshispritz.asc
```

Biztonságos lecsatolás:

```bash
sudo umount /mnt/backup1
sudo cryptsetup luksClose backup1
```

Ismételd meg backup2 esetén. Tárold az USB-meghajtókat külön, biztonságos helyeken (például széfben).

Helyi kulcsok törlése (opcionális): ha hálózattól elszigetelt gépet használsz, töröld a GPG könyvtárat:

```bash
rm -rf ~/.gnupg
```

Ezután a kulcsokat importálni kell azon a gépen, ahol használni fogod őket.

Ha a gép nincs hálózattól elszigetelve, tartsd meg a kulcsokat a YubiKey-re történő átvitelig.

## 4. lépés
Vidd át az aláírási és titkosítási alkulcsokat a YubiKey-re, miközben az elsődleges kulcs offline marad.

Helyezd be a Yubikey-t, és ellenőrizd:

```bash
gpg --card-status
```

A kimenetnek meg kell jelenítenie az OpenPGP appletet (például Version: 2.0).

Változtasd meg az alapértelmezett PIN-eket:

```bash
gpg --change-pin
```

User PIN: állíts be új, 6-8 számjegyű PIN-t (például 654321).
Admin PIN: állíts be új, 8 számjegyű PIN-t (például 87654321).

Szerkeszd a kulcsot az átvitelhez:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Az aláírási alkulcs kiválasztása és átvitele: listázd a kulcsokat az alkulcsindexek azonosításához:

```
gpg> list
```

Példa:

```
sec  rsa4096/3C9BF8B9CB86875D
     created: 2025-07-20  expires: 2028-07-20  usage: C   
     trust: ultimate      validity: ultimate
ssb  rsa4096/426E4AB8E6D72AC3
     created: 2025-07-20  expires: 2027-07-20  usage: S   
ssb  rsa4096/8DC3736F499D6C3E
     created: 2025-07-20  expires: 2027-07-20  usage: E
```

Válaszd ki az aláírási alkulcsot:

```
gpg> key 1
```

Az aláírási alkulcs mellett csillag (*) lesz.

Átvitel a YubiKey-re:

```
gpg> keytocard
Please select where to store the key:
   (1) Signature key
   (3) Authentication key
Your selection?
```

Add meg az Admin PIN-t (például 87654321). A privát aláírási alkulcs átkerül a YubiKey-re, és a keyringben egy stub váltja fel.

A titkosítási alkulcs kiválasztása és átvitele: szüntesd meg az aláírási alkulcs kijelölését:

```
gpg> key 1
```

Válaszd ki a titkosítási alkulcsot:

```
gpg> key 2
```

Átvitel a YubiKey-re:

```
gpg> keytocard
Please select where to store the key:
   (2) Encryption key
Your selection? 2
```

Add meg újra az Admin PIN-t.

Mentsd a módosításokat:

```
gpg> save
```

A privát alkulcsok most a YubiKey-en vannak, helyi stubokkal.

Ellenőrizd a YubiKey-t:

```bash
gpg --card-status
```

Ellenőrizd, hogy a Signature key és Encryption key slotok az alkulcsok fingerprintjeit mutatják.

Privát alkulcsok exportálása (a mentés ellenőrzéséhez):

```bash
gpg --armor --export-secret-subkeys C2033656849FC82BA3C365E33C9BF8B9CB86875D > secret-subkeys-satoshispritz.asc
```

Töröld a helyi GPG könyvtárat:

```bash
rm -rf ~/.gnupg
```

Importáld újra a nyilvános kulcsot és a stubokat:

```bash
gpg --import public.asc
gpg --import secret-subkeys-satoshispritz.asc
```

Az elsődleges privát kulcs már nincs a számítógépen.

## 5. lépés
Használd a YubiKey-t egy fájl titkosítására és aláírására egy címzett számára.

Készíts egy tesztfájlt:

```bash
echo "This is a secret message." > test.txt
```

Szerezd meg a címzett nyilvános kulcsát (például bob@example.com):

```bash
gpg --keyserver hkps://keys.openpgp.org --search-keys bob@example.com
```

Vagy importáld fájlból:

```bash
gpg --import bob_public.asc
```

Titkosítás és aláírás: titkosíts bob@example.com számára, és írj alá Yubikey-vel:

```bash
gpg --encrypt --sign --recipient bob@example.com test.txt
```

Add meg a User PIN-t (például 654321), amikor kéri.

Ha a YubiKey érintéses megerősítést kér (opcionális, ykman openpgp keys set-touch paranccsal állítható be), érintsd meg a YubiKey-t.

A kimenet test.txt.gpg lesz

Fejtsd vissza a fájlt (YubiKey szükséges):

```bash
gpg --decrypt test.txt.gpg > test_decrypted.txt
```

Add meg a User PIN-t, és érintsd meg a Yubikey-t, ha szükséges.

Ellenőrizd, hogy test_decrypted.txt megegyezik-e a test.txt fájllal.

Bob a saját privát kulcsával visszafejtheti, és ellenőrizheti az aláírásodat:

```bash
gpg --decrypt test.txt.gpg
```

Ha csak alá szeretnéd írni a fájlt, a következő parancsokat használhatod.

```bash
gpg --detach-sign test.txt
```

Ez egy test.txt.sig nevű kimeneti fájlt hoz létre

Ellenőrzés:

```bash
gpg --verify test.txt.sig test.txt
```

## Biztonsági gyakorlatok
- Mindig offline gépen generáld a kulcsokat a kitettség elkerülésére.
- A privát kulcsokat tartalmazó USB-meghajtókat külön, biztonságos helyeken tárold (például széfben vagy bankban).
- Használj erős, egyedi PIN-eket. Ha a PIN-próbálkozások száma túllépi a limitet (3 a User, 3 az Admin esetén), a Yubikey lezár, reset szükséges, és minden kulcs elveszik.
- Tartsd a revoke.asc fájlt elérhető, de biztonságos helyen, hogy kompromittálódás esetén visszavonhasd a kulcsot.
- Hozz létre új alkulcsokat a lejárat előtt (például évente) az alábbiak szerint:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
gpg> addkey
```

Vidd át az új alkulcsokat a YubiKey-re, és frissítsd a nyilvános kulcsot a szervereken:

```bash
gpg --keyserver hkps://keys.openpgp.org --send-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Használj második YubiKey-t redundanciához:

```bash
gpg --import secret.asc
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Ismételd meg a keytocard lépéseket a második YubiKey esetén.

Ha resetelni kell a Yubikey-t:

```bash
ykman openpgp reset
```

Alkulcsok visszaállítása mentésből:

```bash
gpg --import secret.asc
```

“Public Key Not Usable”: győződj meg róla, hogy a címzett nyilvános kulcsa importálva van és megbízható:

```bash
gpg --edit-key bob@example.com
gpg> trust
```
Állítsd 5 = Ultimate trust értékre.
