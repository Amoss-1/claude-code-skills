# Claude Code Skills

个人自用的 Claude Code Skills 合集。

## Skills 列表

| Skill | 用途 | 来源 |
|-------|------|------|
| [project-documentation-structure](./project-documentation-structure/) | 项目文档结构管理、记忆优化、文档去重 | openclaw-autoclaw |
| [github-upload](./github-upload/) | git push 不可用时上传文件到 GitHub | 自建 |
| [skill-authoring-workflow](./skill-authoring-workflow/) | 创建/更新/审查 Skill 的决策流程 | openclaw-autoclaw |

## 安装方法

```bash
# 克隆到 ~/.claude/skills/
cd ~/.claude/skills
git clone https://github.com/Amoss-1/claude-code-skills.git

# 复制需要的 skill
cp -r claude-code-skills/project-documentation-structure ~/.claude/skills/
```

## 说明

- 此仓库用于沉淀个人积累的 Claude Code Skills
- Skills 来源包括：官方仓库、社区贡献、自建
- 每个 Skill 目录下有独立的 SKILL.md 说明文件
