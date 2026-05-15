# Claude Code Skills

个人自用的 Claude Code Skills 合集。

## 目录结构

```
claude-code-skills/
├── claude-code-skills/     ← 自建 Skills
│   └── github-upload/
└── openclaw-skills/        ← 来自 openclaw-autoclaw
    ├── project-documentation-structure/
    └── skill-authoring-workflow/
```

## 自建 Skills

| Skill | 用途 |
|-------|------|
| [github-upload](./claude-code-skills/github-upload/) | git push 不可用时上传文件到 GitHub |

## OpenClaw Skills

| Skill | 用途 |
|-------|------|
| [project-documentation-structure](./openclaw-skills/project-documentation-structure/) | 项目文档结构管理、记忆优化、文档去重 |
| [skill-authoring-workflow](./openclaw-skills/skill-authoring-workflow/) | 创建/更新/审查 Skill 的决策流程 |

## 安装方法

```bash
# 克隆仓库
cd ~/.claude/skills
git clone https://github.com/Amoss-1/claude-code-skills.git

# 复制需要的 skill（任选一个）
cp -r claude-code-skills/openclaw-skills/project-documentation-structure ~/.claude/skills/
cp -r claude-code-skills/claude-code-skills/github-upload ~/.claude/skills/
```

## 说明

- `claude-code-skills/` — 自己开发的 Skills
- `openclaw-skills/` — 从 openclaw-autoclaw 项目提取的 Skills
- 每个 Skill 目录下有 SKILL.md（核心规则）和 README.md（中文说明）
