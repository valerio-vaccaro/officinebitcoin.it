---
layout: default
title: "O terminal de caracteres"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lição Bitcoin-only</span> <span>Este projeto é mantido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# O terminal de caracteres

## Introdução
Linux, ou melhor, um sistema GNU Linux, já que Linux é apenas o kernel que inicializa o hardware e fornece as primitivas para usá-lo, utiliza o conceito de arquivo para uma grande variedade de atividades. Arquivos são sequências de dados em um disco rígido, configurações e não só isso: existem filesystems específicos que criam arquivos informativos com os quais se controla o funcionamento do nosso computador, e muitos dispositivos também podem ser usados como arquivos, como dispositivos de caracteres que processam sequências de bytes de várias maneiras.

O processo de carregamento do sistema culmina em uma interface gráfica ou, no nosso caso, em um prompt de shell, isto é, a interface de caracteres que usaremos em nossas aulas.

Conhecer a interface permite executar muitas operações na maioria dos dispositivos Linux; no nosso curso consideraremos `bash` (bourne again shell), a shell mais difundida para Linux. Depois do login, estaremos no diretório home do nosso computador, isto é, em `\home\pippo` supondo que nosso nome de usuário seja pippo, ou em `\root` caso tenhamos entrado com a conta de superusuário (root, justamente).

NUNCA USE a conta root como é costume em outros sistemas operacionais.

Para se mover entre diretórios, você pode usar o comando `cd` (change directory), lembrando que ele aceita tanto caminhos absolutos que começam com `/` quanto caminhos relativos a partir do diretório atual (indicado com `.` ou sem nenhuma indicação) ou de outros diretórios como home (`~`). Se quiser obter uma lista de todos os arquivos presentes na pasta, você pode usar o comando `ls` (list), talvez com o argumento ll, isto é, `ls -ll`.

## Alguns comandos úteis

Alguns comandos úteis:

- `echo` imprime na tela o conteúdo de uma string passada como argumento,
- `man` abre o manual de um determinado comando,
- `mc` gerenciador de arquivos de console,
- `nano` editor de texto minimalista,
- `rm` remove um arquivo,
- `mkdir` cria um diretório,
- `rmdir` remove um diretório (que deve estar vazio),
- `touch` cria um arquivo vazio ou altera a data de um arquivo existente,
- `cat` imprime na tela o conteúdo de um arquivo de texto,
- `ncdu` permite navegar pelo filesystem ordenado pelo tamanho de arquivos e diretórios,
- `wget` permite baixar um arquivo da web,
- `dd` permite transferir informações entre arquivos, dispositivos, ...
- `tail` imprime na tela as últimas linhas de um arquivo (útil para logs com a opção `-f` (follow))
- `chmod` altera as propriedades de um arquivo (por exemplo, o argumento `+x` permite a execução de um arquivo)

Executáveis presentes na pasta atual podem ser executados antepondo `./`, isto é, indicando que o caminho se refere ao diretório atual.

## Redirecionamento de input/output
O redirecionamento de input e output pode ser feito com os símbolos `<` e `>`.

Para escrever em um arquivo, podemos executar

```
echo "pippo" > pippo.txt
```

Isso criará um arquivo chamado pippo.txt com o conteúdo pippo; se depois digitarmos

```
echo "pluto" > pippo.txt
```

O conteúdo do arquivo será substituído por pluto. Se quisermos manter o conteúdo anterior e acrescentar o novo conteúdo no final, devemos usar `>>` em vez de `>`.

O símbolo `<` funciona de modo semelhante para os inputs.

## Pipe
O pipe `|` permite concatenar o output de um programa com o input de outro.

```
cowsay "good evening" | lolcat
```

O output de cowsay é passado para o comando lolcat.

## Variáveis
Variáveis são nomes dados a espaços de memória que podem conter strings, números e mais.

Para definir uma variável, usa-se o comando `=`; para usá-la, basta antepor o caractere `$`. Por convenção, as variáveis são escritas em maiúsculas.

```
VARIABLE="pippo"
echo $VARIABLE > pippo.txt
VARIABLE="pluto"
echo $VARIABLE >> pippo.txt
```

Cria um arquivo com o conteúdo

```
pippo
pluto
```

Também é possível iniciar um programa e salvar o output em uma variável

```
VARIABLE=$(ls)
```

O output do comando ls é salvo na variável chamada VARIABLE.

## Scripts
Scripts são listas de comandos executados em sequência.

O primeiro comando é o interpretador usado para lançar o comando, normalmente `#!/bin/sh`, isto é, o executável `/bin/sh` com o prefixo `#!`.

Antes de executá-los, eles exigem permissões de execução com o comando `chmod +x filename`.

## Repetições
Esta aula é repetitiva e será repetida toda semana. Abaixo está uma lista das repetições já realizadas.

| Data        | Notas                                          |
|-------------|------------------------------------------------|
| 240122-2230 | Primeira aula                                  |
| 240129-2230 | Bash script                                    |
| 240205-2230 | Bash script                                    |
