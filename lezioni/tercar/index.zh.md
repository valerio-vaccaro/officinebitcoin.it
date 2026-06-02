---
layout: default
title: "字符终端"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only 课程</span> <span>本项目由 valerio-vaccaro 维护</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# 字符终端

## 介绍
Linux，或者更准确地说 GNU Linux 系统，因为 Linux 只是初始化硬件并提供使用硬件所需 primitives 的 kernel，它在大量活动中使用文件这一概念。文件是硬盘上的数据序列、配置，但不只是这些：还存在特定的 filesystems，会创建信息性文件，用来控制我们计算机的运行；许多设备也可以作为文件使用，例如字符设备，它们以各种方式处理字节序列。

系统加载过程最终会进入图形界面，或者在我们的情况下进入 shell prompt，也就是我们将在课程中使用的字符界面。

了解这个界面可以让你在大多数 Linux 设备上执行许多操作；在我们的课程中，我们会使用 `bash`（bourne again shell），这是 Linux 上最普遍的 shell。login 之后，我们会位于计算机的 home 目录中，也就是假设用户名是 pippo 时的 `\home\pippo`，或者如果使用 superuser 账户登录，则位于 `\root`（也就是 root）。

绝不要像在其他操作系统中习惯的那样使用 root 账户。

要在目录之间移动，可以使用 `cd`（change directory）命令。请记住，它既接受以 `/` 开头的绝对路径，也接受从当前目录出发的相对路径（用 `.` 表示，或者不加任何表示），还可以从其他目录出发，例如 home（`~`）。如果想列出文件夹中存在的所有文件，可以使用 `ls`（list）命令，也可以加上 ll 参数，即 `ls -ll`。

## 一些有用的命令

一些有用的命令：

- `echo` 将作为参数传入的字符串内容打印到屏幕上，
- `man` 调出某个命令的手册，
- `mc` 控制台文件管理器，
- `nano` 极简文本编辑器，
- `rm` 删除一个文件，
- `mkdir` 创建一个目录，
- `rmdir` 删除一个目录（该目录必须为空），
- `touch` 创建一个空文件，或更改已有文件的日期，
- `cat` 将文本文件的内容打印到屏幕上，
- `ncdu` 允许你按文件和目录大小排序来浏览 filesystem，
- `wget` 允许你从 web 下载文件，
- `dd` 允许在文件、设备、... 之间传输信息，
- `tail` 将文件最后几行打印到屏幕上（配合 `-f`（follow）选项查看 logs 很有用）
- `chmod` 更改文件的属性（例如 `+x` 参数允许执行一个文件）

当前文件夹中的可执行文件可以通过前缀 `./` 来执行，也就是说明该路径指向当前目录。

## Input/output 重定向
Input 和 output 重定向可以使用符号 `<` 和 `>` 完成。

要写入文件，可以执行

```
echo "pippo" > pippo.txt
```

这会创建一个名为 pippo.txt 的文件，内容为 pippo；如果随后输入

```
echo "pluto" > pippo.txt
```

文件内容将被替换为 pluto。如果想保留之前的内容，并把新内容追加到末尾，就必须使用 `>>` 而不是 `>`。

`<` 符号对 inputs 的作用类似。

## Pipe
pipe `|` 允许把一个程序的 output 连接到另一个程序的 input。

```
cowsay "good evening" | lolcat
```

cowsay 的 output 会传给 lolcat 命令。

## 变量
变量是赋予内存空间的名称，这些空间可以包含字符串、数字以及其他内容。

要设置变量，使用 `=` 命令；要使用变量，只需在前面加上 `$` 字符。按照惯例，变量使用大写字母书写。

```
VARIABLE="pippo"
echo $VARIABLE > pippo.txt
VARIABLE="pluto"
echo $VARIABLE >> pippo.txt
```

会创建一个包含以下内容的文件

```
pippo
pluto
```

也可以启动一个程序，并把 output 保存到变量中

```
VARIABLE=$(ls)
```

ls 命令的 output 会被保存到名为 VARIABLE 的变量中。

## Scripts
Scripts 是按顺序执行的命令列表。

第一个命令是用来启动命令的 interpreter，通常是 `#!/bin/sh`，也就是带有 `#!` 前缀的可执行文件 `/bin/sh`。

在执行它们之前，需要通过命令 `chmod +x filename` 赋予执行权限。

## 重复课程
这节课是重复性的，并且会每周重复。下面是已经举行过的重复课程列表。

| 日期        | 备注                                           |
|-------------|------------------------------------------------|
| 240122-2230 | 第一课                                         |
| 240129-2230 | Bash script                                    |
| 240205-2230 | Bash script                                    |
