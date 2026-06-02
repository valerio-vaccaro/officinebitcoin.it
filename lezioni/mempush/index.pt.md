---
layout: default
title: "MemPush: envie e gerencie transações Bitcoin na mempool com simplicidade"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lição Bitcoin-only</span> <span>Este projeto é mantido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# MemPush: envie e gerencie transações Bitcoin na mempool com simplicidade

MemPush (https://mempush.com/) é uma plataforma inovadora que torna simples, seguro e acessível enviar e gerenciar transações Bitcoin na mempool. A mempool, o "reservatório" temporário de transações Bitcoin aguardando confirmação na blockchain, é o coração deste serviço, que elimina complexidades técnicas para usuários e desenvolvedores.

## O que é MemPush?

MemPush é um serviço web que permite enviar raw Bitcoin transactions (em formato hexadecimal) diretamente para a mempool, sem a necessidade de configurações avançadas ou Bitcoin nodes pessoais. Criado por Valerio Vaccaro, o MemPush também oferece suporte à rede Tor para garantir maior privacidade aos usuários.

![alt text](https://officinebitcoin.it/lezioni/mempush/front.png)

O código-fonte, disponível no GitHub (https://github.com/valerio-vaccaro/mempush) sob uma licença open-source, permite que qualquer pessoa verifique a segurança do projeto, contribua para seu desenvolvimento ou hospede uma instância personalizada do serviço.

## Como o MemPush funciona?

A interface do MemPush é intuitiva e fácil de usar:

1. **Acesse o site**: visite https://mempush.com/.
2. **Insira a raw transaction**: cole a transação Bitcoin em formato hexadecimal no campo dedicado.
3. **Envie a transação**: clique em "Submit Raw Transaction" para propagar a transação para a mempool por meio de Bitcoin nodes.
4. **Monitore o status**: acompanhe o progresso da transação com um blockchain explorer.
5. **Retransmissão automática**: o MemPush retransmite automaticamente as transações, se necessário, para garantir sua permanência na mempool.

![alt text](https://officinebitcoin.it/lezioni/mempush/list.png)

Não é necessário registro, e a abordagem open-source elimina riscos ocultos, tornando o MemPush ideal até mesmo para usuários menos experientes.

## Para quem é o MemPush?

O MemPush foi criado para atender a várias necessidades:
1. **Taxas baixas**: transações com taxas baixas são retransmitidas automaticamente para impedir que sejam removidas da mempool durante picos de tráfego.
2. **Transações timelocked**: oferece suporte ao monitoramento e à retransmissão de transações com restrições de tempo, garantindo seu gerenciamento efetivo.
3. **Monitoramento avançado**: o MemPush verifica periodicamente o status das transações, permitindo a remoção apenas de transações confirmadas ou invalidadas (por exemplo, double-spends).
4. **Privacidade aprimorada**: graças ao suporte à rede Tor, o MemPush protege o anonimato do usuário ao enviar transações.

## Características técnicas

O repositório no GitHub (https://github.com/valerio-vaccaro/mempush) mostra uma implementação elegante em Python, baseada no framework Flask e integrada a um banco de dados para o gerenciamento de transações. O MemPush utiliza serviços como blockstream.info e mempool.space para monitorar e propagar transações, com planos futuros para integrar um Bitcoin node local.

Principais pontos fortes:
- **Segurança**: nenhum dado sensível ou chave privada é armazenado, garantindo proteção total.
- **Escalabilidade**: oferece suporte a alto volume de transações graças à conexão direta com a rede Bitcoin.
- **Open-source**: o código público permite verificação, contribuições e personalizações pela comunidade.

## Conclusão

MemPush é uma solução poderosa e acessível para qualquer pessoa que queira enviar e gerenciar transações Bitcoin na mempool sem complicações. Com sua transparência, suporte à privacidade e facilidade de uso, ele representa uma contribuição valiosa para o ecossistema Bitcoin. Visite https://mempush.com/ para experimentá-lo ou explore o código em https://github.com/valerio-vaccaro/mempush.
