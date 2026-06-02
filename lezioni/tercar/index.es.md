---
layout: default
title: "El terminal de caracteres"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lección Bitcoin-only</span> <span>Este proyecto es mantenido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# El terminal de caracteres

## Introducción
Linux, o mejor dicho un sistema GNU Linux, ya que Linux es solo el kernel que inicializa el hardware y proporciona las primitivas para usarlo, utiliza el concepto de archivo para una enorme variedad de actividades. Los archivos son secuencias de datos en un disco duro, configuraciones y no solo eso: existen filesystems específicos que crean archivos informativos con los que controlar el funcionamiento de nuestro ordenador, y muchos dispositivos también pueden usarse como archivos, como dispositivos de caracteres que procesan secuencias de bytes de distintas maneras.

El proceso de carga del sistema culmina en una interfaz gráfica o, en nuestro caso, en un prompt de shell, es decir, la interfaz de caracteres que usaremos en nuestras lecciones.

Conocer la interfaz permite realizar muchas operaciones en la mayoría de los dispositivos Linux; en nuestro curso consideraremos `bash` (bourne again shell), la shell más extendida para Linux. Después del login nos encontraremos en el directorio home de nuestro ordenador, es decir, en `\home\pippo` suponiendo que nuestro nombre de usuario sea pippo, o en `\root` si hemos entrado con la cuenta de superusuario (root, precisamente).

NO USES NUNCA la cuenta root como suele hacerse en otros sistemas operativos.

Para moverte entre directorios puedes usar el comando `cd` (change directory), recordando que acepta tanto rutas absolutas que empiezan por `/` como rutas relativas desde el directorio actual (indicado con `.` o sin ninguna indicación) o desde otros directorios como home (`~`). Si quieres obtener una lista de todos los archivos presentes en la carpeta, puedes usar el comando `ls` (list), quizá con el argumento ll, es decir, `ls -ll`.

## Algunos comandos útiles

Algunos comandos útiles:

- `echo` imprime en pantalla el contenido de una cadena pasada como argumento,
- `man` abre el manual de un determinado comando,
- `mc` gestor de archivos de consola,
- `nano` editor de texto minimalista,
- `rm` elimina un archivo,
- `mkdir` crea un directorio,
- `rmdir` elimina un directorio (que debe estar vacío),
- `touch` crea un archivo vacío o cambia la fecha de un archivo existente,
- `cat` imprime en pantalla el contenido de un archivo de texto,
- `ncdu` permite navegar por el filesystem ordenado por el tamaño de archivos y directorios,
- `wget` permite descargar un archivo de la web,
- `dd` permite transferir información entre archivos, dispositivos, ...
- `tail` imprime en pantalla las últimas líneas de un archivo (útil para logs con la opción `-f` (follow))
- `chmod` cambia las propiedades de un archivo (por ejemplo, el argumento `+x` permite la ejecución de un archivo)

Los ejecutables presentes en la carpeta actual pueden ejecutarse anteponiendo `./`, es decir, indicando que la ruta se refiere al directorio actual.

## Redirección de input/output
La redirección de input y output puede hacerse con los símbolos `<` y `>`.

Para escribir en un archivo podemos ejecutar

```
echo "pippo" > pippo.txt
```

Esto creará un archivo llamado pippo.txt con el contenido pippo; si después escribimos

```
echo "pluto" > pippo.txt
```

El contenido del archivo será reemplazado por pluto. Si quisiéramos conservar el contenido anterior y añadir el nuevo contenido al final, debemos usar `>>` en lugar de `>`.

El símbolo `<` funciona de manera similar para los inputs.

## Pipe
El pipe `|` permite concatenar el output de un programa con el input de otro.

```
cowsay "good evening" | lolcat
```

El output de cowsay se pasa al comando lolcat.

## Variables
Las variables son nombres asignados a espacios de memoria que pueden contener cadenas, números y más.

Para definir una variable, se usa el comando `=`; para utilizarla, basta con anteponer el carácter `$`. Por convención, las variables se escriben en mayúsculas.

```
VARIABLE="pippo"
echo $VARIABLE > pippo.txt
VARIABLE="pluto"
echo $VARIABLE >> pippo.txt
```

Crea un archivo con el contenido

```
pippo
pluto
```

También puedes lanzar un programa y guardar el output en una variable

```
VARIABLE=$(ls)
```

El output del comando ls se guarda en la variable llamada VARIABLE.

## Scripts
Los scripts son listas de comandos ejecutados en secuencia.

El primer comando es el intérprete usado para lanzar el comando, normalmente `#!/bin/sh`, es decir, el ejecutable `/bin/sh` con el prefijo `#!`.

Antes de ejecutarlos, requieren permisos de ejecución con el comando `chmod +x filename`.

## Repeticiones
Esta lección es repetitiva y se repetirá cada semana. A continuación hay una lista de las repeticiones ya realizadas.

| Fecha       | Notas                                          |
|-------------|------------------------------------------------|
| 240122-2230 | Primera lección                                |
| 240129-2230 | Bash script                                    |
| 240205-2230 | Bash script                                    |
