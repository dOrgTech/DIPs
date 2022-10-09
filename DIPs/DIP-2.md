---
dip: 2
title: Passport
description:
discussions-to: <!-- link to the forum or github issue? -->
status: Draft
created: 9 Oct 2022
---

## Abstract

The passport is the members "key to the DAO". The passport is the member's "key to the DAO". It can be used to prove a member's status and membership in the DAO. It is also the index key for referring to members (instead of referring to a member as an address).

## Requirements

- The DAO should be able to transfer the Passport (burn or move).
- The Passport should show up as an NFT in wallets and other "NFT explorers".
- The Passport should not be sellable.

## Specification

The Passport is implemented using the ERC721 standard with the the following changes (not exhaustive):

- The transfer functions are guarded by the `onlyOwner` modifier. This means that only the Avatar can call the basic transfer functions.
- A `mint(to)` function is added. This can only be called by the Avatar (owner). This will create a new Passport and set the to address as the owner.
- A `batchMint(toArray)` function is added. This can only be called by the Avatar (owner). This will create new Passports and set the toArray addresses as the owners.
- A `initiateTransfer(passportId, to)` function is added. This can be called by the owner of the corresponding Passport. To initiate the process of changing the address owning the Passport.
- A `finalizeTransfer(passportId, to)` function is added. This can be called a week (a specific number of blocks) after the `initiateTransfer` function to finalize the transfer. This functionality makes it possible for a Passport holder to move it to another address without the Avatar having to intervene. However, in the case of an unauthorized move (for instance, if it is soled), the Avatar has time to call the `forceTransfer` function before the transfer.
- A `forceTransfer(passportId, to)` function that can only be called by the Avatar. This can move any Passport to any address.
- A `burn(passportId)` function that can only be called by the Avatar. This will burn a Passport.
- A `updateBaseUri(string)` function for setting the base resolution path for updating for instance a Subgraph endpoint that serves the NFT metadata complying with the ERC721 spec (for us to specify how it should show up in "NFT explorers").
