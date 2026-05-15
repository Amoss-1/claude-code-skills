# Project Documentation Structure Skill

## Description
Use this skill when organizing project folders, updating project documentation, deciding where to store information, reducing redundancy between memory/project files, renaming/archiving projects, or creating README/CONTEXT/status-log files. Trigger phrases include: 整理项目, 项目文档, README, CONTEXT, 状态日志, 记忆结构, 文档去重, 项目归档, 项目重命名, 信息该写哪里, memory 要不要优化.

## Purpose
Keep long-term memory and project documentation token-efficient and easy to recover from. Avoid scattering the same content across MEMORY.md, README.md, CONTEXT.md, 状态日志.md, and Skills.

## Core Rule
Use structure to reduce future token cost:

- **MEMORY.md** = startup index + hard global rules.
- **memory/YYYY-MM-DD.md** = raw daily operation log.
- **Project README.md** = human-facing project overview.
- **Project CONTEXT.md** = AI recovery context.
- **Project 状态日志.md** = append-only project change log.
- **Skill** = stable reusable SOP or repeated pitfall.

## File Boundaries

### workspace MEMORY.md
Store only:
- High-frequency global preferences.
- Hard safety/operational rules.
- Canonical project index and important paths.
- High-cost repeated pitfalls.
- Links/pointers to project docs and Skills.

Do not store:
- Project execution details.
- Long historical logs.
- Full project reports.
- Unstable experimental methods.

### memory/YYYY-MM-DD.md
Store:
- Raw chronological activity.
- What was changed, why, and result.
- Temporary findings and debugging trail.
- Crash recovery breadcrumbs.

This file may be verbose and redundant because it is raw history.

### Project README.md
Store human-facing overview:
- What the project is.
- Current status.
- Main entry points.
- How to run/use it.
- Next step.
- Links to CONTEXT/status logs.

Keep it short. Do not paste global rules; reference MEMORY.md or this Skill.

### Project CONTEXT.md
Store AI recovery context:
- Active files and canonical paths.
- Current version/state.
- Data sources and key口径.
- Run commands.
- Local gotchas specific to this project.
- What to read first when resuming.

Avoid generic templates. Avoid historical stream-of-consciousness.

### Project 状态日志.md
Store append-only history:
- Date/time.
- What changed.
- Why it changed.
- Result/verification.
- Follow-up TODOs.

Do not treat status log as the only source of truth; periodically distill current state back into README/CONTEXT.

### Skill
Create/update a Skill only when:
- The method is stable and reusable.
- The same task type recurs.
- The same pitfall happened more than once.
- It reduces future token cost or tool trial-and-error.

Do not create Skills for:
- One-off project state.
- Unverified experiments.
- Current progress notes.
- Long reports.

## Workflow

When asked to organize projects or documentation:

1. Inventory project directories and existing README/CONTEXT/status logs.
2. Identify active, archived, empty-shell, and documentation-only projects.
3. Do not delete directly. Prefer archive/move with recovery path.
4. Rename by content and purpose, not vague labels.
5. Keep backward compatibility if paths are used by scripts (junction/alias or clear migration note).
6. Update or create:
   - README.md for overview.
   - CONTEXT.md for recovery.
   - 状态日志.md for change history.
   - Top-level project index if present.
7. Remove duplicated rule blocks; use references instead.
8. Record the operation in daily memory.

## Documentation Convention Template

Use this table when writing a top-level convention file:

| File | Put here | Avoid |
|---|---|---|
| MEMORY.md | Global hard rules, project index, key paths | Project logs/details |
| memory/YYYY-MM-DD.md | Raw activity log | Permanent canonical rules only |
| README.md | Human overview, status, entry, next step | Full history/global rules |
| CONTEXT.md | Recovery context, active files, commands, gotchas | Generic templates/history |
| 状态日志.md | Append-only change log | Current sole source of truth |
| Skill | Stable reusable SOP | One-off state/experiments |

## Validation Checklist

Before finishing:

- Does every active project have README.md, CONTEXT.md, and 状态日志.md?
- Is MEMORY.md still short and index-like?
- Are project details stored in project docs instead of MEMORY.md?
- Are repeated global rules referenced instead of copied into every project?
- Did you avoid hard deletion and preserve recovery path?
- Did you update daily memory with what changed?

## Memory Index Split Pattern

Use this pattern when optimizing long-term memory for token efficiency.

### When to apply
Apply when:
- MEMORY.md grows beyond a lightweight startup index.
- The user complains about token cost from memory loading.
- Long-term memory mixes user preferences, environment details, project status, pitfalls, and workflows.
- The user references Claude Code-style memory organization or asks for memory structure optimization.

### Target structure

```text
MEMORY.md              # minimal startup index only
memory/
  user.md              # user preferences and communication style
  environment.md       # OS, shell, tools, MCP, database, external-send rules
  projects.md          # project index and key project statuses
  pitfalls.md          # high-frequency hard pitfalls
  workflows.md         # stable workflows and Skill trigger index
  YYYY-MM-DD.md        # daily raw activity log
```

### Rules

- `MEMORY.md` should contain only:
  - startup hard rules
  - pointers to `memory/*.md`
  - current key project entry points
  - key Skill pointers
- Detailed content should move to categorized `memory/*.md` files.
- Default startup should read only `MEMORY.md`.
- Read detailed memory files on demand:
  - user preference task → `memory/user.md`
  - environment/tool/database task → `memory/environment.md`
  - project task → `memory/projects.md` + project README/CONTEXT
  - pitfall/debugging task → `memory/pitfalls.md`
  - documentation/SOP/Skill task → `memory/workflows.md`
- Keep daily logs in `memory/YYYY-MM-DD.md`; do not over-compress daily raw history.

### Migration workflow

1. Back up the existing `MEMORY.md` to `memory/MEMORY_before_index_split_<timestamp>.md`.
2. Extract content into categorized `memory/*.md` files.
3. Rewrite `MEMORY.md` as a compact index.
4. Record the migration in the current daily memory file.
5. If the pattern proves reusable, keep this section updated instead of creating another overlapping Skill.

### Validation checklist

- Is `MEMORY.md` short enough to load every main session without pain?
- Can a future session find user/environment/project/pitfall/workflow details by following the index?
- Are project details still in project README/CONTEXT rather than global memory?
- Was the old MEMORY backed up before rewrite?
