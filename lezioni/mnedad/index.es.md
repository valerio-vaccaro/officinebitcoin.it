---
layout: default
title: "Mnemonics & Dice: aprende a crear tu mnemónica"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lección Bitcoin-only</span> <span>Este proyecto es mantenido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Mnemonics & Dice: aprende a crear tu mnemónica

## Introducción
Crear la mnemónica usando tu propia fuente de entropía reduce la superficie de ataque de un monedero Bitcoin; sin embargo, hay que tener en cuenta algunos factores:

- el proceso debe ser lo más simple y rápido posible, sin adornos ni repeticiones innecesarias,
- la entropía no debe copiarse en dispositivos innecesarios y la necesidad de realizar cálculos o procesamientos debe mantenerse al mínimo,
- debe evitarse el uso de software/scripts/programas salvo que se haya realizado una revisión precisa del código y de todas las dependencias,
- distintas configuraciones pueden requerir procesos ligeramente diferentes.

## Creación de las palabras
El primer paso es calcular las 12 o 24 palabras de la mnemónica; 12 palabras suelen ser más que suficientes para la seguridad de un monedero Bitcoin.

Para generar las palabras, puedes usar el método descrito en [TRGM](https://github.com/valerio-vaccaro/TRMG), usando 3 dados: 1 de 8 caras y 2 de 16 caras. CADA tirada de dados corresponde a UNA Y SOLO UNA palabra; para encontrarla, basta con recorrer la tabla del sitio buscando la correspondencia de los dados con la tirada realizada (el primer dado es SIEMPRE el de 8 caras). La columna de la palabra contiene la palabra que buscas.

La recomendación es generar las 12 o 24 palabras y, si hace falta, corregir la última o, en cualquier caso, usar los dados para generar la entropía relativa a la última palabra.

## Cálculo del checksum
La última palabra no la decidimos completamente nosotros, sino que contiene una parte de control; es decir, no podemos elegir por completo los 11 bits de entropía que la componen. En cambio, podemos elegir los primeros 7 en el caso de una mnemónica de 12 palabras o los primeros 3 en el caso de una mnemónica de 24 palabras.

Supongamos que nuestra última palabra es BACON, correspondiente a las tiradas 1, 9 y 11 (recuerda que el primer dado es SIEMPRE el de 8 caras). La tabla también muestra Group 12 y Group 24, que nos permiten agrupar las palabras considerando solo la entropía de las dos primeras tiradas (group 12) o solo la primera tirada (group 24).

Supongamos que queremos construir una mnemónica de 12 palabras; esto significa que el checksum será una palabra entre las 16 posibles que tienen el mismo group 12 que bacon, es decir, 0001000. Las palabras posibles son:

|First|Second|Third|Index|Word	|Index in binary|Group 12	|Group 24|
|---|---|---|-------|-----------|---------------|-----------|---|
|1  |9	|1	|128	|avoid	    |00010000000	|0001000	|000|
|1  |9	|2	|129	|awake	    |00010000001	|0001000	|000|
|1  |9	|3	|130	|aware	    |00010000010	|0001000	|000|
|1  |9	|4	|131	|away	    |00010000011	|0001000	|000|
|1  |9	|5	|132	|awesome	|00010000100	|0001000	|000|
|1  |9	|6	|133	|awful	    |00010000101	|0001000	|000|
|1  |9	|7	|134	|awkward	|00010000110	|0001000	|000|
|1  |9	|8	|135	|axis	    |00010000111	|0001000	|000|
|1  |9	|9	|136	|baby	    |00010001000	|0001000	|000|
|1  |9	|10	|137	|bachelor	|00010001001	|0001000	|000|
|1  |9	|11	|138	|bacon	    |00010001010	|0001000	|000|
|1  |9	|12	|139	|badge	    |00010001011	|0001000	|000|
|1  |9	|13	|140	|bag    	|00010001100	|0001000	|000|
|1  |9	|14	|141	|balance	|00010001101	|0001000	|000|
|1  |9	|15	|142	|balcony	|00010001110	|0001000	|000|
|1  |9	|16	|143	|ball   	|00010001111	|0001000	|000|

¿Cómo encontrar la única palabra correcta entre las distintas opciones? Depende de tu configuración; veamos algunos ejemplos:

- bruteforce, es decir, probarlas todas en secuencia hasta encontrar la correcta (muy arduo con mnemónicas de 24 palabras); este es el método que se debe usar con Ledger o con Electrum (asegurándose de seleccionar la opción BIP39),
- calcular todas las palabras posibles con las primeras 11 o 23 palabras y buscar la única que pertenece a este conjunto; este método se puede usar con Jade y con otros hardware wallets capaces de calcular todas las posibles palabras finales de una mnemónica,
- introducir la mnemónica completa y dejar que el hardware wallet la corrija por nosotros, como hace Specter-DIY de forma muy elegante, por ejemplo.

## Backup (tema de otra lección)
Es fundamental tener una buena política de backup, por tanto:
- varios backups,
- en varios soportes y
- posiblemente cifrados o divididos (pero hay que saber hacerlo bien).

## Bibliografía

- [TRMG](https://github.com/valerio-vaccaro/TRMG)

## Repeticiones
Esta lección es repetitiva y se repetirá cada mes. A continuación se muestra una lista de las repeticiones ya realizadas.

| Date        | Notes                                          |
|-------------|------------------------------------------------|
| 240102-2100 | First lesson                                   |
