+++
title = 'Introducing solidity-analyzer'
date = 2023-08-01T00:00:00
draft = false
type = 'posts'
summary = 'I have been working on a new solidity LSP called [`solidity-analyzer`](https://github.com/parmanuxyz/solidity-analyzer) for a couple weeks now. It is written in rust and utilizes [`ethers-solc`](https://github.com/gakonst/ethers-rs), [`foundry-fmt`](https://github.com/foundry-rs/foundry) and [`solang-parser`](https://github.com/hyperledger/solang/blob/main/solang-parser/) ...'
tags = ["solidity-analyzer", "solidity", "LSP", "ethereum"]
+++

I have been working on a new solidity LSP called [`solidity-analyzer`](https://github.com/parmanuxyz/solidity-analyzer) for a couple weeks now. It is written in rust and utilizes [`ethers-solc`](https://github.com/gakonst/ethers-rs), [`foundry-fmt`](https://github.com/foundry-rs/foundry) and [`solang-parser`](https://github.com/hyperledger/solang/blob/main/solang-parser/) as the main packages ATM. Immediate goal for me was to get the compiler errors and warnings highlighted into the editor itself. Never worked for me with any of the existing extensions.

Main features that are developed and currently working are:

1. Diagnostics from solc i.e. compiler errors, warnings, information, etc. It uses `ethers-solc` for compiling the projects and assumes the default standard dapptools project structure. Will be updating it to use the `foundry.toml` configs for compiler options.
2. Code formatting with `forge-fmt` using the user foundry configs.
3. Document symbols aka outline using `solang-parser`.

I will be working on this on the side with the final goal being improved devex for foundry projects and maybe even support hardhat projects too at the same level foundry supports hardhat projects.

I would like to hear what features people are interested in that does not exist or can work better in existing extensions and LSPs and prioritize accordingly. Contact me with any of the mediums mentioned on the sidebar or reply here with suggestions, feature requests or any questions. Alternatively can even create a [github discussion on the repo](https://github.com/parmanuxyz/solidity-analyzer/discussions).

Right now will be focusing on getting base level features done and work on performance and optimizations along the way.

