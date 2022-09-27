# dOrg-primitives

# Core Components

An unlimited extendable, and changeable DAO solution leveraging the Safe community.

The DAO solution proposed will not be static; it will be a continually evolving creature inhabiting the dark forest. Since nobody knows the future evolution of this creature, we aim to create a solution that allows for maximum evolvement.

The core components are Passport, Main Safe, and Project Safe.

## Passport

The Passport is an ERC721 contract that is owned by the Main Safe.

**Changes compared to a standard ERC721:**

- The transfer functions are disabled.
- A `mintPassport(to)` function is added. This can only be called by the Main Safe (owner). This will create a new Passport and set the to address as the owner.
- A `requestTransfer(passportId, to)` function is added. This can be called by the owner of the corresponding Passport. To initiate the process of changing the address owning the Passport.
- A `requestTransfer(passportId, to)` function is added. This can be called a week (a specific number of blocks) after the `requestTransfer` function to finalize the transfer. This functionality makes it possible for a Passport holder to move it to another address without the Main Safe having to intervene. However, in the case of an unauthorized move (for instance, if it is soled), the Main Safe has time to call the `forceTransfer` function.
- A `forceTransfer(passportId, to)` function that can only be called by the Main Safe. This can move any Passport to any address.
- A `burn(passportId)` function that can only be called by the Main Safe. This will burn a Passport.

The Passport is the index for "everything". For instance, the Passport is used as the owner of:

- Badges (ERC5114)
- Rep
- Registries (like member details)
- Or any other function we or others create later

## Project Safe

Projects are represented by a Safe with some specific functionality.

- It can accept payment from customers.
- It has a timelock on all transactions (for instance, two days).
- The Main Safe can veto any transaction.
- The Safe's owners (signers) are the addresses currently holding the Passport. This can be updated at any time by calling a `updateOwners(safe)` function on the Project Safe Factory.
- It points to a Payout Modules (hourly, fixed, drips, superfluid) that must be enabled as a Safe Module on the Main Safe.
- Other project details are handled by separate contracts using the Project Safe's address as the key.

### Project Safe Manager

This is a contract that the Main Safe can use to:

- Create new Project Safes - this requires a list of Passport IDs to set as the owners and the address of a Payment Module to use for payment distribution.
- Dismantle the Project Safe.

This can be used by the Project Safe to:

- Change the Payout Module.
- Dismantle the Project Safe

It can be used by anybody to:

- Update the current owners of a Project Safe.
- View the list of Project Safes created by this Project Safe Manager.

## Main Safe

The Main Safe is the Safe we use today.

The Main Safe has the [Usul Module](https://github.com/SekerDAO/Usul) enabled. This module will let us propose transactions to the Main Safe and vote on them (based on Rep).

### Payout Modules

A Payment Module is a Safe Module that is enabled on the Main Safe.

A Payment Module is used by the Project Safe when distributing payments to the Passport holders working on a project. The Payment Module is responsible for collecting the Main Safes' share of the payment and distributing Rep accordingly.

It also emits events that allow for easy accounting in for instance, a Subgraph.

# Road map

We will continue using the Safe we use today. Over time this Safe will morph into a fully on-chain DAO.

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
