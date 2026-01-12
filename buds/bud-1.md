<!----------------------------------------------------------------------
This is a template for creating new BUDs (Blueprints for Upcoming
Development). Copy this file to buds/bud-[number].md (or use TBD for the
number initially) and fill in each section.
----------------------------------------------------------------------->

---
bud: 1 (TBD)
title: The great GitHub migration
author: "@Xophmeister"
pr: 4
---

# The great GitHub migration

## Summary

We have been given the green light to move the Topiary repository from
the Tweag GitHub organisation to our new Topiary organisation, providing
we maintain appropriate branding. The move also gives us an opportunity
to break out some of the peripheral subcomponents of the Topiary
repository into their own, dedicated repositories.

## Motivation

- Having all Topiary repositories under one organisation is clearer and
  aids discovery, at the expense of current users having to update links
  and remotes, etc.

- The Topiary website is orthogonal to the Topiary codebase, so should
  certainly be broken out into its own repository. Similar arguments can
  be made for:

  - The Topiary playground: Not currently under active development, but
    effectively another client of the Topiary core library.

  - The Topiary Book and manpages: These should be synchronised with the
    codebase, so the decoupling argument is weaker, but keeping them
    separate _may_ motivate better code documentation, keeping the Book
    as user documentation.

  - [topiary-opam][https://github.com/tweag/topiary-opam]: This is
    separate from the Topiary repository, but will probably need to be
    updated if the migration goes ahead and, indeed, is a target for
    migration itself.

There may be infrastructural changes required for correctly migrate
(e.g., DNS, Cachix, etc.)

## Proposed design

{TODO: Still under discussion}

## Alternatives considered

Leave the Topiary repository where it is; i.e., do nothing. {TODO: Still
under discussion}

## Drawbacks

- Website downtime during the migration
- Current users would have to update links and remotes
- The decoupling proposal would increase the complexity (warranting a
  multiphase migration) and probably increase the website downtime
- DNS changes take a while to action, which will also impact website
  downtime
- We risk losing access to Tweag infrastructure (e.g., Cachix)

## Backwards compatibility

If current users don't update links/remotes, that may be confusing for
them. We can mitigate this to a certain extent by broadcasting it on
Discord. GitHub _may_ keep the old remote active for a limited time, and
display a warning, like it does when repository names change.

## Testing strategy

{TODO: Still under discussion}

## Documentation impact

{TODO: Still under discussion}

## Unresolved questions

{TODO: Still under discussion}
