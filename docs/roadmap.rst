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

- ``November 2018``: Ad-hoc team, tooling discussion, kick-off at Devcon4
- ``December 2018``: First reference implementation (`RLP library <https://github.com/ethereumjs/rlp/pull/37>`_), toolchain best practices draft
- ``February 2019``: Three more completed transitions, stable toolchain
- ``May 2019``: All major transitions completed, including ``VM``, ``merkle-patricia-tree`` libraries

R18-2 EthereumJS Client
=======================

TODO

Timeline
--------

TODO
  
R18-3 ShasperJS
================

TODO


R18-4 AssemblyScript (eWASM)
============================

TODO
