# 目录结构的阶段演进与组合

不按项目原型平铺模板。先给一个最小**基础结构**，再按需要叠加**结构模块**；每个模块只在对应需求出现时引入。阶段不是等级，可以跳过、重排或只取其中一部分。

## 阶段 0：基础结构

所有项目的起点。README 承载全部说明，不设 docs。

```text
<repo>/
├── README.md
├── README.zh-CN.md
├── AGENTS.md
├── LICENSE                # 开源时
├── .gitignore
├── .editorconfig
├── .gitattributes
└── src/                   # 有源码时
```

根目录 dotfiles：

| 文件 | 作用 | 备注 |
| --- | --- | --- |
| `.gitignore` | 忽略构建产物、缓存、密钥 | 至少覆盖 OS、编辑器、`.env*` |
| `.editorconfig` | 缩进、换行、编码 | 与项目语言一致 |
| `.gitattributes` | 换行、二进制、语言统计 | 二进制文件标记 `binary` |
| `.gitmodules` | 子模块声明 | 仅在有子模块时 |

## 阶段 1：文档层

**触发**：README 超过约 120 行，或开始出现架构、构建、API 细节。

```text
<repo>/
├── docs/
│   ├── architecture.md    # 组成、分层、数据流、边界
│   ├── development.md     # 构建、测试、本地环境、扩展
│   ├── design.md          # 设计约束、架构选择、权衡
│   └── reference.md       # CLI、参数、API、JSON Schema
└── ...
```

变更：README 保留三模块（是什么 / 需要什么 / 怎么用）+ Documentation 链接；细节移入四篇。

## 阶段 2：版本与测试

**触发**：进入版本管理，或开始有稳定的测试。

```text
<repo>/
├── CHANGELOG.md
├── tests/
│   ├── unit/
│   ├── integration/
│   └── regression/
├── .github/workflows/
│   ├── test.yml           # 普通 CI，跑 tests/
│   └── release.yml        # 读 git tag + CHANGELOG
└── ...
```

- `tests/` 的组织跟随源码层级（如 `tests/core/`、`tests/gui/`、`tests/worker/`）。
- release 基础情况只发 GitHub Release，不附带 assets。

## 阶段 3：分发与部署

**触发**：有包分发、构建产物、线上站点或定时数据任务。**按需取用，不必全加**。

```text
<repo>/
├── package.json / pyproject.toml
├── .github/workflows/
│   ├── publish.yml        # npm / PyPI 等包分发
│   ├── build.yml          # 构建产物，与 release assets 搭配
│   ├── deploy.yml         # 网站 / Worker 即时部署
│   └── update.yml         # 定时数据更新
├── worker/                # 边缘函数（可选）
├── public/                # 静态站点（可选）
└── ...
```

## 阶段 4：社区

**触发**：接受外部 issue/PR，或社区开始活跃。

```text
<repo>/
├── CONTRIBUTING.md
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug.yml
│   │   └── feature.yml
│   └── PULL_REQUEST_TEMPLATE.md   # 按需
├── CODE_OF_CONDUCT.md             # 按需
└── ...
```

## 结构模块速查

除阶段增量外，以下目录按项目形态叠加：

| 模块 | 新增结构 | 适用 |
| --- | --- | --- |
| 桌面分发 | `installer/`、`assets/preview.webp`、`assets/screenshots/` | 桌面应用 |
| 内容包 | `content/` | 配置、素材、文章等可替换内容 |
| 边缘服务 | `worker/` | 分发、更新、部署接口 |
| 附属服务 | `services/` | 独立后端或 CMS |
| 静态资源 | `public/` | 静态站点 |
| Agent Skill | `skills/<name>/` | 项目对外提供 agent skill |
| 插件扩展 | `<extension>/` | 插件包，每个扩展一个目录 |
| Monorepo | `packages/`、`apps/`、`pnpm-workspace.yaml` | 多包共享同一仓库 |

## 组合示例（基础 + 模块）

| 项目形态 | 基础 | 叠加 |
| --- | --- | --- |
| 个人博客 / 小工具 | ✔ | 阶段 3（deploy）；**不设文档层** |
| 桌面应用（C++ / Qt） | ✔ | 阶段 1+2+3；`installer/`、`website/`、`worker/`、`content/`、`assets/` |
| Web 应用 / Worker 服务 | ✔ | 阶段 1+2+3；`public/`、`services/` 或 `worker/` |
| Python 包 / CLI | ✔ | 阶段 1+2+3（publish）；`skills/`（可选） |
| 插件包 / Agent Skills | ✔ | 阶段 2+3（publish）；根级扩展目录；文档层可选 |
| Monorepo | ✔ | 阶段 1+2+3；`packages/`、`apps/`、workspace 配置 |

## 组合原则

- 先有需求，再加结构；不预铺空目录。
- 一个模块只回答一类职责；新增模块不改变已有模块的职责。
- 已有合理结构不改造；结构差异不写入 `AGENTS.md`，只有影响维护的例外才写备注。
- 结构变化后，按 `AGENTS.md` 的维护钩子同步更新 README、docs、tests 与第三方声明。
