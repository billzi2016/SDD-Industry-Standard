# SpecKit

> 仓库地址：[github/spec-kit](https://github.com/github/spec-kit)

## 什么是 SpecKit？

**SpecKit** 是 GitHub 官方开源的规格驱动开发（SDD）工具包，核心目标是：

> **更快地构建高质量软件。**

它让开发者专注于产品场景和可预期的交付结果，而不是从零开始"氛围编程"（vibe coding）每一个细节。SpecKit 支持 **30+ 种 AI 编码助手**（Claude Code、GitHub Copilot、Gemini CLI、Codex CLI 等），通过一套标准化的斜杠命令将规格驱动开发流程无缝嵌入到各类 AI 工作流中。

---

## 安装

SpecKit 通过 `specify` CLI 提供，依赖 **uv**（Python 包管理器）：

```bash
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git@vX.Y.Z
```

初始化项目：

```bash
specify init my-project --integration copilot   # 指定 AI 助手集成
specify init .                                   # 在当前目录初始化
```

---

## 核心命令（斜杠命令）

### 主流程命令

| 命令 | 说明 |
|---|---|
| `/speckit.constitution` | 创建或更新项目的治理原则与开发准则，是所有后续开发的基础 |
| `/speckit.specify` | 描述要构建的内容（用户故事 + 功能需求），聚焦于"做什么"和"为什么" |
| `/speckit.plan` | 基于规格和技术栈选择，生成完整的技术实现方案 |
| `/speckit.tasks` | 从实现方案派生可执行任务列表，含依赖顺序和并行标记 |
| `/speckit.taskstoissues` | 将任务列表转换为 GitHub Issues，便于追踪和执行 |
| `/speckit.implement` | 按计划执行所有任务，完成功能实现 |

### 质量增强命令

| 命令 | 说明 |
|---|---|
| `/speckit.clarify` | 对未充分说明的需求进行结构化澄清（建议在 `/plan` 之前运行） |
| `/speckit.analyze` | 跨文档一致性与覆盖率分析（在 `/tasks` 之后、`/implement` 之前运行） |
| `/speckit.checklist` | 生成自定义质量检查清单，验证需求的完整性、清晰度和一致性 |

---

## 完整工作流（7 步）

```
1. /speckit.constitution  →  建立项目原则
2. /speckit.specify       →  描述功能需求（聚焦 what & why，不涉及技术栈）
3. /speckit.clarify       →  澄清模糊需求（可选但强烈推荐）
4. /speckit.plan          →  生成技术实现方案（在此才指定技术栈）
5.   验证计划             →  让 AI 审查计划完整性
6. /speckit.tasks         →  拆解为可执行任务列表
7. /speckit.implement     →  执行实现
```

运行完成后，项目目录结构示例：

```
my-project/
├── .specify/
│   ├── memory/
│   │   └── constitution.md      # 项目原则
│   ├── templates/               # 规格/计划/任务模板
│   └── scripts/                 # 自动化脚本
└── specs/
    └── 001-feature-name/
        ├── spec.md              # 功能规格
        ├── plan.md              # 技术实现方案
        ├── tasks.md             # 任务列表
        ├── data-model.md        # 数据模型
        ├── research.md          # 技术调研
        └── contracts/           # API 契约文件
```

---

## 扩展机制

SpecKit 提供两种定制化方式，优先级从高到低：

| 优先级 | 类型 | 路径 | 用途 |
|---|---|---|---|
| 1 | 项目本地覆盖 | `.specify/templates/overrides/` | 针对单个项目的一次性调整 |
| 2 | 预设（Presets） | `.specify/presets/templates/` | 自定义现有工作流的模板和命令格式 |
| 3 | 扩展（Extensions） | `.specify/extensions/templates/` | 添加全新的命令和能力 |
| 4 | SpecKit 核心 | `.specify/templates/` | 内置默认模板 |

**Extensions**：用于添加新能力，例如 Jira 集成、代码审查流程、V 模型测试追踪等  
**Presets**：用于定制现有工作流，例如强制合规格式、应用敏捷/Kanban/Waterfall 方法论术语、添加安全审查门禁等

```bash
specify extension search        # 搜索可用扩展
specify extension add <name>    # 安装扩展

specify preset search           # 搜索可用预设
specify preset add <name>       # 安装预设
```

---

## 核心哲学

- **意图驱动开发**：规格定义"做什么"，而非"怎么做"
- **丰富的规格创建**：通过防护栏和组织原则生成高质量规格
- **多步精化**：拒绝一次性 prompt 生成代码，强调迭代式精化
- **AI 深度协作**：充分利用先进 AI 模型解读和转化规格

---

## 支持的 AI 编码助手（部分）

Claude Code、GitHub Copilot、Gemini CLI、OpenAI Codex CLI、Cursor、Qwen CLI、Kiro、Mistral、Forge、Goose、Tabnine 等 30+ 种工具。

运行以下命令查看当前版本支持的全部集成：

```bash
specify integration list
```

---

## 社区资源

- [Extensions 扩展列表](https://github.github.io/spec-kit/community/extensions.html)
- [Presets 预设列表](https://github.github.io/spec-kit/community/presets.html)
- [Walkthroughs 端到端示例](https://github.github.io/spec-kit/community/walkthroughs.html)
- [视频概览（YouTube）](https://www.youtube.com/watch?v=a9eR1xsfvHg)

---

## 环境要求

- Linux / macOS / Windows
- Python 3.11+
- Git
- uv（推荐）或 pipx
- 任一受支持的 AI 编码助手
