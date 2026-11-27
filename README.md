# Spacesheep skill template

A skill teaches an agent one job. This repo holds one skill in the [Agent Skills](https://agentskills.io/specification) format, ready to tag and release, so Spacesheep can take each release as a new version.

Use this template, rename the skill, write its words, and tag `v1.0.0`.

## What's in it

| Path | What it is |
|---|---|
| `my-skill/SKILL.md` | The skill: a `name` and `description`, then the instructions an agent reads |
| `my-skill/spacesheep.yaml` | Optional: the title, emoji and tags people see in Spacesheep |
| `my-skill/references/example.md` | A file the instructions point to. Add as many as the skill needs |
| `README.md`, `CHANGELOG.md`, `LICENSE`, `.github/` | The repo's own files. They never enter a version |
| `.github/workflows/check.yml` | Checks the skill on every pull request |
| `.github/workflows/release.yml` | Turns a `v*` tag into a GitHub release |

**A repo holds one skill**, in one top-level folder named after it. The folder's name and the `name` in its `SKILL.md` must match.

## Make it yours

1. Pick a name: lowercase letters, digits and single hyphens, at most 64 characters (`weekly-report`).
2. Rename the folder `my-skill/` to it, and set `name:` in `SKILL.md` to the same.
3. Write the `description`: what the skill does and when to use it, in at most 1,024 characters. An agent decides from it whether to use the skill.
4. Write the instructions under the frontmatter. Keep them under 500 lines, and move detail into `references/`.
5. Set the `title`, `emoji` and `tags` in `spacesheep.yaml`, or delete the file.
6. Change `LICENSE` to your own name, or to the licence you want.

## Check it

```bash
npx -y spacesheep@latest skills lint
```

It reads the repo the way Spacesheep does when it takes a release. It needs no sign-in, and your files never leave your machine. A folder that fails says what to fix, one line each.

Passing means the folder is well-formed. Spacesheep still checks each release when it takes it, including what the skill asks to reach.

To try the skill in Claude Code before you release it, copy the folder into `~/.claude/skills/`.

## Release it

1. Add the version's section to `CHANGELOG.md`, in [Keep a Changelog 1.1](https://keepachangelog.com/en/1.1.0/)'s format: a `## [1.1.0] - YYYY-MM-DD` heading, then each change as a bullet under one of `### Added`, `Changed`, `Deprecated`, `Removed`, `Fixed` or `Security`. Keep it to **at most 6 bullets**: Spacesheep shows them on the skill's Versions tab.

   ```markdown
   ## [Unreleased]

   ## [1.1.0] - 2026-12-01

   ### Added

   - A weekly summary at the top of the report.

   ### Fixed

   - Totals counted the first week twice.
   ```

2. Tag and push:

   ```bash
   git tag v1.1.0
   git push origin v1.1.0
   ```

3. `release.yml` checks the skill at that tag and makes the release. Its notes are the `[1.1.0]` section of `CHANGELOG.md`, so write the section before you tag (a tag without one gets its name as its only note). If you edit a release's notes on GitHub later, Spacesheep updates them.

- **A version is a tag `v<major>.<minor>.<patch>` with a release.** A tag like `v1.1.0-rc1` becomes a pre-release, which Spacesheep ignores.
- **Never move a tag.** Spacesheep keeps each tag once, with the commit it pointed at. A tag moved to other files is refused: tag a new version instead.

## Get it into Spacesheep

Registering a repo opens when skills launch on Spacesheep. Until then, build your skill here, check it with `skills lint`, and release it: the releases you make now are the versions Spacesheep takes once you register.

When it opens, you register the repo once, and install Spacesheep's GitHub App on it. That proves the repo is yours, and it sends each new release to Spacesheep. Private repos work the same way.

Each release becomes a new version, waiting for your approval. Nothing is installed or made public until you approve it.

Public repos can also carry the GitHub topic `spacesheep-skill`, which Spacesheep will use to find them.

## What a skill folder may hold

- At most 500 files, 5 MB a file and 25 MB in all.
- Text: `.md`, `.txt`, `.json`, `.yaml`, `.csv`, `.tsv`, `.html`, `.css`, `.js`, `.mjs`, `.ts`, `.py`, `.sh`, `.svg`, and `LICENSE`, `NOTICE` or `COPYING`. Text must be UTF-8.
- Pictures and PDFs: `.png`, `.jpg`, `.gif`, `.webp`, `.pdf`.
- Anything else is refused. `skills lint` names the file.
