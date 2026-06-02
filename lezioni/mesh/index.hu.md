---
layout: default
title: "Bevezetés a **Mesh Networks** világába, valamint a LoRa és a **LoRaWAN** részletes elemzése"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only lecke</span> <span>Ezt a projektet valerio-vaccaro tartja karban</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Bevezetés a **Mesh Networks** világába, valamint a LoRa és a **LoRaWAN** részletes elemzése

## Bevezetés a **Mesh Networks** világába

A **Mesh Networks** olyan hálózati architektúra, amelyben a csomópontok (eszközök) nem hierarchikus módon kapcsolódnak egymáshoz, lehetővé téve, hogy minden csomópont közvetlenül kommunikáljon másokkal anélkül, hogy egy központi ponton, például routeren vagy gatewayen haladna át. Minden csomópont potenciálisan adóként és vevőként is működhet, az adatok pedig több útvonalon keresztül továbbíthatók a cél eléréséhez.

Ez a struktúra több előnyt kínál:

- **Rugalmasság meghibásodással szemben**: ha egy csomópont kiesik, az adatok más csomópontokon keresztül átirányíthatók, biztosítva a kommunikáció folytonosságát.
- **Skálázhatóság**: a **Mesh Networks** könnyen bővíthetők új csomópontok hozzáadásával, jelentős infrastruktúra-módosítás nélkül.
- **Kiterjesztett lefedettség**: az adattovábbítás lehetővé teszi nagyobb területek lefedését a hagyományos hálózatokhoz képest.
- **Rugalmasság**: sokféle alkalmazásra alkalmasak, az Internet of Things (IoT) megoldásoktól az otthoni és ipari hálózatokig.

Ugyanakkor a **Mesh Networks** bizonyos kihívásokat is jelentenek:

- **Összetettség**: több útvonal kezelése és a csomópontok közötti koordináció növeli az összetettséget.
- **Energiafogyasztás**: az adatokat továbbító csomópontok több energiát fogyasztanak, ami csökkenti az akkumulátor élettartamát.
- **Korlátozott kapacitás**: sűrű hálózatokban a multi-hop átvitel késleltetést okozhat és csökkentheti az összkapacitást.

A **Mesh Networks** olyan vezeték nélküli technológiákban használatosak, mint a **Zigbee**, a **Bluetooth** Mesh, a **Thread**, valamint bizonyos esetekben LoRa-alapú proprietáris protokollok. Az alacsony fogyasztású, nagy hatótávolságú hálózatok egyik legfontosabb technológiája a **LoRaWAN**, amely a hagyományos mesh topológiához képest eltérő megközelítést alkalmaz.

## **LoRa** és **LoRaWAN**: háttér és különbségek

### **LoRa**

A **LoRa** (Long Range) egy szórt spektrumú modulációs technológia, amely a Chirp Spread Spectrum (CSS) technikából származik, és amelyet a Cycleo fejlesztett ki (a Semtech 2012-ben felvásárolta).

A **LoRa** egy vezeték nélküli hálózat fizikai rétegét (PHY) képviseli, meghatározva, hogyan modulálják és továbbítják az adatokat engedély nélküli frekvenciasávokon (például 868 MHz Európában, 915 MHz Észak-Amerikában, 433 MHz bizonyos régiókban).

Fő jellemzői:
- Nagy távolságú átvitel (akár 15 km vidéki területeken, 2-5 km városi környezetben).
- Rendkívül alacsony energiafogyasztás, ideális alacsony adatsebességű és hosszú akkumulátor-élettartamú IoT-alkalmazásokhoz.

### **LoRaWAN**

A **LoRaWAN** (Long Range Wide Area Network) egy LoRa-alapú MAC (Media Access Control) rétegbeli protokoll, amelyet a LoRa Alliance fejlesztett. A LoRa Alliance egy 2015-ben alapított nonprofit szervezet, több mint 500 taggal, köztük a Semtech, Cisco, IBM és Orange vállalatokkal.

