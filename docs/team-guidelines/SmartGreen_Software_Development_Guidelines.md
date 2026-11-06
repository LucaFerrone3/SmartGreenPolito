# SmartGreenPolito

## Software Development Guidelines

*A practical working agreement for repositories, collaboration, and code
quality*

This document defines the common development workflow for SmartGreen
software projects. Its purpose is to make collaboration predictable,
keep the codebase understandable, and ensure that changes are tested and
reviewed before they become part of the shared code.

## 1. Core Principles

-   Keep changes small, focused, and easy to review. A commit or pull
    request should address one coherent task.
-   Prefer readable, maintainable code over clever or unnecessarily
    complex solutions.
-   Follow the conventions already used in the repository. If a
    convention is missing, agree on one with the team and document it.
-   Do not commit secrets, credentials, private keys, personal data,
    generated build artifacts, or local configuration files.
-   Communicate early when blocked, when requirements are unclear, or
    when a change may affect another unit or project.

## 2. Branching Strategy

SmartGreen follows a Git Flow-inspired branching strategy:

| Branch | Purpose | Example |
|---|---|---|
| `main` | Stable, reviewed, and release-ready code. Direct development is not allowed. | `main` |
| `develop` | Integration branch where completed and reviewed features are combined and tested before being released to `main`. | `develop` |
| `feature/<short-description>` | New functionality or enhancements, branched from `develop`. | `feature/sensor-dashboard` |
| `fix/<short-description>` | Bug fixes, branched from `develop`. | `fix/csv-export` |
| `docs/<short-description>` | Documentation-only changes, branched from `develop`. | `docs/setup-guide` |
| `refactor/<short-description>` | Code restructuring without intended behavior changes, branched from `develop`. | `refactor/data-service` |

### Branching Workflow

1. Create feature, fix, docs, or refactor branches from the latest `develop`.
2. Implement the changes and commit them using clear, descriptive messages.
3. Open a pull request targeting `develop`.
4. Have the pull request reviewed and approved by at least one other team member.
5. Merge the approved pull request into `develop` after all required checks pass.
6. Once `develop` is tested and considered stable, open a pull request from `develop` to `main`.
7. Merge into `main` only after the release has been reviewed and approved.

Direct commits to `main` and `develop` are not allowed. All changes must go through pull requests.

## 3. Commits

-   Make commits that represent meaningful, logical steps; avoid huge
    commits that mix unrelated changes.
-   Use short, imperative commit messages, for example:
    `Add greenhouse temperature logging` or
    `Fix sensor timeout handling`.
-   Do not commit code that is knowingly broken, unrelated formatting
    changes, or commented-out blocks of obsolete code.
-   Never include passwords, API keys, tokens, or other secrets in a
    commit---even temporarily. If a secret is exposed, notify the
    repository maintainer immediately and rotate it.

## 4. Pull Requests (PRs)

All changes to `main` must go through a pull request. A PR is a request
to integrate a branch and the place where the team discusses and
validates the change.

### Before opening a PR

-   Confirm the change addresses an agreed task or issue and has a clear
    scope.
-   Run the relevant tests, checks, and build locally; inspect the final
    diff for accidental changes.
-   Update documentation or configuration examples when behavior, setup,
    interfaces, or workflows change.
-   Ensure the branch is reasonably up to date with `main`.

### PR description

Every PR should:

-   Explain what changed and why.
-   Link the related issue or task, if one exists.
-   Describe how the change was tested and include relevant results.
-   Call out known limitations, follow-up work, database or
    configuration changes, and any risks.
-   Add screenshots, logs, or sample outputs when they make a UI or
    data-related change easier to verify.

Keep PRs small enough to review efficiently. If a change is large, split
it into smaller PRs where practical. Do not merge your own PR without
the required review, except for an explicitly agreed emergency
procedure.

## 5. Code Review

-   At least one other team member should review a PR before it is
    merged. Repositories may require more reviewers for sensitive or
    high-impact changes.
-   Review for correctness, readability, maintainability, security, test
    coverage, and consistency with the project's architecture and
    conventions.
-   Reviewers should be respectful, specific, and constructive. Comment
    on the code or its impact, not on the author.
-   Authors should respond to comments, make agreed changes, and resolve
    discussion threads once addressed.
