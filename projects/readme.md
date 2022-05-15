## dOrg Projects

The are multiple kinds of compensation structures for projects.

Examples of compensation models:

1. Hourly rate - flexible hours
2. Fixed monthly income
3. [Drips](https://www.drips.network/)

## The naive approach

Here we solve this ourselves and add new project contracts as needed.

This can be solved via:

- Having one contract of each type (multiple projects per contract).
- Having one main contract for each project type and one clone (minimal proxy) pr. project instance.
  - easies in form of payment reception
  - safest, as each project instance will have its own address

Clone sample

### Fixed percentage of income

- The contract is initialized with a list of attached roles (Sourcing, Coordination Leda, QA Lead, etc.), a list of builders (both represented by Member NFT ids), and a list of each builder's percentage of compensation.
- Payments are made to the contract address for both ERC20 and ETH.
- Have a distribution function that can be called with a list of token addresses. This will distribute the tokens.
- How will everybody be in consensus? It's better to use a gnosis safe. Can we create a module attached to gnosis safe for this instead?

### Hourly rate

- The contract is initialized with a list of attached roles (Sourcing, Coordination Leda, QA Lead, etc.), a list of builders (both represented by Member NFT id's), and a list of builder hourly compensation distribution. Also, the address for the token used for distribution.
- Payments are made to the contract address for both ERC20 and ETH.
- Have a function called add hours where each builder can add work hours.
- Have a distribution function that can be called with a list of token addresses. This will distribute the tokens.
- ...

## Alternative 1

Create a gnosis safe app for managing projects.
Create modules and modifiers to allow:

- The Member NFTs assigned to a project must be the "owners" (the safe will only have the DAO avatar as its owner (how will this work, can a contract be an owner? It will probably need to be implemented as a Module), but instead be managed through modules, that uses the Member NFT's owner as "owners").
- Payouts can be created by any Member connected to the project. The payout will have a timelock. During the timelock period, any connected Member can veto the payout. If all payouts are vetoed, the DAO avatar can execute a payout directly.

## Alternative 2

A Gnosis Safe that is deployed via a factory.

The input for the deployment function is the Member NFT ids of the builders and sourcing lead(s). These will become the safe's owners.

The safe will be equipped with the following modules:

1. A time lock with veto functionality for all transactions
2. A module that lets an address (the DAO avatar) bypass the owners to execute transactions.
3. A module that updates the safe owners to the current holders of the Member NFTs for the members of the project. This module basically consists of a contract with an external function that can be called by anybody that will get the owners of the Member NFTs and update the safe owners as needed. This bypasses the current safe owners.
4. A module for proposing payouts (hourly, fixed, etc.).
