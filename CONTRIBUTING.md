# Contributing to Nlabella's projects

These are personal repositories — a family recipe archive, home automation, a
few tools. Most of the time the only contributor is their author. The rules
below exist anyway, and for one reason: a rule that only applies when someone is
watching is not a rule, and these repositories deploy to a real machine.

This file is the default for repositories owned by `Nlabella`. A repository may
publish its own `CONTRIBUTING.md` when its tooling requires different rules; the
repository-local file takes precedence.

Participation is subject to the
[Code of Conduct](https://github.com/Nlabella/.github/blob/main/CODE_OF_CONDUCT.md).
Never disclose a suspected vulnerability publicly — see
[SECURITY.md](https://github.com/Nlabella/.github/blob/main/SECURITY.md).

## Before contributing

1. Read the target repository's README and its `AGENTS.md`, which is where the
   rules that matter to a change actually live.
2. Search existing issues and pull requests to avoid duplicates.
3. Keep secrets, personal data and production details out of issues, logs,
   examples and commits. A private repository is not a safe place for a
   credential: history outlives the file, and visibility can change.

## Branching

**One branch is permanent: `main`.** There is no `develop` here, and that is a
choice rather than an omission — these repositories release continuously, from
`main`, with nothing waiting between finished and live.

- Work on a short-lived `feature/<description>`, `fix/<description>` or
  `chore/<description>` branch, cut from `main` and merged back into it.
  Those three are the entire list. A tool's default branch name is not an
  exception to it, and neither is an agent's.
- Lowercase with hyphens: `feature/le-ricette-si-cercano`, not
  `feature/Ricerca_Ricette`. The governance check refuses the rest at the
  merge. Branch rules would refuse the creation too, and on this account's
  plan they do not exist on a private repository: the check is the whole
  enforcement, which is why it is in every repository rather than in a
  setting.
- Never push to `main`, including while working alone. Open a pull request for
  every change, including changes made while working alone. Nothing on this
  plan refuses a direct push to a private repository; what refuses to *act* on
  one is the repository itself — a host converges, and an application deploys,
  only a commit some merged pull request produced.
- **Squash merge.** The pull-request title becomes the durable commit message,
  so write it as one. A repository that keeps its history in step with another
  — a fork that takes improvements from its upstream as merges — may prefer a
  merge commit for those pull requests, and says so in the pull request.
- Delete merged branches. This is set to happen automatically; if a repository
  is accumulating branches, that setting is off and it is a bug.

Release and hotfix branches are not part of this workflow. A repository that
needs them needs a different model, and should say so in its own
`CONTRIBUTING.md` rather than bending this one. A repository generated from
`Mylabella/agentic-development-template` is such a repository: it arrives with
`develop` and the template's own rules, and those rules are the ones its gates
enforce.

## Do not stack pull requests

Never open a pull request whose base is another open pull request's branch.
Either make the two changes independent, or finish and merge the first before
opening the second.

Squash merge replaces a branch's commits with one new commit on `main`, so when
the base pull request merges, the stacked one points at a branch that no longer
leads anywhere: **its changes silently do not reach `main`, and nothing reports
this.**

Renaming a branch that has an open pull request is the same class of mistake and
can close the pull request outright. Rename before opening it, or open a new one.

## Who merges

An author may merge their own pull request when every gate is green and the
change is under 1000 hand-written lines. Above that line, or on any of these
triggers, stop and ask the owner instead of deciding:

- a change to a published contract, or a response field removed or narrowed;
- a migration that removes or narrows anything a running previous version reads;
- a new secret, or a new environment variable read at runtime;
- a change to a workflow's `permissions:` or `secrets:` block;
- a new externally reachable route, or any change on an authentication or
  authorization path;
- a new direct dependency;
- a test deleted, skipped, or marked expected-to-fail.

The boundary is the measurement, not the identity. GitHub never lets an author
approve their own pull request, and on a single-person account nobody else can,
so a rule that says "the owner merges" is satisfied by every merge including the
ones nobody read. A size limit and a trigger list can each be checked. For the
same reason nobody is asked to attest that they reviewed their own work: an
attestation written by the party that wrote the change records nothing.

## Dead code

Remove what is no longer used, in the change that stops using it. Do not leave a
commented-out block, an unreferenced function, a module nothing imports, a table
nothing reads, a placeholder never filled, or a document whose claims have become
false.

What a tool can only guess — a module with no importer outside its own test, an
endpoint with no caller, a table with no reader — belongs in the repository's
dead-code inventory, and every entry carries a date. The date is the point: an
entry without a deadline is abandonment with better manners.

Test coverage does not answer this question. A module with its own passing test
suite and no production caller is fully covered and entirely dead.

## Backend and frontend change together

A change to one side carries the other side in the same pull request. Adding an
endpoint means adding its caller; removing a response field means removing its
reader; adding a value to a vocabulary means adding the label that renders it.

Where a generated client exists, the generation is the enforcement, and the
generated file is never edited by hand.

Landing one side alone is permitted only when the owner says so explicitly, in
that pull request. It is then recorded as an open issue labelled `parity-debt`
stating what is missing, on which side, and the date by which it closes. The
circle is closed by closing the issue, never by merging the pull request that
opened it.

## Pull requests

- Say what the change is for and how to check it. Where a repository's gates ask
  for a specific shape — a `## Brief` with numbered criteria and a runnable
  command for each — that shape is the rule, and **a criterion nobody can run is
  a criterion nobody can check.**
- Every gate must be green. A gate that is failing for an unrelated reason is a
  reason to fix the gate, not to merge past it.
- **A new gate must be watched failing before it is trusted**, and the way it was
  broken belongs in its record. A gate nobody has seen refuse something is a
  belief, not a check.
- Keep pull requests focused and reviewable. **A pull request over 6000
  hand-written lines is refused**; lockfiles, generated clients and fixtures do
  not count towards that number, and neither do deleted lines — dead code is
  removed in the change that stops using it, and a gate that refuses a large
  deletion argues with that rule and loses. It is not the same number as the
  one under *Who merges*: that one is about how much a person may land without
  asking, this one is about how much anybody can be expected to read.

That is a gate and not a hope: `tools/quality/check_diff_size.py` counts the
lines a change adds against the merge base with `main` and fails the pull
request over the limit. What does not count is read back out of `main`'s
`.gitattributes` rather than from a list kept here, and out of `main`'s copy on
purpose — a change that could declare its own payload generated would be writing
the rule it is measured by. The base is read by name and the merge base computed
on the spot, rather than taken from what GitHub recorded when the pull request
was opened, so a pull request left open while other work lands is not charged
for that work.

## AI-assisted contributions

AI tools may assist with research, code, tests, or documentation. The human
author remains accountable for the entire contribution and must:

- understand and review every submitted change;
- verify behavior with appropriate tests or direct observation;
- check licenses, attribution, privacy, and security implications;
- never submit secrets, confidential data, or material they are not permitted
  to share to an external model or service.

Do not attribute authorship to a tool. No co-author trailer, no generated-with
footer, and no standing disclosure section in the pull-request body: a squash
turns that body into the commit message, so a line that is true of every change
would be recorded forever on every change while informing nobody.

Saying so is not enough. The trailers arrive anyway when the tool adds them on
its own and nobody reads every commit message, so turn them off at the source.
In Claude Code that is `"attribution": {"commit": "", "pr": ""}` in the
repository's `.claude/settings.json` — committed, so it reaches every clone and
every cloud session, which a setting in a home directory reaches neither of.

Check the identity as well as the message, because it is the half that gets
missed: a cloud session sets `user.name` and `user.email` to the agent in the
*global* git config, so its commits are authored by a tool however clean the
message is. Set them per repository to the person who owns the work, or set
`GIT_AUTHOR_NAME`, `GIT_AUTHOR_EMAIL`, `GIT_COMMITTER_NAME` and
`GIT_COMMITTER_EMAIL` on the environment once.

Generated output is evidence to inspect, not proof that a change is correct.

## Dependencies

Before adding a direct dependency:

1. check the language standard library and existing dependencies;
2. compare maintenance, security history, license, size, and transitive
   dependencies;
3. document why owning a small implementation would be worse;
4. pin or lock the selected version using the stack's standard mechanism;
5. add automated update and vulnerability monitoring where the repository
   supports it.

Remove dependencies that are unused, duplicated, abandoned, or no longer worth
their operational cost.

## Deployments

Applications here deploy to a VPS through GitHub Actions, and which host they
reach is decided by who owns the repository — not by anything written in the
repository itself. Moving a project between owners is therefore a checklist and
not a change to code.

Secrets follow one rule: **if GitHub has to supply it, it lives in the
repository's Actions secrets; if the host can invent it, it never leaves the
host.** Database passwords are generated on the machine and are not in GitHub.
There are no account-level secrets on a personal account, so every application
repository holds its own copy of what it needs, and each copy is a rotation
target.

Publishing a GitHub Release is the production approval event for an
application: it promotes an already-built immutable artifact and must not
rebuild different bytes. A repository that describes infrastructure rather than
producing an artifact has nothing to release, and converges from `main` instead:
there, merging is the approval event. Applications are released because a
release is a decision about a build; shared services are converged because there
is no build to decide about.

## Licensing

No licence is granted by default, which under copyright means all rights are
reserved. That is the correct posture for private work; a repository that means
to grant more publishes its own `LICENSE`.
