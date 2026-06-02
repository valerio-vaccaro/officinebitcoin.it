---
layout: default
title: "Das Zeichenterminal"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only-Lektion</span> <span>Dieses Projekt wird von valerio-vaccaro gepflegt</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Das Zeichenterminal

## Einführung
Linux, genauer gesagt ein GNU-Linux-System, da Linux nur der Kernel ist, der die Hardware initialisiert und die Primitiven zu ihrer Nutzung bereitstellt, verwendet das Konzept der Datei für eine Vielzahl von Tätigkeiten. Dateien sind Datenfolgen auf einer Festplatte, Konfigurationen und nicht nur das: Es gibt spezifische filesystems, die Informationsdateien erzeugen, mit denen sich die Funktionsweise unseres Computers steuern lässt, und auch viele Geräte können als Dateien verwendet werden, etwa als Zeichengeräte, die Bytefolgen auf verschiedene Weise verarbeiten.

Der Ladevorgang des Systems endet in einer grafischen Oberfläche oder, in unserem Fall, in einem Shell-Prompt, also der Zeichenoberfläche, die wir in unseren Lektionen verwenden werden.

Die Kenntnis der Oberfläche ermöglicht viele Operationen auf den meisten Linux-Geräten; in unserem Kurs betrachten wir `bash` (bourne again shell), die am weitesten verbreitete Shell für Linux. Nach dem Login befinden wir uns im Home-Verzeichnis unseres Computers, also in `\home\pippo`, wenn unser Benutzername pippo ist, oder in `\root`, falls wir uns mit dem Superuser-Konto angemeldet haben (eben root).

VERWENDEN SIE NIEMALS das root-Konto so, wie es in anderen Betriebssystemen üblich ist.

Um zwischen Verzeichnissen zu wechseln, kann man den Befehl `cd` (change directory) verwenden. Dabei sollte man beachten, dass er sowohl absolute Pfade akzeptiert, die mit `/` beginnen, als auch relative Pfade vom aktuellen Verzeichnis aus (angegeben mit `.` oder ohne Angabe) oder von anderen Verzeichnissen wie home (`~`). Wenn man eine Liste aller im Ordner vorhandenen Dateien haben möchte, kann man den Befehl `ls` (list) verwenden, vielleicht mit dem Argument ll, also `ls -ll`.

## Einige nützliche Befehle

Einige nützliche Befehle:

- `echo` gibt den Inhalt einer als Argument übergebenen Zeichenkette auf dem Bildschirm aus,
- `man` ruft das Handbuch eines bestimmten Befehls auf,
- `mc` Dateimanager für die Konsole,
- `nano` minimaler Texteditor,
- `rm` entfernt eine Datei,
- `mkdir` erstellt ein Verzeichnis,
- `rmdir` entfernt ein Verzeichnis (das leer sein muss),
- `touch` erstellt eine leere Datei oder ändert das Datum einer vorhandenen Datei,
- `cat` gibt den Inhalt einer Textdatei auf dem Bildschirm aus,
- `ncdu` ermöglicht das Navigieren im filesystem, geordnet nach der Größe von Dateien und Verzeichnissen,
- `wget` ermöglicht das Herunterladen einer Datei aus dem Web,
- `dd` ermöglicht die Übertragung von Informationen zwischen Dateien, Geräten, ...
- `tail` gibt die letzten Zeilen einer Datei auf dem Bildschirm aus (nützlich für Logs mit der Option `-f` (follow))
- `chmod` ändert die Eigenschaften einer Datei (zum Beispiel erlaubt das Argument `+x` die Ausführung einer Datei)

Ausführbare Dateien im aktuellen Ordner können durch Voranstellen von `./` ausgeführt werden, also durch Angabe, dass sich der Pfad auf das aktuelle Verzeichnis bezieht.

## Input-/Output-Umleitung
Input und Output können mit den Symbolen `<` und `>` umgeleitet werden.

Um in eine Datei zu schreiben, können wir ausführen

```
echo "pippo" > pippo.txt
```

Dies erstellt eine Datei namens pippo.txt mit dem Inhalt pippo; wenn wir anschließend eingeben

```
echo "pluto" > pippo.txt
```

wird der Dateiinhalt durch pluto ersetzt. Wenn wir den vorherigen Inhalt behalten und den neuen Inhalt am Ende anhängen möchten, müssen wir `>>` statt `>` verwenden.

Das Symbol `<` funktioniert für inputs auf ähnliche Weise.

## Pipe
Die Pipe `|` erlaubt es, den Output eines Programms mit dem Input eines anderen zu verketten.

```
cowsay "good evening" | lolcat
```

Der Output von cowsay wird an den Befehl lolcat weitergegeben.

## Variablen
Variablen sind Namen für Speicherbereiche, die Zeichenketten, Zahlen und anderes enthalten können.

Um eine Variable zu setzen, verwendet man den Befehl `=`; um sie zu verwenden, stellt man einfach das Zeichen `$` voran. Konventionell werden Variablen in Großbuchstaben geschrieben.

```
VARIABLE="pippo"
echo $VARIABLE > pippo.txt
VARIABLE="pluto"
echo $VARIABLE >> pippo.txt
```

Erstellt eine Datei mit dem Inhalt

```
pippo
pluto
```

Man kann auch ein Programm starten und den Output in einer Variablen speichern

```
VARIABLE=$(ls)
```

Der Output des Befehls ls wird in der Variablen namens VARIABLE gespeichert.

## Scripts
Scripts sind Listen von Befehlen, die nacheinander ausgeführt werden.

Der erste Befehl ist der Interpreter, der zum Starten des Befehls verwendet wird, normalerweise `#!/bin/sh`, also die ausführbare Datei `/bin/sh` mit dem Präfix `#!`.

Vor der Ausführung benötigen sie Ausführungsberechtigungen mit dem Befehl `chmod +x filename`.

## Wiederholungen
Diese Lektion ist wiederkehrend und wird jede Woche wiederholt. Unten steht eine Liste der bereits gehaltenen Wiederholungen.

| Datum       | Notizen                                        |
|-------------|------------------------------------------------|
| 240122-2230 | Erste Lektion                                  |
| 240129-2230 | Bash script                                    |
| 240205-2230 | Bash script                                    |
