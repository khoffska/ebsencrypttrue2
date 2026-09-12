# AGENTS.md — ebsencrypttrue2

Context for AI coding agents (Claude Code, Codex, opencode, Cursor, …) working in this repo.
Read this first; keep it current.

## What this is
One-off shell utility (2022) that turns on **EBS encryption-by-default** for a list of AWS
regions. Parked/unmaintained — it did its job once; last commit 2022-06.

## Layout
- `encrypt.sh` — loops over `regions.txt` and calls `aws ec2 enable-ebs-encryption-by-default`.
- `regions.txt` — 24 AWS region names, one per line.

## Commands
- Run: `bash encrypt.sh` (needs the AWS CLI and credentials allowed to call
  `ec2:EnableEbsEncryptionByDefault`).
- No build, test, or lint setup in-repo.

## Conventions
- Feature branch → PR; never push to `main` directly.

## Gotchas
- `encrypt.sh` exports `AWS_REGION` **inside** the loop but *after* the `aws` call, so every
  iteration actually hits whatever region is already in the environment — it does not walk the
  list as written. Fix the ordering if this is ever reused.
- Shebang is `#/bin/bash` (missing `!`), so it is not executed as bash; invoke it via `bash encrypt.sh`.
- Turning this on is account-wide and awkward to undo cleanly. Treat it as a deliberate one-shot
  action, not a routine script.

## Open items
None. Assumed dead — archive rather than extend.
