# Agent Skills

A personal, agent-agnostic collection of skills. Most are procedural SOPs
(standard operating procedures) that work the same across AI agents —
Claude Code, Cursor, Codex, Gem‑ini, etc. Built for self-use first, shared
in the open.

## Install

```bash
npx skills add <owner>/<repo>
```

Installs every skill in this repo. To install a single skill instead:

```bash
npx skills add <owner>/<repo>/<skill-name>
```

## Skills

| Skill | What it does |
| --- | --- |
| [project-tidy](skills/project-tidy/SKILL.md) | Tidy a project directory: regroup files into standard folders, normalize naming, clean up dead files, produce a structure overview. Edge work only — never touches source code. |

## Layout

```
repo/
└── skills/
    └── <skill-name>/
        └── SKILL.md
```

Each skill is a folder under `skills/` holding its own `SKILL.md` plus
optional `references/`. This follows the [skills.sh](https://skills.sh)
standard, so the pack stays installable through `npx skills add`.

## Contribute

These are personal skills for daily agent workflows — install, fork, or
send a PR. Feedback welcome.