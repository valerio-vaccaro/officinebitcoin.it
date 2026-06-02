---
layout: default
title: "El ciclo de vida de una transacción Bitcoin"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lección Bitcoin-only</span> <span>Este proyecto es mantenido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# El ciclo de vida de una transacción Bitcoin

## Qué es una transacción Bitcoin
Una transacción Bitcoin es una acción registrada en la blockchain que transfiere valor desde una o más entradas (fondos recibidos previamente, llamados UTXOs - Unspent Transaction Outputs) hacia una o más salidas (nuevos destinatarios).
Las entradas son salidas de transacciones anteriores que todavía no se han gastado, mientras que las salidas asignan satoshis a direcciones concretas. Una excepción es la transacción "coinbase", la primera de cada bloque, que genera nuevos bitcoins (recompensa de minería y comisiones) sin entradas. Si no se gastan todos los fondos de una entrada, la diferencia (change) vuelve al remitente mediante una salida adicional o, si no se gestiona, se pierde para siempre.

## Fases del ciclo de vida
Este es el ciclo de vida de la transacción:

- Creación: El wallet construye la transacción eligiendo qué UTXOs gastar según el importe que se va a enviar y la estrategia para minimizar las comisiones. Si la entrada supera a la salida, se genera una salida de "change" que vuelve al remitente, pero esto aumenta el tamaño y el coste de la transacción. Algunos wallets intentan evitarlo.
- Firma: La transacción se firma con una o más firmas digitales por cada entrada, autenticándola. Este paso es crucial para la validez y puede implicar a varias partes en el caso de transacciones multisig.
- Difusión: La transacción firmada se transmite a la red ("broadcast") y se inserta en el mempool del nodo local. El mempool valida la transacción según las reglas de consenso (por ejemplo, firmas válidas, fondos disponibles) y las reglas locales (por ejemplo, tamaño máximo de 400 KB para evitar spam). Después, el nodo la propaga a sus pares, que la validan y la insertan en sus mempools, creando una difusión en cascada. Los mempools varían entre nodos por sus distintas configuraciones o conexiones.
- Confirmación: Un minero incluye la transacción en un bloque, confirmándola en la blockchain. Sin embargo, hasta que tenga más confirmaciones (bloques posteriores), sigue siendo vulnerable a reemplazos o forks. Una transacción con comisiones bajas puede permanecer en el mempool durante mucho tiempo o ser descartada, pero podría minarse incluso después de meses si las entradas siguen sin gastarse.

## Gestión de problemas
- Transacción desaparecida del mempool: Si una transacción con comisiones bajas se elimina (por ejemplo, por picos de tráfico), puede retransmitirse manualmente (rebroadcast) usando el TXID, incluso con scripts o exploradores. Alguien podría hacerlo en nombre de terceros.
- Replace-by-Fee (RBF): Si la comisión es insuficiente, la transacción puede sustituirse por otra que pague más, siempre que esté marcada con la bandera RBF. Una propuesta sugiere que todas las transacciones deberían ser reemplazables de forma implícita, ya que los mineros prefieren comisiones más altas de todos modos.
- Child Pays for Parent (CPFP): Si no se puede usar RBF (por ejemplo, porque no es tu propia transacción o porque los fondos se han agotado), una salida de la transacción atascada se gasta con una nueva transacción que paga comisiones altas, haciendo que ambas resulten atractivas para los mineros. La suma de las comisiones debe cubrir ambas. Los problemas aparecen si los nodos descartan la primera transacción, rompiendo la cadena; un protocolo en desarrollo busca transmitir paquetes de transacciones para evitarlo.

## Confirmación final
Una transacción se considera final solo con múltiples confirmaciones (bloques por encima de ella). Una sola confirmación no basta, porque forks o un doble gasto podrían invalidarla. El White Paper sugiere 6 confirmaciones (unos 60 minutos, con bloques cada 10 minutos de media), pero el número varía según el importe y el riesgo. La variación en los tiempos de bloque es alta, pero la media se mantiene gracias a la dificultad de minería.

## Conclusión
El ciclo se cierra con la transacción "grabada" en la blockchain, registrando de forma permanente la transferencia de valor.

## Programa
Esta lección fue creada para un Satoshi Spritz Connect.
