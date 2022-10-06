# dOrg on-chain

## Abstract

An unlimited extendable, and changeable DAO solution leveraging the Safe ecosystem.

The DAO solution proposed is not static; it is a continually evolving organism inhabiting the dark forest. Since nobody knows the future evolution of this organism, we aim for a solution that allows for maximum evolvement.

In addition to an initial starting point for the DAO, the dOrg Primitives, we propose the DAO/dOrg Improvement Proposals (DIP) standard. The DIP will support the DAO's continued evolvement in standardizing how we suggest changes to the DAO structure.

The suggested core dOrg Primitives are Passport, Main Safe, Project Safe, Project Safe Manager, and Payment Modules. These components forms a thin layer that can support the continued evolvement of the DAO. Components (even the core components) and modules can be removed, replaced, and new once added at any time in the form of a proposed transaction to the Main Safe (or for things specific to a Project Safe, the relevant Project Safe, not all Project Safes needs to be the same). This has the great advantage that non of the contracts will need to be upgradeable.

Also, as the DAO space evolves, it will be easy for us to start using and integrating with new solutions, and discard others.

## DAO Improvement Proposals (DIP)

In order for dORg to be in the for front of DAO landscape we want to propose setting up a standardized process for evolving the DAO.

Standardize the way we evolve the DAO. A structure for how to handle the evolvement of the DAO. This should make it easier for members to propose changes, take into account the impacts on the DAO adn its members etc.

Also, each DIP should be made public after an initial round of internal discussions. So that the world can see what we are working on even if it does not pass voting. This could also help us display our DAO expertise to potential clients and others.

# dOrg Primitives

## Passport

The Passport is an ERC721 contract that is owned by the Main Safe.

**Changes compared to a standard ERC721:**

- The transfer functions are guarded by the `onlyOwner` modifier. This means that only the Main Safe can call the basic transfer functions.
- A `mint(to)` function is added. This can only be called by the Main Safe (owner). This will create a new Passport and set the to address as the owner.
- A `batchMint(toArray)` function is added. This can only be called by the Main Safe (owner). This will create new Passports and set the toArray addresses as the owners.
- A `initiateTransfer(passportId, to)` function is added. This can be called by the owner of the corresponding Passport. To initiate the process of changing the address owning the Passport.
- A `finalizeTransfer(passportId, to)` function is added. This can be called a week (a specific number of blocks) after the `initiateTransfer` function to finalize the transfer. This functionality makes it possible for a Passport holder to move it to another address without the Main Safe having to intervene. However, in the case of an unauthorized move (for instance, if it is soled), the Main Safe has time to call the `forceTransfer` function before the transfer.
- A `forceTransfer(passportId, to)` function that can only be called by the Main Safe. This can move any Passport to any address.
- A `burn(passportId)` function that can only be called by the Main Safe. This will burn a Passport.
- A `updateBaseUri(string)` function for setting the base resolution path for updating for instance a Subgraph endpoint that serves the NFT metadata complying with the ERC721 spec (for us to specify how it should show up in "NFT explorers").

The Passport is the index for "everything" regarding a "member". For instance, the Passport is used as the owner of:

- Badges (ERC5114)
- Rep
- Registries (like member details), can point to both on-chain and off chain stuff, like IPFS, IPNS, Ceramic
- ENS member resolution (like `john.dorg.ens`)
- Or any other function we or others create later

## Project Safe

Projects are represented by a Safe with some specific functionality.

- It can accept payment from customers.
- It has a timelock on all transactions (for instance, two days).
- The Main Safe can veto any transaction.
- The Safe's owners (signers) are the addresses currently holding the Passports added to the Project Safe. This can be updated at any time by calling a `updateOwners(projectSafe)` function on the Project Safe Manager.
- It points to a Payout Module (hourly, fixed, drips, superfluid) that must be enabled as a Safe Module on the Main Safe.
- Other project details are handled by separate contracts using the Project Safe's address as the key.

### Project Safe Manager

The Project Safe Manager is a contract that the Main Safe can use to:

- Create new Project Safes - this requires a list of Passport IDs to set as the owners and the address of a Payment Module to use for payment distribution.
- Dismantle the Project Safe.

The Project Safe Manger can be used by the Project Safe to:

- Change the Payout Module.
- Dismantle the Project Safe.

The Project Safe Manager can be used by anybody to:

- Update the current owners of a Project Safe. Refetch the addresses holding the Passports in case the Passports are moved.
- View the list of Project Safes created by this Project Safe Manager.

## Main Safe

The Main Safe is the Safe we use today.

The Main Safe has the [Usul Module](https://github.com/SekerDAO/Usul) enabled. This module will let us propose transactions to the Main Safe and vote on them (based on Rep). This will also allow us to swap out the voting mechanism later, if needed.

### Payout Modules

A Payment Module is a Safe Module that is enabled on the Main Safe and on Project Safes that use it.

A Payment Module is used by the Project Safe when distributing payments to the Passport holders working on a project. The Payment Module is responsible for collecting the Main Safes' share of the payment, distributing payment to project builders (based on Passport holders or whats specified in a registry to be the Passports payout address) and distributing Rep accordingly.

It also emits events that allow for easy accounting in for instance, a Subgraph.

# Road map

We will continue using the Safe we use today as the Main Safe. Over time this Safe will morph into a fully on-chain DAO.

Start:

- Build and deploy the Passport Contract.
- Mint Passports for our members.
- Build and deploy contracts for Rep (see sample).
- Mint and distribute Rep.
- Build and deploy the Project Safe Manager.
- Build and deploy a simple Payout Module.
- Test it out with an internal project.

Later:

- Add badges
- Make more Payout Modules
- Make a roles Safe Module
- Activate the Usul Module on our Main Safe

Even later (the training wheels come off)

- When we have used the Usul Module with our Main Safe for a while, create a proposal to remove the current owners/signers of the Safe.
- Now we are a "real DAO"!

# Things that will require proposal/voting on the Main Safe

- Miniting, burning, and force transfer Passports.
- Creating new Project Safes.
- Dismantling the Project Safes.
- Adding new Payout Modules.
- Removing Payout Modules.
- Rep slashing.
- Other than that, any transaction can be proposed to the Safe.

# But we also need to!:

- Any transaction can be proposed to the Safe. Even after moving to something like Usul, any transaction can be proposed. Therefore this will not limit what operations are possible.
- To give more usability to the Passport, anybody can create a contract that uses the Passport address and Passport ID as the key. For instance, new kinds of badges and other tokens.
- New payout modules can be proposed at any time.
- New general Safe modules can be proposed at any time, not just the ones we create but also others that are continually being created by the Safe community.
- We can create new Project Safe Managers.

# FAQ

**What about internal projects?**
These are Project Safes with some specific Payout Module.

**How about the active or inactive status of Passports?**
This can be derived from the last time Rep was distributed to the Passport. It can also be derived on-chain if we want to add it.

**How can I set some attribute/property on a Passport?**
This can be implemented by an external (Registry) contract using the Passport ID as the key.

**How will we collect data for accounting and other needs?**
We can create a Dune Analytics dashboard, starting with the basics and expending it as needed over time. Here is a example: [Safe dashboard](https://dune.com/safe/ethereum).

**How will we know whats going on in the DAO?**
We can set up a Push (EPNS) chanel that triggers on certain events, for instance get a mobile notification every time there is a new proposal for the DAO, every time a new member is added or every time a new project is started.
