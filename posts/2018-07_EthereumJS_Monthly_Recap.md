EthereumJS VM v2.4.0 (Partial Constantinople Support) + Recap July 2018

Hi everyone, main news for this month is that we have the ``v2.4.0`` release for our VM out which introduces parallel hardfork support from Byzantium onwards and makes a start by introducing a partial set of the ``Constantinople`` features (bitshift instructions).

Since ``Constantinople`` is not yet finalized this is regarded as ``EXPERIMENTAL``. If you are building developer tools on top of EthereumJS VM you can nevertheless now use this to allow your users an early look and experimentation ground for the new features. Implementations of further Constantinople features will be gradually added to upcoming ``v2.4.x`` releases with a follow-up ``v2.5.0`` release introducing full ``Constantinople`` support once the hardfork specification is finalized and we are ready with the implementation.

The EthereumJS VM release comes with various other new feature introductions and bug fixes, have a look at the release notes for the full list:
https://github.com/ethereumjs/ethereumjs-vm/releases/tag/v2.4.0

Other noteworthy news:

**ethereumjs-client**

We are pleased to announce that we have now found an official team lead for our client project. Vinay Pulim from Brooklyn, New York has taken on the project and was already extremely busy doing a huge structural rewrite on the whole architecture:
https://github.com/ethereumjs/ethereumjs-client/pull/37

If you are interesting in latest client developments you should have a look. This is really exciting stuff taking inspiration from the bcoin project (https://github.com/bcoin-org/bcoin) and setting up dedicated structures for different Node types (FastSync/LightSync), blockchain synchronization strategies and network transports.

All this makes things extremely modular and will allow for easier expansion of (and doing experiments/research on top of) the code base and also allow for easier in-parallel contribution.

If you want to contribute, this is also an exciting time to get involved!

**rustbn.js**

There was a new ``v2.0.0`` release of our ``rustbn.js`` library - which is a Rust to Javascript/Webassembly compilation of ethereum-bn128.rs allowing for ``BN128`` elliptic curve operations - coming with a better Javascript API:
https://github.com/ethereumjs/rustbn.js/releases/tag/v0.2.0

**ethereumjs-tx**

We had a small bug fix release - again for the ``FakeTransaction`` part of the library - fixing a bug causing ``FakeTransaction.from`` to not retrieve the sender address from tx signature. This caused trouble on creating self-signed transactions:
https://github.com/ethereumjs/ethereumjs-tx/releases/tag/v1.3.7

**ethereumjs/common**

The old ``common`` library is now officially deprecated. If you make use of the library update to our new ``ethereumjs-common`` library rewritten from scratch:

Old library: https://github.com/ethereumjs/common
New library: https://github.com/ethereumjs/ethereumjs-common

---

This is the third of a monthly series giving a summary of what happened within the EthereumJS ecosystem, see https://www.reddit.com/r/ethereum/comments/8vhwwj/ethereumjs_monthly_recap_june_2018/ if you want to catch up with the developments from the month before.

Want to get in touch? https://gitter.im/ethereum/ethereumjs

Reddit Link: https://www.reddit.com/user/HolgerD77/comments/921p5a/ethereumjs_vm_v240_partial_constantinople_support/