# Organization

A repo for discussions and other non-code organizing stuff.

## Introduction

This repository is for bundling communication around organization issues, common guidelines and project discussions.

Use the [issue tracker](https://github.com/ethereumjs/organization/issues) as a forum.
 
## Work Updates

Updates within the ``EthereumJS`` ecosystem - also posted on reddit on a monthly basis - can be found in the [posts](./posts/) folder.

Have a look at the list of [all current open issues](https://waffle.io/ethereumjs/organization) for an impression what is being worked on.

## Communication

Gitter channel for everyday communication:

[![Discord][discord-badge]][discord-link]

## Contribution Guidelines

TODO

### Labeling System

Within the EthereumJS repositories [git-labelmaker](https://github.com/himynameisdave/git-labelmaker) is used to maintain an organization-wide issue and PR labeling system. Definitions of labels for different categories can be found in the [labels](./labels/) folder. See the ``git-labelmaker`` repository for instructions on how to distribute (parts of) these labels to a new repository.

Inspirations for the labeling system:

* [Sane GitHub Labels](https://medium.com/@dave_lunny/sane-github-labels-c5d2e6004b63) article
* ``Py-EVM`` [issue](https://github.com/ethereum/py-evm/issues) and [PR](https://github.com/ethereum/py-evm/pulls) label system

### Documentation

Sources for documentation can be found in the [docs](./docs/) directory. Documentation is generated using the Python [Sphinx](http://www.sphinx-doc.org) documentation generator in ``v1.8.x`` using a Python ``3.6`` environment.

Documentation can be manually generated running ``make html`` from the ``docs`` directory.

[discord-badge]: https://img.shields.io/static/v1?logo=discord&label=discord&message=Join&color=blue
[discord-link]: https://discord.gg/TNwARpR
