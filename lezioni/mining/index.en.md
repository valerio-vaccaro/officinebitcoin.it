# Introduction to Mining
Bitcoin mining is a fundamental process of the protocol that serves to propose an order among the transactions present in the mempool, selecting a subset to create a new block and update the blockchain state.

Mining is designed to be decentralized and random (in quotes, since it's based on a cryptographic puzzle), thus avoiding centralized transaction management.

## Purpose of Mining
Mining solves problems related to centralization, such as:

- Censorship: a central entity could block some transactions, but with decentralized miners, transactions have more chances of being included.
- Double spending: without a corruptible miner, it's difficult to rewrite history or favor one transaction at the expense of another.
- Timestamping: provides a secure and shared temporal order, not dependent on a central authority, but on consensus between miners and nodes.

# How Mining Works
The mining process can be explained step by step:

- Transaction selection: the miner chooses transactions from the mempool, often privileging those with higher fees, optimizing profit (an NP-complete problem similar to the "knapsack problem").
- Coinbase construction: the miner creates a special transaction (coinbase) that assigns to itself the block reward (currently 3.125 BTC, halved every four years) plus the fees of the selected transactions.
- Merkle Root: the chosen transactions are organized in a tree data structure (Merkle Tree), which generates a Merkle Root, a hash that represents all transactions and their order.
- Block Header: the miner builds the block header prototype, including:
1. The timestamp.
2. The hash of the previous block.
3. The Merkle Root.
4. The difficulty (target), which depends on the network.
5. A nonce (random number initialized, for example, to zero).
- Cryptographic Puzzle: The miner applies the SHA-256 algorithm twice to the header and verifies if the result has a sufficient number of leading zeros (below the difficulty threshold). If not, it modifies the nonce or other fields (e.g., timestamp or transaction order) and repeats the calculation. This is brute force work without shortcuts, thanks to SHA-256's properties.

## Optimizations
To speed up the process, miners can calculate the first SHA-256 on the first 64 bytes of the header (immutable) and then iterate only on the rest, changing the nonce. Specialization has led to hardware (ASIC) that performs billions of attempts per second.

# Validation Process
When a miner finds a solution, it transmits the complete block (header + transactions) to the network. Nodes validate:
- the header hash (a single SHA-256 to confirm).
- the correctness of the block information (timestamp, previous block hash, Merkle Root, and nonce).
- the reproducibility of the Merkle Root after checking the correctness of all associated transactions.

If valid, the block is added to the blockchain. The reward (coinbase + fees) is spendable only after 100 confirmations (about 16 hours), to ensure stability.

# Mining Costs and Rewards
Costs:

- Electricity: main variable cost.
- Hardware: expensive and short-lived ASICs, quickly surpassed by more efficient models.
- Infrastructure: cooling, installation, maintenance (e.g., solar panels are not "free").

Rewards:

- Fixed reward (halved in 2024 to 3.125 BTC).
- Variable transaction fees.

The miner must respect consensus rules: an invalid block is discarded, wasting resources without reward. Even a valid block can be "orphaned" if another miner wins the race, causing losses.

## Economic Strategy
Mining is competitive: miners seek to maximize uptime to amortize fixed costs. Spot uses (e.g., turning on miners only with excess energy) are impractical, as initial costs require continuity. Return on investment can be long and uncertain.

# Solo and Pool Mining

- Solo Mining: the miner works alone, building the block with a full node or custom software. If it finds a block, it takes the entire reward, but the probability is extremely low (it could take centuries with a single ASIC).
- Pool Mining: protocols like Stratum allow miners to collaborate:
1. The pool provides a template (coinbase, Merkle Root, etc.).
2. Miners send shares (attempts with a certain number of zeros, below block difficulty) as proof of work.
3. When a pool miner finds a block, the reward is divided proportionally to the shares sent.
- Stratum v2: Evolution that allows miners to choose transactions, reducing pool centralization, although it requires checks to ensure correctness (e.g., fees for the pool).

# Hashrate Estimation
Hashrate (computing power) is estimated:
- In a Pool: By counting shares received in a unit of time, multiplied by share difficulty. It's an estimate perturbable by luck.
- Global: Using Bitcoin's difficulty and average time between blocks (about 10 minutes). Oscillations are normal, but the average is reliable.

Hardware like Nerd Miner uses internal counters for precise data, while pools rely on more variable estimates, visible in oscillating graphs.

# Program
This lesson was created for a Satoshi Spritz Connect. 