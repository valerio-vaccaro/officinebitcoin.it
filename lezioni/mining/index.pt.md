---
layout: default
title: "Introdução à mineração"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lição Bitcoin-only</span> <span>Este projeto é mantido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Introdução à mineração
A mineração de Bitcoin é um processo fundamental do protocolo que serve para propor uma ordem entre as transações presentes na mempool, selecionando um subconjunto para criar um novo bloco e atualizar o estado da blockchain.

A mineração foi projetada para ser descentralizada e aleatória (entre aspas, já que se baseia em um quebra-cabeça criptográfico), evitando assim a gestão centralizada das transações.

## Finalidade da mineração
A mineração resolve problemas relacionados à centralização, como:

- Censura: uma entidade central poderia bloquear algumas transações, mas, com mineradores descentralizados, as transações têm mais chances de serem incluídas.
- Gasto duplo: sem um minerador corruptível, é difícil reescrever a história ou favorecer uma transação em detrimento de outra.
- Timestamping: fornece uma ordem temporal segura e compartilhada, não dependente de uma autoridade central, mas do consenso entre mineradores e nós.

# Como a mineração funciona
O processo de mineração pode ser explicado passo a passo:

- Seleção de transações: o minerador escolhe transações da mempool, frequentemente privilegiando aquelas com taxas mais altas, otimizando o lucro (um problema NP-complete semelhante ao "knapsack problem").
- Construção da coinbase: o minerador cria uma transação especial (coinbase) que atribui a si mesmo a recompensa do bloco (atualmente 3.125 BTC, reduzida pela metade a cada quatro anos) mais as taxas das transações selecionadas.
- Merkle Root: as transações escolhidas são organizadas em uma estrutura de dados em árvore (Merkle Tree), que gera uma Merkle Root, um hash que representa todas as transações e sua ordem.
- Block Header: o minerador constrói o protótipo do cabeçalho do bloco, incluindo:
1. O timestamp.
2. O hash do bloco anterior.
3. A Merkle Root.
4. A dificuldade (target), que depende da rede.
5. Um nonce (número aleatório inicializado, por exemplo, em zero).
- Quebra-cabeça criptográfico: o minerador aplica o algoritmo SHA-256 duas vezes ao cabeçalho e verifica se o resultado tem um número suficiente de zeros iniciais (abaixo do limiar de dificuldade). Caso contrário, modifica o nonce ou outros campos (por exemplo, timestamp ou ordem das transações) e repete o cálculo. É trabalho de força bruta sem atalhos, graças às propriedades do SHA-256.

## Otimizações
Para acelerar o processo, os mineradores podem calcular o primeiro SHA-256 sobre os primeiros 64 bytes do cabeçalho (imutáveis) e depois iterar apenas sobre o restante, alterando o nonce. A especialização levou a hardware (ASIC) que realiza bilhões de tentativas por segundo.

# Processo de validação
Quando um minerador encontra uma solução, transmite o bloco completo (cabeçalho + transações) para a rede. Os nós validam:
- o hash do cabeçalho (um único SHA-256 para confirmar).
- a correção das informações do bloco (timestamp, hash do bloco anterior, Merkle Root e nonce).
- a reprodutibilidade da Merkle Root após verificar a correção de todas as transações associadas.

Se for válido, o bloco é adicionado à blockchain. A recompensa (coinbase + taxas) só pode ser gasta após 100 confirmações (cerca de 16 horas), para garantir estabilidade.

# Custos e recompensas da mineração
Custos:

- Eletricidade: principal custo variável.
- Hardware: ASICs caros e de vida curta, rapidamente superados por modelos mais eficientes.
- Infraestrutura: resfriamento, instalação, manutenção (por exemplo, painéis solares não são "gratuitos").

Recompensas:

- Recompensa fixa (reduzida pela metade em 2024 para 3.125 BTC).
- Taxas de transação variáveis.

O minerador deve respeitar as regras de consenso: um bloco inválido é descartado, desperdiçando recursos sem recompensa. Mesmo um bloco válido pode ficar "órfão" se outro minerador vencer a corrida, causando perdas.

## Estratégia econômica
A mineração é competitiva: os mineradores buscam maximizar o tempo de atividade para amortizar os custos fixos. Usos pontuais (por exemplo, ligar mineradores apenas com energia excedente) são pouco práticos, pois os custos iniciais exigem continuidade. O retorno sobre o investimento pode ser longo e incerto.

# Mineração solo e em pool

- Solo Mining: o minerador trabalha sozinho, construindo o bloco com um nó completo ou software personalizado. Se encontrar um bloco, recebe toda a recompensa, mas a probabilidade é extremamente baixa (poderia levar séculos com um único ASIC).
- Pool Mining: protocolos como Stratum permitem que mineradores colaborem:
1. O pool fornece um modelo (coinbase, Merkle Root, etc.).
2. Os mineradores enviam shares (tentativas com certo número de zeros, abaixo da dificuldade do bloco) como prova de trabalho.
3. Quando um minerador do pool encontra um bloco, a recompensa é dividida proporcionalmente às shares enviadas.
- Stratum v2: evolução que permite aos mineradores escolher transações, reduzindo a centralização do pool, embora exija verificações para garantir a correção (por exemplo, taxas para o pool).

# Estimativa do hashrate
O hashrate (poder computacional) é estimado:
- Em um pool: contando as shares recebidas em uma unidade de tempo, multiplicadas pela dificuldade da share. É uma estimativa que pode ser perturbada pela sorte.
- Global: usando a dificuldade do Bitcoin e o tempo médio entre blocos (cerca de 10 minutos). Oscilações são normais, mas a média é confiável.

Hardware como Nerd Miner usa contadores internos para dados precisos, enquanto pools dependem de estimativas mais variáveis, visíveis em gráficos oscilantes.

# Programa
Esta aula foi criada para um Satoshi Spritz Connect.
