EthereumJS Monthly Recap - June 2018

Hi everyone, this is the second of a monthly series giving a summary of what happened within the EthereumJS ecosystem, see https://www.reddit.com/r/ethereum/comments/8nmelx/ethereumjs_monthly_recap_may_2018/ if you want to catch up with the developments in May.

**ethereumjs-block**

Our new common library (https://github.com/ethereumjs/ethereumjs-common) helping with chain and hardfork support is getting more and more stable and we are starting to use this in production and slowly extend chain and fork support on different libraries. The ``ethereumjs-block`` library made the start with a new ``v2.0.0`` release, now supporting chain-dependent genesis block initialization and correct block validation for all known hardforks.
https://github.com/ethereumjs/ethereumjs-block/releases/tag/v2.0.0

**ethereumjs-client**

Development on our new client library is off to a very pleasant start and we have already seen wonderful contributions from the community with substantial and high-quality work bringing the project forward. Thanks to the work of @fgimenez we have now tests and solid code structure for file and DB management ( see https://github.com/ethereumjs/ethereumjs-client/pull/29). @yurenju introduced an extremely solid base structure including middleware for parameter checks and http testing for ``JSON-RPC`` calls (https://github.com/ethereumjs/ethereumjs-client/pull/30), already implementing the ``eth_getBlockByNumber()`` call as a test call (which you can already try with ``curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["0x1b4", true],"id":1}' -H "Content-Type: application/json" http://127.0.0.1:8545|jq``).

Especially the latter one is an extremely good entry point if you want to engage in the project. So if you are looking for stuff you can contribute, just grab yourself another ``JSON-RPC`` call for implementation!
https://github.com/ethereumjs/ethereumjs-client

**rlp**

There was a long-overdue maintenance release ``v2.1.0`` of the ``rlp`` library with some version and dependency updates.
https://github.com/ethereumjs/rlp/releases/tag/v2.1.0

**ethereumjs-devp2p**

We had a bounty for node discover v5 implementation for our p2p library and work has finally started on this and is progressing well. So this should bring us an important step forward on the networking front once ready and allow for efficient light client syncing.
https://github.com/ethereumjs/ethereumjs-devp2p/issues/19

**ethereumjs-vm**

A lot of work to do on the VM - being partly delayed since a big share of our team is currently busy working on the eWASM (https://github.com/ewasm) implementation. If you want to help out on the VM have a look at the issue list.
https://github.com/ethereumjs/ethereumjs-vm/issues

**ethereumjs-tx**

We had a bugfix release ``v1.3.5`` in June which introduced some error-prone behavior around the ``FakeTransaction.hash()`` function which was fixed in a subsequent ``v1.3.6`` release. This can cause problems in third-party libraries (e.g. ``ganache``), so please update if you are on ``v1.3.5``!
https://github.com/ethereumjs/ethereumjs-tx/releases

Want to get in touch? https://gitter.im/ethereum/ethereumjs

Reddit Link: https://www.reddit.com/r/ethereum/comments/8vhwwj/ethereumjs_monthly_recap_june_2018/