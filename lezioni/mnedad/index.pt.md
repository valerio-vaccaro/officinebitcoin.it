---
layout: default
title: "Mnemonics & Dice: aprenda a criar a sua mnemônica"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lição Bitcoin-only</span> <span>Este projeto é mantido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Mnemonics & Dice: aprenda a criar a sua mnemônica

## Introdução
Criar a mnemônica usando a sua própria fonte de entropia reduz a superfície de ataque de uma carteira Bitcoin; no entanto, alguns fatores devem ser levados em conta:

- o processo deve ser o mais simples e rápido possível, sem enfeites nem repetições desnecessárias,
- a entropia não deve ser copiada para dispositivos desnecessários e a necessidade de realizar cálculos ou processamento deve ser mantida ao mínimo,
- o uso de software/scripts/programas deve ser evitado, a menos que você tenha feito uma revisão cuidadosa do código e de todas as dependências,
- configurações diferentes podem exigir processos ligeiramente diferentes.

## Criação das palavras
O primeiro passo é calcular as 12 ou 24 palavras da mnemônica; 12 palavras normalmente são mais do que suficientes para a segurança de uma carteira Bitcoin.

Para a geração das palavras, você pode usar o método descrito em [TRGM](https://github.com/valerio-vaccaro/TRMG), usando 3 dados: 1 com 8 faces e 2 com 16 faces. CADA lançamento dos dados corresponde a UMA E SOMENTE UMA palavra; para encontrá-la, basta percorrer a tabela do site procurando a correspondência dos dados com o lançamento realizado (o primeiro dado é SEMPRE o de 8 faces). A coluna da palavra contém a palavra que você está procurando.

A recomendação é gerar todas as 12 ou 24 palavras e, se necessário, corrigir a última ou, de qualquer forma, usar os dados para gerar a entropia relativa à última palavra.

## Cálculo do checksum
A última palavra não é completamente decidida por nós, mas contém uma parte de controle; ou seja, não podemos escolher integralmente todos os 11 bits de entropia que a compõem. Em vez disso, podemos escolher os primeiros 7 no caso de uma mnemônica de 12 palavras ou os primeiros 3 no caso de uma mnemônica de 24 palavras.

Digamos que a nossa última palavra seja BACON, correspondente aos lançamentos 1, 9 e 11 (lembre-se de que o primeiro dado é SEMPRE o de 8 faces). A tabela também mostra Group 12 e Group 24, que nos permitem agrupar as palavras considerando apenas a entropia dos dois primeiros lançamentos (group 12) ou apenas o primeiro lançamento (group 24).

Vamos supor que queremos criar uma mnemônica de 12 palavras; isso significa que o checksum será uma palavra entre as 16 possíveis que têm o mesmo group 12 de bacon, isto é, 0001000. As palavras possíveis são:

|First|Second|Third|Index|Word	|Index in binary|Group 12	|Group 24|
|---|---|---|-------|-----------|---------------|-----------|---|
|1  |9	|1	|128	|avoid	    |00010000000	|0001000	|000|
|1  |9	|2	|129	|awake	    |00010000001	|0001000	|000|
|1  |9	|3	|130	|aware	    |00010000010	|0001000	|000|
|1  |9	|4	|131	|away	    |00010000011	|0001000	|000|
|1  |9	|5	|132	|awesome	|00010000100	|0001000	|000|
|1  |9	|6	|133	|awful	    |00010000101	|0001000	|000|
|1  |9	|7	|134	|awkward	|00010000110	|0001000	|000|
|1  |9	|8	|135	|axis	    |00010000111	|0001000	|000|
|1  |9	|9	|136	|baby	    |00010001000	|0001000	|000|
|1  |9	|10	|137	|bachelor	|00010001001	|0001000	|000|
|1  |9	|11	|138	|bacon	    |00010001010	|0001000	|000|
|1  |9	|12	|139	|badge	    |00010001011	|0001000	|000|
|1  |9	|13	|140	|bag    	|00010001100	|0001000	|000|
|1  |9	|14	|141	|balance	|00010001101	|0001000	|000|
|1  |9	|15	|142	|balcony	|00010001110	|0001000	|000|
|1  |9	|16	|143	|ball   	|00010001111	|0001000	|000|

Como encontrar a única palavra correta entre as várias opções? Isso depende da sua configuração; vejamos alguns exemplos:

- bruteforce, ou seja, tentar todas elas em sequência até encontrar a correta (muito trabalhoso com mnemônicas de 24 palavras); este é o método a usar com Ledger ou com Electrum (certificando-se de selecionar a opção BIP39),
- calcular todas as palavras possíveis com as primeiras 11 ou 23 palavras e procurar a única que pertence a esse conjunto; este método pode ser usado com Jade e com outros hardware wallets capazes de calcular todas as possíveis palavras finais de uma mnemônica,
- inserir a mnemônica completa e deixar que o hardware wallet a corrija para nós, como o Specter-DIY faz de forma muito elegante, por exemplo.

## Backup (tema de outra aula)
É fundamental ter uma boa política de backup, portanto:
- vários backups,
- em vários suportes e
- possivelmente criptografados ou divididos (mas é preciso saber fazer isso bem).

## Bibliografia

- [TRMG](https://github.com/valerio-vaccaro/TRMG)

## Repetições
Esta aula é repetitiva e será repetida todos os meses. Abaixo está uma lista das repetições já realizadas.

| Date        | Notes                                          |
|-------------|------------------------------------------------|
| 240102-2100 | First lesson                                   |
