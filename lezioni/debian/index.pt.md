---
layout: default
title: "Instalação do Debian"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lição Bitcoin-only</span> <span>Este projeto é mantido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Instalação do Debian
Preparamos uma unidade USB com a imagem do Debian baixada do site oficial.

Conectamos todos os cabos (display, keyboard, mouse, and ethernet).

![alt text](https://officinebitcoin.it/lezioni/debian/1.jpg)

Conectamos a unidade USB de instalação.

![alt text](https://officinebitcoin.it/lezioni/debian/2.jpg)

Ligamos o computador e nos certificamos de que nossa unidade USB com Debian inicialize.

![alt text](https://officinebitcoin.it/lezioni/debian/3.jpg)

## Instalação
Se tudo funcionou corretamente, o instalador do Debian deve iniciar e chegaremos à tela seguinte.

![alt text](https://officinebitcoin.it/lezioni/debian/4.jpg)

Escolhemos a primeira linha e iniciamos a instalação gráfica.

A primeira coisa que nos será perguntada é o idioma; para esta instalação escolherei "English", que considero mais compreensível do que qualquer outra tradução.

![alt text](https://officinebitcoin.it/lezioni/debian/5.jpg)

Neste ponto será solicitada a nossa localização geográfica; para encontrar a Itália, precisamos selecionar OTHER->EUROPE->ITALY.

![alt text](https://officinebitcoin.it/lezioni/debian/6.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/7.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/8.jpg)

Para a localização, também escolho English aqui.

![alt text](https://officinebitcoin.it/lezioni/debian/9.jpg)

E configuro o teclado italiano, já que é o que tenho disponível.

![alt text](https://officinebitcoin.it/lezioni/debian/10.jpg)

Depois escolhemos um nome de usuário e deixamos o domínio em branco.

![alt text](https://officinebitcoin.it/lezioni/debian/11.jpg)

Neste ponto, o Debian pedirá que você selecione uma senha para o usuário root...

![alt text](https://officinebitcoin.it/lezioni/debian/12.jpg)

e crie um usuário com sua respectiva senha.

![alt text](https://officinebitcoin.it/lezioni/debian/13.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/14.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/15.jpg)

Agora precisamos escolher o disco de instalação; usaremos o disco inteiro e precisamos selecionar o disco no qual realizar a instalação.

![alt text](https://officinebitcoin.it/lezioni/debian/16.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/17.jpg)

Depois precisamos selecionar a estrutura de partições; por enquanto deixaremos tudo em uma única partição.

![alt text](https://officinebitcoin.it/lezioni/debian/18.jpg)

O Debian propõe uma tabela de partições, mas... adicionou swap, que não queremos, então vamos selecioná-la e removê-la da lista.

![alt text](https://officinebitcoin.it/lezioni/debian/19.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/20.jpg)

Agora que a removemos, podemos finalmente gravar nossa tabela.

![alt text](https://officinebitcoin.it/lezioni/debian/21.jpg)

O Debian gostaria de voltar à configuração da tabela de partições, mas recusamos o convite.

![alt text](https://officinebitcoin.it/lezioni/debian/22.jpg)

E confirmamos a intenção de gravar a tabela atualizada.

![alt text](https://officinebitcoin.it/lezioni/debian/23.jpg)

Agora nos perguntam se queremos usar um mirror do Debian; escolhemos usá-lo.

![alt text](https://officinebitcoin.it/lezioni/debian/24.jpg)

Escolhemos nosso país.

![alt text](https://officinebitcoin.it/lezioni/debian/25.jpg)

Normalmente o mirror da GARR é rápido e confiável; vamos usá-lo.

![alt text](https://officinebitcoin.it/lezioni/debian/26.jpg)

Não tenho nenhum proxy, então deixo o campo em branco.

![alt text](https://officinebitcoin.it/lezioni/debian/27.jpg)

Mas quais programas instalar? Como estamos montando um servidor, desativamos o ambiente gráfico (removendo as duas primeiras marcações) e selecionamos SSH, de que precisaremos para acesso remoto.

![alt text](https://officinebitcoin.it/lezioni/debian/28.jpg)

A instalação começa.

No final, nos perguntam se queremos instalar o grub, que nos permite inicializar o Linux; respondemos afirmativamente e escolhemos o mesmo disco no qual instalamos o sistema operacional.

![alt text](https://officinebitcoin.it/lezioni/debian/29.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/30.jpg)

Yuhuuu, terminamos; é hora de remover a unidade USB e reiniciar a máquina.

![alt text](https://officinebitcoin.it/lezioni/debian/31.jpg)

Se tudo funcionou corretamente, deveremos nos encontrar diante de um terminal pedindo para fazer login com um dos perfis criados durante a instalação.

## Configuração

### Vamos nos conectar
Conectamo-nos ao nosso servidor com `ssh username@ip`, onde username será o nome escolhido durante a instalação e ip o endereço IP do computador no qual instalamos.

Obviamente, esta etapa pode ser ignorada se você instalar com monitor e teclado em vez de se conectar pela rede.

Observe que o Debian PROÍBE a conexão via ssh usando credenciais de superusuário (ou seja, root).

### Repositório
Agora vamos atualizar os repositórios.

Tornamo-nos superusuário com o comando `su` e digitando a senha de root.

Editamos o arquivo de repositórios com o comando `nano /etc/apt/sources.list` e removemos todas as linhas presentes.

Adicionamos as seguintes linhas.

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

Depois podemos salvar o arquivo pressionando `CTRL+x` e depois `y`.

O comando `apt update` nos permite verificar se tudo correu bem e atualizar a lista de pacotes.

### Atualizar o sistema
Para atualizar o sistema, basta executar os seguintes comandos:

- `apt update` para atualizar a lista de pacotes,
- `apt upgrade` para atualizar os pacotes instalados para os quais existe uma nova versão.

### Instalar tor e usá-lo com ssh
Para instalar tor, basta usar o comando `apt install tor`.

Depois de instalado, podemos configurá-lo com o seguinte comando `nano /etc/tor/torrc`.

No final do arquivo, adicionamos as seguintes linhas.

```
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 22 127.0.0.1:22
```

E reiniciamos o tor com `systemctl restart tor`; agora podemos encontrar nosso endereço onion com `cat /var/lib/tor/hidden_service/hostname`.

Usando tor, agora podemos nos conectar à nossa máquina de qualquer lugar do mundo com `torify ssh username@onionaddress.onion`.

## Programa
A instalação do Debian é uma aula repetitiva; aqui está uma lista das que já foram realizadas:

| Data        | Notas                                          |
|-------------|------------------------------------------------|
| 240415-2200 | Primeira aula                                  |
