<h1 align="center">Block SDK 🧱</h1>

<!-- markdownlint-disable MD013 -->
<!-- markdownlint-disable MD041 -->
[![Project Status: Active – The project has reached a stable, usable state and is being actively developed.](https://www.repostatus.org/badges/latest/active.svg)](https://www.repostatus.org/#wip)
[![GoDoc](https://img.shields.io/badge/godoc-reference-blue?style=flat-square&logo=go)](https://godoc.org/github.com/skip-mev/pob)
[![Go Report Card](https://goreportcard.com/badge/github.com/skip-mev/pob?style=flat-square)](https://goreportcard.com/report/github.com/skip-mev/pob)
[![Version](https://img.shields.io/github/tag/skip-mev/pob.svg?style=flat-square)](https://github.com/skip-mev/pob/releases/latest)
[![License: Apache-2.0](https://img.shields.io/github/license/skip-mev/pob.svg?style=flat-square)](https://github.com/skip-mev/pob/blob/main/LICENSE)
[![Lines Of Code](https://img.shields.io/tokei/lines/github/skip-mev/pob?style=flat-square)](https://github.com/skip-mev/pob)

### 🤔 What is the Block SDK?

**🌐 The Block SDK is a toolkit for building customized blocks**. The Block SDK is a set of Cosmos SDK and ABCI++ primitives that allow chains to fully customize blocks to specific use cases. It turns your chain's blocks into a **`highway`** consisting of individual **`lanes`** with their own special functionality.


Skip has built out a number of plug-and-play `lanes` on the SDK that your protocol can use, including in-protocol MEV recapture and Oracles! Additionally, the Block SDK can be extended to add **your own custom `lanes`** to configure your blocks to exactly fit your application needs.

### ❌ Problems: Blocks are not Customizable

Most Cosmos chains today utilize standard `CometBFT` block construction - which is too limited.

* The standard `CometBFT` block building is susceptible to MEV-related issues, such as front-running and sandwich attacks, since proposers have monopolistic rights on ordering and no verification of good behavior. MEV that is created cannot be redistributed to the protocol.
* The standard `CometBFT` block building uses a one-size-fits-all approach, which can result in inefficient transaction processing for specific applications or use cases and sub-optimal fee markets.
* Transactions tailored for specific applications may need custom prioritization, ordering or validation rules that the mempool is otherwise unaware of because transactions within a block are currently in-differentiable when a blockchain might want them to be.

### ✅ Solution: The Block SDK

You can think of the Block SDK as a **transaction `highway` system**, where each
`lane` on the highway serves a specific purpose and has its own set of rules and
traffic flow.

In the Block SDK, each lane has its own set of rules and transaction flow management systems.

* A lane is what we might traditionally consider to be a standard mempool
  where transaction **_validation_**, **_ordering_** and **_prioritization_** for
  contained transactions are shared.
* lanes implement a **standard interface** that allows each individual lane to
  propose and validate a portion of a block.
* lanes are ordered with each other, configurable by developers. All lanes
  together define the desired block structure of a chain.

### ✨ Block SDK Use Cases

A block with separate `lanes` can be used for:

1. **MEV mitigation**: a top of block lane could be designed to create an in-protocol top-of-block auction (as we are doing with the Block SDK) to recapture MEV in a transparent and governable way.
2. **Free/reduced fee txs**: transactions with certain properties (e.g. from trusted accounts or performing encouraged actions) could leverage a free lane to reward behavior.
3. **Dedicated oracle space** Oracles could be included before other kinds of transactions to ensure that price updates occur first, and are not able to be sandwiched or manipulated.
4. **Orderflow auctions**: an OFA lane could be constructed such that order flow providers can have their submitted transactions bundled with specific backrunners, to guarantee MEV rewards are attributed back to users. Imagine MEV-share but in protocol.
5. **Enhanced and customizable privacy**: privacy-enhancing features could be introduced, such as threshold encrypted lanes, to protect user data and maintain privacy for specific use cases.
6. **Fee market improvements**: one or many fee markets - such as EIP-1559 - could be easily adopted for different lanes (potentially custom for certain dApps). Each smart contract/exchange could have its own fee market or auction for transaction ordering.
7. **Congestion management**: segmentation of transactions to lanes can help mitigate network congestion by capping usage of certain applications and tailoring fee markets.


### 📚 Block SDK Documentation

#### Lane App Store

To read more about Skip's pre-built `lanes` and how to use them, check out the [Lane App Store](https://docs.skip.money/chains/lanes/existing-lanes/default).

#### How the Block SDK works

To read more about how the Block SDK works, check out the [How it Works](https://docs.skip.money/chains/how-it-works).

#### Lane Development

To read more about how to build your own custom `lanes`, check out the [Build Your Own Lane](https://docs.skip.money/chains/lanes/build-your-own-lane).
