.. _roadmap:

=======
Roadmap
=======

.. _roadmap_r181_typescript:

R18-1 Transition to TypeScript
==============================

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
--------

- ``November 2018``

  - ✅ Ad-hoc team, tooling discussion, kick-off at Devcon4
  
- ``December 2018``

  - 🛠️ First reference implementation (`RLP library <https://github.com/ethereumjs/rlp/pull/37>`_)
  - 🛠️ Toolchain best practices draft
  
- ``February 2019``

  - ⭕ Three more completed transitions, stable toolchain
  
- ``May 2019``

  - ⭕ All major transitions completed including ``VM``, ``merkle-patricia-tree``

R18-2 EthereumJS Client
=======================

Being very-much late to the party, we have finally started the development of a 
dedicated EthereumJS client with fast- and light-sync support. Development started 
in June 2018 on https://github.com/ethereumjs/ethereumjs-client and reactions 
from the community have been extremely positive with a wide range of reception 
and development contribution on a high-quality level. With Vinay Pulim we have 
found a very talented JavaScript developer who will take the lead on this project.

Due to limitations of the JavaScript language this is not targeted to be a 
consensus-critical client implementation but serve for various use cases coming 
with the popularity of the JavaScript language in general and its specific role on the web like:

- In-Browser light client (Metamask without Infura)
- In-Browser education applications
- In-Browser/NodeJS client simulations and visualizations
- In-Browser/NodeJS research & development (Sharding, Casper,...) mainly supported by a modular and expendable (plugins) architecture

Generally the EthereumJS client project has larger similarities with the scope of
the Trinity project of the Python team. Since JavaScript (like Python) is an extremely
popular and widely used language, this will draw in a whole new class of developers
who were not able to experiment with and develop on Ethereum client technologies before.

One side goal being nevertheless important is finally to use the client development
as a proxy to “harden” the other EthereumJS libraries against a real production 
environment and serve as a better foundation for testing for our Virtual Machine
implementation.

The client project will also build a solid foundation for continued internal research
and development efforts. We plan to include new communication layer technologies
in an exchangeable way - central will be support for Whisper (SHH) message communication
and libp2p network topology, which will allow to contribute to various communication
experiments and research on the way to a future sharded Ethereum network. Development
in this direction is already in progress (libp2p).

At a later point it is also be desired to have a dedicated website for the client
(similar to https://geth.ethereum.org/) to have a more visible entry point and source
for information around the client for the community.

.. note::
   
   - ``TODO`` Rework project summary text to reflext latest view on project
   - ``TODO`` Develop a combined strategy / consider synergies with ``ShasperJS`` project
   - ``TODO`` Develop an idea on synergies, demarcations and separate focus, emphasis regarding MetaMask `Mustekala <https://github.com/MetaMask/mustekala>`_ client project

Timeline
--------

- ``Q3 2018``

  - ✅ Proof-of-concept chain sync (fast and light)
  - ✅ Libp2p networking and browser support

- ``Q4 2018``

  - 🛠️ Reliable mainnet chain sync (fast and light) including block validation 
  - ⭕ Test setup on hive 

- ``Q2 2018``

  - ⭕ Alpha release of client
  - ⭕ Proof-of-concept Ethereum 2.0 stateless client
  
R18-3 ShasperJS
================

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
   
   - ``TODO`` Rework project summary text to reflext latest view on project
   - ``TODO`` Eventually rename
   - ``TODO`` Develop a combined strategy / consider synergies with ``EthereumJS Client`` project
   - ``TODO`` Some roadmap


R18-4 AssemblyScript (eWASM)
============================

``TODO``

Figure out together with the ``eWASM`` team what could be a shared ground on
progressing on `AssemblyScript <https://github.com/AssemblyScript/assemblyscript>`_.


