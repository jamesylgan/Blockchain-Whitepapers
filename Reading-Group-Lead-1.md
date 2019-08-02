* BOMB [website](https://bombtoken.com/), [relevant reading](https://www.coindesk.com/blockchain-token-velocity-problem)
* Libra [whitepaper](https://libra.org/en-US/white-paper/)	
* Tezos [whitepaper](https://tezos.com/static/white_paper-2dc8c02267a8fb86bd67a108199441bf.pdf), [technical whitepaper](https://developers.libra.org/docs/the-libra-blockchain-paper)
* RChain [whitepaper](
https://docs.google.com/gview?url=https://github.com/rchain/reference/raw/master/docs/RChainWhitepaper.pdf), [system architecture](https://architecture-docs.readthedocs.io/introduction/architecture-overview.html)

# BOMB: A self-depreciating token
Token Velocity problem: 
- Definition: Too many ICOs/companies relying on the (false?) underlying idea that demand for their token will rise, resulting in price and value gain.
	+ We can say that an asset has a velocity of 0 if, over the course of a year, no one buys or sells it. The lack of liquidity would cause the asset to trade at a discount to its “intrinsic” value. Assets need some velocity to achieve their full intrinsic value. The difference is known as the liquidity premium.
- Reduce velocity: Profit-share, staking, burn-and-mint, gamification to encourage holding, store of value.
- Tl;dr, why would you hold the token?
- Bomb: "If you don't hold it, you lose some value!" self-deflationary

# Libra: A centralized Blockchain from Facebook, PayPal, etc, with reserves held in cash to back the token
## Nontechnical Overview
- Try to enable innovation around financial services and accessibility
- Focus on mobile-accessible? Potentially difficult
- Reduce fees via blockchain (like all blockchain)
- **Adoption through scale and reputation (Libra Association)**
- **Governed by Libra Association**
- Stablecoin aspects: backed by reserves held in traditional assets by Libra Association (FB and co)
- Profits from reserves go to Libra Association
- Move (Eth-like types, automatic proofs for txs), BFT (Weak, security through trust of Libra Association), built off existing mechanisms (BFT, Merkle Trees a la Bitcoin, etc), pseudoanonymous (a.k.a Libra Association could regulate in some way and reveal identity to govts)

# Tezos: A self-governing, self-amending, PoS blockchain with FP and provable code
- Big fan of Tezos (not financially invested or incentivized) - why have they not excelled? Lots of contraversy near founding. Lawsuits between technical founders and original organization leadership they hired.
- Traditionally, many forks. E.g. litecoin, Bitcoin Classic, Ethereum Classic. They capture huge portions of capital without providing any meaningful changes or carrying along reasonably sized developer teams. How to avoid this?
- Chain propagates a protocol object, which is used by the Blockchain to change the existing protocol
- Maintains a system timestamp
- Single chain only overwritten if a better chain comes about, not a tree (DoS avoidance)
- Automatically bans malicious nodes (DoS attempts)
- OCaml Type signatures: FP, etc
- Asynchronous Lwt Monad to avoid blocking on disk operations
- Protocol: operation, header, apply
- Self amendment: set_test_protocol, promote_test_protocol. Generally, stakeholder vote to change (to begin) but later more complicated protocol change rules could be implemented.
- Stake to mine and endorse
- Inactive accounts destroyed after a year - later changed to just losing staking, voting rights
	+ introduces a concept of delegation
- Elections every 3 months, 80% supermajority, test-net beta for 1 quarter
- Proof-of-stake: proof-of-burn, chain-of-activity, Slasher
- Clock-based delays to fight DoS
- No selfish mining allowed - Must reveal next mining target or lose bond
- Not UTXO, but accounts
- Contracts destroyed when their balance is too low
- Smart contracts strict with storage and compute, but could be voted on to be changeed in the future

# RChain: A blockchain driven by Rho Calculus
- Built around a person: like BDFL for Python. Good? Bad? Some recent controversy around it. Lots of buzzwords, but also founded in academia
- Rho VM: "Concurrent execution engine, unprecedented speed and scalability"
- Interchain by design: how?
- Auto-migration of languages
- Co-op governance? Discussion around governance. Proof of stake, Council (Eth), distributed (Bitcoin).
- Buy-in from Ethereum lead researcher Vlad Zamfir
- Focus on entire environment, just like Consensys for Ethereum
- Multi-threaded concurrency across network's nodes using Rho calculus, sharding
- Formal verification, which we can see later in Tezos
- Losing a lot of money quicker than expected
- Execution model: 
  + RhoVM is the composition of the rho-calculus reduction semantics, expressed in Rholang, and a persistent key-value data store.
	+ The rho-calculus reduction rule substitutes the value at a key for another value, where a named channel corresponds to a key, and values may be simple or complex.
	+ Substitutions are transactions, which manifest as differences in the bytecode stored at a key. The accurate replication of those bytecode differences, across all nodes operating that instance of RhoVM, is verified via the consensus algorithm.
- Casper consensus algorithm: 
	+ The Casper consensus protocol includes stake-based bonding, unbonding, and betting cycles that result in consensus.
	+ Unlike Ethereum’s betting on a whole blocks, RChain’s betting is on logical propositions. 
  + A proposition is a set of statements about the blockchain, for example: which transactions (i.e. proposed state transitions) must be included, in which order, which transactions should not be included, or other properties. A concrete example of a proposition is: “transaction t should occur before transaction s” and “transaction r should not be included”. 
