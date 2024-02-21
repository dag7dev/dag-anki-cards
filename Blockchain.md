---
date_created: 2024-01-22
date_modified: 2024-01-29
---
TARGET DECK: Blockchain
START
Basic
What a blockchain is?
Back: 
- open **ledger** that can record **transactions** between two parties efficiently
	- **transactions**: blocks
- a copy of blockchain is distributed to **every node**
- **consensus** is achieved through dedicated algorithms
- executing user-defined scripts (**smart contacts**)

> THE BLOCKCHAIN IS NOT A DATABASE: it is a TRANSACTION LIST

Tags: btc definitions
<!--ID: 1706231523626-->
END

---
START
Basic
What's the difference between a database and the blockchain?
Back: 
Databases are used to store data, blockchain are used to **store transactions**

Tags: btc database
<!--ID: 1706231523630-->
END

---

START
Basic
What is a transaction?
Back: 
**Transfer of assets** from account A to B.
Transactions are sequentially stored, **the order matters!**
Tags: btc definitions
<!--ID: 1706231523634-->
END

---

START
Basic
What an account is?
Back: 
An account is a b58 encoding of pk hash with checksum and version (sequence of numbers and letters), we don't care about people or characteristics!

To make sure to verify the person, we could use some methods: the account **signature**: proof that someone is authorized to do operations, and they have a **special private key** they only have that identify himself.


Tags: btc definitions account
<!--ID: 1706231523640-->
END

---

START
Basic
What is the Double Spending Problem?
Back: 
The Double spending problem is a particular problem where **a user is allowed to spend twice a value**.

Let's say:
- we send 100BTC to another account
	- usually our transaction needs to be confirmed before it occurs
- let's say we create another 100BTC transaction towards another account
- both of these transactions need to be confirmed
- once one of them is confirmed, the conflicting one will be discarded, because of the "longest chain first" policy

Therefore, double spending problem could be a real problem, only if we don't have a strong consensus mechanism.

A similar problem, could theoretically be performed by the 51% attack.
- an attacker has **more than the half** of the total mining power in the network
- it creates a private fork in the BTC architecture
- it creates two transactions:
	- one in the public (100btc to A)
	- one in the private (100btc to the original issuer)
- since the attacker has more of 51% of power, he validates and creates blocks faster than the public
	- the public transaction is confirmed on public
	- the private transaction is confirmed on private fork
	- he puts his forked chain into the public network. This chain will be accepted by the network because of the "longest chain first" policy. The precedent transaction become invalid for this reason.
- so the attacker has purchased something and had his BTCs back

Tags: btc problem blockchain consensus
<!--ID: 1706231523645-->
END

---
START
Basic
What blocks are?
Back: 
Blocks group and collate transactions.

They are time units.

As far as transactions grow as long as block are produced
- the order matters as well, exactly like transactions!

Tags: btc definitions
<!--ID: 1706231523649-->
END

---

START
Basic
What a wallet is?
Back: 
A **wallet** is a lightweight client that fetches only blocks it's interested to.
Tags: definitions
<!--ID: 1706231523653-->
END

---

START
Basic
Are data permanent on the blockchain?
Back: 
Yes, data is **immutable**.
Tags: definitions
<!--ID: 1706231523659-->
END

---

START
Basic
What a Smart contract is?
Back: 
Smart Contracts are **mere pieces of code**.

They have no random function, and are turing-complete (**deterministic**).

They live in the ETH layer and they're mainly used for GAMBLING!

> They execute a function when called!

Facts: 
- An account can invoke Smart Contracts. Not the other way!
- it is invoked using a transaction!

A smart contract is **forever**! We can retire a contract, but if we have a bug it will live forever.

Tags: eth ethereum smart-contracts
<!--ID: 1706231523664-->
END

---
START
Basic
A Smart Contract can invoke an account?
Back: 
NOPE. FALSE! THE OTHER WAY ROUND!!!!
Tags: eth ethereum smart-contracts
<!--ID: 1706231523669-->
END

---

