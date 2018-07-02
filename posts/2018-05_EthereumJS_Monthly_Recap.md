EthereumJS Monthly Recap - May 2018

Hi everyone, this is a first of a monthly series giving a summary of what happened within the EthereumJS ecosystem. So let's directly dive in:


**ethereumjs-blockchain**

We had a pretty exciting ``v3.0.0`` release making our blockchain library DB-compatible with Geth. This allows for iterating through a local Geth DB with JS - pretty cool - and provides future ground to test our VM with actual live net chain data.
https://github.com/ethereumjs/ethereumjs-blockchain/releases/tag/v3.0.0

**ethereumjs-common**

We have a new common library providing easy access to genesis params and general config parameters like gas prices. Values are now provided in both a network/chain (mainnet, ropsten,...) and hardfork (spuriousDragon, Bzantium,...) specific way. This will allow us to easier support different network and hardforks for our libraries in future releases.
https://github.com/ethereumjs/ethereumjs-common

**ethereumjs-VM**

Already in late April a really nasty bug in the ``BYTE`` opcode in our VM implementation was found. We fixed that and released ``v2.3.5``, you should update.
https://github.com/ethereumjs/ethereumjs-vm/releases/tag/v2.3.5

**ethereumjs-client**

And finally, you might have already seen the related post on Reddit: (early) development of our client implementation has started. Head over to the repo, the README will provide you with the necessary information where we are now and how you can contribute, you are very invited!
https://github.com/ethereumjs/ethereumjs-client

Reddit Link: https://www.reddit.com/r/ethereum/comments/8nmelx/ethereumjs_monthly_recap_may_2018/