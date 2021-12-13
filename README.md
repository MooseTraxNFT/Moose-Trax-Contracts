# Moose Trax Contracts

This repo contains all of the contracts deployed for [Moose Trax](https://app.moosetrax.art/#/) releases.

There are two main releases:
1. [Moose Trax](https://opensea.io/collection/moose-trax-nft): A collection of 10,000 unique Moose themed profile pictures. Each NFT has it's metadata stored on-chain. The image is created by decoding this metadata and generating an SVG object.
1. [CustoMoose](https://opensea.io/collection/moose-trax-customoose): A collection of customizable Moose themed collectibles. Users hand-select traits to add to a $FRAME token.

## Moose Trax

Contracts:
* [Library.sol](./contracts/Library.sol): Function library for Moose contract
* [Moose.sol](./contracts/Moose.sol): An ERC721 contract forked from Anonymice that produces on-chain SVG from stored data.
* [Trax.sol](./contracts/Trax.sol): An ERC20 token that supports staking an ERC721 token (MOOSE) for ERC20 rewards (TRAX)

Notes:
* Moose Trax is a fork of Anonymice's SVG generation and staking contracts using original artwork.
