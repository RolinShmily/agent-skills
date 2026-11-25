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
| [repo-steward](repo-steward/SKILL.md) | 持久维护并标准化项目的边缘资产:文档层、测试样例、CI workflows、双语 README、CHANGELOG、LICENSE/第三方声明与根目录 dotfiles。通过 AGENTS.md 记录维护钩子,不碰源代码。 |

## 贡献

个人日常 agent 工作流使用的自用 skill——欢迎安装、fork 或发 PR。