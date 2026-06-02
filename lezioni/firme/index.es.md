---
layout: default
title: "Firmas digitales"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lección Bitcoin-only</span> <span>Este proyecto es mantenido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Firmas digitales
El tema de esta lección serán las firmas digitales y cómo se aplican a Bitcoin.

## ¿Qué es una firma?
Necesitamos entender qué queremos decir con firma digital. Cuando pensamos en una firma normal, solemos pensar en otra cosa: como hablamos de documentos digitales, la firma digital vincula tanto la identidad del autor como el estado del documento firmado, de modo que, en esencia, la firma también depende del documento que vamos a firmar.

Esta es una diferencia muy grande respecto al mundo físico, donde ponemos la firma prácticamente sin preocuparnos por el soporte sobre el que la hacemos. Naturalmente, quizá no firmemos cheques u otros documentos sin prestar atención, pero en esencia la firma que vamos a estampar no cambia.

Las firmas digitales son algo un poco distinto; normalmente se basan en algoritmos de clave pública y clave privada. Esto significa que, en algún lugar del mundo, nuestro wallet tiene un par de claves, pública y privada, y nuestra (pseudo-)identidad está vinculada a la clave pública que todos conocen o que daremos a conocer a todos.

Usaremos nuestra clave privada, que es un número, y con cierta magia matemática produciremos una firma que es otro número distinto y que prueba que un cierto estado de un cierto documento pertenece a, o es conocido por, una cierta identidad conectada a una clave pública. Lo que voy a firmar es la huella (o HASH) de un determinado documento (o PAYLOAD).

También necesito algún generador de números aleatorios; meto todos estos datos en una "caja negra" que produce una firma para mí. Por tanto, la firma es algo que prueba la posesión porque estoy firmando con mi secreto, pero también prueba que lo que estoy firmando no ha sido modificado.

Si modifico el PAYLOAD, modifico el HASH y obviamente esto invalida la firma.

Entonces, ¿por qué se introdujo en el mundo digital esta firma más compleja? Porque en el mundo digital, a diferencia del físico (y quizá lo recuerden quienes se saltaron la escuela), copiar una firma es mucho más sencillo.

La firma digital, en cambio, contiene información sobre el documento y por eso cambia para cada documento; no puede pegarse y reutilizarse en un documento diferente.

Por tanto, la firma digital sirve para:
- demostrar que he creado un determinado mensaje, que estoy solicitando una determinada acción o que estoy declarando un determinado estado de un sistema, y
- demostrar que ese mensaje, ese documento o esa cadena de datos no ha sido manipulado, es decir, que realmente es lo que quería firmar.
- hacer que una determinada acción sea no repudiable; si produje una firma, fui realmente yo quien lo hizo para ese documento específico.

## Firmas en Bitcoin
Esta tecnología se usa en Bitcoin bajo el acrónimo ECDSA (Elliptic Curve Digital Signature Algorithm), que es un algoritmo para producir firmas digitales sobre curvas elípticas; por ahora no trataremos otros esquemas de firma.

Recuerda que en Bitcoin se pueden producir firmas para:
- texto arbitrario, poco importante y poco usado
- nuevas transacciones, con el objetivo de autorizar el gasto de un determinado UTXO

Pero ¿cómo se vinculan estas firmas con la transacción? Cada dirección tiene un mecanismo de gasto, scripts que deben ejecutarse para saber si un gasto puede autorizarse. Dentro de estos scripts hay comandos (u OPCODES) destinados a verificar firmas digitales, como OP_CHECKSIG, OP_CHECKSIGVERIFY, OP_CHECKMULTISIG, OP_CHECKMULTISIGVERIFY

Recuerda que una transacción de Bitcoin consta de:
- Inputs, es decir, los fondos que voy a gastar y para los cuales debo producir un script de gasto
- Outputs, es decir, las nuevas direcciones a las que irán los fondos (y para cada dirección está conectado un modo de gasto bien definido.

En esencia, en la mayoría de los casos tendré que producir PARA CADA INPUT la(s) firma(s) necesaria(s) para completar el script de gasto.

Recuerda que esta acción nos permite demostrar que ese input es nuestro y que queremos gastarlo (queremos transferir la propiedad por completo, dividirla o unirla con otros inputs).

Obviamente, la transacción es válida si todos los inputs están firmados correctamente; si incluso uno solo de los inputs no está firmado, esa transacción no puede considerarse válida.

La firma es verificable por todos y es no repudiable, pero por flexibilidad Satoshi introdujo de forma muy inteligente varios modos de firma: la firma es siempre la misma, pero cambia el PAYLOAD, es decir, la porción de transacción que es objeto de la firma. Esto permite, por ejemplo, generar esquemas y protocolos complejos en los que piezas de transacciones pueden combinarse entre sí; Satoshi llamó a estos modos (verdaderas flags en el lenguaje de scripting) SIGHASH.

## SIGHASH
El SIGHASH más simple es SIGHASH_ALL, que significa generar una firma con TODOS LOS INPUTS y TODOS LOS OUTPUTS; es el modo más sencillo y más usado para hacer una firma.

Una primera diferencia aparece con SIGHASH_NONE, que firma TODOS LOS INPUTS, pero NINGUNO de los OUTPUTS, permitiendo añadir outputs o modificar las comisiones después. ATENCIÓN: con este esquema, si no está protegido por multisig u otras funciones, un miner o cualquiera que vea una transacción con este esquema de firma puede reemplazar los outputs redirigiendo los fondos a su propia dirección.

Una flag más interesante es SIGHASH_SINGLE, en la que se firma una pareja de input y output siempre que estén insertados en una transacción al mismo nivel (por ejemplo, quinto input y quinto output); esto permitiría componer transacciones mayores a partir de estas parejas, pero no da la posibilidad de introducir cambio, es decir, exige gastar por completo el input.

En paralelo, todos estos SIGHASH pueden combinarse con la flag ANYONECANPAY, que limita la firma solo al input para el que se está produciendo la firma, dando así a cualquiera la posibilidad de añadir inputs a la transacción.

Todas estas firmas son firmas válidas independientemente del tipo de dirección y de scripts, dejando la máxima flexibilidad de expresión al wallet, que normalmente usará SIGHASH_ALL pero también podría seguir protocolos más complejos que requieran esquemas de firma diferentes. En caso de multisig, además, no es necesario usar el mismo tipo de firma; un wallet 2-of-2 podría firmar algunos de sus UTXO con SIGHASH_NONE y ANYONECANPAY para dar control total al segundo firmante, que podría, por ejemplo, reunir todos estos inputs en una transacción que se firmará con SIGHASH_ALL.

## Firmas sobre texto arbitrario
Para completar, las mismas firmas usadas para los inputs de transacciones también pueden usarse para firmar texto arbitrario.

Bitcoin propone un esquema en el que se añade texto para evitar que esta funcionalidad se use para firmar partes de transacciones; por tanto, si tienes Bitcoin Core o incluso algunos wallets, puedes buscar una funcionalidad de firma de mensajes de texto basada en una determinada dirección tuya.

El wallet usará la clave privada asociada a la clave pública que generó esa dirección para crear firmas de mensajes de texto.

En el momento de la verificación se obtiene la clave pública, que luego puede usarse para regenerar la dirección; así, si tengo el texto y la firma, extraigo la clave pública que lo firmó, y a partir de la clave pública puedo recalcular la dirección y comprobarla, por ejemplo, con la proporcionada.

## Programa
La lección sobre firmas puede repetirse; aquí hay una lista de las ya realizadas:

| Fecha       | Notas                                          |
|-------------|------------------------------------------------|
|||
