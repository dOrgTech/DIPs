---
dip: 3
title: Projects
description:
discussions-to: <!-- link to the forum or github issue? -->
status: Draft
created: 9 Oct 2022
---

## Abstract

Projects are initiatives that has a set of Passports related to it.

## Requirements

- A Project should have a significant degree of autonomy.
- A Project should primarily be governed by its Passport holders.
- It should be able to execute any transaction that the Passport holder agrees to (it should offer flexibility). This way, any situation that is not explicitly supported by the current Project structure, is still possible.
- The DAO should be able to intervene in some cases (disputes within the Project, etc.).
- It should help automate accounting.
- The Project should be able to handle different payout schemes (hourly- rate, fixed rate, stables, stables+token, push payouts, pull-payouts, etc.).

## Specification

Projects are represented by a Safe with some specific functionality.

- The Avatar can veto any transaction.
- The Safe's owners (signers) are the addresses currently specified in the Passports added to the Project Safe. This can be updated at any time by calling a `updateOwners(projectSafe)` function on the Project Safe Manager.
- The Project can have a Payout Module (hourly, fixed, drips, superfluid) that must be enabled as a Safe Module on the Avatar. The Payout Module needs to be enabled on the Avatar in both to show that it is an accepted payout module by the DAO and to allow the module to handle Rep distribution on behalf on the Safe.
- Other project details are handled by separate contracts using the Project Safe's address as the key.

### Project Manager

The Project Manager is a contract that the Avatar can use to:

- Create new Projects - this requires a list of Passports to set as the owners and the address of a Payment Module to use for payment distribution.
- Dismantle the Projects.

The Project Manger can be used by the Project to:

- Change the Payout Module.
- Dismantle the Project.
- Distribute payments.

The Project Manager can be used by anybody to:

- Update the current owners of a Project Safe. Refetch the addresses holding the Passports in case the Passports are moved.
- View the list of Project Safes created by this Project Manager.

### Payout Modules

A Payment Module is a Safe Module that is enabled on the Avatar and on Projects that use it.

A Payment Module is used by the Project when distributing payments to the Passport holders working on a project. The Payment Module is responsible for collecting the DAOs' share of the payment, distributing payment to project builders (based on Passport holders or whats specified in a registry to be the Passports payout address) and distributing Rep accordingly.

It also emits events that allow for easy accounting in for instance, a Subgraph.
