# harness-two

来源：本仓库基于中文模板 [`iFurySt/harness-template-cn`](https://github.com/iFurySt/harness-template-cn) 派生，保留其 Git 历史与模板文档结构，并在此基础上增加双 Agent 协作流程。英文模板参考 [`iFurySt/harness-template`](https://github.com/iFurySt/harness-template)。

公共仓库：[`HotNewAi/harness-two`](https://github.com/HotNewAi/harness-two)

## 简介

harness-two 是一个双 Agent 协作开发模板：Agent 1 负责理解需求、编写和修改程序；Agent 2 在独立会话中只读检查变更、报告可复现的问题；Agent 1 修复后再交由 Agent 2 复查。工作流和角色提示词见 [双 Agent 开发与审查流程](docs/AGENT_WORKFLOW.md)。

模板不绑定模型供应商，也不内置模型 API 调度器。你可以在支持的宿主中配置两个模型/Agent；不支持自动交接时，按流程手动传递 diff 和审查结果。

## 快速开始

```sh
git clone https://github.com/HotNewAi/harness-two.git
cd harness-two
```

1. 可直接将本仓库作为项目起点，或在现有项目中采用这些模板文档。
2. 初始化项目名：`make init PROJECT=你的项目名`。建议使用小写字母、数字和连字符；该命令更新 README 与 `AGENTS.md` 中的模板名。
3. 在宿主平台配置两个独立模型/Agent 会话，分别加载 `docs/agent-prompts/agent-1-implementer.md` 与 `docs/agent-prompts/agent-2-reviewer.md`。尽可能给 Agent 2 配置只读工作区权限。
4. 按 [双 Agent 工作流](docs/AGENT_WORKFLOW.md) 传递需求、验收标准、完整 diff 和实际验证结果；Agent 1 根据审查意见修复后再次交给 Agent 2。

详细的克隆、初始化、Git 提交和审查交接步骤见[使用说明](docs/USAGE.md)。本仓库没有自动模型调度器或统一测试命令。更完整的仓库规则从 [`AGENTS.md`](AGENTS.md) 开始。

## 许可证

[MIT](LICENSE)

## 备注

这套方法主要来自我们自己的持续实践和整理，同时也吸收了 OpenAI 在 [harness engineering 文章](https://openai.com/index/harness-engineering/) 中的一部分思路，最后汇总成了这个模板。
