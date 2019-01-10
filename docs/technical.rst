.. _technical_reference:

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

====================== ================= ===============================
Node Version           Status            Latest Status Change
====================== ================= ===============================
Node.js 8              Supported         2018-11-01
Node.js 10             Supported         2018-11-01
====================== ================= ===============================

Node.js Features
^^^^^^^^^^^^^^^^

Buffer vs safe-buffer
"""""""""""""""""""""
Old Node versions up to versions ``4`` and ``5`` allowed for some unsafe usage
of the ``Buffer`` API which led to the development of a replacement 
`safe-buffer <https://github.com/feross/safe-buffer>`_ library. We have now for
some time dropped support for distibution on all affected Node versions (mainly
``4``) and usage of ``safe-buffer`` is not needed any more.

.. note::
   The ``safe-buffer`` is still in 
   use `on many libraries <https://github.com/search?q=org%3Aethereumjs+safe-buffer&type=Code>`_,
   this should be removed and updated with direct ``Buffer`` usage.

Node.js Best Practices
^^^^^^^^^^^^^^^^^^^^^^

Currently agreed-upon best practices on Node.js development:

- Do not use lock files (``package-lock.json``) on repositories 
  (instead add to ``.gitignore``), see 
  `this <https://github.com/ethereumjs/merkle-patricia-tree/pull/62>`_ discussion


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

Node.js Version
---------------

The following table gives an overview on supported Node versions for distribution:

====================== ================= ===============================
Node Version           Status            Latest Status Change
====================== ================= ===============================
Node.js 4              Dropped           2018-10-01
Node.js 6              Supported         2018-10-01
Node.js 8              Supported         2018-11-01
Node.js 10             In the works      2018-12-01
====================== ================= ===============================


Browser Compatibility
---------------------

``TODO``


Releases
--------

Releases on libraries follow `Semantic Versioning <https://semver.org/>`_, 
normally releases are published on `npm <https://www.npmjs.com/>`_ and as
a tagged release on GitHub in the ``Releases`` section.

Every library contains a ``CHANGELOG.md`` file in the root directory,
listing the changes on the respective release versions (see e.g. 
`CHANGELOG.md <https://github.com/ethereumjs/ethereumjs-util/blob/master/CHANGELOG.md>`_
of the ``ethereumjs-util`` library), the changelog entry is copied to the
GitHub release section on publication of a new release.

Releases go through a PR (see `example PR <https://github.com/ethereumjs/ethereumjs-util/pull/155/files>` 
on ``ethereumjs-util`` ``v6.0.0`` release), containing the ``package.json``
version number update, a new CHANGELOG entry and eventually some update on the
docs.


.. _git_workflow:

Git Workflow
============

.. _branching_model:

Branching Model
---------------

We are using a feature-centric branching model, the 
`GitHub flow <https://guides.github.com/introduction/flow/>`_ model is coming 
very much close.

Development of new features is taking place on a dedicated branch and should 
have some descriptive name for the work done (e.g. ``api-doc-fixes``, 
``remove-vm-accesses-to-statemanager-trie-cache``, ``new-bloom-filter-tests``).

Once work on the feature branch is completed and all tests and checks from CI
(see :ref:`continuous_integration`) pass it goes through a review and eventually
discussion process and is afterwards merged into a protected ``master`` branch. 
The ``master`` branch should always be stable and theoretically ready for deployment.

.. _git_guidelines:

Git Guidelines
--------------

Some guidelines for the ``EthereumJS`` libraries when working with ``Git``
version control:

Feature branch for all PRs
^^^^^^^^^^^^^^^^^^^^^^^^^^
Always do your work on a separate feature branch (see :ref:`branching_model`),
this also applies when doing work from an own fork of a library.

This makes it easier for reviewers and others interested to test your code
locally by fetching your code changes from your remote feature branch.

Separate PRs for separate Features
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
If you have separate things you want to change on a library, do separate PRs
for this. So if you e.g. have some ideas for how to improve the build process and
want to fix some bug from an issue, theses are two separate PRs.

This is a precondition for a successful review of a PR, since a reviewer has
a smaller subset of changes and can connect changes undoubtfully to a certain feature.
It also avoids the situation where unexpected discussions and disagreements
on a certain subfeature set blocks the whole PR with all other changes.

Meaningful Commit History
^^^^^^^^^^^^^^^^^^^^^^^^^
Make sure that you end up with a meaningful commit history on your work:

- Choose self-descriptive commit messages
- Avoid inconsistent state between commits
- If you do changes correcting your prior committed work, rebase and squash commits afterwards

.. note::
   Rebasing can be a hairy process, if you do for the first time it is highly
   recommended to do a local backup of your repository.

.. note::
   Rebase work like the above can normally be done with ``git rebase -i master``
   from the feature branch with an up-to-date ``master`` branch.

Regular Master Rebase
^^^^^^^^^^^^^^^^^^^^^
PRs are only reviewed if the branch is up-to-date on the latest ``master`` changes.
Rebase your branch often (with ``git rebase master``) and force-push the changes,
to make sure that your changes work well on top of the latest commits and tests
keep passing.

.. _workflow_best_practices:

Workflow Best Practices
-----------------------

Some best practices which turned out to be practical over time and should be
followed when working on a new feature:

In doubt: Issue before PR
^^^^^^^^^^^^^^^^^^^^^^^^^
If you are planning on introducing major feature changes on a library file an
issue and describe what you are up to before directly work on a PR. This gives
others the chance to discuss around your intended changes and avoids potential
further conflicts along the road.

This especially applies for stuff like:

- Introducing new language features (``Promises``,...)
- Changing the API of a library
- Planning security-sensitive changes
- Switch or introduce new tooling

Describe your Work
^^^^^^^^^^^^^^^^^^
Take some time to make both the scope of your work and your work process transparent
for others. This will ease both discussions and the review process around the
work being done.

In particular:

- Do a proper and complete task description on your issue or PR
- Give some regular updates on the current status of your work
- Especially: drop a note once you are ready


Pull Request Reviews
--------------------

All PRs making changes to the production code base are going through a review
process. This will normally take some time and will come along with some
back-and-forth between contributor and reviewer until everyone is happy.

Code Quality
============

.. _testing:

Testing
-------

Test Framework
^^^^^^^^^^^^^^

Most ``EthereumJS`` libaries use `tape <https://github.com/substack/tape>`_ 
for running tests. Have a look at one of the libraries (e.g.
`merkle-patricia-tree <https://github.com/ethereumjs/merkle-patricia-tree>`_)
for reference.

.. note::
   It should be examined if this is a good choice and eventually
   `Mocha <https://mochajs.org/>`_ should be preferred, see e.g. 
   `this comparison <https://www.slant.co/versus/12696/12698/~mocha_vs_tape>`_.

Code Coverage
^^^^^^^^^^^^^

For coverage runs `nyc <https://istanbul.js.org/>`_ is used. Results are passed on
to the `coveralls.io <https://coveralls.io/>`_ service for coverage reports on
CI runs.

.. note::
   If you stumble over libraries still using ``istanbul`` as a coverage runner,
   do an update to ``nyc``!

.. _documentation:

Documentation
-------------

Libraries come with an API documentation generated automatically from comments
in the code. The actual tool and standard for generating API documentation differs
for JavaScript and TypeScript projects.

Apart from that, the following documentation should be kept up-to-date:

- ``README`` with setup and installation instructions
- Usage instructions, up-to-date code examples

JavaScript
^^^^^^^^^^^^^

In many of the JavaScript libraries `documentation.js <https://documentation.js.org/>`_ is used
for generating an API documentation from `JSDoc <http://usejsdoc.org/>`_
comments.

TypeScript
^^^^^^^^^^^^^

To generate API documentation for a TypeScript project, `TypeDoc <https://github.com/TypeStrong/typedoc>`_ is employed.
By default, TypeDoc generates HTML documentation. In order to generate Markdown suitable for GitHub, the
`typedoc-plugin-markdown <https://github.com/tgreyuk/typedoc-plugin-markdown>`_ can be used as a theme for TypeDoc.

.. _continuous_integration:

Continuous Integration (CI)
---------------------------

Most ``EthereumJS`` libraries use `Travis CI <https://travis-ci.org/>` for CI
runs on every PR submitted. Have a look at a ``.travis.yml`` file in the 
repository you are interested in to get an overview on what is run during the
CI process.

One exception is the EthereumJS VM which is using ``CircleCI`` as a platform
for performance reasons.

Security
========

Security aspects around the EthereumJS libraries should be taken seriously,
since many of the libraries are used in production in security-sensitive
environments.

.. _dependency_management:

Dependency Management
---------------------

Dependencies are a main source for also importing security vulnerabilities on a
library, so the set of dependencies on the libraries should be actively managed
and regularly reviewed.

Some guidelines:

Minimal Dependencies
^^^^^^^^^^^^^^^^^^^^
Every introduction of a new dependency on a library should be carefully considered
and there has to be solid argument why a new dependency is necessary. This primarily
applies for production but also for development dependencies. Dependencies listed
in ``package.json`` should be reviewed on a regular basis if they are still
necessary or could be removed.


Established and maintained Dependencies
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Only (somewhat) established and actively maintained dependencies should be 
used on the libraries. Some indicators for a not-so-established dependency:

- Low number of ``GitHub`` stars or a similar metric
- No commit activity for a longer period of time
- Low download rate on ``npm``

Regular Dependency Updates
^^^^^^^^^^^^^^^^^^^^^^^^^^
Dependency versions should be updated on a regular basis, this is also very
welcome to be done as a ``first-time-contributor`` PR. Don't underestimate
this task though, since a dependency update almost always come along with some
necessary changes on a library. It is recommended to always only do one
dependency at a time, since it becomes easier to attribute if things break at
some point.

.. _shared_libs:

Shared Library Ressources
=========================

The following libraries set up some shared infrastructure for certain purposes.

.. _shared_libs_testing:

ethereumjs-testing
------------------

The `ethereumjs-testing <https://github.com/ethereumjs/ethereumjs-testing>`_
library is a proxy library for the common `Ethereum Tests <https://github.com/ethereum/tests>_`
consensus tests. There are additional methods for easily select a specific
subset of the tests.

The common test library is integrated as a submodule and there are tagged
releases (no publishing to ``npm`` due to size constraints) which can be used 
for running the latest tests in ``JavaScript`` libraries.

.. _shared_libs_common:

ethereumjs-common
-----------------

The `ethereumjs-common` library provides access to chain and hardfork specific
parameters as well as utilities to easier manage hardfork-specific logic 
within other ``EthereumJS`` libraries.

.. _shared_libs_config:

ethereumjs-config
-----------------

``[IN DEVELOPMENT]``

The `ethereumjs-config <https://github.com/ethereumjs/ethereumjs-config>`_ library
aims to reduce redundancy on library configuration by providing a unified set
of configuration options (e.g. on linting or code formatting) which can be integrated
within other libraries.

