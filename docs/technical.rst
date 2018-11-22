===================
Technical Reference
===================

This guide gives an overview on common practices and technical standards
shared within the ``EthereumJS`` ecosystem.

Source Code
===========

Development Runtime
-------------------

Node.js Version
^^^^^^^^^^^^^^^

Runtime environment for development is `node.js <https://nodejs.org/en/>`_.

Development should always be possible running the last two ``LTS`` Node.js versions,
see Node.js `release schedule table <https://github.com/nodejs/Release#release-schedule>`_.

====================== =================================================
Node.js 8              Supported
Node.js 10             Supported
====================== =================================================

Node.js Features
^^^^^^^^^^^^^^^^

``TODO``

Notes on ``Buffer``, ``safe-buffer``, stuff like that.

Programming Language
--------------------

We use both `JavaScript <https://www.w3schools.com/js/>`_ and 
`TypeScript <https://www.typescriptlang.org/>`_ in our libraries, with a 
transition of libraries to ``TypeScript`` on the way (see: :ref:`roadmap_r181_typescript`).

All libraries are transpiled to a lower common denominator JavaScript version
(see section below), this section describes what language features are safe to
be used in the non-transpiled source code of the libraries.

Main aspects to consider when choosing language version and features for 
the development code base are:

- ``Node.js`` compatibility (see also: `node.green <https://node.green/>`_ Website)
- Support by transpilation tools in-use

.. note::
   Not all libraries have transpilation included, have a closer look along
   when using new language features!

JavaScript
^^^^^^^^^^

Features supported, encouraged and discouraged from the different ``JavaScript`` versions:

- `ES5 <https://www.w3schools.com/js/js_es5.asp>`_
  
  - All features supported

- `ES6 / ES2015 <http://es6-features.org>`_

  - All features supported
  - Usage of ``let``, ``const`` encouraged
  - Transition to ES6 ``classes`` encouraged

- `ES2016 (ES7) <https://medium.freecodecamp.org/ecmascript-2016-es7-features-86903c5cab70>`_

  - ``TODO``

- `ES2017 (ES8) <https://hackernoon.com/es8-was-released-and-here-are-its-main-new-features-ee9c394adf66>`_

  - ``TODO``

.. note::
   This table does not aim to be complete but just wants to hint to the practically
   most common pitfall cases!


TypeScript
^^^^^^^^^^

``TODO``


Linting and Formatting
----------------------

JavaScript
^^^^^^^^^^

All ``EthereumJS`` ``JavaScript`` libraries use `standard.js <https://standardjs.com/>`_
for code formatting and linting with no extra configuration files added or 
rules adopted, see the `VM repository <https://github.com/ethereumjs/ethereumjs-vm>`_
as an example.

The ``standard`` dependency in the ``devDependencies`` section of ``package.json``
should be upgraded on a regular basis. Count in some time for this, since this
normally goes along with some code changes necessary through the introduction
of new rules.

Linting can be triggered on the different libraries with an ``npm run lint`` command
being added to ``package.json``.

.. note::
   For convenience a ``lint:fix`` command should be added to the various library
   ``package.json`` files.

TypeScript
^^^^^^^^^^

``TypeScript`` libraries are using `TSLint <https://palantir.github.io/tslint/>`_
for linting and `Prettier <https://prettier.io/>`_ for code formatting. See the
`RLP <https://github.com/ethereumjs/rlp>`_ library for a first example (changes might
still be located in TypeScript transition PR `#37 <https://github.com/ethereumjs/rlp/pull/37>`_).

.. note::
   It is intended to integrate both linting and formatting config into a shared
   `ethereumjs-config <https://github.com/ethereumjs/ethereumjs-config>`_ library
   (see: :ref:`shared_libs_config`), this effort is still ongoing.

Distribution
============

Transpilation
-------------

Current transpilation target: ``ES5``-compatible ``JavaScript`` code

JavaScript
^^^^^^^^^^

For ``JavaScript`` libraries, `Babel <https://babeljs.io/>`_ is used for 
transpilation, probably the most up-to-date example can be found in the
`merkle-patricia-tree <https://github.com/ethereumjs/merkle-patricia-tree>`_
library.

.. note::
   ``TODO``: This section has to be expanded.

TypeScript
^^^^^^^^^^

For ``TypeScript`` libraries, transpilation is done through the ``TypeScript``
compiler ``tsc`` command line tool.

.. note::
   ``TODO``: This section has to be expanded.

Browser Compatibility
---------------------

``TODO``


Releases
--------



Version Control
===============

Git

Branching Model
---------------


Pull Requests
-------------




Code Quality
============

Testing
-------


Continuous Integration (CI)
---------------------------


Documentation
-------------

.. _shared_libs:

Shared Library Ressources
=========================


.. _shared_libs_testing:

ethereumjs-testing
------------------


.. _shared_libs_common:

ethereumjs-common
-----------------


.. _shared_libs_config:

ethereumjs-config
-----------------