A **LoRaWAN** meghatározza:
- A hálózati architektúrát.
- A kommunikációs protokollt.
- Olyan szempontokat, mint az átviteli frekvencia, adatsebesség, biztonság és interoperabilitás.

A LoRa-val ellentétben, amely csak a jelmodulációt kezeli, a **LoRaWAN** azt határozza meg, hogyan kommunikálnak az eszközök (végcsomópontok) a gatewayekkel, és ezek hogyan kapcsolódnak a hálózati szerverekhez backhaul kapcsolatokon keresztül (például Ethernet, Wi-Fi vagy cellular).

#### **Mesh Networks** és **LoRaWAN** összehasonlítása

A hagyományos **Mesh Networks** rendszerekkel (például **Zigbee**, **Bluetooth**) ellentétben a **LoRaWAN** csillag topológiát használ, amelyben a végcsomópontok közvetlenül kommunikálnak a gatewayekkel, amelyek az adatokat egy központi hálózati szerverhez továbbítják. Az alábbiakban részletes összehasonlítás következik:

1. Hálózati topológia
**Mesh Networks**: a csomópontok ismétlőként működnek, adatokat továbbítva a lefedettség kiterjesztéséhez. Ez növeli az összetettséget és az energiafogyasztást.
**LoRaWAN**: csillag topológia, amelyben a csomópontok közvetlenül a gatewayeknek továbbítanak. Ez megszünteti az ismétlő csomópontokat, egyszerűsíti a hálózatot és csökkenti az energiafogyasztást.

2. Energiafogyasztás
**Mesh Networks**: az ismétlő csomópontok több energiát fogyasztanak, csökkentve az akkumulátor élettartamát.
**LoRaWAN**: a végberendezések csak szükség esetén továbbítanak (például Class A ALOHA-val), ami akár 10-15 éves akkumulátor-élettartamot tesz lehetővé.

3. Hatótávolság és lefedettség
**Mesh Networks**: a hatótávolság multi-hop útján bővül, de minden ugrás késleltetést vihet be és csökkentheti a hatékonyságot.
**LoRaWAN**: a CSS modulációnak köszönhetően akár 15 km (vidéki) vagy 2-5 km (városi) hatótávolságot kínál ismétlő csomópontok nélkül.

4. Kapacitás és skálázhatóság
**Mesh Networks**: sűrű hálózatokban a multi-hop szűk keresztmetszeteket okozhat és csökkentheti a kapacitást.
**LoRaWAN**: több ezer eszköztől érkező több millió üzenetet támogat, a gateway redundanciának és a csillag topológiának köszönhetően.

5. Biztonság
**Mesh Networks**: a biztonság a protokolltól függ (például a **Zigbee** AES-128-at használ). A multi-hop továbbítás sebezhetőségeket vihet be.
**LoRaWAN**: end-to-end titkosítás AES-128 munkamenetkulcsokkal (Network Session Key és Application Session Key).

6. Összetettség és költségek
**Mesh Networks**: a továbbítási útvonalak kezelése növeli az összetettséget. A költségek ismétlő csomópontok hozzáadásával nőhetnek.
**LoRaWAN**: a csillag topológia egyszerűbb. A gatewayek drágák lehetnek, de a szenzorok olcsók, és az engedély nélküli ISM sávok csökkentik a költségeket.

## **LoRa** és **LoRaWAN** részletes elemzése
### **LoRa**: fizikai réteg
A **LoRa** Chirp Spread Spectrum (CSS) modulációt használ, amely az adatokat változó frekvenciájú szinuszos jelekkel kódolja, és a jelet szélesebb sávszélességen osztja el a zajállóság javítása érdekében. Nagy érzékenységet kínál (-110 dBm és -140 dBm között), ami ideálissá teszi zajos környezetekben.

A fő paraméterek:

- Spreading Factor (SF): 7-től 12-ig, befolyásolja az adatsebességet és a hatótávolságot. Az SF12 nagy hatótávolságot, de alacsony bitrate-et kínál (0.3 kbps); az SF7 nagyobb sebességet (27 kbps), de csökkentett hatótávolságot kínál.
- Bandwidth (BW): 125 kHz, 250 kHz vagy 500 kHz, befolyásolja a bitrate-et és a robusztusságot.
- ISM frekvenciák: 863-870 MHz (Európa), 902-928 MHz (Észak-Amerika), 433 MHz (más régiók).

