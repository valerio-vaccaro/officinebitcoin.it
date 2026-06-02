---
layout: default
title: "Descriptores de Bitcoin"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lección Bitcoin-only</span> <span>Este proyecto es mantenido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Descriptores de Bitcoin

## Introducción

## Descriptores
Los descriptores son un concepto relativamente nuevo y todavía poco extendido, pero son útiles para describir la estructura de una wallet Bitcoin. Los descriptores son cadenas de caracteres legibles (alfanuméricas, hexadecimales y algunos símbolos como paréntesis), diseñadas para representar de forma clara y estandarizada una wallet, es decir, el conjunto de claves públicas y privadas necesarias para calcular saldos, recibir y gastar Bitcoin.

## Evolución de la gestión de wallets
Para contextualizar los descriptores, el ponente recorre la evolución de las wallets:

- Wallets iniciales (pre-BIP-32): en los primeros tiempos, con Bitcoin Core, las wallets eran archivos que contenían claves generadas aleatoriamente. Cada vez que se agotaban las direcciones, se añadían nuevas, por lo que era necesario hacer copias de seguridad frecuentes para no perder fondos. Este sistema era ineficiente.
- BIP-32 (HD Wallet): con la introducción de la generación determinista jerárquica, un seed generaba una clave maestra, de la que derivaban todas las direcciones. Bastaba con guardar una copia de seguridad del seed, pero aún no era una solución completa.
- Mnemónicos (BIP-39): posteriormente, el seed se derivó de una secuencia de 12 o 24 palabras (mnemonic), más fácil de conservar. Sin embargo, para reconstruir una wallet también hacía falta información sobre las rutas de derivación (por ejemplo, Legacy, SegWit); de lo contrario, los fondos podían volverse irrecuperables.

El mnemonic por sí solo no basta, sobre todo para wallets complejas como las multisig (que requieren varias firmas) o las que tienen scripts avanzados (por ejemplo, timelock o condiciones de herencia). Algunas wallets prueban todas las derivaciones posibles para encontrar fondos, mientras que otras (por ejemplo, Electrum) requieren especificar el tipo de wallet. En multisig, además, se necesitan las claves públicas de los demás participantes, lo que complica aún más la copia de seguridad.

## Qué son los descriptores y por qué hacen falta
Los descriptores nacieron para superar estas limitaciones, ofreciendo una descripción completa y flexible de la estructura de una wallet. No sustituyen al mnemonic, sino que lo complementan, incluyendo:

- Claves públicas extendidas (xpub, ypub, etc.).
- Rutas de derivación (por ejemplo, m/44'/0'/0' para Legacy).
- Cualquier script o condición de gasto (por ejemplo, multisig, timelock).

## Ejemplos prácticos
- Legacy single-sig: un descriptor sencillo podría ser `pk([fingerprint/derivation]xpub...)`, donde:
1. pk indica una clave pública.
2. [fingerprint/derivation] especifica la clave maestra y la ruta.
3. xpub genera direcciones (por ejemplo, 0/* para recibir, 1/* para change).
- Multisig: un ejemplo es `sortedmulti(2, xpub1, xpub2, xpub3)`, que describe una wallet 2-of-3 y ordena las claves para mantener la coherencia.
- Scripts complejos: con scripts como p2sh (pay to script hash) o p2wsh (pay to witness script hash), se pueden incluir condiciones avanzadas, como timelock o combinaciones lógicas (and, or).

## Descriptores y Taproot
Un caso interesante es el descriptor para Taproot (tr), que admite dos modos de gasto:

- Firma directa con una clave específica.
- Un árbol de condiciones (por ejemplo, herencia o timelock), que mantiene la complejidad oculta en la blockchain hasta el momento del gasto.

## Ventajas de los descriptores
- Copia de seguridad completa: contienen toda la información necesaria para reconstruir una wallet sin intentos a ciegas.
- Compatibilidad: ideales para watch-only wallets, donde se supervisan fondos sin claves privadas.
- Flexibilidad: admiten single-sig, multisig y scripts complejos.
- Privacidad: no revelan secretos y pueden compartirse como un xpub.

## Limitaciones y compatibilidad
No todas las wallets admiten plenamente los descriptores. Por ejemplo, Bitcoin Core solo implementa un subconjunto y requiere dos descriptores separados para direcciones y change. Software como Sparrow o Specter ofrece mejor soporte, permitiendo importar/exportar descriptores y visualizar su estructura.

Se pueden hacer experimentos con:
- Sparrow: admite descriptores, con una interfaz gráfica para crearlos o analizarlos.
- BDK: biblioteca con interfaz de línea de comandos para gestionar descriptores complejos.
- Testnet/Signet: entornos seguros para probar sin arriesgar fondos reales.

## Referencias

- [BIP-380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)
- [Bitcoin Improvement Proposal 380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)
- [Bitcoin Improvement Proposal 380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)

## Programa
Esta lección se creó para un Satoshi Spritz Connect.
