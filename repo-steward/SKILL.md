---
name: repo-steward
description: 持久维护并标准化项目的边缘资产（双语 README、docs 四件套、CHANGELOG、CONTRIBUTING、LICENSE、THIRD_PARTY_NOTICES、.git* 配置、tests/、GitHub workflows），聚焦文档、测试样例与自动化，并生成/更新 AGENTS.md 维护钩子。当用户要求"整理项目目录""标准化项目结构""补齐开源文件""理一理 CI/发布/CHANGELOG""给项目写 AGENTS.md"等时使用。不修改源码逻辑。
---

# repo-steward — 边缘资产的持久化维护与标准化

把项目"除源码之外"的边缘资产整理清楚，聚焦三块：**文档层**（README、docs 四件套）、**测试样例**、**自动化**（GitHub workflows）；顺带整理根目录边缘文件与 dotfiles，并把维护钩子写进 `AGENTS.md`。

**不判断项目成熟度，不做等级评定，也不做范围分级。** 按标准资产目录盘点，按项目实际与用户确认执行。`AGENTS.md` 只记录需要持久执行的维护钩子与影响维护的例外，不记录 skill 的判断过程。

## 操作范围

范围按**边缘资产**划定，不以目录层级为界：

- 入口：双语 README、`AGENTS.md`。
- 文档：`docs/` 四件套。
- 版本与测试：`CHANGELOG.md`、`tests/`。
- 自动化：`.github/workflows/`。
- 合规与仓库配置：`LICENSE`、`THIRD_PARTY_NOTICES`、`.git*`。
- 贡献：`CONTRIBUTING.md`、issue/PR 模板、`CODE_OF_CONDUCT.md`。
- 资产出现在子目录时（如 monorepo 子项目入口），仍按资产类型处理，不按层级扩张。

不在范围内：源码逻辑、测试代码内容、依赖版本、实际发布/部署、敏感文件。

## 触发词

- 「整理项目目录 / 标准化项目结构 / 理一理这个项目」
- 「补齐开源文件 / README 规范化 / 加 CHANGELOG / CONTRIBUTING」
- 「CI 梳理 / 发布流程整理 / workflow 命名」
- 「给项目写 AGENTS.md / 让 agent 记住维护约定」

## 标准资产目录

| 层 | 资产 | 说明 |
| --- | --- | --- |
| 入口 | `README.md` + `README.zh-CN.md` | 三模块：是什么 / 需要什么 / 怎么用；保持精简 |
| 入口 | `AGENTS.md` | 维护钩子清单，本 skill 生成/更新 |
| 文档 | `docs/` 四件套 | 见下 |
| 版本 | `CHANGELOG.md` | 进入版本管理后引入；与 release 配套 |
| 版本 | `tests/` | 按源码层级组织测试样例 |
| CI | `test.yml` | 普通 CI：checkout → setup → install → 跑 `tests/` 样例 |
| CI | `deploy.yml` | 网站 / Worker 即时部署 |
| CI | `publish.yml` | 包分发（npm / PyPI 等） |
| CI | `build.yml` | 构建产物，与 release assets 搭配 |
| CI | `release.yml` | 读 git tag + CHANGELOG 生成 Release；基础情况不发 assets |
| CI | `update.yml` | 定时数据更新 |
| 合规 | `LICENSE` | 默认 MIT，写姓名与年份 |
| 合规 | `THIRD_PARTY_NOTICES` | 保留原文 + 引用位置 |
| Git | `.gitignore` / `.editorconfig` / `.gitattributes` / `.gitmodules` | 按需 |
| 贡献 | `CONTRIBUTING.md` | 指向构建/测试文档与 issue/PR 路径 |
| 贡献 | `.github/ISSUE_TEMPLATE/bug.yml` / `feature.yml` | 接受 issue 时 |
| 贡献 | `.github/PULL_REQUEST_TEMPLATE.md` / `CODE_OF_CONDUCT.md` | 社区活跃后按需，形式大于操作 |

### 文档层（docs 四件套）

README 保持精简（是什么 / 需要什么 / 怎么用），其余说明由 `docs/` 承担：

| 文件 | 职责 |
| --- | --- |
| `docs/architecture.md` | 架构：系统组成、分层、数据流、边界 |
| `docs/development.md` | 开发：构建流程、测试规范、本地环境、扩展方式 |
| `docs/design.md` | 设计约束：为什么这样架构，权衡与取舍 |
| `docs/reference.md` | 速查：CLI 用法、参数、API 结构、JSON Schema 标准等 |

启用 docs 时固定为这四篇；README 足以独立承载全部说明的项目（如个人博客）可刻意不设，并在 `AGENTS.md` 的备注中写明。

## 工作流程

### 0. 前置检查

- `pwd` 确认目标项目；`git status` 确认没有未提交的并发改动。
- 读取根目录 `AGENTS.md`（若存在）作为既有维护钩子，后续按它审计。
- 涉及删除或移动时，先确认目标不在敏感清单（`.env*`、密钥、token）。

### 1. 盘点（只读）

