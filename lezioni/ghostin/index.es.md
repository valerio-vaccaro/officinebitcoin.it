---
layout: default
title: "Ghostinbox.it: usar email sin tener una cuenta email"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lección Bitcoin-only</span> <span>Este proyecto es mantenido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Ghostinbox.it: usar email sin tener una cuenta email

Ghostinbox es una plataforma web que permite a los usuarios crear direcciones de email temporales para recibir mensajes sin revelar su dirección de email real. El servicio es ideal para registros rápidos, verificaciones de cuenta, pruebas de entregabilidad de email o cualquier situación en la que quieras evitar el spam o proteger tu identidad.

A diferencia de los servicios de email tradicionales, Ghostinbox no exige registro ni almacena datos personales, por lo que es una excelente opción para quienes dan prioridad a la privacidad. Además, el soporte para la red Tor permite acceder al servicio de forma anónima, ocultando la dirección IP del usuario. La naturaleza open-source del proyecto garantiza transparencia y permite a los desarrolladores examinar el código en busca de posibles vulnerabilidades o personalizaciones.

## ¿Cómo funciona Ghostinbox?
![alt text](https://officinebitcoin.it/lezioni/ghostin/front.png)

Usar Ghostinbox es extremadamente intuitivo y no requiere conocimientos técnicos:

1. **Accede al sitio**: Visita https://ghostinbox.it/ (o accede mediante Tor para mayor anonimato).
2. **Genera una dirección de email temporal**: Haz clic en el botón para crear una nueva dirección de email temporal (por ejemplo, random@ghostinbox.it). La dirección queda activa de inmediato y lista para usarse.
3. **Recibe mensajes**: Usa la dirección generada para recibir emails, por ejemplo para registros en servicios online, verificaciones de cuenta o pruebas. Los mensajes aparecen en tiempo real en la bandeja de entrada del sitio.
4. **Supervisa los mensajes**: Accede a la bandeja temporal directamente en Ghostinbox para ver los mensajes recibidos. No se necesita ningún cliente de email externo.

![alt text](https://officinebitcoin.it/lezioni/ghostin/email.png)

El servicio está diseñado para ser rápido y sin fricciones: no hace falta crear una cuenta, y la interfaz minimalista hace que la experiencia sea fluida incluso para usuarios no técnicos. La posibilidad de acceder mediante Tor añade un nivel adicional de protección para quienes quieren mantener un anonimato completo.

## Del alias al email
Para usar el servicio, debes elegir un alias lo bastante largo y aleatorio como para que otros usuarios no puedan adivinarlo. Este alias será como una contraseña para acceder al email y, por lo tanto, no debe olvidarse.

A partir de este alias se deriva una dirección de email HASH@ghostinbox.it, donde HASH equivale a `sha256(alias)`, es decir, el hash del alias usando SHA-256; después, el usuario puede utilizar este email (mostrado en el esquema de recepción) para recibir emails. La página de recepción se actualiza automáticamente mostrando los emails recibidos. Un usuario puede crear una dirección de email sin acceder al servicio y usar el sitio web solo para consultar.

Al hacer clic en el email, puedes leer su texto y, si es necesario, copiar enlaces para abrirlos; el formato del email es deliberadamente solo texto y, por tanto, no mostrará ninguna de las características gráficas de los emails basados en HTML.

## ¿Quién necesita Ghostinbox?
Ghostinbox responde a varias necesidades relacionadas con la privacidad y la gestión de emails temporales:

1. **Protección contra spam**: Al usar una dirección temporal, los usuarios pueden evitar que su dirección de email real se llene de spam o newsletters no deseadas.
2. **Registros seguros**: Perfecto para registrarse en servicios online, foros o plataformas que requieren verificación por email sin comprometer el email personal.
3. **Pruebas de entregabilidad**: Desarrolladores y responsables de marketing pueden usar Ghostinbox para probar el envío y la recepción de emails sin involucrar direcciones reales.
4. **Privacidad avanzada**: Gracias al soporte para Tor, el servicio es ideal para usuarios que quieren mantener el anonimato durante la interacción con sitios web o servicios online.
5. **Uso temporal**: Adecuado para situaciones en las que se necesita una dirección de email desechable, como promociones, pruebas gratuitas o comunicaciones de corta duración.

![alt text](https://officinebitcoin.it/lezioni/ghostin/stats.png)

## Características técnicas
El repositorio GitHub de Ghostinbox (https://github.com/valerio-vaccaro/ghostinbox.it) muestra una implementación ligera, escrita principalmente en Python con el framework Flask, con las siguientes características:

- **Enfoque serverless**: no hay servidor de email, sino que se aprovecha un servicio gratuito de email y reenvío de email, lo que hace que la arquitectura del servicio sea extremadamente simple y económica.
- **Arquitectura**: Ghostinbox usa una arquitectura cliente-servidor basada en Flask para gestionar la generación de direcciones de email temporales y la visualización de mensajes. La simplicidad del diseño garantiza un alto rendimiento incluso con grandes volúmenes de solicitudes.
- **Generación de direcciones**: Las direcciones de email temporales se generan dinámicamente a partir del alias introducido.
- **Soporte Tor**: El servicio está configurado para ser accesible mediante onion routing, lo que garantiza que la dirección IP del usuario no se rastree durante la interacción con el sitio.
- **Gestión de mensajes**: Los mensajes recibidos se eliminan después de 30 días.
- **Seguridad**: No se almacenan de forma permanente datos personales ni mensajes. El diseño del servicio minimiza los riesgos de brechas, y la ausencia de registro elimina la necesidad de proporcionar información sensible.
- **Open-source**: El código público permite a los desarrolladores verificar la integridad del sistema, aportar mejoras o alojar una instancia personalizada.

Puntos fuertes técnicos:
- **Privacidad absoluta**: La eliminación de emails después de 30 días y el soporte para Tor garantizan una experiencia anónima y segura.
- **Ligereza**: La implementación en Flask está optimizada para pocos recursos, lo que hace que el servicio sea escalable y rápido.
- **Transparencia**: La licencia open-source permite auditorías del código y personalizaciones, aumentando la confianza de los usuarios.

## Conclusión
Ghostinbox es una solución elegante y funcional para quienes buscan un servicio de email temporal rápido, seguro y orientado a la privacidad. Con su interfaz intuitiva, el soporte para Tor y la transparencia del código open-source, resulta útil tanto para usuarios comunes que quieren proteger su bandeja de entrada del spam como para desarrolladores que necesitan un sistema fiable para pruebas o registros temporales. Para probar Ghostinbox, visita https://ghostinbox.it/. Para explorar el código o contribuir al proyecto, consulta el repositorio en https://github.com/valerio-vaccaro/ghostinbox.it.

