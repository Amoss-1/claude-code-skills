---
name: skill-authoring-workflow
description: Create, update, review, or decide whether to create an OpenClaw/Claude-style Skill. Use for 创建Skill, 更新Skill, 沉淀成Skill, 做一个SKILLS, skill SOP, 技能创建, whether something should become a Skill, skill frontmatter/description/references/scripts/assets, reducing token cost, and avoiding duplicate or bloated Skills.
---

# Skill Authoring Workflow

## Decision Gate
Create/update a Skill only when at least one is true:
- Workflow is stable and reusable.
- Same task/correction recurs.
- Repeated pitfall should become a guardrail.
- It reduces future token cost/tool trial-and-error.
- It contains domain/tool knowledge general models will not reliably know.

Do not create a Skill for one-off project state, unverified experiments, long reports, daily logs, or content that belongs in project README/CONTEXT/status logs.

## Required Location
`C:\Users\PC\.openclaw-autoclaw\skills\<skill-name>\SKILL.md`

Do not install into `~/.agents/skills/`.

## Minimal Structure
```text
<skill-name>/
  SKILL.md
  references/   # optional detailed docs
  scripts/      # optional deterministic helpers
  assets/       # optional templates/static assets
```


## Core Knowledge Placement Rule
Skill 精简不是把关键知识藏进 references。判断放哪里：

- **必须放 SKILL.md 本体**：高频硬规则、高风险口径、触发后立刻要用的步骤、不读就会犯错的 guardrail。
- **放 references/**：低频细节、长 SQL 模板、完整 schema、长案例、扩展说明。
- **放 scripts/**：重复、确定性、容易写错的可执行动作。
- **不要放 Skill**：项目当前状态、未验证实验、一次性流水。

判断标准：如果 Skill 触发后不读 reference 就可能犯核心错误，说明 SKILL.md 本体太瘦，必须内联关键规则。

## Authoring Workflow
1. Clarify trigger examples and non-trigger boundaries.
2. Decide: update existing Skill vs create new Skill.
3. Write concise YAML frontmatter (`name`, `description`).
4. Keep SKILL.md body lean: core rules, workflow, reference map.
5. Move long schemas/口径/examples/checklists to `references/`.
6. Move deterministic repeatable code to `scripts/`.
7. Validate trigger specificity, overlap, body size, references discoverability.
8. Record creation/update in daily memory; add pointer to `memory/workflows.md` or `MEMORY.md` only if globally important.

## Update Existing Skill When
- New rule is a sub-pattern of an existing workflow.
- New Skill would share most triggers with an old Skill.
- User is refining the same type of work.

## References
- Design principles: `references/skill-design-principles.md`
- Local Skill index: `references/local-skill-index.md`
