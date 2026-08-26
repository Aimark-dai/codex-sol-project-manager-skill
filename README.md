# Codex SOL Project Manager Skill

面向 Codex 的多模型项目管理 Skill。它只在用户明确输入“启动 SOL 总负责模式”或调用 `$sol-project-manager` 时启用。

## 组织结构

```text
SOL 总负责层
  > GPT 管理与专业层（Terra、Luna 等）
    > MiniMax-M3 执行层
```

- SOL 是唯一总负责人，拥有组队、模型任命、创建任务窗口、任务改派和最终验收权。
- GPT 模型承担产品、架构、测试、研究和审查等管理或专业工作，不得自行扩张团队。
- MiniMax-M3 是叶子执行者，只负责编码、修改、调试、测试和返工，不得委派或创建子智能体。
- 所有跨窗口沟通必须由 SOL 中转。

## 安装

将本仓库复制到 Codex 用户 Skill 目录：

```powershell
git clone https://github.com/Aimark-dai/codex-sol-project-manager-skill.git "$env:USERPROFILE\.codex\skills\sol-project-manager"
```

如果目标目录已存在，请先自行备份或选择其他安装目录，不要直接覆盖。

## 使用

在新项目中选择 SOL 模型，然后输入：

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

普通聊天、能力询问和示例讨论不会自动启动多模型团队。

## 文件

- `SKILL.md`：入口规则、模型分层、权限边界和完成标准。
- `references/team-workflow.md`：多窗口状态机、任务契约、返工和失败恢复流程。
- `agents/openai.yaml`：Codex 界面元数据和默认提示。

## 已验证行为

- Skill 结构通过官方 `quick_validate.py`。
- SOL、Terra、MiniMax-M3、Luna 的真实可见任务完成过端到端闭环验证。
- MiniMax-M3 在同一任务中完成 TDD 开发与返工，未调用子智能体。
- 普通聊天不触发；明确启动口令才进入 SOL 总负责模式。

## 已知限制

ChatGPT 账户内部的 MiniMax-M3 子智能体通道可能不受支持。工作流会优先使用独立的本地可见 MiniMax-M3 任务，并如实报告实际模型和降级情况。

