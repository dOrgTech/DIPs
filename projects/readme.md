## dOrg Projects

The are multiple kinds of compensation structures for projects.

Examples of compensation models:

1. Hourly rate - flexible hours
2. Fixed monthly income
3. [Drips](https://www.drips.network/)

## Proposed solution

The DAO will deploy a Gnosis Safe via a factory.

The input for the deployment function is the Member NFT ids of the builders and sourcing lead(s). These will become the safe's owners.

The Gnosis project safe will be added to a registry of projects started by the DAO.

The safe will be equipped with the following modules (during deployment, in the factory):

1. A time lock with veto functionality for all transactions.
2. A module that lets an address (the DAO avatar) bypass the owners to execute transactions.
3. A module that updates the safe owners to the current holders of the Member NFTs for the members of the project. This module basically consists of a contract with an external function that can be called by anybody that will get the owners of the Member NFTs and update the safe owners as needed. This bypasses the current safe owners.
4. A module for proposing payouts (hourly, fixed, etc.) via the Member NFT payout routing.
