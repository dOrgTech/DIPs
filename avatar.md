## dOrg Avatar

This is the core DAO component with the power to govern many of the other parts of the DAO.

This can be represented as a Gnosis Safe with now owners. It can however have attached roles something like https://github.com/gnosis/zodiac-modifier-roles that can give specific members specific and limited access to the Gnosis Safe (granted and revoked via voting).

Needs some mechanisms for proposing arbitrary transactions and letting the members come to consensus on them (rep-weighted voting). This can be implemented as a Gnosis Safe module.

### What will happen via the Avatar?

- Starting new projects (spinning up new Gnosis project safes via the factory)
- Grant and revoke member roles
- Adding or removing Avatar modules (Gnosis Safe modules)
- Minting new Member NFTs
- Rep slashing
