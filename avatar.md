## dOrg Avatar

This is the core DAO component with the power to govern many of the other parts of the DAO.

This can be represented as a Safe with no owners. It can however have attached roles something like https://github.com/gnosis/zodiac-modifier-roles that can give specific members specific and limited access to the Safe (granted and revoked via voting).

We could use https://github.com/SekerDAO/Usul for the proposal/rep-weighted voting.

### What will happen via the Avatar?

- Starting new projects (spinning up new Gnosis project safes via the factory)
- Grant and revoke member roles
- Adding or removing Avatar modules (Gnosis Safe modules)
- Minting new Member NFTs
- Rep slashing
