---
layout: default
title: "Introduction aux **Mesh Networks** et analyse détaillée de LoRa et **LoRaWAN**"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Leçon Bitcoin-only</span> <span>Ce projet est maintenu par valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Introduction aux **Mesh Networks** et analyse détaillée de LoRa et **LoRaWAN**

## Introduction aux **Mesh Networks**

Les **Mesh Networks** sont une architecture réseau dans laquelle les nœuds (appareils) sont interconnectés de manière non hiérarchique, ce qui permet à chaque nœud de communiquer directement avec les autres sans passer par un point central, comme un router ou un gateway. Chaque nœud peut potentiellement agir à la fois comme émetteur et comme récepteur, et les données peuvent être relayées par plusieurs chemins pour atteindre leur destination.

Cette structure offre plusieurs avantages :

- **Résilience** : si un nœud tombe en panne, les données peuvent être redirigées par d'autres nœuds, assurant la continuité de la communication.
- **Scalabilité** : les **Mesh Networks** peuvent facilement s'étendre par l'ajout de nouveaux nœuds sans modifications importantes de l'infrastructure.
- **Couverture étendue** : le relais des données permet de couvrir des zones plus vastes que les réseaux traditionnels.
- **Flexibilité** : adaptées à de multiples applications, de l'Internet of Things (IoT) aux réseaux domestiques et industriels.

Cependant, les **Mesh Networks** présentent aussi certains défis :

- **Complexité** : la gestion de chemins multiples et la coordination entre nœuds augmentent la complexité.
- **Consommation d'énergie** : les nœuds qui relaient les données consomment plus d'énergie, ce qui réduit l'autonomie des batteries.
- **Capacité limitée** : dans les réseaux denses, la transmission multi-hop peut introduire de la latence et réduire la capacité globale.

Les **Mesh Networks** sont utilisées dans des technologies sans fil comme **Zigbee**, **Bluetooth** Mesh, **Thread** et, dans certains cas, des protocoles propriétaires basés sur LoRa. L'une des technologies les plus pertinentes pour les réseaux basse consommation et longue portée est **LoRaWAN**, qui adopte une approche différente de la topologie mesh traditionnelle.

## **LoRa** et **LoRaWAN** : contexte et différences

### **LoRa**

**LoRa** (Long Range) est une technologie de modulation à spectre étalé dérivée de la technique Chirp Spread Spectrum (CSS), développée par Cycleo (acquise par Semtech en 2012).

**LoRa** représente la couche physique (PHY) d'un réseau sans fil, définissant la façon dont les données sont modulées et transmises sur des bandes de fréquences sans licence (par exemple 868 MHz en Europe, 915 MHz en Amérique du Nord, 433 MHz dans certaines régions).

