# Agent operating contract

These rules apply to every human-guided or autonomous coding agent working in
this repository.

Read `CONTRIBUTING.md` first. It is the engineering workflow in full, this file
is what an agent needs before its first edit, and where they overlap
`CONTRIBUTING.md` is the longer explanation rather than a second opinion.

## Memoria condivisa

Prima di qualunque altra cosa, carica la memoria degli agenti:

1. Se lavori sul PC e Claude Code ha già `MEMORY.md` in contesto, vai al
   punto 3. Altrimenti aggiungi `Mylabella/agent-memory` alla sessione (in
   Claude Code cloud: strumento `add_repo`, in lettura) e clonalo accanto a
   questo repository:
   `git clone -b develop https://github.com/Mylabella/agent-memory ../agent-memory`
2. Leggi `../agent-memory/MEMORY.md` per intero.
3. Apri `shared/`, poi la cartella di questo account e di questo repository
   se esistono, seguendo i `[[link]]`.

Un fatto imparato qui si scrive là, mai in questo repository: la procedura è
in `../agent-memory/AGENTS.md`.

## The shared contract is not replicated here

Every repository generated from `agentic-development-template` carries a block
of shared rules, identical byte for byte, delimited by
`<!-- BEGIN organization contract -->`. The template holds the canonical text
and `check_agents_contract.py` propagates it with `--write`. This account is a
person rather than an organization, and the block still governs the personal
repositories born from that template, because they carry its machinery.

**That block is deliberately absent from this repository**, and the absence is
the rule rather than an oversight to correct. `check_agents_contract.py`
requires a repository to adopt the contract and the machinery together, or
neither: the contract names the check that verifies each rule, and a rule whose
detector is missing is a promise nothing keeps. Of the files it requires, this
repository has two — `tools/quality/check_diff_size.py` and
`.claude/settings.json`. The rest are absent, and most of them have no subject
here at all: this repository has no database, no committed contract, no decision
log and no release path, because `main` is its only branch.

Copying the block in without them would be the failure the check exists to
catch. Editing the block to remove the sentences that point at missing files is
the same failure by the other road, and it has happened once already: a
repository reworded the shared text to fix a broken promise, which is exactly
how one rule became four versions.

So the contract is honoured here by reference. **Read it in
`agentic-development-template/AGENTS.md` before working in any repository of
this account, including this one.** What follows is only what is specific to
this one, and it does not repeat what the contract already says.

## What this repository is

The account's default community health files. GitHub serves the supported ones
as fallbacks to any repository of this account that does not carry its own, so
a change here can take effect in repositories nobody touched. Review a change as
a change to every repository at once.

What is inherited is a closed list: `CODE_OF_CONDUCT.md`, `CONTRIBUTING.md`,
discussion category forms, `FUNDING.yml`, issue and pull request templates with
their `config.yml`, `SECURITY.md`, `SUPPORT.md`.

**Workflows are not on it.** `.github/workflows/` is not inherited by anything;
it runs for this repository alone. A gate that should apply everywhere has to be
added to every repository, and on a personal account there is no organization
ruleset to require it from one place: the template is what carries it.

This repository sets policy for private repositories and is itself public. That
asymmetry is the reason for the strictest rule below.

## What this repository may contain

Only general engineering policy. Never a hostname, an address, a filesystem
path, the name of a secret, a credential, infrastructure topology, personal
data, or anything specific to a deployment environment.

`verify_public_content.py` enforces this over **every tracked file outside
`tools/` and `tests/`** — this file included, and workflow comments and commit-
adjacent prose with it. It refuses a link to a host outside a short allowlist,
so naming a service beats linking it, and an API endpoint under `api.github.com`
fails even inside a code fence. It also refuses truncation and merge-conflict
markers, because text that was never finished is something a reader assumes
they misread.

Run it before proposing any change to a published file.

## How a branch is named

`feature/<description>`, `fix/<description>` or `chore/<description>`, lowercase
with hyphens, and nothing else: these repositories release from `main` and have
no release or hotfix branches to name. `dependabot/` is exempt, because
Dependabot names its own branches.

This repository has no `.claude/hooks/branch_guard.py`, so a cloud session's
assigned `claude/...` branch **is not renamed for you**. Rename it by hand,
before any work exists on it:

```sh
git branch -m chore/<description>
git branch --unset-upstream
```

The rename is local; it touches no remote ref and cannot close a pull request. A
remote branch the harness already created is left where it is — deleting a
remote ref is destructive and is not needed to get the name right.

The step named "Check the branch name" in `.github/workflows/governance.yml`
speaks at the merge. It carries the grammar inline rather than in a script,
because this repository does not have `check_branch_name.py` either. A ruleset
would not do the job: metadata rules are not enforced below an Enterprise plan,
and a private repository on this account's plan has no rulesets at all.

## Nobody but the author is credited

The rule is the shared contract's; read it there. Two things are specific to
this repository.

`.claude/settings.json` carries `"attribution": {"commit": "", "pr": ""}` and
**nothing else** — no hooks. `authorship_guard.py` and `branch_guard.py` import
their patterns from `check_authorship.py`, which is not here, and declaring
hooks that do not exist would print an error on every shell call: noise that
stops nothing. So the tool's own footers are suppressed, and everything else is
manual.

That setting governs what the tool appends. It does not reach the identity: a
cloud session sets an agent's name and address in the *global* git config, so
its commits are authored by a tool however clean the message is. Set
`user.name` and `user.email` for this repository before the first commit.
Nothing here checks it — `check_authorship.py` is one of the absent files — so
it is on you.

## Where a change goes, and how large

Open the pull request against `main`; there is no other permanent branch. Never
push to `main` directly, including while working alone: nothing on this plan
refuses the push, so the rule is kept by the person, and `CONTRIBUTING.md` says
why it is a rule anyway.

A pull request is refused above 6000 hand-written added lines by
`check_diff_size.py`, measured against the merge base with `main`. Lockfiles,
generated files and deletions do not count, and what does not count is read out
of `main`'s `.gitattributes` rather than the branch's, so a change cannot exempt
its own payload.

## Before it is finished

Run what the pull request will run:

```sh
python3 tools/quality/check_diff_size.py
python3 tools/quality/verify_public_content.py
python3 -m unittest discover -s tests
```

The pull-request body follows `.github/pull_request_template.md`. This
repository has no `check_pr_brief.py`, so the `## Brief` and `## Rischi
residui` sections that template-born repositories require are not used here.

Never weaken, skip or delete a gate to make a change pass, and never report
success without having run the checks.
