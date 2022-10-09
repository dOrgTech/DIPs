---
dip: 4
title: Avatar
description: This main DAO entity
discussions-to: <!-- link to the forum or github issue? -->
status: Draft
created: 9 Oct 2022
---

## Abstract

This is the entity that represents the collective wishes of all the DAO's Passport holders, weighted by their associated Rep.

## Requirements

- Must be able to execute any transaction, based on the will of the Passport holders, weighted by Rep.
- It must be possible to gradually evolve into it, from what we have today.

In addition to the ability to execute any transaction, the Avatar should have custom support for:

- Miniting, burning, and force transfer Passports.
- Creating new Projects via the Project Manager.
- Dismantling the Projects.
- Adding new Payout Modules.
- Removing Payout Modules.
- Rep slashing.

## Specification

- The main Safe (that we use today) represents the Avatar.
- The Safe must equip some sort of governance module. Some alternatives:
  - On-chain: The [Usul Module](https://github.com/SekerDAO/Usul) enabled. This module will let us propose transactions to the Avatar and vote on them (based on Rep).
  - Off-chain with escalation to on-chain Rep weighted resolution: The Zodiac Reality module.
