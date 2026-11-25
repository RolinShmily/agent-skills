# Agent Skills

**[English](README.md) | [中文](README_zh-CN.md)**

个人维护、跨 agent 通用的 skills 集合。大部分是标准作业流程(SOP),在
Claude Code、Cursor、Codex、Gemini 等不同 agent 之间行为一致。以自用为主,开放共享。

## 安装

```bash
npx skills add <owner>/<repo>
```

自动检测仓库内全部 skill,并交互式选择安装哪些 skill、装到哪些 agent。
非交互式只装某一个 skill 用:

```bash
npx skills add <owner>/<repo> --skill <skill-name>
```

## Skill 向导

| Skill | 用途 |
| --- | --- |
| [project-tidy](project-tidy/SKILL.md) | 整理项目目录:散落文件归入标准结构、统一命名规范、清理无用文件、生成结构说明。只处理源码核心之外的边缘工作,不碰源代码。 |

## 贡献

个人日常 agent 工作流使用的自用 skill——欢迎安装、fork 或发 PR。