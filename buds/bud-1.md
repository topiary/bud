---
bud: 1 (TBD)
title: The great GitHub migration
author: "@Xophmeister"
pr: 4
---

# The great GitHub migration

## Summary

We have been given the green light to move the Topiary repository from
the Tweag GitHub organisation to our newly acquired `@topiary`
organisation, providing we maintain appropriate branding. The move also
gives us an opportunity to break out some of the peripheral
subcomponents of the Topiary repository into their own, dedicated
repositories.

## Motivation

- Having all Topiary repositories under one organisation is clearer and
  aids discovery, at the expense of current users having to update links
  and (maybe) remotes, etc.

- Many Topiary components are not directly synchronised with the Topiary
  codebase and, arguably, not relevant to downstream users:

  - The Topiary website is a simple landing page, with links to the
    Topiary Book and playground. The only connection it has to the main
    Topiary codebase is that these components are built and deployed by
    the same CI.

  - The Topiary playground is not currently under active development,
    but is effectively an orthogonal client of the Topiary core library,
    targeting WASM. It is a dependent on the Topiary codebase, but there
    is no implicit synchronisation and can be developed independently.

  - The Topiary Book and manpages: This is less clear. The Topiary Book
    is the user documentation for Topiary, including usage of the CLI
    frontend which _is_ a part of the Topiary codebase. Moreover, the
    manpages -- which are generated from a subset of the Book -- are
    specific to the CLI. Finally, the majority of the Book documents the
    formatting capture names, which again are inherent to the Topiary
    core library.

    As a compromise, the Topiary Book and manpages should remain part of
    the Topiary codebase. However, the mdBook pre- and post-processor
    (`mdbook-manmunge`) used to help _generate_ the manpages should be
    factored out into its own repository.

  - [`topiary-opam`](https://github.com/tweag/topiary-opam): This is
    separate from the Topiary repository, but is also a target for
    migration for the same reasons. Moreover, having it under the same
    roof will remind us to keep it up-to-date with Topiary releases.

## Proposed design

1. Confirm Topiary core team have necessary access to all relevant
   resources.

2. Announce the migration on Discord, with a reasonable amount of lead
   time and an expectation of the downtime.

3. Migrate `tweag/topiary` and `tweag/topiary-opam` to the `@topiary`
   organisation.

4. Break out subcomponents:

   - `mdbook-manmunge` and update Topiary manpage generator to use new
     dependency.

   - Topiary playground, updating its CI to confirm the build.

   - Topiary website, updating to use the new sources for the Topiary
     repository, Book and playground.

5. Announce completed migration on Discord.

### Infrastructure changes

- The main Topiary repository will need its Cachix credentials set to
  point to the original Tweag Cachix account.

- The Topiary website's CI will need to change to build/retrieve all
  upstream dependencies (the Topiary Book and playground) before
  deployment.

- The GitHub Pages configuration will need to be changed appropriately,
  for the Topiary website.

- The Tweag DNS records will need to be updated to point to the new
  GitHub Pages endpoint.

## Alternatives considered

Leave the Topiary repository where it is; i.e., do nothing. However,
there is now a precedent at Tweag to move its open source projects into
their own organisations (e.g., [`nickel-lang/nickel`](https://github.com/nickel-lang/nickel)
and [`bazel-contrib/rules_img`](https://github.com/bazel-contrib/rules_img)).

Regarding Cachix, they offer a 5GB free plan for open source projects,
which could be used instead of the Tweag account. This may be a good
long-term option.

## Drawbacks

- Website downtime during the migration.
- Current users would have to update links.
  - GitHub redirects old remotes, so providing `tweag/topiary` isn't
    recreated, this should not be an issue.
- The decoupling proposal would increase the complexity (warranting a
  multiphase migration) and probably increase the website downtime.
- DNS and other infra changes take a while to action, which will also
  impact website downtime.

## Backwards compatibility

If current users don't update links, that may be confusing for them. We
can mitigate this to a certain extent by broadcasting it on Discord.
GitHub will keep the old remote active for a limited time, and display a
warning, like it does when repository names change.

## Testing strategy

- Check CI jobs all run to successful completion.

- Check updated DNS records.

- Manual inspection of migrated website. (The website is small enough to
  make this preferable to automating the process.)

## Documentation impact

Documentation will remain under the Topiary repository, so there will be
no impact.

## Unresolved questions

- For the broken out subcomponents that are dependencies of the website,
  should we:

  1. Build the subcomponents in the broken out repository's CI and let
     the website pull in the latest release, when its CI builds?

  2. Or: When the website's CI builds, checkout the appropriate
     subcomponents and build them as subtasks?

  This question is focused on the Topiary playground.

  For the Topiary Book, option (2) is probably the only appropriate
  strategy because the Book is not manifested as a release artefact (and
  cannot be without interfering with Topiary's `dist` release process).
