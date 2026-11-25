# 资产目录与启用条件

按**资产类型**盘点，不以目录层级为界。每项标注路径、作用、启用条件与依赖关系。

## 1. 入口层

| 资产 | 路径 | 作用 | 启用条件 |
| --- | --- | --- | --- |
| 双语 README | `README.md` + `README.zh-CN.md` | 项目入口；三模块：是什么 / 需要什么 / 怎么用；保持精简 | 所有项目 |
| 维护钩子 | `AGENTS.md` | 只含“触发 → 同步更新”钩子表与备注 | 所有项目 |

- README 只做路由，不承载长篇架构或 API 细节；细节放 `docs/`。
- README-only 项目（如个人博客）把全部说明留在 README，并在 `AGENTS.md` 的备注中写明“不设 docs”。
- 双语文件名统一为 `README.zh-CN.md`，不混用 `README_zh.md`。

## 2. 文档层

| 资产 | 路径 | 作用 | 启用条件 |
| --- | --- | --- | --- |
| 架构 | `docs/architecture.md` | 系统组成、分层、数据流、边界 | 启用 docs 时 |
| 开发 | `docs/development.md` | 构建、测试、本地环境、扩展 | 启用 docs 时 |
| 设计 | `docs/design.md` | 设计约束、架构选择的权衡 | 启用 docs 时 |
| 参考 | `docs/reference.md` | CLI、参数、API、JSON Schema 速查 | 启用 docs 时 |

默认启用 docs；README 足以独立承载全部说明的项目可刻意不设。四件套之外不额外加索引文件，README 直接链接四篇。职责边界见 `docs-set.md`。

## 3. 版本与测试

| 资产 | 路径 | 作用 | 启用条件 |
| --- | --- | --- | --- |
| 变更日志 | `CHANGELOG.md` | 版本历史；release workflow 的数据源 | 进入版本管理后 |
| 测试样例 | `tests/` | 按源码层级组织测试样例与夹具 | 有测试时 |

- `CHANGELOG.md` 与 `.github/workflows/release.yml` 配套：Action 读取 tag 对应段落生成 Release 文案。
- `tests/` 的组织跟随源码层级，例如 `tests/core/`、`tests/gui/`、`tests/worker/`。
- 基础 release 不附带 assets；需要二进制或安装包时再加 `build.yml`。

## 4. CI / 自动化

| 资产 | 路径 | 作用 | 启用条件 |
| --- | --- | --- | --- |
| 测试 | `.github/workflows/test.yml` | 普通 CI:checkout → setup → install → 跑 `tests/` 样例 | 有测试时 |
| 部署 | `.github/workflows/deploy.yml` | 网站 / Worker 即时部署 | 有线上服务时 |
| 发布包 | `.github/workflows/publish.yml` | npm / PyPI 等包分发 | 有包分发时 |
| 构建 | `.github/workflows/build.yml` | 构建产物，与 release assets 搭配 | 有二进制或产物时 |
| 版本发布 | `.github/workflows/release.yml` | 读 git tag + CHANGELOG 生成 GitHub Release | 有 tag 发布时 |
| 定时更新 | `.github/workflows/update.yml` | 定时拉取或生成数据 | 有数据更新任务时 |

workflow 文件统一使用小写短名，一个文件只承担一个目的。模板见 `templates/workflows/`。

> 模板默认以 Node 为例；Python 换 `setup-python` + `uv`/`pip`，C++ 换 CMake 构建步骤，静态站点把 deploy 步骤换成对应平台的部署 action。

## 5. 合规与仓库配置

| 资产 | 路径 | 作用 | 启用条件 |
| --- | --- | --- | --- |
| 许可证 | `LICENSE` | 开源许可证 | 开源项目 |
| 第三方声明 | `THIRD_PARTY_NOTICES` | 第三方代码/资源的许可证原文与引用位置 | 含第三方内容时 |
| 忽略规则 | `.gitignore` | 忽略构建产物、缓存、密钥 | 所有项目 |
| 编辑器约定 | `.editorconfig` | 缩进、换行、编码 | 所有项目 |
| 属性 | `.gitattributes` | 换行、二进制、语言统计 | 所有项目 |
| 子模块 | `.gitmodules` | 子模块声明 | 有子模块时 |

- `LICENSE` 默认 MIT，写年份与作者名；使用其他许可证时保留原文不改。
- `THIRD_PARTY_NOTICES` 必须保留第三方许可证原文，并标注项目内的引用位置（文件或目录）。

## 6. 贡献与社区

| 资产 | 路径 | 作用 | 启用条件 |
| --- | --- | --- | --- |
| 贡献指南 | `CONTRIBUTING.md` | 指引构建/测试文档、issue/PR 路径 | 接受外部贡献时 |
| issue 模板 | `.github/ISSUE_TEMPLATE/bug.yml` / `feature.yml` | bug 定位 / 新功能提案 | 接受 issue 时 |
| PR 模板 | `.github/PULL_REQUEST_TEMPLATE.md` | PR 自检清单 | 社区活跃后按需 |
| 行为契约 | `CODE_OF_CONDUCT.md` | 社区行为规范 | 社区活跃后按需 |

- PR 模板与 `CODE_OF_CONDUCT.md` 属于“形式大于操作”的资产；没有社区活动时不必预置。
- `CONTRIBUTING.md` 只做指引，不重复 `docs/development.md` 的内容。

## 7. 依赖关系

| 上游 | 下游 |
| --- | --- |
| `README.md` | `docs/*`、`LICENSE`、`CONTRIBUTING.md` |
| `CHANGELOG.md` | `release.yml` |
| `tests/` | `test.yml` |
| `package.json` / `pyproject.toml` | `publish.yml` |
| 构建产物 | `build.yml` → `release.yml` assets |
| 依赖变更 | `THIRD_PARTY_NOTICES` |
| 根目录入口变更 | `AGENTS.md`、README 结构说明 |

## 8. 命名约定

- 目录与文件：小写 + 连字符，或遵循生态惯例（如 `CMakeLists.txt`、`pyproject.toml`）。
- 双语 README：`README.md` / `README.zh-CN.md`。
- 日期：`YYYY-MM-DD`；版本：`vX.Y.Z`；不使用 `final`、`new`、`old`、`copy`。
- workflow：`test.yml`、`deploy.yml`、`publish.yml`、`build.yml`、`release.yml`、`update.yml`。

## 9. 刻意缺失

未启用的资产不视为缺陷。只有影响维护的例外（如“不设 docs，README 即事实源”）才写入 `AGENTS.md` 的备注；普通缺失不写。例如：

- `不设 docs/：README 即事实源。`
- `不维护 CODE_OF_CONDUCT：暂无社区治理需求。`
