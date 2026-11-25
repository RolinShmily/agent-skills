# Contributing

Thanks for taking the time to contribute.

## Before you start

- Read [README](README.md) for installation and usage.
- Read [repo-steward/SKILL.md](repo-steward/SKILL.md) for the skill's scope and workflow.
- Skill references and templates live under `repo-steward/references/`.

## Ways to contribute

- **Bug**: open an issue with the **Bug** template. Include the agent and version used, the skill version or commit, steps to reproduce, expected vs actual behavior, and relevant logs.
- **Feature**: open an issue with the **Feature** template. Describe the problem first, then the proposal.
- **Pull request**: fork the repository, create a branch, make the change, and open a PR.

## Skill changes

- Keep `SKILL.md` frontmatter `name` and `description` accurate.
- Every `references/...` path mentioned in `SKILL.md` must exist.
- Replace all `{{...}}` placeholders when adding or editing templates.
- If a skill is added, renamed, or removed, update the skill table in both `README.md` and `README.zh-CN.md`.
- Keep the bilingual READMEs in sync.

## Pull request checklist

- [ ] `SKILL.md` frontmatter is valid.
- [ ] Referenced paths exist; no `{{...}}` placeholders remain.
- [ ] Both READMEs are updated when the skill list or install steps change.
- [ ] Changes stay within the skill assets.
