# An evolving DOA structure [WIP]

## Abstract

An unlimited extendable, and changeable DAO solution leveraging the Safe ecosystem.

The DAO solution proposed is not static; it is a continually evolving organism inhabiting the dark forest. Since nobody knows the future evolution of this organism, we aim for a solution that allows for maximum evolvement.

In addition to an initial starting point for the DAO, we propose the DAO Improvement Proposals (DIP) standard. The DIP will support the DAO's continued evolvement in standardizing how we suggest changes to the DAO structure.

## DAO Improvement Proposals (DIP) [[DIP-1](./DIPs/DIP-1.md)]

In order for dOrg to be in the for front of DAO landscape we want to propose setting up a standardized process for evolving the DAO.

Standardize the way we evolve the DAO. A structure for how to handle the evolvement of the DAO. This should make it easier for members to propose changes, take into account the impacts on the DAO adn its members etc.

Also, each DIP should be made public after an initial round of internal discussions. So that the world can see what we are working on even if it does not pass voting. This could also help us display our DAO expertise to potential clients and others.

# Core Components

The core components are the Avatar, the Passports, and the Projects. These components forms a thin layer that can support the continued evolvement of the DAO. Components (even the core components) and modules can be removed, replaced, and new once added at any time in the form of a proposed transaction to the Avatar (or for things specific to a Project, the relevant Project, not all Projects needs to be the same). This has the great advantage that non of the contracts will need to be upgradeable.

Also, as the DAO space evolves, it will be easy for us to start using and integrating with new solutions, and discard others.

## Passport [[DIP-2](./DIPs/DIP-2.md)]

The Passport is an ERC721 contract that is owned by the Avatar.

The Passport is the index for "everything" regarding a "member". For instance, the Passport is used as the owner of:

- Badges (ERC5114)
- Rep
- Registries (like member details), can point to both on-chain and off chain stuff, like IPFS, IPNS, Ceramic
- ENS member resolution (like `john.dorg.ens`)
- Or any other function we or others create later

### Rep [[DIP-5](./DIPs/DIP-5.md)]

Rep is a representation of each Passport Holders contribution to the DAO.

## Project [[DIP-3](./DIPs/DIP-3.md)]

The Projects are the structure when forming both internal projects and external projects.

### Project Manager

The Project is a set of utilities used for managing a Project; It is used from the perspective of the DAO Avatar (The DAO), a project's Passport holder collectively (The Project), and a project's Passport holders individually (The Member). For instance, it is used for creating new Projects.

## Avatar [[DIP-4](./DIPs/DIP-4.md)]

This is the entity that represents the collective wishes of all the DAO's Passport holders, weighted by their associated Rep.

# Road map

We will continue using the Safe we use today as the Avatar. Over time this Safe will morph into a full Avatar.

Start:

- Build and deploy the Passport Contract.
- Mint Passports for our members.
- Build and deploy contracts for Rep (see sample).
- Mint and distribute Rep.
- Build and deploy the Project Manager.
- Build and deploy a simple Payout Module.
- Test it out with an internal project.

Later:

- Add badges
- Make more Payout Modules
- Make a roles Safe Module
- Activate a governance module for the Avatar

# But we also need to!:

- Any transaction can be proposed to the Safe. Even after moving to something like Usul, any transaction can be proposed. Therefore this will not limit what operations are possible.
- To give more usability to the Passport, anybody can create a contract that uses the Passport address and Passport ID as the key. For instance, new kinds of badges and other tokens.
- New payout modules can be proposed at any time.
- New general Safe modules can be proposed at any time, not just the ones we create but also others that are continually being created by the Safe community.
- We can create new Project Safe Managers.

# FAQ

**How about the active or inactive status of Passports?**
This can be derived from the last time Rep was distributed to the Passport. It can also be derived on-chain if we want to add it.

**How can I set some attribute/property on a Passport?**
This can be implemented by an external (Registry) contract using the Passport ID as the key.

**How will we collect data for accounting and other needs?**
We can create a Dune Analytics dashboard, starting with the basics and expending it as needed over time. Here is a example: [Safe dashboard](https://dune.com/safe/ethereum).

**How will we know whats going on in the DAO?**
We can set up a Push (EPNS) chanel that triggers on certain events, for instance get a mobile notification every time there is a new proposal for the DAO, every time a new member is added or every time a new project is started.
