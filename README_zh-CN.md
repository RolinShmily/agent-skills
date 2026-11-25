# Agent Skills

**[English](README.md) | [中文](README_zh-CN.md)**

个人维护、跨 agent 通用的 skills 集合。大部分是标准作业流程(SOP),在
Claude Code、Cursor、Codex、Gemini 等不同 agent 之间行为一致。以自用为主,开放共享。

## 安装

```bash
npx skills add <owner>/<repo>
```

安装本仓库全部 skill。只装其中某一个 skill 用:

```bash
npx skills add <owner>/<repo>/<skill-name>
```

## Skill 向导

| Skill | 用途 |
| --- | --- |
| [project-tidy](skills/project-tidy/SKILL.md) | 整理项目目录:散落文件归入标准结构、统一命名规范、清理无用文件、生成结构说明。只处理源码核心之外的边缘工作,不碰源代码。 |

## 目录结构

```
repo/
└── skills/
    └── <skill-name>/
        └── SKILL.md
```

每个 skill 是 `skills/` 下一个文件夹,内含自身的 `SKILL.md` 及可选的
`references/`。遵循 [skills.sh](https://skills.sh) 标准,因此可用
`npx skills add` 一键安装。

## 贡献

个人日常 agent 工作流使用的自用 skill——欢迎安装、fork 或发 PR。