-   A reviewer should approve only when the change is understood and no
    blocking issues remain. Use **Request changes** for issues that must
    be fixed before merging.
-   The author is responsible for ensuring that review feedback and
    automated checks are addressed before merging.

## 6. Definition of Done

In accordance with the Agile Scrum approach, the Definition of Done (DoD)
establishes the shared quality standards that work must satisfy to be
considered complete.

The Definition of Done applies to all team members and work items,
ensuring that every contribution meets the quality, reliability, and
documentation standards required by SmartGreen.

A task can be considered Done only when all applicable criteria below
are satisfied:

### Implementation and Quality

- [ ] The agreed requirements and acceptance criteria are implemented.
- [ ] The code follows repository conventions and is understandable
      and maintainable by other team members.
- [ ] Relevant tests have been added or updated and pass.
- [ ] The application or relevant component builds and runs successfully,
      with no known critical regressions.
- [ ] Errors and relevant edge cases are handled appropriately.
- [ ] Logging does not expose secrets or sensitive information.

### Documentation and Integration

- [ ] Comments, README files, setup instructions, API documentation,
      or configuration examples are updated when necessary.
- [ ] The changes have been submitted through a Pull Request (PR)
      targeting the appropriate branch.
- [ ] The PR has been reviewed and approved by at least one other
      team member.
- [ ] All required automated checks and CI workflows pass.
- [ ] The changes have been merged into the appropriate target branch,
      and the related task is updated or closed.

### Additional Considerations

For work involving the Smart Greenhouse, sensors, or experimental data,
the Definition of Done also includes, where applicable:

- [ ] Sensor units, sampling intervals, and relevant calibration
      assumptions are documented.
- [ ] Data collection and processing have been validated against
      the agreed requirements.
- [ ] Experimental results, limitations, and relevant assumptions
      are documented and reproducible.

The Definition of Done is a shared commitment to quality. Meeting the
Definition of Done does not automatically mean that the Sprint Goal
has been achieved; the Sprint Goal is evaluated separately at the
Sprint Review.

## 7. Comments and Documentation

Comments should explain intent and context, not translate obvious code
into English.

-   Write comments when the reason for a decision, a non-obvious
    constraint, a workaround, a physical sensor behavior, or a
    scientific assumption is not clear from the code.
-   Document units, calibration assumptions, sampling intervals, sensor
    identifiers, and data formats where these affect interpretation.
-   Use `TODO` or `FIXME` markers sparingly and include enough context
    to understand the follow-up; link an issue when possible.
-   Remove stale, misleading, redundant, or commented-out code rather
    than preserving it as a substitute for version control.
-   Document public interfaces, complex algorithms, setup steps,
    environment variables, and non-obvious deployment procedures.

## 8. Testing and Data Quality

-   Test at the appropriate level: unit tests for isolated logic,
    integration tests for connected components, and end-to-end or manual
    tests for complete workflows.
-   For sensor and greenhouse software, test missing, delayed,
    out-of-range, or malformed readings where relevant.
-   For data-processing code, validate units, timestamps, missing
    values, and assumptions before producing datasets or conclusions.
-   Use synthetic or anonymized sample data in tests and examples. Do
    not commit private, sensitive, or unapproved experimental data.
-   Record manual test steps and outcomes in the PR when automated
    testing is not practical.

## 9. Collaboration and Ownership

-   Discuss architectural changes, new dependencies, data schema
    changes, and cross-unit interfaces with the affected team members
    before implementation.
-   During sprint planning, team members decompose agreed work into
    manageable tasks and coordinate ownership with the team.
-   Raise blockers and integration risks promptly rather than waiting
    until the end of the sprint.
-   Leave the codebase in a state that another member can run,
    understand, and continue working on.

## 10. Quick Checklist

Before requesting review, check that:

-   [ ] I worked on the correct branch and kept the change focused.
-   [ ] I checked the diff and removed debug code and accidental files.
-   [ ] I ran relevant tests/builds and recorded the results.
-   [ ] I updated comments or documentation where necessary.
-   [ ] My PR explains the purpose, scope, and verification steps.
-   [ ] A teammate reviewed and approved the PR, and required checks
    pass.

------------------------------------------------------------------------

*These guidelines are a shared baseline. Repository-specific README
files and agreed team decisions may add stricter requirements.*
