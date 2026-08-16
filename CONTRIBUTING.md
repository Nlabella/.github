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
  `feature/Ricerca_Ricette`. The governance check refuses the rest, and the
  branch rules refuse to create it in the first place.
- Never push to `main`, including while working alone. Open a pull request for
  every change, including changes made while working alone.
- **Squash merge.** The pull-request title becomes the durable commit message,
  so write it as one.
- Delete merged branches. This is set to happen automatically; if a repository
  is accumulating branches, that setting is off and it is a bug.

Release and hotfix branches are not part of this workflow. A repository that
needs them needs a different model, and should say so in its own
`CONTRIBUTING.md` rather than bending this one.

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

## Deployments

Applications here deploy to a VPS through GitHub Actions, and which host they
reach is decided by who owns the repository — not by anything written in the
repository itself. Moving a project between owners is therefore a checklist and
not a change to code.

Secrets follow one rule: **if GitHub has to supply it, it lives in the
repository's Actions secrets; if the host can invent it, it never leaves the
host.** Database passwords are generated on the machine and are not in GitHub.

## Licensing

No licence is granted by default, which under copyright means all rights are
reserved. That is the correct posture for private work; a repository that means
to grant more publishes its own `LICENSE`.
