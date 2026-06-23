# Matt Pocock Skills Codex Plugin

[English](./README.md)

这是一个面向 Codex 的公开 plugin 包，内容来自 [mattpocock/skills](https://github.com/mattpocock/skills) 的精选 skills。

本仓库提供 Codex 原生 plugin 结构：

```text
.agents/plugins/marketplace.json  Codex marketplace 配置
.codex-plugin/plugin.json         Codex plugin manifest
assets/                           plugin 图标
skills/                           已打包的 skill 目录
```

## 来源

- 原仓库：[mattpocock/skills](https://github.com/mattpocock/skills)
- 当前仓库：[PathGao/mattpocock-skills-codex-plugin](https://github.com/PathGao/mattpocock-skills-codex-plugin)
- 上游基线：`mattpocock/skills` `1.0.1`
- 许可证：MIT，沿用原项目 metadata

本包从上游 `1.0.1` 内容派生，默认去掉上游仓库中的 `personal`、`deprecated`、`in-progress` 部分。目前唯一拉回来的 `in-progress` skill 是 `review`，来源是上游 `skills/in-progress/review`，作为公开包例外处理。上游 `misc/*` 也未纳入，因为这些内容主要是工具类或 Claude 相关 guardrails，不适合作为默认 Codex plugin skill。

plugin 安装名保持为 `mattpocock-skills`，安装后 skill 命名空间为 `mattpocock-skills:`。

## 包含的 Skills

| 工作流 | Skills | 用途 |
|---|---|---|
| 初始化 | `setup-matt-pocock-skills` | 配置 issue 与文档 |
| 路由 | `ask-matt` | 选择合适流程 |
| 想法到交付 | `grill-with-docs`, `to-prd`, `to-issues`, `implement` | 澄清、写规格、拆任务、实现 |
| 原型分支 | `prototype`, `handoff` | 验证未知、迁移上下文 |
| 实现纪律 | `tdd`, `review` | 测试先行、审查 diff |
| 输入处理 | `triage`, `diagnosing-bugs` | 分类请求、诊断故障 |
| 代码库健康 | `improve-codebase-architecture`, `codebase-design`, `domain-modeling` | 改结构、沉淀语言 |
| 独立工具 | `grill-me`, `grilling`, `teach`, `writing-great-skills` | 拷问、学习、写 skill |

## 安装

推荐让 Codex 按官方 personal plugin 机制安装。这样 plugin 会进入个人 Codex plugin 配置，不会把外部 skills 复制到当前项目的 `.agents/skills`。

可以直接对 Codex 说：

```text
请以官方 personal plugin 的形式安装这个 Codex plugin：
https://github.com/PathGao/mattpocock-skills-codex-plugin.git

安装目标 plugin 名称是 mattpocock-skills。
请添加该仓库作为 personal plugin marketplace，然后安装 mattpocock-skills。
```

如果当前 Codex 支持 slash command，也可以手动执行：

```text
/plugin marketplace add PathGao/mattpocock-skills-codex-plugin
/plugin install mattpocock-skills
```

按 marketplace plugin 方式安装后，Codex 会继续按该 marketplace 跟踪这个仓库。以后有新版本时，可以让 Codex 通过 marketplace 更新；如果当前界面提供升级按钮，也可以直接点击升级。

如果你的 Codex 环境使用 CLI 而不是 slash command，使用等价的 plugin marketplace add 和 plugin install 命令即可。

## 使用

安装后，通过 `mattpocock-skills:` 命名空间调用。

常用入口：

```text
mattpocock-skills:ask-matt
mattpocock-skills:to-prd
mattpocock-skills:to-issues
mattpocock-skills:tdd
mattpocock-skills:implement
mattpocock-skills:review
mattpocock-skills:handoff
```

`ask-matt` 是路由 skill。需求不清、需要拷问方案、写 PRD、拆 issue、做教学、做交接或诊断工程问题时，优先使用它。

## 维护规则

- `.codex-plugin/plugin.json` 的 `version` 当前对应上游基线 `1.0.1`。
- `.agents/plugins/marketplace.json` 中的 plugin 名称必须与 `.codex-plugin/plugin.json` 保持一致。
- 不加入上游 `personal`、`deprecated`、`misc` 或其他 `in-progress` skill，除非公开包策略明确改变。目前只包含 `review` 这一个 `in-progress` skill。
- 同步上游时，先审查新增 skill，再决定是否暴露到本 plugin。
