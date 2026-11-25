# Agent Skills

**[English](README.md) | [中文](README.zh-CN.md)**

A personal, agent-agnostic collection of skills. Most are procedural SOPs
(standard operating procedures) that work the same across AI agents —
Claude Code, Cursor, Codex, Gemini, etc. Built for self-use first, shared
in the open.

## What you need

- Node.js 22.20 or later (includes `npx`)

## Install

```bash
npx skills add RolinShmily/agent-skills
```

Discovers every skill in the repo, then lets you choose which skills and
which agents to install to. To install a specific skill non-interactively:

```bash
npx skills add RolinShmily/agent-skills --skill <skill-name>
```

## Skills

| Skill | What it does |
| --- | --- |
| [repo-steward](repo-steward/SKILL.md) | Persistently maintain and standardize a project's edge assets: docs set, test samples, CI workflows, bilingual README, changelog, license/notices, and root dotfiles. Records maintenance hooks in AGENTS.md; never touches source code. |

## Contribute

These are personal skills for daily agent workflows — install, fork, or
send a PR. See [CONTRIBUTING.md](CONTRIBUTING.md) for the skill format and
PR checklist. Feedback welcome.

## License

[MIT](LICENSE)
