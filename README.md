# Nlabella account defaults

This public repository is the shared community and engineering baseline for the
repositories owned by `Nlabella`. GitHub uses supported files here as fallbacks
for repositories of this account that do not provide a local version.

## Repository map

| Path | Purpose |
| --- | --- |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Contribution and engineering workflow |
| [`AGENTS.md`](AGENTS.md) | Operating contract for coding agents |
| [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md) | Community participation standards |
| [`SECURITY.md`](SECURITY.md) | Private vulnerability reporting |
| [`SUPPORT.md`](SUPPORT.md) | Routing for bugs, questions, and proposals |
| [`.github/ISSUE_TEMPLATE/`](.github/ISSUE_TEMPLATE/) | Default bug and feature forms |
| [`.github/pull_request_template.md`](.github/pull_request_template.md) | Default pull-request body |
| [`.github/workflows/governance.yml`](.github/workflows/governance.yml) | The gates this repository runs on itself |
| [`tools/quality/`](tools/quality/) | The checks that keep the content rule and the size rule honest |

This repository publishes no `LICENSE`, and neither does any repository of this
account by default: no licence granted means all rights reserved, which is the
correct posture for private work.

## How account defaults work

- A file inside an individual repository takes precedence over the default
  published here. Add a local file only when a repository genuinely needs a
  different policy.
- GitHub inherits only supported community health files and templates. Workflows
  are not inherited: a gate that should apply everywhere is carried into each
  repository by the template it was generated from.
- Changes here can affect every repository that relies on the default. Review
  them as a change to every repository at once.
- This repository is public. It must contain only general engineering policy.
  Never add hostnames, addresses, file system paths, secret names, credentials,
  infrastructure topology, personal data, or anything specific to a deployment
  environment. The list is deliberately enumerable, because a rule a check can
  be written against outlives a rule that only sounds careful.
- GitHub does not support an inherited default `LICENSE`. A repository that
  means to grant more than nothing publishes its own.

## License

This repository does not publish a license, so default copyright applies and
its contents are not licensed for reuse. `CODE_OF_CONDUCT.md` is the exception:
it is the Contributor Covenant and carries its own CC BY 4.0 terms.
