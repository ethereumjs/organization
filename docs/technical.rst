.. _technical_reference:

===================
Technical Reference
===================

This guide gives an overview on common practices and technical standards
shared within the ``EthereumJS`` ecosystem.

Development
===========

Node.js
-------

Development Version
^^^^^^^^^^^^^^^^^^^

Runtime environment for development is `node.js <https://nodejs.org/en/>`_.

Development should always be possible running latest ``LTS`` Node.js version,
see Node.js `release schedule table <https://github.com/nodejs/Release#release-schedule>`_.

====================== ================= ===============================
Node Version           Status            Latest Status Change
====================== ================= ===============================
Node.js 12              Supported         2020-10-19
====================== ================= ===============================

package-lock Files
^^^^^^^^^^^^^^^^^^

**Standalone Libraries**

Do not use lock files (``package-lock.json``) on repositories 
(instead add to ``.gitignore``), see 
`this <https://github.com/ethereumjs/merkle-patricia-tree/pull/62>`_ discussion

**Monorepo**

Since we use hoisting, all package node_modules are brought to the root, so the packages
do not need package-locks anymore. the only exception is vm which is using one version 
prior of nyc for a compatibility issue, which may be resolved in the future.

(latest state taken from `this <https://github.com/ethereumjs/ethereumjs-vm/pull/861#issue-480572588>`_
PR comment.


JavaScript
----------

All libraries are transpiled to a lower common denominator JavaScript version
(see section below), this section describes what language features are agreed upon to be
be used in the non-transpiled source code of the libraries.


Supported Versions
^^^^^^^^^^^^^^^^^^

Features from the following ``JavaScript`` version standards are safe to be used:

- `ES5 <https://www.w3schools.com/js/js_es5.asp>`_
- `ES6 / ES2015 <http://es6-features.org>`_

Partially Supported Versions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Be careful when using language features from the following ``JavaScript`` standards:

- `ES2016 (ES7) <https://medium.freecodecamp.org/ecmascript-2016-es7-features-86903c5cab70>`_
- `ES2017 (ES8) <https://hackernoon.com/es8-was-released-and-here-are-its-main-new-features-ee9c394adf66>`_
- Beyond

Feature Notes
^^^^^^^^^^^^^

**BigInt**

``BigInt`` support is an often requested feature within the ``EthereumJS`` ecosystem and
we are constantly re-evaluating usage. Current discussion state is that we are not quite there
on the browser/runtime support side yet to integrate in the libraries, see e.g.
`Can I use bigint? <https://caniuse.com/bigint>`_ page for context.

We are getting close though, so if you feel a pressing need here it might be worth to re-trigger
the discussion.

TypeScript
----------

All the major **EthereumJS** libraries use `TypeScript <https://www.typescriptlang.org/>`_,

``TypeScript`` version and configuration is centrally managed in the ``ethereumjs-config``
`typescript <https://github.com/ethereumjs/ethereumjs-config/tree/master/packages/typescript>`_
package.

Linting and Formatting
----------------------

Linting and formatting of package source code can be triggered on the different libraries 
with an ``npm run lint`` respectively a ``npm run lint:fix`` command from ``package.json``.

Tool usage and configuration is centrally managed in the ``ethereumjs-config``
`lint <https://github.com/ethereumjs/ethereumjs-config/tree/master/packages/lint>`_
package.

Distribution
============

Transpilation Targets
---------------------

For ``TypeScript`` libraries, transpilation is done through the ``TypeScript``
compiler ``tsc`` command line tool.

See the ``ethereumjs-config``
`typescript <https://github.com/ethereumjs/ethereumjs-config/tree/master/packages/typescript>`_
``tsconfig.*.json`` files for an overview on transpilation targets.

Node.js Distribution Versions
-----------------------------

The following table gives an overview on the targeted Node.js version support:

====================== ================= ===============================
Node Version           Status            Latest Status Change
====================== ================= ===============================
Node.js 4              Dropped           2018-10-01
Node.js 6              Dropped           2019-02-19
Node.js 8              Dropped           2020-01-29
Node.js 10             Supported         2020-03-01
Node.js 12             Supported         2019-06-01
Node.js 13             Partly Supported  2020-10-19
Node.js 14             Mostly Untested   2020-10-19
====================== ================= ===============================

For a concrete overview on supported Node.js versions have a look at the 
``GitHub Actions`` CI setup within the ``.github`` folder of a repository,
see `build.yml <https://github.com/ethereumjs/merkle-patricia-tree/blob/master/.github/workflows/build.yml>`_
as an example from the ``merkle-patricia-tree`` library.

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

Feature Branch for All PRs
^^^^^^^^^^^^^^^^^^^^^^^^^^
Always do your work on a separate feature branch (see :ref:`branching_model`),
this also applies when doing work from an own fork of a library.

This makes it easier for reviewers and others interested to test your code
locally by fetching your code changes from your remote feature branch.

Separate PRs for Separate Features
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
If you have separate things you want to change on a library, do separate PRs
for this. So if you e.g. have some ideas for how to improve the build process and
want to fix some bug from an issue, theses are two separate PRs.

This is a precondition for a successful review of a PR, since a reviewer has
a smaller subset of changes and can connect changes definitively to a certain feature.
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

Most ``EthereumJS`` libraries use `tape <https://github.com/substack/tape>`_
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

Shared Library Resources
=========================

The following libraries set up some shared infrastructure for certain purposes.

.. _shared_libs_testing:

ethereumjs-testing
------------------

The `ethereumjs-testing <https://github.com/ethereumjs/ethereumjs-testing>`_
library is a proxy library for the common `Ethereum Tests <https://github.com/ethereum/tests>`_
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

