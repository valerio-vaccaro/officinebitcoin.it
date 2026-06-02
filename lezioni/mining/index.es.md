---
layout: default
title: "Introducción a la minería"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lección Bitcoin-only</span> <span>Este proyecto es mantenido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Introducción a la minería
La minería de Bitcoin es un proceso fundamental del protocolo que sirve para proponer un orden entre las transacciones presentes en la mempool, seleccionando un subconjunto para crear un nuevo bloque y actualizar el estado de la blockchain.

La minería está diseñada para ser descentralizada y aleatoria (entre comillas, ya que se basa en un acertijo criptográfico), evitando así la gestión centralizada de las transacciones.

## Finalidad de la minería
La minería resuelve problemas relacionados con la centralización, como:

- Censura: una entidad central podría bloquear algunas transacciones, pero con mineros descentralizados las transacciones tienen más posibilidades de ser incluidas.
- Doble gasto: sin un minero corruptible, es difícil reescribir la historia o favorecer una transacción en detrimento de otra.
- Sellado temporal: proporciona un orden temporal seguro y compartido, que no depende de una autoridad central, sino del consenso entre mineros y nodos.

# Cómo funciona la minería
El proceso de minería puede explicarse paso a paso:

- Selección de transacciones: el minero elige transacciones de la mempool, a menudo dando prioridad a las que tienen comisiones más altas, optimizando el beneficio (un problema NP-complete similar al "knapsack problem").
- Construcción de la coinbase: el minero crea una transacción especial (coinbase) que se asigna a sí mismo la recompensa del bloque (actualmente 3.125 BTC, reducida a la mitad cada cuatro años) más las comisiones de las transacciones seleccionadas.
- Merkle Root: las transacciones elegidas se organizan en una estructura de datos en árbol (Merkle Tree), que genera una Merkle Root, un hash que representa todas las transacciones y su orden.
- Block Header: el minero construye el prototipo de la cabecera del bloque, incluyendo:
1. La marca de tiempo.
2. El hash del bloque anterior.
3. La Merkle Root.
4. La dificultad (target), que depende de la red.
5. Un nonce (número aleatorio inicializado, por ejemplo, en cero).
- Acertijo criptográfico: el minero aplica dos veces el algoritmo SHA-256 a la cabecera y verifica si el resultado tiene un número suficiente de ceros iniciales (por debajo del umbral de dificultad). Si no, modifica el nonce u otros campos (por ejemplo, la marca de tiempo o el orden de las transacciones) y repite el cálculo. Es trabajo de fuerza bruta sin atajos, gracias a las propiedades de SHA-256.

## Optimizaciones
Para acelerar el proceso, los mineros pueden calcular el primer SHA-256 sobre los primeros 64 bytes de la cabecera (inmutables) y luego iterar solo sobre el resto, cambiando el nonce. La especialización ha llevado a hardware (ASIC) que realiza miles de millones de intentos por segundo.

# Proceso de validación
Cuando un minero encuentra una solución, transmite el bloque completo (cabecera + transacciones) a la red. Los nodos validan:
- el hash de la cabecera (un único SHA-256 para confirmar).
- la corrección de la información del bloque (marca de tiempo, hash del bloque anterior, Merkle Root y nonce).
- la reproducibilidad de la Merkle Root después de comprobar la corrección de todas las transacciones asociadas.

Si es válido, el bloque se añade a la blockchain. La recompensa (coinbase + comisiones) solo puede gastarse después de 100 confirmaciones (unas 16 horas), para garantizar la estabilidad.

# Costes y recompensas de la minería
Costes:

- Electricidad: principal coste variable.
- Hardware: ASIC caros y de corta vida útil, superados rápidamente por modelos más eficientes.
- Infraestructura: refrigeración, instalación, mantenimiento (por ejemplo, los paneles solares no son "gratis").

Recompensas:

- Recompensa fija (reducida a la mitad en 2024 a 3.125 BTC).
- Comisiones de transacción variables.

El minero debe respetar las reglas de consenso: un bloque inválido se descarta, desperdiciando recursos sin recompensa. Incluso un bloque válido puede quedar "huérfano" si otro minero gana la carrera, causando pérdidas.

## Estrategia económica
La minería es competitiva: los mineros buscan maximizar el tiempo en funcionamiento para amortizar los costes fijos. Los usos puntuales (por ejemplo, encender mineros solo con energía excedente) son poco prácticos, porque los costes iniciales requieren continuidad. El retorno de la inversión puede ser largo e incierto.

# Minería en solitario y en pool

- Solo Mining: el minero trabaja solo, construyendo el bloque con un nodo completo o software personalizado. Si encuentra un bloque, se lleva toda la recompensa, pero la probabilidad es extremadamente baja (podría tardar siglos con un solo ASIC).
- Pool Mining: protocolos como Stratum permiten a los mineros colaborar:
1. El pool proporciona una plantilla (coinbase, Merkle Root, etc.).
2. Los mineros envían shares (intentos con cierto número de ceros, por debajo de la dificultad del bloque) como prueba de trabajo.
3. Cuando un minero del pool encuentra un bloque, la recompensa se divide proporcionalmente a las shares enviadas.
- Stratum v2: evolución que permite a los mineros elegir transacciones, reduciendo la centralización del pool, aunque requiere comprobaciones para asegurar la corrección (por ejemplo, las comisiones para el pool).

# Estimación del hashrate
El hashrate (potencia de cálculo) se estima:
- En un pool: contando las shares recibidas en una unidad de tiempo, multiplicadas por la dificultad de share. Es una estimación que puede verse alterada por la suerte.
- Global: usando la dificultad de Bitcoin y el tiempo medio entre bloques (unos 10 minutos). Las oscilaciones son normales, pero la media es fiable.

Hardware como Nerd Miner usa contadores internos para obtener datos precisos, mientras que los pools se basan en estimaciones más variables, visibles en gráficos oscilantes.

# Programa
Esta lección fue creada para un Satoshi Spritz Connect.
