---
layout: default
title: "Introduction au minage"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Leçon Bitcoin-only</span> <span>Ce projet est maintenu par valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Introduction au minage
Le minage de Bitcoin est un processus fondamental du protocole qui sert à proposer un ordre parmi les transactions présentes dans la mempool, en sélectionnant un sous-ensemble pour créer un nouveau bloc et mettre à jour l'état de la blockchain.

Le minage est conçu pour être décentralisé et aléatoire (entre guillemets, puisqu'il repose sur une énigme cryptographique), évitant ainsi une gestion centralisée des transactions.

## Objectif du minage
Le minage résout des problèmes liés à la centralisation, tels que:

- Censure: une entité centrale pourrait bloquer certaines transactions, mais avec des mineurs décentralisés, les transactions ont davantage de chances d'être incluses.
- Double dépense: sans mineur corruptible, il est difficile de réécrire l'histoire ou de favoriser une transaction au détriment d'une autre.
- Timestamping: fournit un ordre temporel sûr et partagé, qui ne dépend pas d'une autorité centrale, mais du consensus entre mineurs et nœuds.

# Fonctionnement du minage
Le processus de minage peut être expliqué étape par étape:

- Sélection des transactions: le mineur choisit des transactions dans la mempool, en privilégiant souvent celles dont les frais sont plus élevés, afin d'optimiser le profit (un problème NP-complete similaire au "knapsack problem").
- Construction de la coinbase: le mineur crée une transaction spéciale (coinbase) qui s'attribue la récompense du bloc (actuellement 3.125 BTC, divisée par deux tous les quatre ans) plus les frais des transactions sélectionnées.
- Merkle Root: les transactions choisies sont organisées dans une structure de données en arbre (Merkle Tree), qui génère une Merkle Root, un hash représentant toutes les transactions et leur ordre.
- Block Header: le mineur construit le prototype de l'en-tête du bloc, comprenant:
1. Le timestamp.
2. Le hash du bloc précédent.
3. La Merkle Root.
4. La difficulté (target), qui dépend du réseau.
5. Un nonce (nombre aléatoire initialisé, par exemple, à zéro).
- Énigme cryptographique: le mineur applique deux fois l'algorithme SHA-256 à l'en-tête et vérifie si le résultat possède un nombre suffisant de zéros initiaux (inférieur au seuil de difficulté). Sinon, il modifie le nonce ou d'autres champs (par exemple, le timestamp ou l'ordre des transactions) et répète le calcul. C'est un travail de force brute sans raccourci, grâce aux propriétés de SHA-256.

## Optimisations
Pour accélérer le processus, les mineurs peuvent calculer le premier SHA-256 sur les 64 premiers octets de l'en-tête (immuables), puis itérer seulement sur le reste en changeant le nonce. La spécialisation a conduit à du hardware (ASIC) capable d'effectuer des milliards de tentatives par seconde.

# Processus de validation
Lorsqu'un mineur trouve une solution, il transmet le bloc complet (en-tête + transactions) au réseau. Les nœuds valident:
- le hash de l'en-tête (un seul SHA-256 pour confirmer).
- l'exactitude des informations du bloc (timestamp, hash du bloc précédent, Merkle Root et nonce).
- la reproductibilité de la Merkle Root après vérification de l'exactitude de toutes les transactions associées.

S'il est valide, le bloc est ajouté à la blockchain. La récompense (coinbase + frais) ne peut être dépensée qu'après 100 confirmations (environ 16 heures), afin de garantir la stabilité.

# Coûts et récompenses du minage
Coûts:

- Électricité: principal coût variable.
- Hardware: ASIC coûteux et de courte durée, rapidement dépassés par des modèles plus efficaces.
- Infrastructure: refroidissement, installation, maintenance (par exemple, les panneaux solaires ne sont pas "gratuits").

Récompenses:

- Récompense fixe (réduite de moitié en 2024 à 3.125 BTC).
- Frais de transaction variables.

Le mineur doit respecter les règles de consensus: un bloc invalide est rejeté, gaspillant des ressources sans récompense. Même un bloc valide peut devenir "orphelin" si un autre mineur gagne la course, entraînant des pertes.

## Stratégie économique
Le minage est concurrentiel: les mineurs cherchent à maximiser leur disponibilité afin d'amortir les coûts fixes. Les usages ponctuels (par exemple, allumer les mineurs uniquement avec de l'énergie excédentaire) sont peu pratiques, car les coûts initiaux exigent de la continuité. Le retour sur investissement peut être long et incertain.

# Minage en solo et en pool

- Solo Mining: le mineur travaille seul, en construisant le bloc avec un nœud complet ou un logiciel personnalisé. S'il trouve un bloc, il reçoit toute la récompense, mais la probabilité est extrêmement faible (cela pourrait prendre des siècles avec un seul ASIC).
- Pool Mining: des protocoles comme Stratum permettent aux mineurs de collaborer:
1. Le pool fournit un modèle (coinbase, Merkle Root, etc.).
2. Les mineurs envoient des shares (tentatives avec un certain nombre de zéros, sous la difficulté du bloc) comme preuve de travail.
3. Lorsqu'un mineur du pool trouve un bloc, la récompense est répartie proportionnellement aux shares envoyées.
- Stratum v2: évolution qui permet aux mineurs de choisir les transactions, réduisant la centralisation du pool, bien qu'elle exige des vérifications pour garantir la correction (par exemple, les frais pour le pool).

# Estimation du hashrate
Le hashrate (puissance de calcul) est estimé:
- Dans un pool: en comptant les shares reçues dans une unité de temps, multipliées par la difficulté de share. C'est une estimation qui peut être perturbée par la chance.
- Global: en utilisant la difficulté de Bitcoin et le temps moyen entre les blocs (environ 10 minutes). Les oscillations sont normales, mais la moyenne est fiable.

Du hardware comme Nerd Miner utilise des compteurs internes pour obtenir des données précises, tandis que les pools s'appuient sur des estimations plus variables, visibles dans des graphiques oscillants.

# Programme
Cette leçon a été créée pour un Satoshi Spritz Connect.
