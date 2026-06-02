---
layout: default
title: "Introducción a las **Mesh Networks** y análisis detallado de LoRa y **LoRaWAN**"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lección Bitcoin-only</span> <span>Este proyecto es mantenido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Introducción a las **Mesh Networks** y análisis detallado de LoRa y **LoRaWAN**

## Introducción a las **Mesh Networks**

Las **Mesh Networks** son una arquitectura de red en la que los nodos (dispositivos) están interconectados de forma no jerárquica, lo que permite que cada nodo se comunique directamente con otros sin pasar por un punto central, como un router o gateway. Cada nodo puede actuar potencialmente tanto como transmisor como receptor, y los datos pueden reenviarse a través de múltiples rutas para alcanzar el destino.

Esta estructura ofrece varias ventajas:

- **Resiliencia**: si un nodo falla, los datos pueden redirigirse a través de otros nodos, garantizando la continuidad de la comunicación.
- **Escalabilidad**: las **Mesh Networks** pueden ampliarse fácilmente añadiendo nuevos nodos sin modificaciones significativas de infraestructura.
- **Cobertura extendida**: el reenvío de datos permite cubrir áreas más grandes que las redes tradicionales.
- **Flexibilidad**: son adecuadas para múltiples aplicaciones, desde Internet of Things (IoT) hasta redes domésticas e industriales.

Sin embargo, las **Mesh Networks** también presentan algunos desafíos:

- **Complejidad**: gestionar múltiples rutas y coordinar los nodos aumenta la complejidad.
- **Consumo energético**: los nodos que reenvían datos consumen más energía, reduciendo la duración de la batería.
- **Capacidad limitada**: en redes densas, la transmisión multi-hop puede introducir latencia y reducir la capacidad general.

Las **Mesh Networks** se usan en tecnologías inalámbricas como **Zigbee**, **Bluetooth** Mesh, **Thread** y, en algunos casos, protocolos propietarios basados en LoRa. Una de las tecnologías más relevantes para redes de baja potencia y largo alcance es **LoRaWAN**, que adopta un enfoque diferente respecto a la topología mesh tradicional.

## **LoRa** y **LoRaWAN**: contexto y diferencias

### **LoRa**

**LoRa** (Long Range) es una tecnología de modulación de espectro ensanchado derivada de la técnica Chirp Spread Spectrum (CSS), desarrollada por Cycleo (adquirida por Semtech en 2012).

**LoRa** representa la capa física (PHY) de una red inalámbrica, definiendo cómo se modulan y transmiten los datos en bandas de frecuencia sin licencia (por ejemplo, 868 MHz en Europa, 915 MHz en Norteamérica, 433 MHz en algunas regiones).

Sus características principales son:
- Transmisión a largas distancias (hasta 15 km en áreas rurales, 2-5 km en áreas urbanas).
- Consumo energético extremadamente bajo, ideal para aplicaciones IoT con bajas tasas de datos y larga vida de batería.

### **LoRaWAN**

**LoRaWAN** (Long Range Wide Area Network) es un protocolo de capa MAC (Media Access Control) basado en LoRa, desarrollado por la LoRa Alliance, una asociación sin ánimo de lucro fundada en 2015 con más de 500 miembros, incluidos Semtech, Cisco, IBM y Orange.

**LoRaWAN** define:
- Arquitectura de red.
- Protocolo de comunicación.
- Aspectos como frecuencia de transmisión, tasa de datos, seguridad e interoperabilidad.

A diferencia de LoRa, que solo gestiona la modulación de la señal, **LoRaWAN** establece cómo los dispositivos (nodos finales) se comunican con los gateways y cómo estos se conectan a los servidores de red mediante conexiones de backhaul (por ejemplo, Ethernet, Wi-Fi o cellular).

#### Comparación entre **Mesh Networks** y **LoRaWAN**

A diferencia de las **Mesh Networks** tradicionales (por ejemplo, **Zigbee**, **Bluetooth**), **LoRaWAN** usa una topología en estrella, donde los nodos finales se comunican directamente con gateways, que reenvían los datos a un servidor de red central. A continuación se muestra una comparación detallada:

1. Topología de red
**Mesh Networks**: los nodos actúan como repetidores, reenviando datos para extender la cobertura. Esto aumenta la complejidad y el consumo energético.
**LoRaWAN**: topología en estrella, con nodos que transmiten directamente a los gateways. Esto elimina nodos repetidores, simplifica la red y reduce el consumo energético.

2. Consumo energético
**Mesh Networks**: los nodos repetidores consumen más energía, reduciendo la duración de la batería.
**LoRaWAN**: los dispositivos finales transmiten solo cuando es necesario (por ejemplo, Class A con ALOHA), permitiendo una vida de batería de hasta 10-15 años.

3. Alcance y cobertura
**Mesh Networks**: el alcance se extiende mediante multi-hop, pero cada salto puede introducir latencia y reducir la eficiencia.
**LoRaWAN**: gracias a la modulación CSS, ofrece un alcance de hasta 15 km (rural) o 2-5 km (urbano) sin nodos repetidores.

