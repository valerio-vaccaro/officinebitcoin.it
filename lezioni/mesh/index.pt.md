---
layout: default
title: "Introdução às **Mesh Networks** e análise detalhada de LoRa e **LoRaWAN**"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lição Bitcoin-only</span> <span>Este projeto é mantido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Introdução às **Mesh Networks** e análise detalhada de LoRa e **LoRaWAN**

## Introdução às **Mesh Networks**

As **Mesh Networks** são uma arquitetura de rede na qual os nós (dispositivos) são interconectados de maneira não hierárquica, permitindo que cada nó se comunique diretamente com outros sem passar por um ponto central, como um router ou gateway. Cada nó pode potencialmente atuar tanto como transmissor quanto como receptor, e os dados podem ser encaminhados por múltiplos caminhos para chegar ao destino.

Essa estrutura oferece várias vantagens:

- **Resiliência**: se um nó falhar, os dados podem ser redirecionados por outros nós, garantindo continuidade da comunicação.
- **Escalabilidade**: as **Mesh Networks** podem se expandir facilmente com a adição de novos nós, sem modificações significativas de infraestrutura.
- **Cobertura estendida**: o encaminhamento de dados permite cobrir áreas maiores em comparação com redes tradicionais.
- **Flexibilidade**: adequadas a múltiplas aplicações, de Internet of Things (IoT) a redes domésticas e industriais.

No entanto, as **Mesh Networks** também apresentam alguns desafios:

- **Complexidade**: gerenciar múltiplos caminhos e coordenar os nós aumenta a complexidade.
- **Consumo de energia**: nós que encaminham dados consomem mais energia, reduzindo a vida útil da bateria.
- **Capacidade limitada**: em redes densas, a transmissão multi-hop pode introduzir latência e reduzir a capacidade geral.

As **Mesh Networks** são usadas em tecnologias sem fio como **Zigbee**, **Bluetooth** Mesh, **Thread** e, em alguns casos, protocolos proprietários baseados em LoRa. Uma das tecnologias mais relevantes para redes de baixa potência e longo alcance é **LoRaWAN**, que adota uma abordagem diferente em comparação com a topologia mesh tradicional.

## **LoRa** e **LoRaWAN**: contexto e diferenças

### **LoRa**

**LoRa** (Long Range) é uma tecnologia de modulação de espectro espalhado derivada da técnica Chirp Spread Spectrum (CSS), desenvolvida pela Cycleo (adquirida pela Semtech em 2012).

**LoRa** representa a camada física (PHY) de uma rede sem fio, definindo como os dados são modulados e transmitidos em bandas de frequência não licenciadas (por exemplo, 868 MHz na Europa, 915 MHz na América do Norte, 433 MHz em algumas regiões).

Suas principais características são:
- Transmissão por longas distâncias (até 15 km em áreas rurais, 2-5 km em áreas urbanas).
- Consumo de energia extremamente baixo, ideal para aplicações IoT com baixas taxas de dados e longa vida útil de bateria.

### **LoRaWAN**

**LoRaWAN** (Long Range Wide Area Network) é um protocolo de camada MAC (Media Access Control) baseado em LoRa, desenvolvido pela LoRa Alliance, uma associação sem fins lucrativos fundada em 2015 com mais de 500 membros, incluindo Semtech, Cisco, IBM e Orange.

**LoRaWAN** define:
- Arquitetura de rede.
- Protocolo de comunicação.
- Aspectos como frequência de transmissão, taxa de dados, segurança e interoperabilidade.

Ao contrário de LoRa, que lida apenas com a modulação do sinal, **LoRaWAN** estabelece como os dispositivos (nós finais) se comunicam com gateways e como estes se conectam a servidores de rede por conexões de backhaul (por exemplo, Ethernet, Wi-Fi ou cellular).

#### Comparação entre **Mesh Networks** e **LoRaWAN**

Ao contrário das **Mesh Networks** tradicionais (por exemplo, **Zigbee**, **Bluetooth**), **LoRaWAN** usa uma topologia em estrela, na qual os nós finais se comunicam diretamente com gateways, que encaminham os dados para um servidor de rede central. Abaixo está uma comparação detalhada:

1. Topologia de rede
**Mesh Networks**: nós atuam como repetidores, encaminhando dados para ampliar a cobertura. Isso aumenta a complexidade e o consumo de energia.
**LoRaWAN**: topologia em estrela, com nós transmitindo diretamente para gateways. Isso elimina nós repetidores, simplificando a rede e reduzindo o consumo de energia.

2. Consumo de energia
**Mesh Networks**: nós repetidores consomem mais energia, reduzindo a vida útil da bateria.
**LoRaWAN**: dispositivos finais transmitem apenas quando necessário (por exemplo, Class A com ALOHA), permitindo vida útil de bateria de até 10-15 anos.

3. Alcance e cobertura
**Mesh Networks**: o alcance é estendido via multi-hop, mas cada salto pode introduzir latência e reduzir a eficiência.
**LoRaWAN**: graças à modulação CSS, oferece alcance de até 15 km (rural) ou 2-5 km (urbano) sem nós repetidores.

