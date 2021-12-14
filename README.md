# Moose Trax Contracts

This repo contains all of the contracts deployed for [Moose Trax](https://app.moosetrax.art/#/) releases.

There are two main releases:
1. [Moose Trax](https://opensea.io/collection/moose-trax-nft): A collection of 10,000 unique Moose themed profile pictures. Each NFT has it's metadata stored on-chain. The image is created by decoding this metadata and generating an SVG object.
1. [CustoMoose](https://opensea.io/collection/moose-trax-customoose): A collection of customizable Moose themed collectibles. Users hand-select traits to add to a $FRAME token.

## Moose Trax ($MOOSE + $TRAX)

Moose Trax OG is a collection of 10,000 unique and randomly generated on-chain avatars. The contract uses staking and burning mechanics during the mint. The first 2000 Moose cost ETH to mint. The remaining 8000 Moose require an increasing amount of TRAX tokens to mint, or a Moose can be burned to mint another. The burning mechanic allows "re-rolling" for more rare traits as well as reducing overall supply when the mint is complete.

Contracts:
* [Library.sol](./contracts/Library.sol): Function library for Moose contract
* [Moose.sol](./contracts/Moose.sol): An ERC721 contract forked from Anonymice that produces on-chain SVG from stored data.
* [Trax.sol](./contracts/Trax.sol): An ERC20 token that supports staking an ERC721 token (MOOSE) for ERC20 rewards (TRAX)

About:
* Moose Trax is a fork of Anonymice's SVG generation and staking contracts using original artwork
* Each Moose is randomly generated at mint time
* Each Moose has a unique set of traits
* A Moose can be staked on the TRAX ERC20 contract to receive 1 TRAX per day per staked Moose
  * These rewards are used by the CustoMoose collection to pay for minting trait customization
* Contract supports 8 layers, but can be expanded easily

Encoding:
* Each trait is stored by the ERC721 contract as an encoded string of pixel locations and colors
  * The encoding is in the following format: `[y for y coordinate][x for x coordinate][cc for color][yxcc][yxcc]...`
  * `x` and `y` values are stored as a single character
  * Example: `id50jc51je52kc51ke51lc50le50mc50me50nc50ne50oc51oe51pc52pd18pe51qd58`

## CustoMoose ($FRAME)

CustoMoose is a collection of 10,000 customizable FRAME tokens. FRAME tokens are customized with traits using the Moose Trax dapp.

Contracts:
* [TraitLibrary.sol](./contracts/TraitLibrary.sol): This contract simply stores traits and retrieves them. The ERC721 contract will reference this library to 
* [Customoose.sol](./contracts/Customoose.sol): An ERC721 contract that decodes text strings from TraitLibrary into SVG images on-chain.

About:
*

Encoding:
* 
