---
layout: default
title: "Ghostinbox.it: usar email sem ter uma conta email"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lição Bitcoin-only</span> <span>Este projeto é mantido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Ghostinbox.it: usar email sem ter uma conta email

Ghostinbox é uma plataforma web que permite aos usuários criar endereços de email temporários para receber mensagens sem revelar seu endereço de email real. O serviço é ideal para registros rápidos, verificações de conta, testes de entregabilidade de email ou qualquer situação em que você queira evitar spam ou proteger sua identidade.

Ao contrário dos serviços de email tradicionais, Ghostinbox não exige registro nem armazena dados pessoais, tornando-se uma excelente opção para quem prioriza a privacidade. Além disso, o suporte à rede Tor permite acesso anônimo ao serviço, ocultando o endereço IP do usuário. A natureza open-source do projeto garante transparência e permite que desenvolvedores examinem o código em busca de possíveis vulnerabilidades ou personalizações.

## Como o Ghostinbox funciona?
![alt text](https://officinebitcoin.it/lezioni/ghostin/front.png)

Usar o Ghostinbox é extremamente intuitivo e não exige conhecimentos técnicos:

1. **Acesse o site**: Visite https://ghostinbox.it/ (ou acesse via Tor para maior anonimato).
2. **Gere um endereço de email temporário**: Clique no botão para criar um novo endereço de email temporário (por exemplo, random@ghostinbox.it). O endereço fica ativo imediatamente e pronto para uso.
3. **Receba mensagens**: Use o endereço gerado para receber emails, por exemplo para registros em serviços online, verificações de conta ou testes. As mensagens aparecem em tempo real na caixa de entrada do site.
4. **Monitore as mensagens**: Acesse a caixa de entrada temporária diretamente no Ghostinbox para ver as mensagens recebidas. Nenhum cliente de email externo é necessário.

![alt text](https://officinebitcoin.it/lezioni/ghostin/email.png)

O serviço foi projetado para ser rápido e sem atritos: não é preciso criar conta, e a interface minimalista torna a experiência fluida até para usuários sem perfil técnico. A possibilidade de acesso via Tor acrescenta um nível adicional de proteção para quem deseja manter anonimato completo.

## Do alias ao email
Para usar o serviço, é necessário escolher um alias que seja longo e aleatório o suficiente para não poder ser adivinhado por outros usuários. Esse alias será como uma senha para acessar o email e, portanto, não deve ser esquecido.

A partir desse alias, é derivado um endereço de email HASH@ghostinbox.it, em que HASH equivale a `sha256(alias)`, ou seja, o hash do alias usando SHA-256; então o usuário pode usar esse email (mostrado no esquema de recebimento) para receber emails. A página de recebimento é atualizada automaticamente mostrando os emails recebidos. Um usuário pode criar um endereço de email sem acessar o serviço e usar o site apenas para consulta.

Ao clicar no email, você pode ler seu texto e, se necessário, copiar links para abrir; o formato do email é deliberadamente apenas texto e, portanto, não mostrará nenhum dos recursos gráficos dos emails baseados em HTML.

## Quem precisa do Ghostinbox?
Ghostinbox atende a várias necessidades relacionadas à privacidade e ao gerenciamento de emails temporários:

1. **Proteção contra spam**: Usando um endereço temporário, os usuários podem evitar que seu endereço de email real seja inundado por spam ou newsletters indesejadas.
2. **Registros seguros**: Perfeito para se cadastrar em serviços online, fóruns ou plataformas que exigem verificação por email sem comprometer o email pessoal.
3. **Testes de entregabilidade**: Desenvolvedores e profissionais de marketing podem usar o Ghostinbox para testar envio e recebimento de emails sem envolver endereços reais.
4. **Privacidade avançada**: Graças ao suporte ao Tor, o serviço é ideal para usuários que desejam manter anonimato ao interagir com sites ou serviços online.
5. **Uso temporário**: Adequado para situações em que é necessário um endereço de email descartável, como promoções, testes gratuitos ou comunicações de curto prazo.

![alt text](https://officinebitcoin.it/lezioni/ghostin/stats.png)

## Características técnicas
O repositório GitHub do Ghostinbox (https://github.com/valerio-vaccaro/ghostinbox.it) revela uma implementação leve, escrita principalmente em Python com o framework Flask, com as seguintes características:

- **Abordagem serverless**: não há servidor de email; em vez disso, é aproveitado um serviço gratuito de email e encaminhamento de email, tornando a arquitetura do serviço extremamente simples e econômica.
- **Arquitetura**: Ghostinbox usa uma arquitetura cliente-servidor baseada em Flask para gerenciar a geração de endereços de email temporários e a exibição de mensagens. A simplicidade do design garante alto desempenho mesmo com grandes volumes de requisições.
- **Geração de endereços**: Os endereços de email temporários são gerados dinamicamente com base no alias informado.
- **Suporte Tor**: O serviço é configurado para ser acessível via onion routing, garantindo que o endereço IP do usuário não seja rastreado durante a interação com o site.
- **Gerenciamento de mensagens**: As mensagens recebidas são apagadas após 30 dias.
- **Segurança**: Nenhum dado pessoal ou mensagem é armazenado permanentemente. O desenho do serviço minimiza riscos de violação, e a ausência de registro elimina a necessidade de fornecer informações sensíveis.
- **Open-source**: O código público permite que desenvolvedores verifiquem a integridade do sistema, contribuam com melhorias ou hospedem uma instância personalizada.

Pontos fortes técnicos:
- **Privacidade absoluta**: A exclusão dos emails após 30 dias e o suporte ao Tor garantem uma experiência anônima e segura.
- **Leveza**: A implementação em Flask é otimizada para poucos recursos, tornando o serviço escalável e rápido.
- **Transparência**: A licença open-source permite auditoria do código e personalizações, aumentando a confiança dos usuários.

## Conclusão
Ghostinbox é uma solução elegante e funcional para quem procura um serviço de email temporário rápido, seguro e orientado à privacidade. Com sua interface intuitiva, suporte ao Tor e transparência do código open-source, ele atende tanto usuários comuns que desejam proteger sua caixa de entrada contra spam quanto desenvolvedores que precisam de um sistema confiável para testes ou registros temporários. Para experimentar o Ghostinbox, visite https://ghostinbox.it/. Para explorar o código ou contribuir com o projeto, consulte o repositório em https://github.com/valerio-vaccaro/ghostinbox.it.

