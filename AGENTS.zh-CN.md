# AGENTS.md（中文版）

## 项目概览

Awesome GitHub Copilot 仓库是一个由社区驱动的集合，包含自定义 agent、指令、技能、钩子、工作流和插件，旨在提升 GitHub Copilot 的使用体验，覆盖多种领域、语言和应用场景。该项目包含：

- **Agents** - 专门的 GitHub Copilot agent，可与 MCP 服务器集成
- **Instructions** - 通过特定文件模式自动应用的编码规范与最佳实践
- **Skills** - 自包含的文件夹，包含说明和打包资源
- **Hooks** - 在开发过程中由特定事件触发的自动化工作流
- **Workflows** - 用于 GitHub Actions 的 [Agentic Workflows](https://github.github.com/gh-aw) 自动化工作流
- **Plugins** - 可安装的软件包，用于将相关 agent、命令和技能打包为特定工作流

## 仓库结构

```
.
├── agents/           # 自定义 GitHub Copilot agent 定义（.agent.md 文件）
├── instructions/     # 编码标准与指南（.instructions.md 文件）
├── skills/           # Agent Skills 文件夹（每个文件夹包含 SKILL.md 和可选的打包资源）
├── hooks/            # 自动化工作流钩子（文件夹中包含 README.md + hooks.json）
├── workflows/        # Agentic Workflows（用于 GitHub Actions 自动化的 .md 文件）
├── plugins/          # 可安装插件包（包含 plugin.json 的文件夹）
├── extensions/       # 可复用的画布扩展源文件（extension.mjs 和资源）
├── docs/             # 不同资源类型的文档
├── eng/              # 构建和自动化脚本
└── scripts/          # 工具脚本
```

## 设置命令

```bash
# 安装依赖
npm ci

# 构建项目（生成 README.md 和 marketplace.json）
npm run build

# 校验插件清单
npm run plugin:validate

# 仅生成 marketplace.json
npm run plugin:generate-marketplace

# 创建新插件
npm run plugin:create -- --name <plugin-name>

# 校验 agent skills
npm run skill:validate

# 创建新 skill
npm run skill:create -- --name <skill-name>
```

## 开发工作流

### 使用 Agents、Instructions、Skills 和 Hooks

所有 agent 文件（`*.agent.md`）和 instruction 文件（`*.instructions.md`）都必须包含正确的 Markdown 前置配置。Agent Skills 是包含 `SKILL.md` 文件的文件夹，并带有可选的打包资源。Hooks 是包含前置配置的 `README.md` 和 `hooks.json` 配置文件的文件夹：

#### Agent 文件（*.agent.md）

- 必须包含 `description` 字段（使用单引号包裹）
- 文件名应使用小写字母，并用短横线分隔单词
- 建议包含 `tools` 字段
- 强烈建议指定 `model` 字段

#### Instruction 文件（*.instructions.md）

- 必须包含 `description` 字段（使用单引号包裹，且不能为空）
- 必须包含 `applyTo` 字段，用于指定文件匹配模式（例如 `'**.js, **.ts'`）
- 文件名应使用小写字母，并用短横线分隔单词

#### Agent Skills（skills/*/SKILL.md）

- 每个 skill 都是一个包含 `SKILL.md` 文件的文件夹
- SKILL.md 必须包含 `name` 字段（小写短横线命名，且与文件夹名一致，最多 64 个字符）
- SKILL.md 必须包含 `description` 字段（使用单引号包裹，长度 10-1024 个字符）
- 文件夹名应使用小写字母，并用短横线分隔单词
- Skills 可以包含打包资源（脚本、模板、数据文件）
- 打包资源应在 SKILL.md 的说明中被引用
- 资源文件大小应保持合理（单个文件小于 5MB）
- Skills 遵循 [Agent Skills 规范](https://agentskills.io/specification)

#### Canvas 扩展（extensions/*）

- 每个扩展文件夹都必须包含 `extension.mjs`
- 扩展是可复用的源组件，而不是独立插件
- 可发布的扩展插件通过匹配的 `plugins/<extension-id>/plugin.json` 注册
- 一个插件可以通过在 `extensions.com.github.awesome-copilot.extensions` 中列出 `./extensions/<name>` 路径来捆绑其他可复用扩展
- 每个扩展都必须包含 `assets/preview.png` 作为主要视觉资源
- 扩展元数据来自 `plugins/` 中对应的插件清单

#### Hook 文件夹（hooks/*/README.md）

- 每个 hook 都是一个包含 `README.md` 文件和前置配置的文件夹
- README.md 必须包含 `name` 字段（人类可读名称）
- README.md 必须包含 `description` 字段（使用单引号包裹，且不能为空）
- 必须包含 `hooks.json` 配置文件，用于定义钩子配置（钩子事件从该文件中提取）
- 文件夹名应使用小写字母，并用短横线分隔单词
- 可以包含打包资源（脚本、工具、配置文件）
- 打包脚本应在 README.md 和 hooks.json 中被引用
- 遵循 [GitHub Copilot hooks 规范](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/use-hooks)
- 可选包含 `tags` 字段用于分类

#### Workflow 文件（workflows/*.md）

- 每个 workflow 都是 `workflows/` 目录下的独立 `.md` 文件
- 必须包含 `name` 字段（人类可读名称）
- 必须包含 `description` 字段（使用单引号包裹，且不能为空）
- 包含 agentic workflow 前置配置（`on`、`permissions`、`safe-outputs`）以及自然语言说明
- 文件名应使用小写字母，并用短横线分隔单词
- 仅接受 `.md` 文件；`.yml`、`.yaml` 和 `.lock.yml` 文件会被 CI 阻止
- 遵循 [GitHub Agentic Workflows 规范](https://github.github.com/gh-aw/reference/workflow-structure/)

#### Plugin 文件夹（plugins/*）

- 每个插件都是一个包含根目录 `plugin.json` 的文件夹
- plugin.json 必须包含 `"$schema": "https://agent-plugins.org/schemas/1.0.0/plugin.schema.json"`（Agent Plugins v1.0.0）
- plugin.json 必须包含 `name` 字段，且与文件夹名一致
- plugin.json 必须包含 `description` 字段，用于描述插件用途
- plugin.json 必须包含 `version` 字段（语义化版本，例如 "1.0.0"）
- 插件内容通过 `plugin.json` 中 `extensions.com.github.awesome-copilot` 命名空间下的声明式字段定义（如 `agents`、`commands`、`hooks`、`skills` 和 `extensions`）。源文件位于顶层目录中，并由 CI 生成到插件中。
- `marketplace.json` 文件会在构建时自动生成
- 插件可通过 GitHub Copilot CLI 发现并安装

### 添加新资源

当添加新的 agent、instruction、skill、hook、workflow 或 plugin 时：

**对于 Agents 和 Instructions：**

1. 使用正确的前置配置创建文件
2. 将文件放入相应目录
3. 运行 `npm run build` 更新 README.md
4. 验证资源已经出现在生成后的 README 中

**对于 Hooks：**

1. 在 `hooks/` 中创建一个新文件夹，取一个描述性名称
2. 创建 `README.md`，包含前置配置（name、description、hooks、tags）
3. 创建 `hooks.json`，遵循 GitHub Copilot hooks 规范配置
4. 添加任何打包脚本或资源到文件夹中
5. 使脚本可执行：`chmod +x script.sh`
6. 运行 `npm run build` 更新 README.md
7. 验证 hook 出现在生成后的 README 中

**对于 Workflows：**

1. 在 `workflows/` 中创建一个新的 `.md` 文件，取一个描述性名称（例如 `daily-issues-report.md`）
2. 包含前置配置（`name`、`description`）以及 agentic workflow 相关字段（`on`、`permissions`、`safe-outputs`）
3. 运行 `gh aw compile --validate` 验证其有效性
4. 运行 `npm run build` 更新 README.md
5. 验证 workflow 出现在生成后的 README 中

**对于 Skills：**

1. 运行 `npm run skill:create` 初始化一个新的 skill 文件夹
2. 编辑生成的 SKILL.md 文件，填入说明
3. 向 skill 文件夹中添加打包资源（脚本、模板、数据文件）
4. 运行 `npm run skill:validate` 校验 skill 结构
5. 运行 `npm run build` 更新 README.md
6. 验证 skill 出现在生成后的 README 中

**对于 Plugins：**

1. 运行 `npm run plugin:create -- --name <plugin-name>` 初始化一个新的插件
2. 在 `plugin.json` 中的 `extensions.com.github.awesome-copilot` 下定义 agent、命令、hook、skill 和可复用扩展
3. 编辑生成的 `plugin.json`，补充元数据
4. 运行 `npm run plugin:validate` 校验插件结构
5. 运行 `npm run build` 更新 README.md 和 marketplace.json
6. 验证插件出现在 `.github/plugin/marketplace.json` 中

**对于 Canvas 扩展：**

1. 在 `extensions/<extension-id>/` 中创建或更新扩展，包含 `extension.mjs`
2. 在 `plugins/<extension-id>/plugin.json` 中添加对应插件清单：
   ```json
   {
     "$schema": "https://agent-plugins.org/schemas/1.0.0/plugin.schema.json",
     "name": "<extension-id>",
     "description": "...",
     "version": "1.0.0",
     "extensions": {
       "com.github.copilot": {
         "logo": "assets/preview.png"
       }
     }
   }
   ```
3. 确保 `assets/preview.png` 存在，并作为主要视觉资源
4. 运行 `npm run plugin:validate` 校验插件和扩展元数据
5. 运行 `npm run build` 重新生成网站数据和 marketplace 输出

若要将扩展打包到另一个插件中而不复制源码，可以将有序的 `./extensions/<name>` 路径添加到 `plugins/<plugin-id>/plugin.json` 的 `extensions.com.github.awesome-copilot.extensions` 中。

**对于外部插件：**

1. 不要直接提交修改 `plugins/external.json` 的 PR 以提交公共第三方插件
2. 公共外部插件提交使用 [CONTRIBUTING.md](CONTRIBUTING.md#adding-external-plugins) 中描述的外部插件问题工作流
3. 在 v1 中，公共提交仅接受 GitHub 托管插件，需使用公共仓库以及不可变的 `ref`、`sha` 或两者
4. `eng/external-plugin-validation.mjs` 中的共享校验器是外部插件数据规则的权威来源；请复用它，而不要在脚本或工作流中重复检查
5. 提交问题会经过 `external-plugin` + `awaiting-review`，随后根据自动化质量门槛进入 `ready-for-review` 或 `requires-submitter-fixes`
6. 在问题编辑后，作者或维护者可以评论 `/rerun-intake` 重新运行自动化 intake 和质量门槛，而无需重新提交问题
7. 维护者可以通过 `/mark-ready-for-review [可选原因]` 显式覆盖质量门槛阻塞，从而将问题转入 `ready-for-review`
8. 维护者在问题进入 `ready-for-review` 后，可通过评论 `/approve` 或 `/reject <reason>` 做出决定；审批通过的 issue 会被关闭，并作为六个月复审锚点
9. 审批自动化会创建或更新指向 `main` 的 PR，更新 `plugins/external.json`，并重新生成 marketplace 输出
10. 每晚复审自动化会查找至少六个月前关闭的 `external-plugin` + `approved` issue，添加 `re-review-due` 标签，并为维护者创建或更新跟踪 issue
11. 维护者可在原始审批提交 issue 上完成复审，使用 `/re-review-keep`、`/re-review-needs-changes` 或 `/re-review-remove`；`keep` 会重置 issue 的 `closed_at`，`remove` 会向 `main` 发起 PR

### 测试说明

```bash
# 运行所有校验
npm run plugin:validate
npm run skill:validate

# 构建并验证 README 生成
npm run build

# 修复行尾符（提交前必需）
bash eng/fix-line-endings.sh
```

提交前：

- 确保所有 Markdown 前置配置格式正确
- 验证文件名符合小写字母 + 短横线命名规范
- 运行 `npm run build` 更新 README
- **始终运行 `bash eng/fix-line-endings.sh`** 规范化换行符（CRLF → LF）
- 检查你的新资源是否正确出现在 README 中

## 代码风格指南

### Markdown 文件

- 使用正确的前置配置字段
- 保持描述简洁且信息丰富
- 将 `description` 字段值使用单引号包裹
- 使用小写字母 + 短横线命名文件

### JavaScript/Node.js 脚本

- 位于 `eng/` 和 `scripts/` 目录下
- 遵循 Node.js ES Module 规范（`.mjs` 扩展名）
- 使用清晰、描述性强的函数和变量名

## Pull Request 指南

创建 Pull Request 时：

> **重要：** 所有 Pull Request 都应针对 **`main`** 分支，而不是 `staged`。

1. **README 更新**：运行 `npm run build` 后，新文件会自动出现在 README 中
2. **Front matter 校验**：确保所有 Markdown 文件都包含所需的前置配置字段
3. **文件命名**：验证所有新文件遵循小写字母 + 短横线命名规范
4. **构建检查**：提交前运行 `npm run build`，确认 README 生成正常
5. **换行符**：**始终运行 `bash eng/fix-line-endings.sh`** 将换行符规范化为 LF（Unix 风格）
6. **描述**：提供清晰说明，说明你的 agent/instruction 的作用
7. **测试**：如果添加插件，请运行 `npm run plugin:validate` 确保有效
