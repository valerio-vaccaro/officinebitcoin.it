---
layout: default
title: "Instalación de Debian"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lección Bitcoin-only</span> <span>Este proyecto es mantenido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Instalación de Debian
Preparamos una unidad USB con la imagen de Debian descargada desde el sitio web oficial.

Conectamos todos los cables (display, keyboard, mouse, and ethernet).

![alt text](https://officinebitcoin.it/lezioni/debian/1.jpg)

Conectamos la unidad USB de instalación.

![alt text](https://officinebitcoin.it/lezioni/debian/2.jpg)

Encendemos el ordenador y nos aseguramos de que arranque nuestra unidad USB con Debian.

![alt text](https://officinebitcoin.it/lezioni/debian/3.jpg)

## Instalación
Si todo ha funcionado correctamente, debería iniciarse el instalador de Debian y llegaremos a la siguiente pantalla.

![alt text](https://officinebitcoin.it/lezioni/debian/4.jpg)

Elegimos la primera línea e iniciamos la instalación gráfica.

Lo primero que se nos pedirá es el idioma; para esta instalación elegiré "English", que me parece más comprensible que cualquier otra traducción.

![alt text](https://officinebitcoin.it/lezioni/debian/5.jpg)

En este punto se nos pedirá nuestra ubicación geográfica; para encontrar Italia debemos seleccionar OTHER->EUROPE->ITALY.

![alt text](https://officinebitcoin.it/lezioni/debian/6.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/7.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/8.jpg)

Para la localización también elijo English aquí.

![alt text](https://officinebitcoin.it/lezioni/debian/9.jpg)

Y configuro el teclado italiano, ya que es el que tengo disponible.

![alt text](https://officinebitcoin.it/lezioni/debian/10.jpg)

Luego elegimos un nombre de usuario y dejamos el dominio en blanco.

![alt text](https://officinebitcoin.it/lezioni/debian/11.jpg)

En este punto Debian nos pedirá seleccionar una contraseña para el usuario root...

![alt text](https://officinebitcoin.it/lezioni/debian/12.jpg)

y crear un usuario con su contraseña correspondiente.

![alt text](https://officinebitcoin.it/lezioni/debian/13.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/14.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/15.jpg)

Ahora debemos elegir el disco de instalación; usaremos todo el disco y debemos seleccionar el disco en el que realizar la instalación.

![alt text](https://officinebitcoin.it/lezioni/debian/16.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/17.jpg)

Luego debemos seleccionar la estructura de particiones; por ahora dejaremos todo en una sola partición.

![alt text](https://officinebitcoin.it/lezioni/debian/18.jpg)

Debian propone una tabla de particiones, pero... ha añadido swap, que no queremos, así que la seleccionamos y la eliminamos de la lista.

![alt text](https://officinebitcoin.it/lezioni/debian/19.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/20.jpg)

Ahora que la hemos eliminado, por fin podemos escribir nuestra tabla.

![alt text](https://officinebitcoin.it/lezioni/debian/21.jpg)

Debian querría volver a la configuración de la tabla de particiones, pero rechazamos la invitación.

![alt text](https://officinebitcoin.it/lezioni/debian/22.jpg)

Y confirmamos la intención de escribir la tabla actualizada.

![alt text](https://officinebitcoin.it/lezioni/debian/23.jpg)

Ahora se nos pregunta si queremos usar un mirror de Debian; elegimos usarlo.

![alt text](https://officinebitcoin.it/lezioni/debian/24.jpg)

Elegimos nuestro país.

![alt text](https://officinebitcoin.it/lezioni/debian/25.jpg)

Normalmente el mirror de GARR es rápido y fiable; usemos ese.

![alt text](https://officinebitcoin.it/lezioni/debian/26.jpg)

No tengo ningún proxy, así que dejo el campo en blanco.

![alt text](https://officinebitcoin.it/lezioni/debian/27.jpg)

Pero, ¿qué programas instalar? Como estamos preparando un servidor, desactivamos el entorno gráfico (quitando las dos primeras marcas) y seleccionamos SSH, que necesitaremos para el acceso remoto.

![alt text](https://officinebitcoin.it/lezioni/debian/28.jpg)

La instalación comienza.

Al final se nos pregunta si queremos instalar grub, que nos permite arrancar Linux; respondemos afirmativamente y elegimos el mismo disco en el que hemos instalado el sistema operativo.

![alt text](https://officinebitcoin.it/lezioni/debian/29.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/30.jpg)

Yuhuuu, hemos terminado; es hora de retirar la unidad USB y reiniciar la máquina.

![alt text](https://officinebitcoin.it/lezioni/debian/31.jpg)

Si todo ha funcionado correctamente, deberíamos encontrarnos frente a una terminal que nos pide iniciar sesión con uno de los perfiles creados durante la instalación.

## Configuración

### Conectémonos
Nos conectamos a nuestro servidor con `ssh username@ip`, donde username será el nombre elegido durante la instalación e ip la dirección IP del ordenador en el que instalamos.

Obviamente, este paso se puede omitir si instalas con monitor y teclado en lugar de conectarte por red.

Ten en cuenta que Debian PROHÍBE conectarse por ssh usando credenciales de superusuario (es decir, root).

### Repositorio
Ahora actualicemos los repositorios.

Nos convertimos en superusuario con el comando `su` y escribiendo la contraseña de root.

Editamos el archivo de repositorios con el comando `nano /etc/apt/sources.list` y eliminamos todas las líneas presentes.

Añadimos las siguientes líneas.

```                                                                    
deb http://deb.debian.org/debian/ bookworm contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm contrib main non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-updates contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm-updates contrib main non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-proposed-updates contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm-proposed-updates contrib main non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-backports contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm-backports contrib main non-free non-free-firmware

deb http://deb.debian.org/debian-security/ bookworm-security contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian-security/ bookworm-security contrib main non-free non-free-firmware

```

Luego podemos guardar el archivo pulsando `CTRL+x` y después `y`.

El comando `apt update` nos permite comprobar que todo ha ido bien y actualizar la lista de paquetes.

### Actualizar el sistema
Para actualizar el sistema, basta con ejecutar los siguientes comandos:

- `apt update` para actualizar la lista de paquetes,
- `apt upgrade` para actualizar los paquetes instalados para los que exista una nueva versión.

### Instalar tor y usarlo con ssh
Para instalar tor, basta con usar el comando `apt install tor`.

Una vez instalado, podemos configurarlo con el siguiente comando `nano /etc/tor/torrc`.

Al final del archivo añadimos las siguientes líneas.

```
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 22 127.0.0.1:22
```

Y reiniciamos tor con `systemctl restart tor`; ahora podemos encontrar nuestra dirección onion con `cat /var/lib/tor/hidden_service/hostname`.

Usando tor, ahora podemos conectarnos a nuestra máquina desde cualquier parte del mundo con `torify ssh username@onionaddress.onion`.

## Programa
La instalación de Debian es una lección repetitiva; aquí tienes una lista de las que ya se han realizado:

| Fecha       | Notas                                          |
|-------------|------------------------------------------------|
| 240415-2200 | Primera lección                                |
