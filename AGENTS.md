# AGENTS.md

Ansible role that installs and configures Tor Onion Services (v3) on Debian (bookworm, trixie).

## Layout

- `defaults/main.yml`: all role variables with defaults; document them in the README
- `tasks/`: `main.yml` (tor, onion services, keys) and `monit.yml` (optional monit checks)
- `templates/`: `torrc.j2`, hostname and key templates; `files/`: apt and monit config
- `handlers/`, `meta/`: handlers and role metadata
- `molecule/default/`: integration test (Docker); depends on `requirements.yml`

## Checks

- `ansible-lint .` must pass without warnings (config in `.ansible-lint`, which excludes `molecule/` and `.github/`)
- `yamllint .` uses `.yamllint`
- `molecule test` runs the role in a container; CI runs it on Debian 12 and 13
- `ansible-lint` creates `.ansible/`; it is git ignored, never commit it

## Conventions

- Use fully qualified module names, quoted octal `mode` values and `true`/`false` booleans in new code
- Give every task a `name`
- New or changed role variables need an entry in `defaults/main.yml` and the README
- Pin GitHub Actions to commit SHAs with a `# vX.Y.Z` comment; Dependabot keeps them current

## Commits and PRs

- Write in English, use conventional commit titles (`feat:`, `fix:`, `chore:`, `ci:`; `!` for breaking changes)
- The PR title sets the release-drafter label (`enhancement`, `bug`, `chore`, `breaking`); a breaking change bumps the major version
- Open PRs as draft and fill in `.github/pull_request_template.md`: what changed and why, plus a breaking changes section if needed
- Do not list changed files or claim test results in the description; CI covers that