4. Capacidade e escalabilidade
**Mesh Networks**: em redes densas, multi-hop pode causar gargalos e reduzir a capacidade.
**LoRaWAN**: suporta milhões de mensagens de milhares de dispositivos, graças à redundância de gateways e à topologia em estrela.

5. Segurança
**Mesh Networks**: a segurança depende do protocolo (por exemplo, **Zigbee** usa AES-128). O encaminhamento multi-hop pode introduzir vulnerabilidades.
**LoRaWAN**: criptografia end-to-end com chaves de sessão AES-128 (Network Session Key e Application Session Key).

6. Complexidade e custos
**Mesh Networks**: gerenciar caminhos de encaminhamento aumenta a complexidade. Os custos podem crescer com a adição de nós repetidores.
**LoRaWAN**: a topologia em estrela é mais simples. Gateways podem ser caros, mas sensores são baratos e bandas ISM não licenciadas reduzem custos.

## Análise detalhada de **LoRa** e **LoRaWAN**
### **LoRa**: camada física
**LoRa** usa modulação Chirp Spread Spectrum (CSS), que codifica dados com sinais sinusoidais de frequência variável, distribuindo o sinal por uma largura de banda maior para melhorar a resistência a ruído. Oferece alta sensibilidade (-110 dBm a -140 dBm), ideal para ambientes ruidosos.

Os principais parâmetros incluem:

- Spreading Factor (SF): de 7 a 12, influencia taxa de dados e alcance. SF12 oferece longo alcance, mas baixo bitrate (0.3 kbps); SF7 oferece velocidades maiores (27 kbps), mas alcance reduzido.
- Bandwidth (BW): 125 kHz, 250 kHz ou 500 kHz, afeta bitrate e robustez.
- Frequências ISM: 863-870 MHz (Europa), 902-928 MHz (América do Norte), 433 MHz (outras regiões).

LoRa é ideal para aplicações IoT com pequenos pacotes de dados, como monitoramento ambiental, smart metering e agricultura de precisão.

## **LoRaWAN**: protocolo e arquitetura

**LoRaWAN** define três classes de dispositivos:

- Class A: dispositivos bidirecionais de baixa potência com transmissões uplink e janelas curtas de recepção downlink (ALOHA). Ideais para sensores alimentados por bateria.
- Class B: adiciona janelas de recepção programadas (a cada 128 segundos, sincronizadas via GPS beacon) para downlinks planejados.
- Class C: dispositivos sempre escutando downlinks, adequados para dispositivos alimentados pela rede elétrica.

A arquitetura **LoRaWAN** inclui:
- Nós finais (End Devices): sensores ou dispositivos IoT que coletam e transmitem dados.
- Gateways: recebem dados dos nós e os encaminham ao servidor de rede via backhaul.
- Network Server: gerencia a rede, elimina duplicatas e seleciona o gateway para downlinks.
- Application Server: processa dados para análise ou visualização.

## **Mesh Networks** com LoRa
Embora **LoRaWAN** use uma topologia em estrela, é possível implementar uma rede mesh usando modulação LoRa com um protocolo externo. Em uma rede mesh LoRa, os nós atuam como repetidores para ampliar a cobertura, o que é útil em áreas sem gateways.

No entanto, isso exige:
- Protocolo personalizado: **LoRaWAN** não suporta mesh nativamente.
- Maior consumo de energia: nós repetidores consomem mais energia.
- Complexidade: gerenciamento de caminhos de encaminhamento e prevenção de colisões (por exemplo, CSMA-CA).

Exemplo: módulos LoRa (por exemplo, SX1276 da Semtech) com microcontroladores como ESP32 para **Mesh Networks** privadas.

Vantagens de **LoRaWAN**

- Eficiência energética: a topologia em estrela elimina nós repetidores.
- Simplicidade: comunicação direta com gateways.
- Escalabilidade: suporta milhares de dispositivos e milhões de mensagens.
- Segurança: segurança robusta com criptografia AES-128.
- Interoperabilidade: padrão aberto da LoRa Alliance.

Limitações de **LoRaWAN**

- Baixa taxa de dados: 0.3-50 kbps, não adequada para dados volumosos.
- Latência: Class A introduz atrasos para downlinks.
- Custo de gateway: significativo para redes privadas.

# Conclusão
As **Mesh Networks** oferecem resiliência e flexibilidade por meio de encaminhamento multi-hop, mas são complexas e consomem mais energia. **LoRaWAN**, com sua topologia em estrela e modulação LoRa, é ideal para aplicações IoT de baixa potência e longo alcance, graças à simplicidade, escalabilidade e vida útil de bateria de até 15 anos.

A escolha entre **Mesh Networks** e **LoRaWAN** depende dos requisitos: mesh para ambientes com nós próximos entre si, **LoRaWAN** para comunicações de longa distância com consumo mínimo. Embora seja possível com LoRa, mesh é menos comum em comparação com **LoRaWAN**, que domina graças à sua padronização e ao apoio da LoRa Alliance.
