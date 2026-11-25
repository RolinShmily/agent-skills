# 维护钩子

| 触发 | 同步动作 |
| --- | --- |
| 新增 / 重命名 / 删除 skill | 更新 `README.md` 与 `README.zh-CN.md` 的 skill 表；核对 `SKILL.md` 的 `name` / `description` 与 `references/` 路径 |
| 修改 `SKILL.md` 或 `references/` | 核对被引用路径存在；模板占位符不残留 |
| 修改安装方式 / 命令 | 同步 `README.md` 与 `README.zh-CN.md` |
| 修改 README 任一模块 | 同步另一语言版本 |
| 修改贡献流程 / issue 模板 | 同步 `CONTRIBUTING.md`、`.github/ISSUE_TEMPLATE/` 与两份 README 的贡献段 |
| 根目录入口或 skill 目录改名 / 移动 | 更新两份 README 的链接与 `SKILL.md` 引用；本地重新安装 skill |

## 备注

- 不设 docs/：README 即事实源。
