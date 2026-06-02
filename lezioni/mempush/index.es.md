---
layout: default
title: "MemPush: enviar y gestionar transacciones Bitcoin en la mempool con sencillez"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lección Bitcoin-only</span> <span>Este proyecto es mantenido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# MemPush: enviar y gestionar transacciones Bitcoin en la mempool con sencillez

MemPush (https://mempush.com/) es una plataforma innovadora que hace que enviar y gestionar transacciones Bitcoin en la mempool sea simple, seguro y accesible. La mempool, el "depósito" temporal de transacciones Bitcoin que esperan confirmación en la blockchain, es el centro de este servicio, que elimina las complejidades técnicas para usuarios y desarrolladores.

## ¿Qué es MemPush?

MemPush es un servicio web que permite enviar raw Bitcoin transactions (en formato hexadecimal) directamente a la mempool, sin necesidad de configuraciones avanzadas ni Bitcoin nodes personales. Diseñado por Valerio Vaccaro, MemPush también admite la red Tor para garantizar mayor privacidad a los usuarios.

![alt text](https://officinebitcoin.it/lezioni/mempush/front.png)

El código fuente, disponible en GitHub (https://github.com/valerio-vaccaro/mempush) bajo una licencia open-source, permite que cualquiera verifique la seguridad del proyecto, contribuya a su desarrollo o aloje una instancia personalizada del servicio.

## ¿Cómo funciona MemPush?

La interfaz de MemPush es intuitiva y fácil de usar:

1. **Accede al sitio**: visita https://mempush.com/.
2. **Introduce la raw transaction**: pega la transacción Bitcoin en formato hexadecimal en el campo correspondiente.
3. **Envía la transacción**: haz clic en "Submit Raw Transaction" para propagar la transacción a la mempool a través de Bitcoin nodes.
4. **Supervisa el estado**: comprueba el progreso de la transacción con un blockchain explorer.
5. **Retransmisión automática**: MemPush retransmite automáticamente las transacciones, si es necesario, para asegurar su permanencia en la mempool.

![alt text](https://officinebitcoin.it/lezioni/mempush/list.png)

No se requiere registro, y el enfoque open-source elimina riesgos ocultos, lo que hace que MemPush sea ideal incluso para usuarios con menos experiencia.

## ¿Para quién es MemPush?

MemPush está diseñado para responder a distintas necesidades:
1. **Comisiones bajas**: las transacciones con comisiones bajas se retransmiten automáticamente para evitar que sean eliminadas de la mempool durante picos de tráfico.
2. **Transacciones timelocked**: admite la supervisión y retransmisión de transacciones con restricciones temporales, asegurando su gestión efectiva.
3. **Supervisión avanzada**: MemPush comprueba periódicamente el estado de las transacciones y permite eliminar solo las transacciones confirmadas o invalidadas (por ejemplo, double-spends).
4. **Privacidad mejorada**: gracias al soporte para la red Tor, MemPush protege el anonimato del usuario al enviar transacciones.

## Características técnicas

El repositorio de GitHub (https://github.com/valerio-vaccaro/mempush) muestra una implementación elegante en Python, basada en el framework Flask e integrada con una base de datos para la gestión de transacciones. MemPush se apoya en servicios como blockstream.info y mempool.space para supervisar y propagar transacciones, con planes futuros para integrar un Bitcoin node local.

Principales puntos fuertes:
- **Seguridad**: no se almacenan datos sensibles ni claves privadas, lo que garantiza una protección total.
- **Escalabilidad**: admite un alto volumen de transacciones gracias a la conexión directa con la red Bitcoin.
- **Open-source**: el código público permite verificaciones, contribuciones y personalizaciones por parte de la comunidad.

## Conclusión

MemPush es una solución potente y accesible para cualquiera que quiera enviar y gestionar transacciones Bitcoin en la mempool sin complicaciones. Con su transparencia, soporte para la privacidad y facilidad de uso, representa una valiosa incorporación al ecosistema Bitcoin. Visita https://mempush.com/ para probarlo o explora el código en https://github.com/valerio-vaccaro/mempush.
