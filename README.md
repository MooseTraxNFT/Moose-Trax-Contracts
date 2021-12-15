# Moose Trax Contracts

This repo contains all of the contracts deployed for [Moose Trax](https://app.moosetrax.art/#/) releases.

There are two main releases:
1. [Moose Trax](https://opensea.io/collection/moose-trax-nft): A collection of 10,000 unique Moose themed profile pictures. Each NFT has it's metadata stored on-chain. The image is created by decoding this metadata and generating an SVG object.
1. [CustoMoose](https://opensea.io/collection/moose-trax-customoose): A collection of customizable Moose themed collectibles. Users hand-select traits to add to a $FRAME token.

## Moose Trax ([$MOOSE](https://etherscan.io/address/0x3146dd9c200421a9c7d7b67bd1b75ba3e2c15310) + [$TRAX](https://etherscan.io/address/0xc92e730eebaca3d16d6c17f7f4646dce923663e8))

Moose Trax OG is a collection of 10,000 unique and randomly generated on-chain avatars. The contract uses staking and burning mechanics during the mint. The first 2000 Moose cost ETH to mint. The remaining 8000 Moose require an increasing amount of TRAX tokens to mint, or a Moose can be burned to mint another. The burning mechanic allows "re-rolling" for more rare traits as well as reducing overall supply when the mint is complete.

Contracts:
* [Library.sol](./contracts/Library.sol): Function library for Moose contract
* [Moose.sol](./contracts/Moose.sol): An ERC721 contract forked from Anonymice that produces on-chain SVG from stored data.
* [Trax.sol](./contracts/Trax.sol): An ERC20 token that supports staking an ERC721 token (MOOSE) for ERC20 rewards (TRAX)

About:
* Moose Trax is a fork of Anonymice's SVG generation and staking contracts using original artwork
* Each Moose is randomly generated at mint time
* Each Moose is made up of 7 visual traits and 1 "burned" trait
* Each Moose is unique from every other Moose
* A Moose can be staked on the TRAX ERC20 contract to receive 1 TRAX per day per staked Moose
  * These rewards are used by the CustoMoose collection to pay for minting trait customization
* Contract supports 8 layers, but can be expanded easily

Encoding:
* Each trait is stored by the ERC721 contract as an encoded string of pixel locations and colors
  * The encoding is in the following format: `[y for y coordinate][x for x coordinate][cc for color][yxcc][yxcc]...`
  * `x` and `y` values are stored as a single character
  * Example: `id50jc51je52kc51ke51lc50le50mc50me50nc50ne50oc51oe51pc52pd18pe51qd58`
* Traits are added to the contract in transactions after deployment of the ERC721 contract

## CustoMoose ([$FRAME](https://etherscan.io/address/0xc91D89828Cd0d635d0475eC6785c497dC1bF240F))

CustoMoose is a collection of 10,000 customizable FRAME tokens. FRAME tokens are customized with traits using the Moose Trax dapp.

Contracts:
* [TraitLibrary.sol](./contracts/TraitLibrary.sol): This contract simply stores trait prices and encodings, and has functions to retrieve them from storage.
* [Customoose.sol](./contracts/Customoose.sol): An ERC721 contract that decodes text strings from TraitLibrary into SVG images.
* [BytesLib.sol](./contracts/BytesLib.sol): A gas-efficient library of byte array utils ([source](https://github.com/GNSPS/solidity-bytes-utils/blob/master/contracts/BytesLib.sol))

About:
* Each $FRAME token is a fully mutable and customizable NFT created from metadata stored on-chain
* Holders can visit the Moose Trax dapp to swap out traits, using their staking rewards from Moose Trax OG as payment
* Traits are stored on a contract separate from the ERC721 contract. This allows for future composability, as these encodings can be reused by future contracts

Encoding:
* The pixel encoding in this contract is significantly improved compared to Moose Trax OG in both compression and storage
* Traits are compressed by combining similarly colored pixels places in a row or column using a proprietary compression technique
  * The encoding is in the following format: `[r or c for row or column][ccc for color][x for x coordinate][y for y coordinate][l for length][xyl][xyl][xyl]|[ccc][xyl]...`
  * `x`, `y`, and `l` values are stored as a single character using values retrieved from BytesLib
  * This encoding reduces the encoded string length by up to 90% in some cases
  * Example: `c2918m09n0am0ao0bn0bp0co0|3146h1`
