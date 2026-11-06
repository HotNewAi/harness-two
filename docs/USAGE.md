# harness-two 使用说明

## 来源与定位

`harness-two` 基于 [iFurySt/harness-template-cn](https://github.com/iFurySt/harness-template-cn) 中文模板派生，沿用其 Git 提交历史和模板文档结构，并改造成双 Agent 协作流程。英文参考模板为 [iFurySt/harness-template](https://github.com/iFurySt/harness-template)。

本仓库提供 Agent 角色提示词、审查交接流程和初始化脚本，不内置模型 API、凭据管理或自动调度器。实际运行两个模型会话由使用者所选的宿主平台提供。

## 克隆到本地

```sh
git clone https://github.com/HotNewAi/harness-two.git
cd harness-two
```

确认 Git 工作区和远端：

```sh
git status --short --branch
git remote -v
```

## 用作新项目模板

推荐用小写字母、数字和连字符作为项目名：

```sh
make init PROJECT=my-project
```

该命令替换 `README.md` 和 `AGENTS.md` 中的 `harness-two` 模板名，不会改 GitHub 仓库名、远端地址或其它文档里的来源链接。随后根据项目实际情况更新 `docs/ARCHITECTURE.md`、产品规格与检查命令。

若为新项目另建了 GitHub 仓库，可将本地 `origin` 指向新仓库，再推送：

```sh
git remote set-url origin https://github.com/<owner>/<repo>.git
git push -u origin main
```

替换尖括号中的 owner 和 repo 为新仓库的实际名称。将项目改名初始化，不会自动创建 GitHub 仓库。

## 配置两个 Agent

1. 在宿主平台开启两个独立会话。优先使用不同模型；如果宿主支持权限控制，将 Agent 2 的工作区设为只读。
2. 将 [`agent-1-implementer.md`](agent-prompts/agent-1-implementer.md) 配置给 Agent 1，将 [`agent-2-reviewer.md`](agent-prompts/agent-2-reviewer.md) 配置给 Agent 2。
3. Agent 1 接收用户目标、验收条件和仓库规则，实施变更并运行与变更相关的检查。
4. Agent 1 把完整 diff、目标、验收条件、相关规则、真实验证结果和已知未覆盖范围交给 Agent 2。不要把 Agent 1 的自我评价作为审查结论。
5. Agent 2 只读审查，按文件位置、触发条件、影响、证据和修复建议返回发现，或明确给出通过/阻塞结论。
6. Agent 1 逐条核实并修复，重新运行受影响的检查，再把新 diff 交给 Agent 2。旧 diff 的审查结论不能替代对新 diff 的复查。
7. 默认最多进行三轮审查。仍有重要分歧、验证阻塞或高影响未决项时，汇总证据交给用户决策；不要将阻塞标成通过。

如果宿主不支持自动交接，手动复制 diff 和审查材料即可。完整规则与交接格式见 [`AGENT_WORKFLOW.md`](AGENT_WORKFLOW.md)。

## 保存本地变更

完成并复核后，可以用 Git 记录改动：

```sh
git status --short
git add README.md AGENTS.md docs/
git commit -m "docs: customize harness-two project"
git push
```

根据本次改动调整 `git add` 路径和提交说明。提交前按项目自身规则运行适用的检查；本模板没有统一的 `make test` 或 CI 命令。