4. Capacidad y escalabilidad
**Mesh Networks**: en redes densas, el multi-hop puede causar cuellos de botella y reducir la capacidad.
**LoRaWAN**: soporta millones de mensajes de miles de dispositivos, gracias a la redundancia de gateways y a la topología en estrella.

5. Seguridad
**Mesh Networks**: la seguridad depende del protocolo (por ejemplo, **Zigbee** usa AES-128). El reenvío multi-hop puede introducir vulnerabilidades.
**LoRaWAN**: cifrado end-to-end con claves de sesión AES-128 (Network Session Key y Application Session Key).

6. Complejidad y costes
**Mesh Networks**: gestionar rutas de reenvío aumenta la complejidad. Los costes pueden crecer con la adición de nodos repetidores.
**LoRaWAN**: la topología en estrella es más simple. Los gateways pueden ser costosos, pero los sensores son baratos y las bandas ISM sin licencia reducen los costes.

## Análisis detallado de **LoRa** y **LoRaWAN**
### **LoRa**: capa física
**LoRa** usa modulación Chirp Spread Spectrum (CSS), que codifica datos con señales sinusoidales de frecuencia variable, distribuyendo la señal sobre un ancho de banda más amplio para mejorar la resistencia al ruido. Ofrece alta sensibilidad (-110 dBm a -140 dBm), ideal para entornos ruidosos.

Los parámetros principales incluyen:

- Spreading Factor (SF): de 7 a 12, influye en la tasa de datos y el alcance. SF12 ofrece largo alcance pero bajo bitrate (0.3 kbps); SF7 ofrece velocidades más altas (27 kbps) pero alcance reducido.
- Bandwidth (BW): 125 kHz, 250 kHz o 500 kHz, afecta al bitrate y a la robustez.
- Frecuencias ISM: 863-870 MHz (Europa), 902-928 MHz (Norteamérica), 433 MHz (otras regiones).

LoRa es ideal para aplicaciones IoT con paquetes de datos pequeños, como monitorización ambiental, smart metering y agricultura de precisión.

## **LoRaWAN**: protocolo y arquitectura

**LoRaWAN** define tres clases de dispositivos:

- Class A: dispositivos bidireccionales de baja potencia con transmisiones uplink y ventanas cortas de recepción downlink (ALOHA). Ideales para sensores alimentados por batería.
- Class B: añade ventanas de recepción programadas (cada 128 segundos, sincronizadas mediante GPS beacon) para downlinks planificados.
- Class C: dispositivos siempre escuchando downlinks, adecuados para dispositivos alimentados por red eléctrica.

La arquitectura **LoRaWAN** incluye:
- Nodos finales (End Devices): sensores o dispositivos IoT que recopilan y transmiten datos.
- Gateways: reciben datos de los nodos y los reenvían al servidor de red mediante backhaul.
- Network Server: gestiona la red, elimina duplicados y selecciona el gateway para downlinks.
- Application Server: procesa datos para análisis o visualización.

## **Mesh Networks** con LoRa
Aunque **LoRaWAN** usa una topología en estrella, es posible implementar una red mesh usando modulación LoRa con un protocolo externo. En una red mesh LoRa, los nodos actúan como repetidores para extender la cobertura, lo que resulta útil en áreas sin gateways.

Sin embargo, esto requiere:
- Protocolo personalizado: **LoRaWAN** no soporta mesh de forma nativa.
- Mayor consumo energético: los nodos repetidores consumen más energía.
- Complejidad: gestión de rutas de reenvío y prevención de colisiones (por ejemplo, CSMA-CA).

Ejemplo: módulos LoRa (por ejemplo, SX1276 de Semtech) con microcontroladores como ESP32 para **Mesh Networks** privadas.

Ventajas de **LoRaWAN**

- Eficiencia energética: la topología en estrella elimina nodos repetidores.
- Simplicidad: comunicación directa con gateways.
- Escalabilidad: soporta miles de dispositivos y millones de mensajes.
- Seguridad: seguridad robusta con cifrado AES-128.
- Interoperabilidad: estándar abierto de la LoRa Alliance.

Limitaciones de **LoRaWAN**

- Baja tasa de datos: 0.3-50 kbps, no adecuada para datos voluminosos.
- Latencia: Class A introduce retrasos para downlinks.
- Coste de gateway: significativo para redes privadas.

# Conclusión
Las **Mesh Networks** ofrecen resiliencia y flexibilidad mediante reenvío multi-hop, pero son complejas y consumen más energía. **LoRaWAN**, con su topología en estrella y modulación LoRa, es ideal para aplicaciones IoT de baja potencia y largo alcance, gracias a su simplicidad, escalabilidad y vida de batería de hasta 15 años.

La elección entre **Mesh Networks** y **LoRaWAN** depende de los requisitos: mesh para entornos con nodos cercanos entre sí, **LoRaWAN** para comunicaciones de larga distancia con consumo mínimo. Aunque es posible con LoRa, mesh es menos común que **LoRaWAN**, que domina gracias a su estandarización y al apoyo de la LoRa Alliance.
