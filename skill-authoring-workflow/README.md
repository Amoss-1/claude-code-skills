# Skill Authoring Workflow

## 功能

指导如何创建、更新、审查 Claude Code Skills，避免创建臃肿或无用的 Skill。

## 适用场景

- 决定某个工作流是否应该沉淀为 Skill
- 创建新 Skill 或更新已有 Skill
- 优化 Skill 结构，控制 token 成本
- 审查 Skill 质量（触发词、本体大小、引用可达性）

## 核心决策门

满足以下**至少一条**才创建 Skill：
- 工作流稳定且可复用
- 同类任务/纠正反复出现
- 反复出现的坑应该变成防护栏
- 能减少未来的 token 成本或工具试错
- 包含通用模型不可靠知道的领域/工具知识

**不要**为以下内容创建 Skill：一次性项目状态、未验证实验、长报告、日志。

## 文件结构

```
<skill-name>/
  SKILL.md          ← 核心规则（高频硬规则、触发后立即要用的步骤）
  references/       ← 低频细节、长模板、完整 schema
  scripts/          ← 重复性、确定性的可执行脚本
  assets/           ← 模板、静态资源
```

## 知识放置规则

| 放哪里 | 什么内容 |
|--------|----------|
| SKILL.md 本体 | 高频硬规则、高风险口径、不读就会犯错的 guardrail |
| references/ | 低频细节、长 SQL、完整 schema、长案例 |
| scripts/ | 重复、确定性、容易写错的可执行动作 |
| 不放 Skill | 项目当前状态、未验证实验、一次性流水 |

## 触发词

创建Skill、更新Skill、沉淀成Skill、做一个SKILLS、skill SOP、技能创建

## 来源

从 openclaw-autoclaw 项目提取。