输出一份清单：

- 根目录入口文件与目录
- `docs/` 四件套是否存在、职责是否错位
- `.github/workflows/`、`.github/ISSUE_TEMPLATE/`、PR 模板
- `tests/` 目录结构
- 按标准资产目录逐项标注：存在 / 缺失 / 命名不一致
- 双语 README 是否具备三模块，是否足够精简

盘点结果只用于本次提案，不写入 `AGENTS.md`。

### 2. 提案

用表格逐条列出：

| 操作 | 对象 | 从 → 到 | 原因 |
| --- | --- | --- | --- |

操作类别：新建、移动、重命名、合并、归档、补模板、拆分/收敛文档。每项注明是标准项还是项目特有取舍；不确定用途的文件不删、不移，列入待确认。

### 3. 执行

- 只动边缘资产：根目录入口文件与目录、`docs/`、`.github/`、`tests/`、`AGENTS.md`。
- 文件内容使用 `references/templates/` 下的模板生成，替换全部 `{{...}}` 占位符。
- 移动/重命名后同步更新引用（README 链接、workflow 路径、配置指向）。
- 删除一律精确路径 + 用户确认；禁止 `rm -rf`。

### 4. 生成/更新 AGENTS.md（维护钩子，增量追加）

`AGENTS.md` 是给后续 agent 的**维护钩子清单**，不是项目清单或检查报告。按 `references/agents-md.md` 写入，整个文件只保留：

1. **维护钩子（主体）**：一个大标题下的“触发 → 同步动作”表
2. **备注**：只在“异”时写（影响维护的例外，如“不设 docs，README 即事实源”）

不写项目介绍、结构清单、构建/测试命令、红线或盘点结果。非标准结构（如源码不是 `src/` 而是自定义名称平铺）不属于“异”，不写入。

**有则加操作，异则加备注，无则什么也不加。**

维护钩子至少覆盖：

| 触发 | 同步动作 |
| --- | --- |
| 功能新增 / 行为变更 | `CHANGELOG.md` 未发布段；README 三模块；`docs/architecture.md` 或 `docs/design.md`；`tests/` 对应样例 |
| CLI / 参数 / API / JSON Schema 变更 | `docs/reference.md` |
| 构建 / 测试流程变更 | `docs/development.md` |
| 依赖 / 第三方代码 / 资源变更 | `THIRD_PARTY_NOTICES` |
| 版本发布（tag） | `CHANGELOG.md` 归档；GitHub Release 文案 |
| 根目录入口文件/目录或资产位置变更 | README 结构说明（如有）；`AGENTS.md` 自身；workflow 路径 |
| workflow 新增 / 触发变更 | `AGENTS.md` workflow 地图；`docs/development.md` |
| `tests/` 结构与样例变更 | `AGENTS.md` tests 约定；`test.yml` 路径 |

钩子是给 agent 读的 SOP，不是可执行脚本；如需映射到具体 agent 的 hook 机制，另行处理，不在本 skill 默认范围。

**写入方式：增量追加。** 先读取现有 `AGENTS.md`，只在末尾追加；不重写、不删除、不重排既有条目。需要修正旧条目时，追加一条带日期与原因的「修订」记录，保留原文。

**追加克制。** `AGENTS.md` 是每轮 loop 都会追加的记忆文件，必须控制体积：

- 追加前查重：已有条目能覆盖的，不重复追加。
- 优先写通用钩子（按变化类别），而不是一次一事的细碎记录。
- 只追加持久有效的维护义务；一次性判断、本轮操作日志、临时说明不写入。
- 没有新增维护义务时，本轮不追加。

### 5. 复核报告

- 最终资产清单与根目录树
- 改动明细（新建/移动/重命名/合并/归档）
- `AGENTS.md` 的新增或变更摘要
- 遗留待确认项

## 参考

references 是参考资料与模板，不是强制结构；最终以项目实际与用户确认为准。

- `references/asset-catalog.md`：资产完整清单与启用条件
- `references/docs-set.md`：docs 四件套的职责边界
- `references/agents-md.md`：`AGENTS.md` 维护钩子模板
- `references/templates/`：README、docs、CHANGELOG、CONTRIBUTING、LICENSE/NOTICES、dotfiles、workflows、issue/PR 模板
- `references/structures.md`：目录结构的阶段演进与模块组合

## 红线

- 不改源码逻辑，不重写测试内容。
- 不删未确认文件；不碰敏感文件。
- 不执行发布、部署、发包。
- 不自动提交、推送或改写 git 历史；需要时由用户明确要求。
- 不输出项目成熟度评级，不做范围分级；只按标准资产目录与项目实际执行。
- `AGENTS.md` 只写维护钩子与影响维护的备注，不写项目上下文、结构清单或 skill 的判断过程。
- `AGENTS.md` 只做增量追加，不重写、不删除既有内容；追加须克制（查重、写通用钩子、无新增义务不写）。
- 不强制套模板；结构差异不写入 `AGENTS.md`，只记录维护钩子与影响维护的例外。
