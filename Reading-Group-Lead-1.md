* RChain [whitepaper](
https://docs.google.com/gview?url=https://github.com/rchain/reference/raw/master/docs/RChainWhitepaper.pdf), [system architecture](https://architecture-docs.readthedocs.io/introduction/architecture-overview.html)
* Tezos [whitepaper](https://tezos.com/static/white_paper-2dc8c02267a8fb86bd67a108199441bf.pdf)
* BOMB [website](https://bombtoken.com/), [relevant reading](https://www.coindesk.com/blockchain-token-velocity-problem)
* Libra [whitepaper](https://libra.org/en-US/white-paper/)

# RChain
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
		

# Tezos
??

# BOMB
Token Velocity problem: 
- Definition: Too many ICOs/companies relying on the (false?) underlying idea that demand for their token will rise, resulting in price and value gain.
	+ We can say that an asset has a velocity of 0 if, over the course of a year, no one buys or sells it. The lack of liquidity would cause the asset to trade at a discount to its “intrinsic” value. Assets need some velocity to achieve their full intrinsic value. The difference is known as the liquidity premium.
- Reduce velocity: Profit-share, staking, burn-and-mint, gamification to encourage holding, store of value.
- Tl;dr, why would you hold the token?
- Bomb: "If you don't hold it, you lose some value!" self-deflationary

# Libra
