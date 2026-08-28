# Codex SOL Project Manager Skill

面向 Codex 的官方模型团队管理 Skill。它只在用户明确输入“启动 SOL 总负责模式”、调用 `$sol-project-manager`，或明确要求 SOL 统筹多角色项目时启用。

本 Skill 只使用当前 Codex 实际提供的 OpenAI 模型，不接入第三方模型、本地模型服务或额外密钥。

## 工作方式

```text
用户
  ↓
SOL：唯一总负责人，负责目标、组队、模型选择、返工和最终验收
  ↓
Codex 官方模型角色：按能力承担产品、架构、开发、测试、研究或审查
```

- `gpt-5.6-sol`：旗舰能力，用于复杂专业工作、跨模块决策、关键审查和最终验收。
- `gpt-5.6-terra`：兼顾质量与成本，用于日常专业开发、复杂调试、集成和独立复核。
- `gpt-5.6-luna`：快速高效，用于边界明确的实现、批处理、测试、文档和低风险重构。
- 其他 Codex 官方模型按当前模型目录的能力说明归入旗舰、均衡或高效档，不固定绑定职位。

模型分工依据 [OpenAI Model Guidance](https://developers.openai.com/api/docs/guides/latest-model)，并以当前 Codex 执行面实际可用的模型和推理档为准。

## 安装

将本仓库复制到 Codex 用户 Skill 目录：

```powershell
git clone https://github.com/Aimark-dai/codex-sol-project-manager-skill.git "$env:USERPROFILE\.codex\skills\sol-project-manager"
```

如果目标目录已经存在，请先备份或改用其他目录，不要直接覆盖个人修改。

## 使用

在新项目中选择 SOL，然后输入：

```text
启动 SOL 总负责模式。

项目目标：
验收标准：
约束：
```

也可以输入：

```text
$sol-project-manager 帮我完成……
```

普通聊天、能力询问和示例讨论不会启动团队模式。小任务仍由 SOL 直接完成；多角色任务默认使用当前会话的内部模型代理。只有用户明确要求时才创建独立可见任务。

## 核心规则

- SOL 是唯一组队者和最终验收者。
- 同时最多三个角色，只有文件范围和验收条件独立时才并行。
- 一个文件或强耦合区域同一时间只有一个写入负责人。
- 实现者不能批准自己的交付，复核意见必须回到 SOL。
- 模型不可用时只在 Codex 官方模型之间明确降级，不静默替换。
- 删除重要数据、发布部署、对外发送、付费、项目外访问和新密钥仍需相应授权。

## 文件

- `SKILL.md`：触发条件、能力路由、执行原则、权限和完成标准。
- `references/team-workflow.md`：多角色任务契约、状态、返工和模型故障处理。
- `agents/openai.yaml`：Codex 界面元数据和默认启动提示。

## 验证

- 使用 Skill Creator 的 `quick_validate.py` 验证目录和元数据。
- 静态扫描确认不存在第三方模型、本地模型端口、路由配置或凭据。
- 用复杂项目、高吞吐项目和模型容量故障场景验证能力路由、独立复核与降级行为。
