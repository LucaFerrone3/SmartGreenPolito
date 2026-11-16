# SmartGreen Software Development Guidelines

*A practical working agreement for repositories, collaboration, and code
quality*

This document defines the common development workflow for the SmartGreen
software unit. Its purpose is to make collaboration predictable,
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
    when a change may affect another team or research project.

## 2. Branching Strategy

SmartGreen follows a Git Flow-inspired branching strategy with a single
integration branch shared by all teams.

### Long-lived branches

| Branch | Purpose |
|---|---|
| `main` | Stable, reviewed, and release-ready code. Direct development is not allowed. |
| `dev` | The single integration branch for all teams. Completed and reviewed work is combined and tested here before being released to `main`. |

All five teams share one `dev`; teams do not have their own
integration branches. Integrating often in one place surfaces conflicts
and broken cross-team interfaces early, while they are still small.

### Working branches

Every other branch is a short-lived working branch, created from
`dev` for exactly one YouTrack task:

```text
<type>/<team>/<issue-id>-<short-description>
```

| Part | Allowed values | Notes |
|---|---|---|
| `<type>` | `feature`, `fix`, `docs`, `refactor` | The kind of change (see the table below). |
| `<team>` | `team-1`, `team-2`, `team-3`, `team-4`, `team-5` | The team that owns the YouTrack task. |
| `<issue-id>` | e.g. `SG-42` | The YouTrack issue ID, written exactly as it appears in YouTrack. |
| `<short-description>` | e.g. `leaf-detection` | 2–5 lowercase English words separated by hyphens. |

| Type | Use it for | Example |
|---|---|---|
| `feature` | New functionality or enhancements. | `feature/team-2/SG-42-leaf-detection` |
| `fix` | Bug fixes. | `fix/team-1/SG-57-sensor-timeout` |
| `docs` | Documentation-only changes. | `docs/team-4/SG-61-setup-guide` |
| `refactor` | Code restructuring without intended behavior changes. | `refactor/team-3/SG-70-data-service` |

Naming rules:

-   No task, no branch: find or create the YouTrack issue before
    creating the branch.
-   One branch per task. If the work grows, split the task in YouTrack
    and open a separate branch for the new part.
-   Use only lowercase letters, digits, and hyphens (the issue ID keeps
    its uppercase key). No spaces, accents, or underscores.
-   If a task involves more than one team, use the code of the team that
    owns the task in YouTrack and ask the other teams to review the PR.
-   Keep branches short-lived: merge them within the sprint in which
    they were created, and delete them once the PR is merged.

### Branching Workflow

1. Pick a YouTrack task and create its branch from the latest `dev`:

   ```bash
   git switch dev
   git pull
   git switch -c feature/team-2/SG-42-leaf-detection
   ```

2. Implement the changes and commit them following the commit
   conventions (see Section 3).
3. Merge the latest `dev` into your branch at least once a week and
   before opening the pull request, so conflicts are solved early.
4. Open a pull request targeting `dev`. Write the PR title in the same
   format as a commit message (see Section 3) and end it with the
   YouTrack issue ID in parentheses, for example
   `feat: add leaf detection model (SG-42)`. YouTrack links the PR to
   the task through the ID in the title.
5. Have the pull request reviewed and approved by at least one other team member.
6. After all required checks pass, merge the approved pull request into
   `dev` with **Squash and merge**, keeping the PR title as the commit
   message, then delete the branch.
7. Once `dev` is tested and considered stable, open a pull request from `dev` to `main`.
8. Merge into `main` with **Create a merge commit** (never squash), only
   after the release has been reviewed and approved by the Software
   Unit Lead.

Why two different merge methods:

-   **Squash and merge into `dev`** turns each task into exactly one
    commit on `dev`, whose message has a type and the YouTrack issue ID.
    The history of `dev` stays readable, and every commit is linked to
    its task.
-   **Create a merge commit into `main`** keeps all the commits of `dev`
    in `main`, so the next release merges cleanly. Squashing a release
    would rewrite those commits on `main`, and the following release
    would show the same changes again and could conflict.

Direct commits to `main` and `dev` are not allowed. All changes must go through pull requests.

## 3. Commits

