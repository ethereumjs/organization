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

  - ✅ First reference implementation (`RLP library <https://github.com/ethereumjs/rlp/pull/37>`_)
  - ✅ Toolchain best practices draft (new `ethereumjs-config <https://github.com/ethereumjs/ethereumjs-config>`_ library)

- ``February 2019``

  - ✅  Three+ more completed transitions (``acount``, ``util``, ``common``)
  - ✅  Stable toolchain, ``ethereumjs-config`` ``v1.1.0`` release
  - ✅  TypeScript preparation for ``VM``, ``merkle-patricia-tree`` library (code modernization, ``ES6``)

- ``March 2019``

  - 🛠️ ``merkle-patricia-tree`` TypeScript release
  - 🛠️  More toolchain automations (candidates: tests, docs)
  - 🛠️  1-2 other transitions

- ``April 2019``

  - 🛠️ ``VM`` ``v4.0`` TypeScript release
  - ⭕  1-2 other transitions

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

- ``Q1 2019``

  - ✅️ Reliable mainnet chain sync (fast and light)

- ``Q2 2019``

  - 🛠 Block validation
  - 🛠 Implement state downloading

- ``Q3 2019``

  - ⭕ Test setup on hive
  - ⭕ Determine Ethereum 2.0 strategy (ShasperJS collaboration? stateless client?)

- ``Q4 2019``

  - ⭕ Alpha release of client


.. _roadmap_r193_ewasm_vm:

R19-3 eWASM VM/Refactoring
--------------------------

`eWASM <https://github.com/ewasm/design>`_ is being seriously considered as an
alternative for the current Ethereum Virtual Machine (EVM) for Ethereum 2.0.
Parts of eWASM might get integrated into the current Ethereum mainnet as part
of the Eth 1.x roadmap.

As such, a major focus of the team is to provide tooling for eWASM and integrate
it into the Javascript `VM implementation <https://github.com/ethereumjs/ethereumjs-vm>`_
to facilitate eWASM research and prepare for when eWASM makes it to mainnet.

The current implementation is tightly coupled to EVM as the only VM. Therefore
part of this project is to refactor parts of ethereumjs-vm that are relevant
to the VM, to make them modular enough for eWASM to be integrated. This refactoring
is occuring hand-in-hand with the modernization effort.

Timeline
^^^^^^^^

- ``January 2019``

  - ✅  Started refactoring to prepare for future ewasm integration (`#424 <https://github.com/ethereumjs/ethereumjs-vm/pull/424>`_)
  - ✅  Open PR on basic support for ewasm precompiles (`#431 <https://github.com/ethereumjs/ethereumjs-vm/pull/431>`_)

- ``February 2019``

  - ✅  Refactored memory manipulation of EVM (`#442 <https://github.com/ethereumjs/ethereumjs-vm/pull/442>`_)
  - ✅  Replaced static vm logTable with dynamic inline version in EXP opcode (`#450 <https://github.com/ethereumjs/ethereumjs-vm/pull/450>`_)


- ``March 2019``

  - ✅  Refactor stack manipulation in EVM (`#460 <https://github.com/ethereumjs/ethereumjs-vm/pull/460>`_)
  - 🛠️ Refactor EVM execution logic, i.e. interpreter (`#441 <https://github.com/ethereumjs/ethereumjs-vm/pull/441>`_)
  - 🛠️ Design and refactor rest of EVM, including message execution (Also see `#455 <https://github.com/ethereumjs/ethereumjs-vm/issues/455>`_)

- ``April 2019``

  - 🛠️ Rebase EVM changes to the ewasm precompile PR, and merge
  - 🛠️ Experiment with solutions for the `sync/async problem <https://github.com/ewasm/design/blob/master/interface_questions.md#ewasm-interface-methods-synchronous-vs-asynchronous>`_


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


.. _roadmap_finished:

Finished Projects
=================

Move projects here once finished (with some note on the outcome).


.. _roadmap_canceled:

Canceled Projects
=================

Move canceled projects here (with some notes on in-between outcome and
cancellation reason).