A LoRa ideális kis adatcsomagokat használó IoT-alkalmazásokhoz, például környezeti monitorozáshoz, smart meteringhez és precíziós mezőgazdasághoz.

## **LoRaWAN**: protokoll és architektúra

A **LoRaWAN** három eszközosztályt határoz meg:

- Class A: kétirányú, alacsony fogyasztású eszközök uplink átvitelekkel és rövid downlink vételi ablakokkal (ALOHA). Ideálisak akkumulátoros szenzorokhoz.
- Class B: ütemezett vételi ablakokat ad hozzá (128 másodpercenként, GPS beacon segítségével szinkronizálva) tervezett downlinkekhez.
- Class C: állandóan downlinkekre figyelő eszközök, hálózati táplálású eszközökhöz alkalmasak.

A **LoRaWAN** architektúra részei:
- Végcsomópontok (End Devices): szenzorok vagy IoT-eszközök, amelyek adatokat gyűjtenek és továbbítanak.
- Gateways: fogadják a csomópontok adatait, és backhaulon keresztül továbbítják a hálózati szerverhez.
- Network Server: kezeli a hálózatot, eltávolítja a duplikátumokat, és kiválasztja a gatewayt a downlinkekhez.
- Application Server: elemzéshez vagy megjelenítéshez feldolgozza az adatokat.

## **Mesh Networks** LoRa-val
Bár a **LoRaWAN** csillag topológiát használ, külső protokollal LoRa modulációt használó mesh hálózat is megvalósítható. Egy LoRa mesh hálózatban a csomópontok ismétlőként működnek a lefedettség kiterjesztésére, ami hasznos gateway nélküli területeken.

Ez azonban megköveteli:
- Egyedi protokoll: a **LoRaWAN** natívan nem támogatja a mesht.
- Magasabb energiafogyasztás: az ismétlő csomópontok több energiát fogyasztanak.
- Összetettség: továbbítási útvonalak kezelése és ütközésmegelőzés (például CSMA-CA).

Példa: LoRa modulok (például a Semtech SX1276) ESP32-höz hasonló mikrokontrollerekkel privát **Mesh Networks** céljára.

A **LoRaWAN** előnyei

- Energiahatékonyság: a csillag topológia megszünteti az ismétlő csomópontokat.
- Egyszerűség: közvetlen kommunikáció a gatewayekkel.
- Skálázhatóság: több ezer eszközt és több millió üzenetet támogat.
- Biztonság: erős biztonság AES-128 titkosítással.
- Interoperabilitás: a LoRa Alliance nyílt szabványa.

A **LoRaWAN** korlátai

- Alacsony adatsebesség: 0.3-50 kbps, nem alkalmas nagy méretű adatokhoz.
- Késleltetés: a Class A késleltetést vezet be a downlinkeknél.
- Gateway költség: privát hálózatok esetén jelentős.

# Következtetés
A **Mesh Networks** multi-hop továbbítással rugalmasságot és meghibásodástűrést kínálnak, de összetettek és több energiát fogyasztanak. A **LoRaWAN**, csillag topológiájával és LoRa modulációjával, ideális alacsony fogyasztású, nagy hatótávolságú IoT-alkalmazásokhoz, egyszerűségének, skálázhatóságának és akár 15 éves akkumulátor-élettartamának köszönhetően.

A **Mesh Networks** és a **LoRaWAN** közötti választás a követelményektől függ: mesh olyan környezetekhez, ahol a csomópontok egymáshoz közel helyezkednek el, **LoRaWAN** pedig minimális fogyasztású, nagy távolságú kommunikációhoz. Bár LoRa-val lehetséges, a mesh kevésbé gyakori a **LoRaWAN**-hoz képest, amely szabványosításának és a LoRa Alliance támogatásának köszönhetően dominál.
