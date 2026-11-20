# Standards

The standards this repository is held to, as hydraflow init set them up. Each is about a product's own code. .hydraflow/layout.yaml says which are on and what each reads; every other one is declared not_applicable there, with its reason.

## What each standard holds this repository to

- **adr_enforcement** (off, and this repository can switch it on): an accepted architecture decision record names the check that enforces it, or says plainly that its enforcement is planned or exempt.
- **ci_is_configured** (not yet one this repository can switch on by itself): the repository's continuous integration runs every check its build declares, and no required check is skipped or left unrun.
- **code_craft** (off, and this repository can switch it on): the code stays small enough to hold in one head: short functions with few parameters, shallow nesting, and bounded classes and modules, counted against a baseline that may fall and never rise.
- **domain_entities** (off, and this repository can switch it on): a change reaches the tests of its own domain entity and not those of every other: each entity owns its address, its repository interface and, where work must survive a restart, its queue.
- **fail_closed** (off, and this repository can switch it on): every failure path denies or names itself: an error handler returns nothing permissive, and a choice over a closed set ends in a refusal rather than falling through.
- **hygiene** (on): a suppressed lint or type finding carries a code, the number of suppressions may fall and never rise, and no test carries a literal shaped like a credential.
- **line_contract** (not yet one this repository can switch on by itself): the repository answers the same named build lanes as every other product the factory builds, and only the lanes that install, deploy or smoke-test may touch the network.
- **no_second_copy** (not yet one this repository can switch on by itself): a fact is stated in exactly one file: a document cites a declaration rather than restating it, and code reads a declared value rather than carrying a second copy.
- **ports_and_adapters** (off, and this repository can switch it on): every boundary where the code does input or output is an interface with a fake that satisfies it, and a real adapter is constructed only at a declared composition site.
- **testing** (off, and this repository can switch it on): every kind of change carries the tests its shape requires, end-to-end tests are capped, and a test asserts something that could have been false, counted against a baseline that may fall and never rise.
- **ubiquitous_language** (not yet one this repository can switch on by itself): every term the product's glossary declares names something in the code, and one name means one thing.

## Switched on, at the tree's own count

- **hygiene**: total 4, measured at commit 0bf7bd2ff578, kept in tests/architecture/suppression_baseline.json.

Each count was measured over this tree when the standard was switched on, so the tree arrived green. hydraflow line-layout check holds the repository to it: a count may fall and never rise, and only a rise is red.

## Switching one on

This repository can switch on by itself the standards it keeps its own count for: adr_enforcement, code_craft, domain_entities, fail_closed, hygiene, ports_and_adapters, testing. For one of those that is off, replace its not_applicable in .hydraflow/layout.yaml with the roots it reads, then run

    hydraflow line-layout baseline --standard <name>

and commit the count it writes in the same change as the switch.

Every other standard above says what this repository's code will be held to, and is not yet one it can switch on by itself: the command refuses it by name (line-baseline/not-offered), because its check does not read a repository of your own yet.
