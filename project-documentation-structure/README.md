# Project Documentation Structure Skill

## 功能

管理项目文档结构，优化记忆系统，减少冗余，提升 token 效率。

## 适用场景

- 整理项目文件夹结构
- 决定信息该写到哪个文件（MEMORY.md / README.md / CONTEXT.md / 状态日志.md）
- 记忆文件去重和优化
- 项目归档、重命名
- 创建 README / CONTEXT / 状态日志文件

## 核心理念

用结构降低未来的 token 成本：

| 文件 | 存什么 | 不存什么 |
|------|--------|----------|
| MEMORY.md | 全局硬规则、项目索引、关键路径 | 项目执行细节、长日志 |
| memory/YYYY-MM-DD.md | 原始活动日志 | 仅作历史记录，不作权威来源 |
| README.md | 项目概览、状态、入口、下一步 | 完整历史、全局规则 |
| CONTEXT.md | 恢复上下文、活跃文件、命令、坑 | 通用模板、流水账 |
| 状态日志.md | 追加式变更记录 | 不作为唯一真相来源 |
| Skill | 稳定可复用的 SOP | 一次性状态、未验证实验 |

## 安装

```bash
cp -r project-documentation-structure ~/.claude/skills/
```

## 触发词

整理项目、项目文档、README、CONTEXT、状态日志、记忆结构、文档去重、项目归档、项目重命名、信息该写哪里、memory 要不要优化

## 来源

从 openclaw-autoclaw 项目提取。