-   Make commits that represent meaningful, logical steps; avoid huge
    commits that mix unrelated changes.
-   Write commit messages following
    [Conventional Commits](https://www.conventionalcommits.org/):
    `<type>: <short description>`, with the description in English,
    lowercase, and in the imperative mood. An optional scope in
    parentheses can name the affected component.
-   Use one of these types:

| Type | Use it for | Example |
|---|---|---|
| `feat` | New functionality or enhancements | `feat: add greenhouse temperature logging` |
| `fix` | Bug fixes | `fix(sensors): handle sensor timeout` |
| `docs` | Documentation-only changes | `docs: update setup guide` |
| `refactor` | Code restructuring without behavior changes | `refactor: split data service` |
| `test` | Adding or updating tests | `test: cover missing sensor readings` |
| `chore` | Maintenance, configuration, dependencies | `chore: update python dependencies` |

-   Pull request titles follow the same format, followed by the YouTrack
    issue ID: `<type>: <short description> (<issue-id>)`. When a PR is
    squash-merged into `dev`, its title becomes the commit message (see
    Section 2).
-   Do not commit code that is knowingly broken, unrelated formatting
    changes, or commented-out blocks of obsolete code.
-   Never include passwords, API keys, tokens, or other secrets in a
    commit, even temporarily. If a secret is exposed, notify the
    repository maintainer immediately and rotate it.

## 4. Pull Requests (PRs)

All changes to `main` and `dev` must go through a pull request. A PR is a request
to integrate a branch and the place where the team discusses and
validates the change.

### Before opening a PR

-   Confirm the change addresses an agreed YouTrack task and has a clear
    scope.
-   Run the relevant tests, checks, and build locally; inspect the final
    diff for accidental changes.
-   Update documentation or configuration examples when behavior, setup,
    interfaces, or workflows change.
-   Ensure the branch is reasonably up to date with `dev`.

### PR description

Every PR should:

-   Explain what changed and why.
-   Include the YouTrack issue ID in the title, so that the PR is linked
    to its task (see Section 2).
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

As part of our Agile approach (see [How We Work](how-we-work.md)), the
Definition of Done (DoD)
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
- [ ] All required automated checks pass (once CI workflows are
      configured).
- [ ] The changes have been merged into the appropriate target branch,
      and the related YouTrack task is updated or closed.

### Additional Considerations

For work involving the Smart Greenhouse, sensors, or experimental data,
the Definition of Done also includes, where applicable:

- [ ] Sensor units, sampling intervals, and relevant calibration
      assumptions are documented.
- [ ] Data collection and processing have been validated against
      the agreed requirements.
- [ ] Experimental results, limitations, and relevant assumptions
      are documented and reproducible.

The Definition of Done is a shared commitment to quality. A user story
is complete only when all of its tasks meet the Definition of Done.
Only completed stories are presented at the Sprint Review; unfinished
stories go back to the backlog and are prioritized again by the Project
Manager.

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
    changes, and interfaces shared between teams with the affected
    teams before implementation.
-   During Sprint Planning, each team breaks the user stories assigned
    to it into tasks and agrees who owns each one (see
    [How We Work](how-we-work.md#sprint-planning)).
-   Raise blockers and integration risks promptly rather than waiting
    until the end of the sprint.
-   Leave the codebase in a state that another member can run,
    understand, and continue working on.

## 10. Quick Checklist

Before requesting review, check that:

-   [ ] My branch follows the naming convention
    (`<type>/<team>/<issue-id>-<short-description>`) and the change is
    focused on one task.
-   [ ] I checked the diff and removed debug code and accidental files.
-   [ ] I ran relevant tests/builds and recorded the results.
-   [ ] I updated comments or documentation where necessary.
-   [ ] My PR title follows `<type>: <short description> (<issue-id>)`.
-   [ ] My PR explains the purpose, scope, and verification steps.

Before merging, check that:

-   [ ] A teammate reviewed and approved the PR.
-   [ ] Required checks pass.
-   [ ] The related YouTrack task is updated.

------------------------------------------------------------------------

*These guidelines are a shared baseline. Repository-specific README
files and agreed team decisions may add stricter requirements.*
