---
layout: default
title: "Debian telepítése"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only lecke</span> <span>Ezt a projektet valerio-vaccaro tartja karban</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Debian telepítése
Előkészítünk egy USB-meghajtót a hivatalos weboldalról letöltött Debian-képpel.

Csatlakoztatjuk az összes kábelt (display, keyboard, mouse, and ethernet).

![alt text](https://officinebitcoin.it/lezioni/debian/1.jpg)

Csatlakoztatjuk a telepítő USB-meghajtót.

![alt text](https://officinebitcoin.it/lezioni/debian/2.jpg)

Bekapcsoljuk a számítógépet, és meggyőződünk róla, hogy a Debian-t tartalmazó USB-meghajtónk elindul.

![alt text](https://officinebitcoin.it/lezioni/debian/3.jpg)

## Telepítés
Ha minden megfelelően működött, a Debian telepítőjének el kell indulnia, és a következő képernyőre jutunk.

![alt text](https://officinebitcoin.it/lezioni/debian/4.jpg)

Kiválasztjuk az első sort, és elindítjuk a grafikus telepítést.

Az első kérdés a nyelv lesz; ehhez a telepítéshez az "English" lehetőséget választom, mert ezt érthetőbbnek találom bármely más fordításnál.

![alt text](https://officinebitcoin.it/lezioni/debian/5.jpg)

Ezen a ponton meg kell adnunk a földrajzi helyünket; Olaszország megtalálásához az OTHER->EUROPE->ITALY útvonalat kell kiválasztanunk.

![alt text](https://officinebitcoin.it/lezioni/debian/6.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/7.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/8.jpg)

A lokalizációhoz itt is az English lehetőséget választom.

![alt text](https://officinebitcoin.it/lezioni/debian/9.jpg)

És beállítom az olasz billentyűzetet, mivel ez áll rendelkezésemre.

![alt text](https://officinebitcoin.it/lezioni/debian/10.jpg)

Ezután választunk egy felhasználónevet, a domaint pedig üresen hagyjuk.

![alt text](https://officinebitcoin.it/lezioni/debian/11.jpg)

Ezen a ponton a Debian megkéri, hogy válasszon jelszót a root felhasználóhoz...

![alt text](https://officinebitcoin.it/lezioni/debian/12.jpg)

és hozzon létre egy felhasználót a hozzá tartozó jelszóval.

![alt text](https://officinebitcoin.it/lezioni/debian/13.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/14.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/15.jpg)

Most ki kell választanunk a telepítési lemezt; a teljes lemezt fogjuk használni, és ki kell választanunk azt a lemezt, amelyre a telepítést végezzük.

![alt text](https://officinebitcoin.it/lezioni/debian/16.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/17.jpg)

Ezután ki kell választanunk a partíciószerkezetet; egyelőre mindent egyetlen partícióban hagyunk.

![alt text](https://officinebitcoin.it/lezioni/debian/18.jpg)

A Debian felajánl egy partíciós táblát, de... hozzáadott egy swap területet, amit nem szeretnénk, ezért kiválasztjuk és eltávolítjuk a listából.

![alt text](https://officinebitcoin.it/lezioni/debian/19.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/20.jpg)

Most, hogy eltávolítottuk, végre kiírhatjuk a táblánkat.

![alt text](https://officinebitcoin.it/lezioni/debian/21.jpg)

A Debian szeretne visszatérni a partíciós tábla beállításához, de mi elutasítjuk a felkérést.

![alt text](https://officinebitcoin.it/lezioni/debian/22.jpg)

És megerősítjük, hogy ki akarjuk írni a frissített táblát.

![alt text](https://officinebitcoin.it/lezioni/debian/23.jpg)

Most megkérdezik, hogy szeretnénk-e Debian mirror-t használni; úgy döntünk, hogy használjuk.

![alt text](https://officinebitcoin.it/lezioni/debian/24.jpg)

Kiválasztjuk az országunkat.

![alt text](https://officinebitcoin.it/lezioni/debian/25.jpg)

Általában a GARR mirror gyors és megbízható; használjuk azt.

![alt text](https://officinebitcoin.it/lezioni/debian/26.jpg)

Nincs proxy-m, ezért üresen hagyom a mezőt.

![alt text](https://officinebitcoin.it/lezioni/debian/27.jpg)

De milyen programokat telepítsünk? Mivel szervert készítünk, letiltjuk a grafikus környezetet (eltávolítjuk az első két jelölést), és kiválasztjuk az SSH-t, amelyre a távoli hozzáféréshez lesz szükségünk.

![alt text](https://officinebitcoin.it/lezioni/debian/28.jpg)

A telepítés elindul.

A végén megkérdezik, hogy szeretnénk-e telepíteni a grub-ot, amely lehetővé teszi a Linux indítását; igenlően válaszolunk, és ugyanazt a lemezt választjuk, amelyre az operációs rendszert telepítettük.

![alt text](https://officinebitcoin.it/lezioni/debian/29.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/30.jpg)

Yuhuuu, készen vagyunk; ideje eltávolítani az USB-meghajtót, és újraindítani a gépet.

![alt text](https://officinebitcoin.it/lezioni/debian/31.jpg)

Ha minden megfelelően működött, egy terminál előtt kell találnunk magunkat, amely arra kér, hogy jelentkezzünk be a telepítés során létrehozott profilok egyikével.

## Beállítás

### Csatlakozzunk
A szerverünkhöz a `ssh username@ip` paranccsal csatlakozunk, ahol a username a telepítés során választott név, az ip pedig annak a számítógépnek az IP-címe, amelyre telepítettünk.

Ez a lépés természetesen kihagyható, ha hálózati csatlakozás helyett monitorral és billentyűzettel telepítünk.

Vegye figyelembe, hogy a Debian MEGTILTJA, hogy ssh-n keresztül superuser hitelesítő adatokkal (vagyis root-ként) csatlakozzunk.

### Repository
Most frissítsük a repository-kat.

Superuser-ré válunk az `su` paranccsal és a root jelszó beírásával.

A repository fájlt a `nano /etc/apt/sources.list` paranccsal szerkesztjük, és eltávolítjuk az összes benne lévő sort.

Hozzáadjuk a következő sorokat.

```                                                                    
deb http://deb.debian.org/debian/ bookworm contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm contrib main non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-updates contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm-updates contrib main non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-proposed-updates contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm-proposed-updates contrib main non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-backports contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm-backports contrib main non-free non-free-firmware

deb http://deb.debian.org/debian-security/ bookworm-security contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian-security/ bookworm-security contrib main non-free non-free-firmware

```

Ezután a fájlt a `CTRL+x`, majd a `y` megnyomásával menthetjük.

Az `apt update` parancs lehetővé teszi, hogy ellenőrizzük, minden rendben ment-e, és frissítsük a csomaglistát.

### A rendszer frissítése
A rendszer frissítéséhez egyszerűen futtassuk a következő parancsokat:

- `apt update` a csomaglista frissítéséhez,
- `apt upgrade` azoknak a telepített csomagoknak a frissítéséhez, amelyekhez létezik új verzió.

### tor telepítése és használata ssh-val
A tor telepítéséhez egyszerűen használjuk az `apt install tor` parancsot.

Telepítés után a következő paranccsal konfigurálhatjuk: `nano /etc/tor/torrc`.

A fájl végére hozzáadjuk a következő sorokat.

```
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 22 127.0.0.1:22
```

És újraindítjuk a tor-t a `systemctl restart tor` paranccsal; most megtalálhatjuk az onion címünket a `cat /var/lib/tor/hidden_service/hostname` paranccsal.

A tor használatával most a világ bármely pontjáról csatlakozhatunk a gépünkhöz a `torify ssh username@onionaddress.onion` paranccsal.

## Program
A Debian telepítése ismétlődő lecke; itt van a már megtartott alkalmak listája:

| Dátum       | Jegyzetek                                      |
|-------------|------------------------------------------------|
| 240415-2200 | Első lecke                                     |