START
Basic
What is the process to create a new smart contract?
Back: 
- To deploy a new smart contract we begin our transaction with our data in a payload to an empty address (pick by a protocol, we don't handle it).
- A new smart contract account will be created.
- From now on, everytime someone wants to execute that code will pay that address.
- The code needs to be complicated (fees)!
- The code is half public and half not.
Tags: eth ethereum smart-contracts
<!--ID: 1706231523674-->
END

---
START
Basic
What the web3.0 is?
Back: 
- classic client-server infrastructure with smart contracts behind
Tags: eth ethereum smart-contracts
<!--ID: 1706231523679-->
END

---

START
Basic
Why PoW exists? 
Back: 
PoW in Bitcoin forces node to prove computational effort to publish new blocks
Tags: btc bitcoin
<!--ID: 1706231523683-->
END

---

START
Basic
What hashing is?
Back: 
Hashing is a function that associates k to values.

You have a deterministic algorithm -> if you input something twice it must output the same thing twice!

This output is unreadable, no secret key involved: FINDING A SOLUTION IS HARD BUT EVERYONE MUST BE ABLE TO CHECK IT!

Tags: definitions
<!--ID: 1706231523688-->
END

---

START
Basic
Token vs crypto
Back: 
- crypto is the euro
- token is the bubbles, flowers, whatever

We can resell tokens in terms of money.
I can buy some flowers coins in euros

Tags: 
<!--ID: 1706231523693-->
END

---

START
Basic
What a ledger is?
Back: 
- **ledger** is a **collation of transactions**
Tags: definitions
<!--ID: 1706231523698-->
END

---

START
Basic
What mining nodes are?
Back: 
**Mining nodes** are the subset of nodes that **maintain the blockchain** by **publishing new blocks**


If we win at mining game, we are rewarded with coins!
Who writes the special value? **The miner itself!** 
If we mine a block, we would like that the entire world knows this thing!

If a transaction **is not known** to any other node in the network **but you**, then the transaction is **not accepted** by the network.

So basically a miner wants to:
- mine blocks
- gain consensus by spreading its work
	- if they don't, the transaction has never happened!

The usual steps are:
1. New transactions are broadcast to all node
2. Each node collects new transactions into a block
3. Each node works on finding a difficult PoW for its block
4. When it founds, it broadcasts to all nodes
5. Nodes accept the block iff transactions in it are valid and **not already spent**
6. They express their **acceptance** of the block by working on creating the next block in the chain, using the hash of the accepted block as the previous block


Tags: btc mining
<!--ID: 1706231523703-->
END

---

START
Basic
How mining works?
Back: 
- **transactions** are added to the blockchain **when a mining node publishes a block**
- a block collates transactions
	- transactions are stored and **sorted** in block
- validity is ensured by **checking** that
	- input accounts have signed the transaction
	- input accounts have sufficient funds on their account
	- the **block timestamp** (needs deep revision)
- the other mining nodes WILL NOT accept a block if it contains any invalid transactions!


- higher the fees for a transaction, higher the chance to include the transaction with the higher fees into the processing block
	- Fees = _Sum(Inputs) – Sum(Outputs_).

Tags: btc mining transactions
<!--ID: 1706231523707-->
END

---

START
Basic
Privacy of a blockchain: public, private, permission-less, permissioned
Back: 

Tags: definitions
<!--ID: 1706231523712-->
END

---

START
Basic
What PoW is? (Proof of work)
Back: 
A very hard crypto-puzzle: you need to find a hash value with content of a block and other stuff.

PoW is not consensus!

You need to resolve this riddle:
- hash(previous block hash + version info + merkle root (hash of the hashes of the transactions) + timestamp + difficulty level + nonce) must produces a hash with leading 0 = difficulty level

The algorithm:
1. Start with Nonce at 0.
2. Combine the block data and Nonce, i.e., the calculation target is the string “Hello, world!0.”
3. Apply the SHA-256 hash function to “Hello, world!0” and calculate the hash value.
4. Check if the calculated hash value meets the Difficulty conditions (starting with “0000”).
5. If not met, increase the Nonce by 1 and repeat steps 2–4.
6. If met, the calculation is complete.

To speed up calculations we use ASICS inexpensive machines that do not have the full hardware of a computer (they have ton of memory).

Tags: definitions proof-of-work btc
<!--ID: 1706231523716-->
END

---

START
Basic
How a block is made of?
Back: 
Inside a block there is:
- block size
- block header
	- hash previous block header
	- timestamp
	- nonce
	- merkle root hash
- transaction counter
- transaction list

Tags: transactions blocks
<!--ID: 1706231523720-->
END

---

START
Basic
What a UTXO is?
Back: 
It stands for "Unspent Transaction Output".

In Bitcoin nothing is "made from nothing".

Whenever someone receives a Bitcoin, this someone has an UTXO.

Once you have an unspent transaction it could never be split up.

For example: if you have a 20 bitcoin UTXO and want to pay 1 bitcoin, your transaction must consume the entire 20 bitcoin UTXO and produce two outputs: one paying 1 bitcoin to your desired recipient and another paying 19 bitcoin in change back to your wallet. As a result, most bitcoin transactions will generate change.

Usually Bitcoin exceeding part transaction could be used in two ways:
- as a charge back
- as a fee

> [!important]
> if you don't generate another returning to your wallet transaction, the exceeding
> part will be returned as miner's fee

- every transaction creates **outputs**, which are recorded on the bitcoin ledger
	- UTXO
- transaction inputs are pointers to UTXO
	- they point to a specific UTXO by reference to the transaction hash and sequence number where the UTXO is recorded in the blockchain
- to use each other, we use a locking/unlocking script


Tags: transactions
<!--ID: 1706231523724-->
END

---

START
Basic
When a transaction occurs? 
Back: 
Transaction occurs, if and only if:
1. Every **input** must be **valid and not yet spent**
2. The transaction must have a signature matching the owner of the input
3. The **total** value of the **inputs** **must equal or exceed** the **total** value of the **outputs**

Tags: transactions
<!--ID: 1706231523728-->
END

---

START
Basic
Coinbase transaction
Back: 
- The coinbase transaction is the first transaction in a block. Always **created by a miner**, it includes a single coinbase.
- A **coinbase** is a special field used as the sole input for coinbase transactions. The coinbase allows **claiming the block reward** and provides up to 100 bytes for arbitrary data.

Tags: transactions
<!--ID: 1706231523732-->
END

---

START
Basic
What a SPV is? (Simple Payment Verification)
Back: 
SPV allows a lightweight client to **verify that a transaction** is included in the Bitcoin blockchain, **without downloading the entire blockchain**.

**The SPV client** only needs download the block headers, which are much smaller than the full blocks. To verify that a transaction is in a block, a SPV client requests a proof of inclusion, in the form of a Merkle branch.

Tags: clients spv
<!--ID: 1706231523737-->
END

---

START
Basic
In the Bitcoin network, accounts 0xA, 0xB, and 0xC have balances worth 10, 5, and 7 BTC, respectively. 0xA issues a signed transaction worth 12 BTC to 0xB (ID: 0xA12B). Thereafter, 0xC issues another signed transaction worth 5 BTC to 0xA (ID: 0xC05A). To what nominal value the accounts amount?
Back: 
10 / 5 / 7
Tags: exercise
<!--ID: 1706231523741-->
END

---

START
Basic
In the Bitcoin network, account 0xA has the following UTXOs whose nominal values are 10, 5, and 2 BTCs. 0xB has UTXOs worth 1 and 2 BTCs. 0xA issues a signed transaction taking the UTXOs worth 10 and 5 BTCs, and making a UTXO worth 12 BTCs to 0xB and a UTXO worth 3.5 BTCs to 0xA. To what nominal value do the accounts amount thereafter?
Back: 
17 / 3
Tags: exercise
<!--ID: 1706231523745-->
END

---

START
Basic
Which of the following units is in use for Bitcoin payments?
Back: 
Satoshi
Tags: definition
<!--ID: 1706231523749-->
END

---

START
Basic
In Bitcoin the block (mining) reward
Back: 
is right-shifted every 210.000 txs

IT IS WRONG " is halved every 105.000 transactions"
Tags: definition
<!--ID: 1706231523754-->
END

---

START
Basic
What transaction fee is?
Back: 
The difference between input and output of a tx.
- **input is always higher than output**

Tags: definition
<!--ID: 1706231523758-->
END

---

START
Basic
What stale blocks are?
Back: 
- **Stale blocks** are created when two miners found the solution at the same time
	- **longest** chains are confirmed
	- if they have the same chains, then **who arrives before**
In ethereum they're called **ommers** and 
Tags: blocks
<!--ID: 1706231523762-->
END

---

START
Basic
Why Ethereum exists?
Back: 
To allow smart contract to be runned on the network.
Tags: eth ethereum definitions
<!--ID: 1706231523766-->
END

---

START
Basic
EOA account vs. CA
Back: 
- In Ethereum we have two kinds of accounts:
	- **EOA**: **simple accounts**, don't know the owner (classic PK, contain balance...) 
	- **CA**: **contract**, that can be triggered by sending a transaction and can also create or call other contracts.

Tags: eth ethereum
<!--ID: 1706231523770-->
END

---

START
Basic
What's the notation of addresses in ethereum?
Back: 
Addresses in Ethereum have UUID using **Keccak-256 algorithm**, that produces mixed capitals letteres encoded
	- given a generic character, we compute hash and if the **hashed value is greater than 8, we capitalize it**.
		- EIP-55
			- for example:
				- 0 0 1 d 3 f (original)
				- 2 3 a 6 9 c (hash)
				- 0 0 1 d 3 F (so original + hash, the Keccak version)

Tags: keccak address eth ethereum
<!--ID: 1706231523774-->
END

---

START
Basic
How an account is identified?
Back: 
- it identified by an **address**
- keep local info
	- **nonce** 1: **EOA**: number of transactions
	- **nonce** 2: **CA**: number of contracts emitted
	- **balance**: number of weis

Tags: eth ethereum
<!--ID: 1706231523778-->
END

---

START
Basic
What a nonce is? Why is it important? What's the difference between btc and ethereum?

Back: 
- in ethereum they are in transaction -> they're **similar to TCP packet numbering**
	- 3 -> 4 ok
	- 3 -> 5 hold
	- 3 -> 2 discarded
- we need nonce to **determine the order of transactions**, like a packet id in TCP

Putting a nonce **protect from double-spending**: a malicious user since ETH transactions are public could re-broadcast a transaction over and over, but this wouldn't work because the nonce would be the same of the original one, and since it has been used it cannot be re-used again

**It is not possible to change the nonce**, because the hash would change and we're able to create a transaction using the original private key

In bitcoin, transactions don't have nonce at all, you use only only for proof of work

Tags: eth ethereum nonce
<!--ID: 1706231523782-->
END

---

START
Basic
What the EVM is?
Back: 
- smart contracts are run on **EVM**, the Ethereum Virtual Machine
	- **everywhere and nowhere**: run on multiple nodes, there is no mainframe at all
	- EVM has its own bytecode and can run any program written in any language (Java, Python, Rust...)
	- There is a cost associated to the running of programs on the EVM: this is called **gas**

Tags: eth ethereum
<!--ID: 1706231523786-->
END

---

START
Basic
What gas is?
Back: 
Cost associated to the running of programs on the EVM.

> GAS IS NOT ETHER

The ether is traded publicly on cryptocurrencies exchanges, so the core computation stays the same.

Gas is used for one purpose only: **measuring the computational effort required to execute operations in smart contracts**.

The more operations, the more contracts deploying, the more data exchange, the higher gas.

Every operation has a **different gas price** (logarithm, store data...)

Transactors are free to specify any gasPrice that they wish, however miners are free to ignore transactions as they choose.

This **limit** is applied to **total gas execution**, including sub transactions and sub executions.

As usual, the lower gas price, the higher chance that their transactions will be mined soon.

Tags: eth ethereum
<!--ID: 1706231523790-->
END

---

START
Basic
What the London Upgrade is?

Back: 
This upgrade adds a lot of complexity to the fee logic, but it’s an interesting approach that could potentially stabilize the fee dynamics

Before London, up to 50% of the refunded gas could be used to execute further computation within the same block.

Before the upgrade, users would essentially participate in an open auction every block, where they would have to place a bid with a miner in something referred to as a “first-price auction.” The closed-bid setting meant that users were often taking a stab in the dark when proposing transaction fees (known as “gas prices”), picking a number that they felt would guarantee their inclusion in the next block of transactions.

Rather than holding a blind auction every block to determine the gas price, ethereum’s protocol will algorithmically decide the transaction fee based upon overall demand on the network.
Tags: eth ethereum
<!--ID: 1706231523794-->
END

---

START
Basic
Proof of stake vs. proof of work
Back: 
- in Proof Of Stake, validators **stake** capital in ETH
- in Proof Of Work, miners put capital at risk by **expending energy**

Tags: eth ethereum
<!--ID: 1706231523798-->
END

---

START
Basic
LMD-GHOST
Back: 
LMD: latest message-driven greedy heaviest observed sub-tree 

- Casper+LMD-GHOST: algorithm that decides when the validators have different views of the **head** of the chain
	- usually the favored one is the fork with the **greatest accumulated weight of attestations**
	- if multiple messages are received from a validator, only the latest one is considered
	- Latest message-driven greedy heaviest observed sub-tree
![[Screenshot_20231126_193729.png]]

Tags: eth ethereum algorithms
<!--ID: 1706231523802-->
END

---
START
Basic
How time is calculated?
Back: 
- **slots**: 12 seconds, for every slot one validator is randomly selected to be a block **proposer** and it has 6 seconds to forge a new block
- **epoch** (32 slots)
	- the first block is a **checkpoint**

Validators should then vote for pairs of **checkpoints**:
- the **most recent** one become **justified** if attested with votes of at least 2/3 of the total staked ETH
- the **least recent** one become **finalized** if it gets the 2/3 majority

Only epoch-boundary blocks can be justified and finalized.

A supermajority link must exist between successive checkpoint A and B.

Every 256 epochs a **sync committee** is randomly assigned
- a group of 512 validators
- the committee signs block header for each new slot

Certified HAHA moment:
- where are attestations saved?
	- **EPHEMERAL DATA**

- sync committees output when?
	- after a while!

Tags: eth ethereum
<!--ID: 1706231523806-->
END

---
START
Basic
How rewards in ethereum work?
Back: 
- attestation rewards: correct head, source and target attestation
- sync comittee reward
- proposer reward for an attested block
Tags: eth ethereum
<!--ID: 1706231523811-->
END

---
START
Basic
Are there penalties in Ethereum? How they are called? Tel me more about slashing
Back: 
Slashing are punishments for:
1. Double proposal (**equivocation**): a proposer signs **two** different beacon blocks for the **same slot**

2. **FFG Double vote**: two checkpoint attestations for the same target epoch

3. attester signs a checkpoint attestation that surrounds another one
	- in other words, **contradicts** what a validator already said

These can be busted by a **whistleblower** that can be entitled to a reward.

**Slashing: you've done on purpose**

But there may be penalties:
- **inactivity** penalty
	- if the chain fails to finalize for more than 4 epochs
- **sync committee** penalty
	- not participating or signing the wrong header

Tags: eth ethereum
<!--ID: 1706231523815-->
END

---
START
Basic
What does ethereum relies on? PoW?
Back: 
No, PoS, Proof of Stakes!

Ethereum uses a proof-of-stake-based consensus mechanism that derives its crypto-economic security from a set of rewards and penalties applied to capital locked by stakers. This incentive structure encourages individual stakers to operate honest validators, punishes those who don't, and creates an extremely high cost to attack the network.

The replacement of the PoW chain with the PoS chain in Ethereum was named… the merge!
Tags: definitions ethereum eth
<!--ID: 1706231523819-->
END

---
START
Basic
Transactions in Ethereum are serialised via a scheme named?
Back: 
RLP
Tags: transactions definitions ethereum eth
<!--ID: 1706231523823-->
END

---
START
Basic
A1 Seminar: blockchain based resource governance for decentralized web environments. Solid, ReGov
Back: 
Big companies have big data, but users don't know where their data is. 
Tim Berners Lee is the father of WWW and creator of SOLID to make the web decentralized and give to users ownership of their data.
IN **SOLID**, each user has its own POD in which it places their data and constraints to allow someone to use thata data.

**ReGov** is a platform created for the shared resources' governance using Solid.
Two roles:
- **resource provider**: interaction with store manager and resource send using resource storage
- **resource retriever**: data consumption
Once ReGov receives a request, it begins a monitoring session to learn how data are used.

**Data provision and data consumption** are two standalone entities.
Data is always exchanged from consumer node to owner node and viceversa. In the middle there is governance ecosystem.

Constraints may be:
- access **counter**
	- a resource can be opened only a **specific number of times**
- **domain** obligation
	- a resource can be processed only for **some reasons**
- **temporal** obligation
	- a resource can be stored only for a **set period of time**
- **country** obligation
	- a resource can be loaded only for a **specific set of regions**

Tags: eth ethereum seminars
<!--ID: 1706231523827-->
END

---
START
Basic
A2: decentralized oracles for the ethereum blockchain platform
Back: 
Oracles are bridges from blockchain and real world.

They are:
- **reliable**: DApp MUST trust oracles, like infos are on blockchain
- **shared usage protocol**: bridge among different technologies

They can be classified depending on:
- **source** 
	- **software**: interact with resources and transmit information to the blockchain
	- **hardware**: gather information from real world and transmit them to smart contracts
	- **humans**: human experts interact with smart contracts
- **flow direction**
	- information: outbound or inbound
	- initiatior:
		- pull: receive data  
		- push: send data
		- both of them have in or out: realworld to blockchain and viceversa

An oracle has two kinds:
- on-chain tier: interaction between oracle and on-chain world
- off-chain tier: oracle and real world

Using a centralized oracle doesn't preserve blockchain's decentralized characteristics.

Using decentralized oracles on the other hand, has a bad performance (gas, latency), it adds a overhead for reaching consensus, but preserve blockchain's decentralized characteristics.

Tags: seminars eth ethereum
<!--ID: 1706231523831-->
END

---

START
Basic
A3: Algorand
Back: 
Algorand, è troppo complicato e io non ho sbatti di scrivere nulla.
Tags: seminars
<!--ID: 1706231523836-->
END

---
START
Basic
A4: Rug Pull, Defi and Dex
Back: 
See Distributed Systems notes on Google Drive.
Tags: seminars eth ethereum
<!--ID: 1706231523840-->
END

---
START
Basic
A5: enabling data confidentiality with public blockchains (Describe IPFS system with blockchain)
Back: 
Peer to peer google drive: distributed storage in the world.

CP-ABE: CP -> Ciphertext-Policy and ABE -> Attribute Based Encryption
Tags: seminars eth ethereum
<!--ID: 1706231523844-->
END

---
START
Basic
Consensus on bitcoin vs. consensus on ethereum
Back: 
The term consensus mechanism refers to the entire stack of protocols, incentives and ideas that allow a network of nodes to agree on the state of a blockchain.

- **Proof-of-work based**: Miners compete to create new blocks filled with processed transactions. The winner shares the new block with the rest of the network and earns some freshly minted ETH. The race is won by the computer which is able to solve a math puzzle fastest. This produces the cryptographic link between the current block and the block that went before. Solving this puzzle is the work in "proof-of-work". The canonical chain is then determined by a fork-choice rule that selects the set of blocks that have had the most work done to mine them.
- The network is kept secure by the fact that you'd need 51% of the network's computing power to defraud the chain. This would require such huge investments in equipment and energy; you're likely to spend more than you'd gain.

- **Ethereum**: uses a proof-of-stake-based consensus mechanism that derives its crypto-economic security from a set of rewards and penalties applied to capital locked by stakers. This incentive structure encourages individual stakers to operate honest validators, punishes those who don't, and creates an extremely high cost to attack the network.

Tags: eth btc ethereum blockchain
<!--ID: 1706231523847-->
END