* BOMB [website](https://bombtoken.com/), [relevant reading](https://www.coindesk.com/blockchain-token-velocity-problem)
* Libra [whitepaper](https://libra.org/en-US/white-paper/)	
* Tezos [whitepaper](https://tezos.com/static/white_paper-2dc8c02267a8fb86bd67a108199441bf.pdf), [technical whitepaper](https://developers.libra.org/docs/the-libra-blockchain-paper)
* RChain [whitepaper](
https://docs.google.com/gview?url=https://github.com/rchain/reference/raw/master/docs/RChainWhitepaper.pdf), [system architecture](https://architecture-docs.readthedocs.io/introduction/architecture-overview.html)

------------

# BOMB: A self-depreciating token
Token Velocity problem: 
- Definition: Too many ICOs/companies relying on the (false?) underlying idea that demand for their token will rise, resulting in price and value gain.
	+ We can say that an asset has a velocity of 0 if, over the course of a year, no one buys or sells it. The lack of liquidity would cause the asset to trade at a discount to its “intrinsic” value. Assets need some velocity to achieve their full intrinsic value. The difference is known as the liquidity premium.
- Reduce velocity: Profit-share, staking, burn-and-mint, gamification to encourage holding, store of value.
- Tl;dr, why would you hold the token?
- Bomb: "If you don't hold it, you lose some value!" self-deflationary

------------

# Libra: A centralized Blockchain from Facebook, PayPal, etc, with reserves held in cash to back the token
## Discussion Points
- Similarities to Ethereum
- Governance model: Libra Association
- Transition to open membership
- Stablecoin mechanism / Reserves
- Financial inclusion (40Mbps requirement?)
- Throughput -> 70x slower than Ripple with 2.5x the finalization speed
- Centralization?
- See technical assumptions, cool mechanisms sections below.
	+ Stablecoin assumptions from reserves
	+ Require 40Mbps internet connection
	+ Assuming that it's easy to scale from parallelism on a Blockchain network
	+ Allowing any authorized reseller to mint new coins, with no verifiable way that deposits were actually made, with Libra Association choosing who gets to be an authorized reselled. Lots of points of exposure, and they claim a guaruntee that Libra cannot mint new counts themselves even though they get to choose who can
	+ Merkle Tree Optimization
	+ Account Rent, like the Whale Protocol
## Stated Goals:
- Global collaborative effort
- Foster innovation
- Lower barriers to entry
- Improve access to financial services, capital
## Technical Assumptions I Found
1. "Coin will inherit low inflation, stability due to reserves in bank deposits basket" - not necessarily. Lots of stablecoin literature debating this, with various reserve-backed coins failing to maintain peg. p2
2. "Bank deposits basket will be stable" ->  What about in a global financial crisis? Bank runs? Other issues? Un-peg resulting in lack of faith with Libra? Would it recover? How? p2
3. "Most blockchains are UTXO based" p14. Fairly old paradigm.
4. "Require a 40Mbps internet connection" for throughput estimates, p22. VERY high. Geopartitioning difficult. Financial exclusion. Many blockchains aim far lower especially when trying to be inclusive. Loses out on benefits from validator design while also not being decentralized.
5. "Easy to scale through parallelism" p23
6. "For new coins to be minted, must be commensurate fiat deposit in the reserve" p24 -> How is this verified? Off chain actions... **Oracles**
## Issues
- "New global currency" - obvious issues with government. 
- Deferring many of the most challenging parts of implementation, p7, etc.
- No capacity for randomness, probably fine, p8.
- Throughput estimates 1000 TPS at release, 10s finalization. Ripple, similar validator design, 70,000 NOW, 3.7s finalization.
- How do validators take turns? (Might be in LibraBFT paper) Time or # based leadership? Ripple makes more effort to clarify.
- Maintains pseudonymity of every other Blockchain, difficult to ensure KYC/other regulatory requirements
- Authorized resellers for reserves - potentially opens up monopolistic behavior (high fees to swap) or security concerns (too many auth keys with high power)
- Libra Association manually *(?)* controls minting/destroying supply of Libra Coin, in response to authorized reseller orders.
	+ How will deposits into reserve be verified to ensure no hyperinflation from minting new coins?
	+ They manually control who is an authorized reseller - how does this eliminate the potential that new coins are minted by them? p24
- Goal of full decentralization, but not there yet, currently permissioned, closed network. p24. Why? Ethereum is PoW right now with plans to go to PoS and is very, very similar.
	+ No explanation for what PoS standards they will be using
## Interesting Technical Mechanisms
- Trying to figure out how to update modules, **a la Tezos, p6.**
- Event emission, p6. Quicker confirmation than not doing it, but more overhead. p6.
- Verification of transaction scripts and modules, p10.
- Merkle tree acculumator, p14.
- Pruning old states, p14.
- Merkle Tree optimization, p15. Similar to Ethereum optimization but shorter proof. But how often does this occur on a normal Blockchain?
- Account rent, p16, like Whale Protocol.
- Considering punishing bad actors, p25, rewarding participation in votes. Tezos and others already do this.
--------------------
## In General
- **VERY** Similar to Ethereum, including gas model, account model, smart contract model.
- PoS based
- Starting out Libra Association only, later will be open to all
- Validator leader similar to Ripple, but undefined of how leadership transfers.
- Merkle Trees
- Accounts, not UTXO. *Claim that most are UTXO based,* but many are account based already, not original.
- Networking is fairly standard, gossip, direct lines because validators are controlled for now. p19.
- Built with Rust
## Nontechnical Overview
- Try to enable innovation around financial services and accessibility
- Focus on mobile-accessible? Potentially difficult
- Reduce fees via blockchain (like all blockchain)
- **Adoption through scale and reputation (Libra Association)**
- **Governed by Libra Association** ***temporarily***
- Stablecoin aspects: backed by reserves held in cash and government securities by Libra Association (FB and co)
- Profits from reserves go to Libra Association members
- Move (Eth-like types, automatic proofs for txs), BFT (Weak, security through trust of Libra Association), built off existing mechanisms (BFT, Merkle Trees a la Bitcoin, etc), pseudoanonymous (a.k.a Libra Association could regulate in some way and reveal identity to govts)

------------

# Tezos: A self-governing, self-amending, PoS blockchain with FP and provable code
## Talking Points
- Big fan of Tezos (not financially invested or incentivized) - why have they not excelled? Lots of contraversy near founding. Lawsuits between technical founders and original organization leadership they hired.
- Traditionally, many forks. E.g. litecoin, Bitcoin Classic, Ethereum Classic. They capture huge portions of capital without providing any meaningful changes or carrying along reasonably sized developer teams. How to avoid this?
- Governance: What is it, what are different approaches?
- Proof-of-stake mechanisms, proof-of-burn, chain-of-activity, Slasher, good? bad?
- Functional programming, provable code for contracts
- Selfish mining protections
## Details
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

------------

# RChain: A blockchain driven by Rho Calculus
## Talking Points
- Built around a person: like BDFL for Python. Good? Bad? Some recent controversy around it. Lots of buzzwords, but also founded in academia
- Interchain
- Governance, co-op?
- Buy-in from Ethereum lead researcher Vlad Zamfir, Casper
- Rho Calculus?
## Details
- Rho VM: "Concurrent execution engine, unprecedented speed and scalability"
- Interchain by design: how?
- Auto-migration of languages
- Co-op governance? Discussion around governance. Proof of stake, Council (Eth), distributed (Bitcoin).
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
