---
layout: default
title: "O ciclo de vida de uma transação Bitcoin"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lição Bitcoin-only</span> <span>Este projeto é mantido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# O ciclo de vida de uma transação Bitcoin

## O que é uma transação Bitcoin
Uma transação Bitcoin é uma ação registrada na blockchain que transfere valor de uma ou mais entradas (fundos recebidos anteriormente, chamados UTXOs - Unspent Transaction Outputs) para uma ou mais saídas (novos destinatários).
As entradas são saídas de transações passadas que ainda não foram gastas, enquanto as saídas atribuem satoshis a endereços específicos. Uma exceção é a transação "coinbase", a primeira de cada bloco, que gera novos bitcoins (recompensa de mineração e taxas) sem entradas. Se nem todos os fundos de uma entrada forem gastos, a diferença (change) volta ao remetente por meio de uma saída adicional ou, se não for gerenciada, é perdida para sempre.

## Fases do ciclo de vida
Este é o ciclo de vida da transação:

- Criação: O wallet constrói a transação escolhendo quais UTXOs gastar com base no valor a enviar e na estratégia para minimizar taxas. Se a entrada exceder a saída, é gerada uma saída de "change" que volta ao remetente, mas isso aumenta o tamanho e o custo da transação. Alguns wallets tentam evitar isso.
- Assinatura: A transação é assinada com uma ou mais assinaturas digitais para cada entrada, autenticando-a. Esta etapa é crucial para a validade e pode envolver várias partes no caso de transações multisig.
- Transmissão: A transação assinada é transmitida para a rede ("broadcast") e inserida no mempool do nó local. O mempool valida a transação de acordo com as regras de consenso (por exemplo, assinaturas válidas, fundos disponíveis) e regras locais (por exemplo, tamanho máximo de 400 KB para evitar spam). Em seguida, o nó a propaga para seus pares, que a validam e a inserem em seus mempools, criando uma transmissão em cascata. Os mempools variam entre nós por causa de configurações ou conexões diferentes.
- Confirmação: Um minerador inclui a transação em um bloco, confirmando-a na blockchain. No entanto, até que ela tenha mais confirmações (blocos subsequentes), continua vulnerável a substituições ou forks. Uma transação com taxas baixas pode permanecer no mempool por muito tempo ou ser descartada, mas ainda poderia ser minerada depois de meses se as entradas continuarem não gastas.

## Gestão de problemas
- Transação desaparecida do mempool: Se uma transação com taxas baixas for removida (por exemplo, devido a picos de tráfego), ela pode ser retransmitida manualmente (rebroadcast) usando o TXID, até mesmo com scripts ou exploradores. Alguém pode fazer isso em nome de terceiros.
- Replace-by-Fee (RBF): Se a taxa for insuficiente, a transação pode ser substituída por outra que pague mais, desde que esteja marcada com a flag RBF. Uma proposta sugere que todas as transações deveriam ser implicitamente substituíveis, já que mineradores preferem taxas mais altas de qualquer forma.
- Child Pays for Parent (CPFP): Se RBF não puder ser usado (por exemplo, por não ser sua própria transação ou por fundos esgotados), uma saída da transação presa é gasta com uma nova transação que paga taxas altas, tornando ambas atraentes para os mineradores. A soma das taxas deve cobrir as duas. Surgem problemas se os nós descartarem a primeira transação, quebrando a cadeia; um protocolo em desenvolvimento busca transmitir pacotes de transações para evitar isso.

## Confirmação final
Uma transação é considerada final somente com múltiplas confirmações (blocos acima dela). Uma única confirmação não é suficiente, pois forks ou gasto duplo poderiam invalidá-la. O White Paper sugere 6 confirmações (cerca de 60 minutos, com blocos a cada 10 minutos em média), mas o número varia conforme o valor e o risco. A variação nos tempos de bloco é alta, mas a média é mantida graças à dificuldade de mineração.

## Conclusão
O ciclo se encerra com a transação "gravada" na blockchain, registrando permanentemente a transferência de valor.

## Programa
Esta aula foi criada para um Satoshi Spritz Connect.
