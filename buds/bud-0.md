---
bud: 0
title: Topiary BUD (RFC) process and governance
author: "@Xophmeister"
pr: 1
---

# BUD process and governance

## Summary

This document defines the BUD (Blueprints for Upcoming Development)
process, which provides a structured RFC (Request for Comments)
mechanism for proposing, discussing and tracking non-trivial changes and
enhancements to Topiary. BUDs use a PR-based workflow with GitHub
Projects to manage the full lifecycle from initial proposal to
implementation.

## Motivation

Open source projects benefit from transparent decision-making and clear
documentation of design rationale. Whilst small bug fixes and routine
maintenance can proceed through normal pull requests, non-trivial
changes -- those that affect architecture, introduce new features, or
require significant coordination -- need more thorough discussion and
documentation. The BUD process ensures that:

- Design decisions are documented and reviewable
- The community can participate in technical discussions
- Implementation has clear direction and approval
- Historical context is preserved for future reference

## Proposed design

### What is a BUD?

A BUD is a design document that describes a proposed change to Topiary.
BUDs are specifically for **non-trivial changes and enhancements**, not
everyday maintenance tasks. Each BUD progresses through a defined
lifecycle tracked via [GitHub Project board][project-board], with the PR itself serving
as both the proposal document and discussion forum.

### Who can create BUDs?

Anyone can create a BUD, regardless of whether they have write access to
the repository. Contributors without write access should fork the
repository and submit their BUD via pull request.

### BUD lifecycle

BUDs progress through the following stages, tracked as columns on the
[GitHub Project board][project-board]:

1. **Draft**
   New BUDs start here when a PR is first opened. The author develops
   and refines the proposal based on early feedback. The PR number is
   established at this stage.

2. **Under Review**
   When the author is satisfied with their proposal, the BUD moves to
   review. The core team provides feedback iteratively until consensus
   is reached.

3. **Accepted**
   The BUD has been approved by the core team and the PR is merged to
   the default branch. The BUD document is now part of the official
   record. At this point, the BUD number is assigned if not already
   done so.

4. **In Progress**
   Implementation work is underway. If the BUD document did not define
   an implementation checklist, then the PR description can be updated
   to expose this.

> [!NOTE]
> Implementation happens in the Topiary repository, not the BUD
> repository.

5. **Completed**
   The implementation has been finished and merged into Topiary's
   default branch. The BUD's purpose has been fulfilled.

6. **Rejected**
   The BUD was not accepted, was cancelled by its author, or was
   abandoned. This can branch from any earlier stage.

### How to create a new BUD

1. **Copy the template**: Start by copying
   [`TEMPLATE.md`](../TEMPLATE.md) to `buds/bud-[number].md`. If you
   don't know the BUD number yet, use `TBD` in the filename (e.g.,
   `buds/bud-TBD.md`) and in the frontmatter.

2. **Fill in the frontmatter**:

   | Field    | Description                                                                   |
   | :------- | :---------------------------------------------------------------------------- |
   | `bud`    | Set to `TBD` initially; the number will be assigned during the review process |
   | `title`  | A brief, descriptive title                                                    |
   | `author` | Your GitHub username or name                                                  |
   | `pr`     | Set to `TBD` initially; update with the PR number once created                |

3. **Write your proposal**: Complete each section of the template. Focus
   on the "what" and "why" initially, though "how" is encouraged if you
   have implementation ideas. The document can evolve as the BUD
   progresses.

4. **Create a pull request**:
   - If you have write access, create a branch and open a draft PR
   - If you don't have write access, fork the repository first, then
     create a draft PR from your fork
   - Once the PR is created, update the `pr` field in the frontmatter
     with the PR number
   - The PR will automatically appear in the "Draft" column of the
     [GitHub Project board][project-board]

5. **Iterate and progress**: Respond to feedback, refine your proposal
   and move through the lifecycle stages.

### The role of PRs and the kanban board

The BUD process is PR-centric:
- **The PR is the BUD**: The PR content is the proposal document itself
- **State tracking**: The PR's position on the [GitHub Project
  board][project-board] indicates its current stage
- **Discussion**: All discussion happens in the PR comments
- **Progress tracking**: During implementation ("In Progress" stage),
  checklists can be added to track specific tasks

This approach provides a single source of truth and integrates naturally
with GitHub's workflow.

### Template structure

All BUDs follow the structure defined in [`TEMPLATE.md`](../TEMPLATE.md):

- **Frontmatter**: Metadata (BUD number, title, author, PR link)
- **Summary**: One-paragraph overview
- **Motivation**: Why this change is needed
- **Proposed design**: Architectural approach (what, why, and optionally
  how)
- **Alternatives considered**: Other approaches that were evaluated
- **Drawbacks**: Potential concerns or limitations
- **Backwards compatibility**: Breaking changes and migration paths
- **Testing strategy**: How the feature will be tested
- **Documentation impact**: What documentation needs updating
- **Unresolved questions**: (Optional) Open questions for discussion

## Alternatives considered

### Separate RFC repository vs Topiary repository

We chose a dedicated BUD repository rather than keeping RFCs in the main
Topiary repository. This separation:

- Keeps the Topiary repository focused on Topiary
- Provides a clear archive of design decisions
- Makes it easier to browse historical proposals
- Allows different access controls if needed

### Issue-based vs PR-based process

We chose a PR-based process over an issue-based one because:

- PRs provide built-in version control for the document
- The diff view shows how proposals evolve
- Merging a PR creates a natural "accepted" event
- GitHub Projects work well with PRs for workflow management

### Lightweight vs comprehensive templates

We chose a lightweight template that balances thoroughness with
accessibility. More comprehensive templates (like Python PEPs) can be
intimidating and slow down proposals, whilst overly minimal templates
lack necessary structure for good decision-making.

## Drawbacks

- **Process overhead**: BUDs add ceremony compared to just opening a PR
  with code
- **Adoption barrier**: Contributors must learn a new process
- **Maintenance burden**: The BUD repository and kanban board require
  ongoing curation
- **Risk of abandonment**: Proposals may stall in "Draft" or "Under
  Review"

These drawbacks are mitigated by limiting BUDs to non-trivial changes
only and keeping the template lightweight.

## Backwards compatibility

This is the inaugural BUD (BUD-0), which defines no changes to Topiary
itself, so there are no backwards compatibility concerns. Future changes
to the BUD process itself should follow the BUD process; meta, but
consistent.

## Testing strategy

The BUD process itself will be validated through use. We should monitor:

- Whether contributors find the process clear and accessible
- Whether BUDs successfully capture design rationale
- Whether the kanban board accurately reflects BUD states
- Whether rejected or stalled BUDs indicate process friction

Adjustments to the process can be made through subsequent BUDs.

## Documentation impact

This document (BUD-0) serves as the primary documentation for the BUD
process.

## Unresolved questions

None at this time. This initial process can be refined through
subsequent BUDs as we gain experience with the workflow.

<!-- Links -->
[project-board]: https://github.com/orgs/topiary/projects/1/views/1
