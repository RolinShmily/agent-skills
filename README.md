# Agent Skills

**[English](README.md) | [中文](README_zh-CN.md)**

A personal, agent-agnostic collection of skills. Most are procedural SOPs
(standard operating procedures) that work the same across AI agents —
Claude Code, Cursor, Codex, Gem‑ini, etc. Built for self-use first, shared
in the open.

## Install

```bash
npx skills add <owner>/<repo>
```

Discovers every skill in the repo, then lets you choose which skills and
which agents to install to. To install a specific skill non-interactively:

```bash
npx skills add <owner>/<repo> --skill <skill-name>
```

## Skills

| Skill | What it does |
| --- | --- |
| [project-tidy](project-tidy/SKILL.md) | Tidy a project directory: regroup files into standard folders, normalize naming, clean up dead files, produce a structure overview. Edge work only — never touches source code. |

## Contribute

These are personal skills for daily agent workflows — install, fork, or
send a PR. Feedback welcome.