Ses principales caractéristiques sont :
- Transmission sur de longues distances (jusqu'à 15 km en zone rurale, 2-5 km en zone urbaine).
- Consommation d'énergie extrêmement faible, idéale pour les applications IoT à faible débit de données et longue autonomie de batterie.

### **LoRaWAN**

**LoRaWAN** (Long Range Wide Area Network) est un protocole de couche MAC (Media Access Control) basé sur LoRa, développé par la LoRa Alliance, une association à but non lucratif fondée en 2015 et comptant plus de 500 membres, dont Semtech, Cisco, IBM et Orange.

**LoRaWAN** définit :
- L'architecture réseau.
- Le protocole de communication.
- Des aspects tels que la fréquence de transmission, le débit de données, la sécurité et l'interopérabilité.

Contrairement à LoRa, qui ne gère que la modulation du signal, **LoRaWAN** établit comment les appareils (nœuds finaux) communiquent avec les gateways et comment ceux-ci se connectent aux serveurs réseau via des connexions de backhaul (par exemple Ethernet, Wi-Fi ou cellular).

#### Comparaison entre **Mesh Networks** et **LoRaWAN**

Contrairement aux **Mesh Networks** traditionnelles (par exemple **Zigbee**, **Bluetooth**), **LoRaWAN** utilise une topologie en étoile, où les nœuds finaux communiquent directement avec des gateways, qui relaient les données vers un serveur réseau central. Voici une comparaison détaillée :

1. Topologie réseau
**Mesh Networks** : les nœuds agissent comme des répéteurs, relayant les données pour étendre la couverture. Cela augmente la complexité et la consommation d'énergie.
**LoRaWAN** : topologie en étoile, avec des nœuds qui transmettent directement aux gateways. Cela élimine les nœuds répéteurs, simplifie le réseau et réduit la consommation d'énergie.

2. Consommation d'énergie
**Mesh Networks** : les nœuds répéteurs consomment plus d'énergie, réduisant l'autonomie de la batterie.
**LoRaWAN** : les appareils finaux ne transmettent que lorsque c'est nécessaire (par exemple Class A avec ALOHA), permettant une autonomie de batterie allant jusqu'à 10-15 ans.

3. Portée et couverture
**Mesh Networks** : la portée est étendue via multi-hop, mais chaque saut peut introduire de la latence et réduire l'efficacité.
**LoRaWAN** : grâce à la modulation CSS, offre une portée allant jusqu'à 15 km (rural) ou 2-5 km (urbain) sans nœuds répéteurs.

4. Capacité et scalabilité
**Mesh Networks** : dans les réseaux denses, le multi-hop peut provoquer des goulots d'étranglement et réduire la capacité.
**LoRaWAN** : prend en charge des millions de messages provenant de milliers d'appareils, grâce à la redondance des gateways et à la topologie en étoile.

5. Sécurité
**Mesh Networks** : la sécurité dépend du protocole (par exemple **Zigbee** utilise AES-128). Le relais multi-hop peut introduire des vulnérabilités.
**LoRaWAN** : chiffrement end-to-end avec clés de session AES-128 (Network Session Key et Application Session Key).

6. Complexité et coûts
**Mesh Networks** : la gestion des chemins de relais augmente la complexité. Les coûts peuvent croître avec l'ajout de nœuds répéteurs.
**LoRaWAN** : la topologie en étoile est plus simple. Les gateways peuvent être coûteux, mais les capteurs sont bon marché et les bandes ISM sans licence réduisent les coûts.

## Analyse détaillée de **LoRa** et **LoRaWAN**
### **LoRa** : couche physique
**LoRa** utilise la modulation Chirp Spread Spectrum (CSS), qui encode les données au moyen de signaux sinusoïdaux à fréquence variable, en répartissant le signal sur une bande passante plus large pour améliorer la résistance au bruit. Elle offre une grande sensibilité (-110 dBm à -140 dBm), idéale pour les environnements bruyants.

Les principaux paramètres comprennent :

- Spreading Factor (SF) : de 7 à 12, influence le débit de données et la portée. SF12 offre une longue portée mais un faible bitrate (0.3 kbps) ; SF7 offre des vitesses plus élevées (27 kbps) mais une portée réduite.
- Bandwidth (BW) : 125 kHz, 250 kHz ou 500 kHz, affecte le bitrate et la robustesse.
- Fréquences ISM : 863-870 MHz (Europe), 902-928 MHz (Amérique du Nord), 433 MHz (autres régions).

LoRa est idéale pour les applications IoT avec de petits paquets de données, comme la surveillance environnementale, le smart metering et l'agriculture de précision.

## **LoRaWAN** : protocole et architecture

**LoRaWAN** définit trois classes d'appareils :

- Class A : appareils bidirectionnels basse consommation avec transmissions uplink et courtes fenêtres de réception downlink (ALOHA). Idéals pour les capteurs alimentés par batterie.
- Class B : ajoute des fenêtres de réception planifiées (toutes les 128 secondes, synchronisées via GPS beacon) pour des downlinks planifiés.
- Class C : appareils toujours à l'écoute des downlinks, adaptés aux appareils alimentés par le secteur.

L'architecture **LoRaWAN** comprend :
- Nœuds finaux (End Devices) : capteurs ou appareils IoT qui collectent et transmettent des données.
- Gateways : reçoivent les données des nœuds et les relaient au serveur réseau via backhaul.
- Network Server : gère le réseau, élimine les doublons et sélectionne le gateway pour les downlinks.
- Application Server : traite les données pour l'analyse ou la visualisation.

## **Mesh Networks** avec LoRa
Bien que **LoRaWAN** utilise une topologie en étoile, il est possible de mettre en œuvre un réseau mesh en utilisant la modulation LoRa avec un protocole externe. Dans un réseau mesh LoRa, les nœuds agissent comme des répéteurs pour étendre la couverture, ce qui est utile dans les zones sans gateways.

Cependant, cela nécessite :
- Protocole personnalisé : **LoRaWAN** ne prend pas en charge mesh nativement.
- Consommation d'énergie plus élevée : les nœuds répéteurs consomment plus d'énergie.
- Complexité : gestion des chemins de relais et prévention des collisions (par exemple CSMA-CA).

Exemple : modules LoRa (par exemple SX1276 de Semtech) avec des microcontrôleurs comme ESP32 pour des **Mesh Networks** privées.

Avantages de **LoRaWAN**

- Efficacité énergétique : la topologie en étoile élimine les nœuds répéteurs.
- Simplicité : communication directe avec les gateways.
- Scalabilité : prend en charge des milliers d'appareils et des millions de messages.
- Sécurité : sécurité robuste avec chiffrement AES-128.
- Interopérabilité : standard ouvert de la LoRa Alliance.

Limites de **LoRaWAN**

- Faible débit de données : 0.3-50 kbps, non adapté aux données volumineuses.
- Latence : Class A introduit des retards pour les downlinks.
- Coût du gateway : significatif pour les réseaux privés.

# Conclusion
Les **Mesh Networks** offrent résilience et flexibilité grâce au relais multi-hop, mais elles sont complexes et consomment plus d'énergie. **LoRaWAN**, avec sa topologie en étoile et sa modulation LoRa, est idéale pour les applications IoT basse consommation et longue portée, grâce à sa simplicité, sa scalabilité et une autonomie de batterie pouvant atteindre 15 ans.

Le choix entre **Mesh Networks** et **LoRaWAN** dépend des exigences : mesh pour les environnements avec des nœuds proches les uns des autres, **LoRaWAN** pour les communications longue distance à consommation minimale. Bien que possible avec LoRa, mesh est moins courant que **LoRaWAN**, qui domine grâce à sa standardisation et au soutien de la LoRa Alliance.
