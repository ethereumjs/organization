.. _roadmap:

=======
Roadmap
=======

.. _roadmap_active:

Active Projects
===============

.. _roadmap_r181_typescript:

R18-1 Transition to TypeScript
------------------------------

There is currently a transition of EthereumJS libraries from JavaScript to 
`TypeScript <https://www.typescriptlang.org/>`_ in the works. This is a somewhat
larger effort since it not only requires significant updates to the source code 
but also comes with changes to the toolchain (e.g. regarding testing, code 
analysis (linting) and formatting) on all libraries transitioned. This fact 
nevertheless is an opportunity to rethink parts of tooling and systematically 
introduce improved procedures along the way.

Bringing type safety to the EthereumJS libraries should bring large mid-term 
benefits regarding overall security and robustness of the libraries.

Timeline
^^^^^^^^

- ``November 2018``

  - ✅ Ad-hoc team, tooling discussion, kick-off at Devcon4
  
- ``December 2018``

  - 🛠️ First reference implementation (`RLP library <https://github.com/ethereumjs/rlp/pull/37>`_)
  - 🛠️ Toolchain best practices draft
  
- ``February 2019``

  - ⭕ Three more completed transitions, stable toolchain
  
- ``May 2019``

  - ⭕ All major transitions completed including ``VM``, ``merkle-patricia-tree``

.. _roadmap_r182_client:

R18-2 EthereumJS Client
-----------------------

Although popular clients like Geth and Parity already exist, given the popularity of
the JavaScript language we have finally started the development of a dedicated
JavaScript Ethereum client with fast- and light-sync support. Development started
in June 2018 on https://github.com/ethereumjs/ethereumjs-client and reactions
from the community have been extremely positive.

Initially, rather than focus on building a consensus-critical client, we want to
focus on the following use cases (in order of importance):

- In-Browser/NodeJS research & development (sharding, libp2p, etc.) mainly supported by a modular and extensible (plugin-based) architecture
- In-Browser education applications
- In-Browser/NodeJS client simulations and visualizations
- In-Browser light client (Metamask without Infura)

Generally the EthereumJS client project has larger similarities with the scope of
the Trinity project of the Python team. Since JavaScript (like Python) is an extremely
popular and widely used language, this will draw in a whole new class of developers
who were not able to experiment with and develop on Ethereum client technologies before.

One side goal being nevertheless important is finally to use the client development
as a proxy to “harden” the other EthereumJS libraries against a real production 
environment and serve as a better foundation for testing for our Virtual Machine
implementation.

The client project will also build a solid foundation for continued internal research
and development efforts. We've already incorporated support for libp2p as an alternate
transport to RLPx/Devp2p that enables the in-browser light client use-case. In the future,
we hope to implement a Clique PoA engine and test it on the Goerli testnet, and later build
a working Ethereum 2.0 stateless client.

At a later point it is also be desired to have a dedicated website for the client
(similar to https://geth.ethereum.org/) to have a more visible entry point and source
for information around the client for the community.

Timeline
^^^^^^^^

- ``Q3 2018``

  - ✅ Proof-of-concept chain sync (fast and light)
  - ✅ Libp2p networking and browser support

- ``Q4 2018``

  - ✅ Achieve > 90% code coverage via unit/integration tests
  - 🛠️ Reliable mainnet chain sync (fast and light) including block validation
  - 🛠 Implement state downloading

- ``Q1 2019``

  - ⭕ Test setup on hive
  - ⭕ Participate in Kitsunet (https://github.com/MetaMask/mustekala/blob/master/docs/architecture.md#layer-3-kitsunet-peers)
  - ⭕ Determine Ethereum 2.0 strategy (ShasperJS collaboration? stateless client?)

- ``Q2 2019``

  - ⭕ Alpha release of client
  - ⭕ Become a signer on the Goerli testnet

.. _roadmap_considered:

Considered Projects
===================

Projects currently under consideration or in a draft state.

.. _roadmap_r191_sharding_tools:

R19-1 Sharding Tools
--------------------

The all-dominating topic regarding the evolution of Ethereum for the upcoming years 
will be the implementation of a sharded network together with the integration of 
the PoS consensus mechanics introduced with Casper.

While it is not intended by the EthereumJS team to provide a full stack solution 
for these problems on its own, there will be a minimal role for JavaScript implementations 
in this area to provide a basis for/support:

- 3rd party developer tools with integrated sharding support, e.g. to simulate a sharded deployment
- Sharding R&D on the web
- Sharding chain data structure components (collations, cross-links,...), e.g. for block explorers and other tools

Due to the ongoing research and late-changing specifications in this field, there 
is still an ongoing debate in the team about the scope of work to be done here. 
There is consensus though that there will be a minimal targeted need with various 
useful expansions on this without going too broad in scope.

.. note::
   For this to be moved to the ``active`` section this needs a more concrete focus
   first.

.. _roadmap_r192_assemblyscript:

R19-2 AssemblyScript (eWASM)
----------------------------

Currently the ``eWASM`` team is working on the implementation of an upgraded 
Ethereum virtual machine (VM), replacing the existing EVM with a 
`WebAssembly <https://webassembly.org/>`_ (WASM) compatible VM, a testnet supporting
this is already `up and running <https://github.com/ewasm/testnet>`_.

This will allow to write smart contracts in various classical non-blockchain
specific languages. One language specifically targeted for support by the
eWASM team is `AssemblyScript <https://github.com/AssemblyScript/assemblyscript>`_.
This language is a subset of ``TypeScript`` which is basically ``JavaScript``
with type additions. ``TypeScript`` is already supported and will become the default 
language for ``EthereumJS`` libraries once :ref:`roadmap_r181_typescript` is
completed.

While ``AssemblyScript`` is syntactically compatible with ``(e)WASM`` it will
nevertheless take some signifcant high-level work to make this a trusted
Ethereum smart contract language.

Tasks in this regard are:

- Define and spec out some practically usable high-level API
- Create code examples
- Build up some tooling infrastructure
- Create helper libraries
- Think about security best practices
- ...

It would be some natural fit for the ``EthereumJS`` team to take on the 
high-level part of the ``AssemblyScript`` work (in contrast to the low-level
task to secure ``AssemblyScript`` to ``eWASM`` compatibility) due to the 
familiarity with the language and the close relationship with the eWASM team.

.. _roadmap_r193_ewasm_vm:

R19-3 eWASM Kernel VM
---------------------

In a not-too-distant future the current Ethereum Virtual Machine (EVM) will
at least gradually and eventually completely be replaced with an 
`eWASM <https://github.com/ewasm>`_ virtual machine.

For this to be prepared the execution engine/kernel of the ``EthereumJS``
`VM implementation <https://github.com/ethereumjs/ethereumjs-vm>`_ needs to be
modularized to allow for a pluggable exchange with a new ``eWASM`` engine.
On top of this work bindings have to be created to allow communication with
the execution engine implemented by the ``eWASM`` team.


.. _roadmap_finished:

Finished Projects
=================

Move projects here once finished (with some note on the outcome).


.. _roadmap_canceled:

Canceled Projects
=================

Move canceled projects here (with some notes on in-between outcome and
cancellation reason).

