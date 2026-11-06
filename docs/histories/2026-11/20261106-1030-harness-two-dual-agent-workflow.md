## [2026-11-06 10:28] | Task: 创建 harness-two 双 Agent 工作流

### 🤖 Execution Context

- **Agent 1 / Model**: `Codex / GPT-6 Luna`
- **Agent 2 / Model**: `只读设计审阅子 Agent / 模型标识不可用`
- **Runtime / Review rounds**: `文档模板仓库；3 轮只读 Agent 2 审查；首轮 3 项、后两轮各 1 项发现均已处理；bash -n、git diff --check 和初始化脚本字面替换检查通过`

### 📥 User Query

> 把项目改成 harness-two：Agent 1 编写程序，Agent 2 检查并提出意见，Agent 1 按意见继续修改，形成两个模型分工协作。

### 🛠 Changes Overview

**Scope:** 仓库品牌、协作流程、提示词、架构和项目初始化脚本。

**Key Actions:**

- **双 Agent 流程**：定义 Agent 1 唯一写入、Agent 2 独立只读审查、逐轮修复复查和最多三轮后的用户升级路径。
- **角色提示词**：新增实现者与审查者提示词，要求审查意见含定位、触发条件、影响、证据和修复建议。
- **仓库入口**：将项目品牌改为 harness-two，并更新 README、AGENTS、架构、协作指南、PR 协作说明和计划模板。
- **初始化与记录**：初始化脚本支持以数据安全方式替换 harness-two 名称；history 模板记录两个 Agent；更新质量评分、发布记录和 PR 验证/Review 模板。
- **不绑定模型平台**：没有模型 SDK 或调度代码；使用者通过两个宿主会话加载角色提示词，或手动传递 review 材料。
- **验证结果**：`bash -n scripts/init-project.sh` 与 `git diff --check` 通过；隔离副本中的初始化脚本正确保留含特殊字符的项目名和上游 URL。

### 🧠 Design Intent (Why)

现有仓库是文档与脚本模板，没有运行时、模型 API 或凭据配置。用厂商无关的流程和提示词提供明确、可立即照做的分工；将自动交接与权限隔离留给使用者选择的宿主能力。

### 📁 Files Modified

- `AGENTS.md`
- `README.md`
- `CONTRIBUTING.md`
- `.github/PULL_REQUEST_TEMPLATE.md`
- `scripts/init-project.sh`
- `docs/AGENT_WORKFLOW.md`
- `docs/agent-prompts/agent-1-implementer.md`
- `docs/agent-prompts/agent-2-reviewer.md`
- `docs/ARCHITECTURE.md`
- `docs/REPO_COLLAB_GUIDE.md`
- `docs/QUALITY_SCORE.md`
- `docs/design-docs/core-beliefs.md`
- `docs/design-docs/index.md`
- `docs/exec-plans/templates/execution-plan.md`
- `docs/exec-plans/completed/2026-11-06-harness-two-dual-agent-workflow.md`
- `docs/histories/template.md`
- `docs/releases/feature-release-notes.md`
