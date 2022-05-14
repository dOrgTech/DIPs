## dOrg Member

A dOrg member represented by a ERC721.

### Spec

A Member NFT is an ERC721 with the following changes:

- The contract has an owner; expected to point to a DAO avatar.
- The contract owner can transfer ownership of the contract.
- New Member NFTs can be minted by the contract owner for creating new memberships.
- A Member NFT can only be transferred via:
  - **Request transfer** of ownership by the Member NFT owner -> the contract owner approves the transfer, used when a member wants to move its Member NFT to a different address.
  - **Force transfer**, used in emergencies where the member is no longer in control of the address owning the Member NFT. This is only callable by the contract owner. _I am unsure about this; I don't think it's optimal that the owner (DAO) can "take" a Member from an owner._

#### Notes

- Member's status (active or non-active, etc.) is not a part of the Member NFT it selves. It can be implemented as an external registry contract.
- The Member NFT will be the holder of the rep token (can be an ERC888) (does there exist an ERC for ERC721 owning ERC20 tokens? ERC998?).
- Badges are not part of the Member NFT. It can be implemented as a separate ERC721 that can belong to a Member NFT (ERC998?).
- If we want to set other properties on a Member, this will be implemented as a separate contract. For instance, to allow the Member NFT owner to set properties on itself or let others (for instant, the ERC721 owner/DAO avatar) set properties.
- The token URI can point to a subgraph that indexes the properties (from any external contracts/ registries), tokens, etc. owned by the Member NFT (that we want to show off).

#### References

- https://vitalik.ca/general/2022/01/26/soulbound.html
- https://ethereum-magicians.org/t/eip-4973-account-bound-tokens/8825/27
- https://github.com/ethereum/EIPs/blob/master/EIPS/eip-998.md
- https://github.com/ethereum/EIPs/blob/3fba38040b8b7fcc7ba44b85373f1e66462e3394/EIPS/eip-4671.md
