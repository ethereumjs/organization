EthereumJS Recap August 2018 - Client Light Sync Support / Chain & Hardfork Support for Blockchain Library

Hi everyone, this is what happened in EthereumJS in August:

**ethereumjs-client**

Partial implementation of [light sync support](https://github.com/ethereumjs/ethereumjs-client/pull/47) just got merged by Vinay. This currently only downloads headers and does not yet serve headers/blocks to other clients. If you are interested in client development, you should nevertheless have a look and play around.

https://github.com/ethereumjs/ethereumjs-client

**ethereumjs-blockchain**

The latest version [v3.2.0](https://github.com/ethereumjs/ethereumjs-blockchain/releases/tag/v3.2.0) (respectively [v3.2.1](https://github.com/ethereumjs/ethereumjs-blockchain/releases/tag/v3.2.1) additionally fixing an ``iterator()`` function bug) of the library now allows for hardfork-specific validation by integrating with the new ``ethereumjs-common`` library. This also introduces new header-chain functionality and comes with two bug fixes (one with caching, one also affecting the Blockchain.iterator() function).

https://github.com/ethereumjs/ethereumjs-blockchain

**ethereumjs-wallet**

Bugfix release [v0.6.2](https://github.com/ethereumjs/ethereumjs-wallet/releases/tag/v0.6.2) fixing a bug introduced with the v0.6.1 release. This caused some headaches in 3rd-party applications like Embark or Truffle, if you are experiencing any problems regarding import paths you should update.

https://github.com/ethereumjs/ethereumjs-wallet

**ethereumjs-common**

Minor release [v0.4.1](https://github.com/ethereumjs/ethereumjs-common/releases/tag/v0.4.1) updating the ``Ropsten`` bootstrap nodes and adding a genesis ``timestamp`` field, mainly for the Rinkeby chain, followed by a [v0.5.0](https://github.com/ethereumjs/ethereumjs-common/releases/tag/v0.5.0) release introducing support for private chains by passing a custom chain parameter dictionary.

https://github.com/ethereumjs/ethereumjs-common

**ethereumjs-block**

Bugfix release [v2.0.1](https://github.com/ethereumjs/ethereumjs-block/releases/tag/v2.0.1) fixing a bug in header validation logic.

https://github.com/ethereumjs/ethereumjs-block

---

This is part of a monthly series giving a summary of what happened within the EthereumJS ecosystem, see https://www.reddit.com/r/ethereum/comments/923woh/ethereumjs_vm_v240_partial_constantinople_support/ if you want to catch up with the developments from the month before.

Want to get in touch? https://gitter.im/ethereum/ethereumjs

Reddit Link: 
https://www.reddit.com/r/ethereum/comments/9eci4u/ethereumjs_recap_august_2018_client_light_sync/