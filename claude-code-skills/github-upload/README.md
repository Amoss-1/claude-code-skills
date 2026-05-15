# GitHub Upload Skill

## 功能

在 `git push` 不可用时（如公司内网限制），通过 gh CLI API 或 ghpush 工具上传文件到 GitHub。

## 适用场景

- 上传本地项目/文件到 GitHub
- 创建新仓库并初始化
- 更新/删除 GitHub 上的文件
- 公司内网无法 git push 时的替代方案

## 核心工具

| 工具 | 优点 | 缺点 |
|------|------|------|
| ghpush | 简单，支持目录批量上传 | 不保留子目录结构，文件扁平上传 |
| gh api | 精确控制路径，支持增删改 | 需要手动处理 base64 编码和 sha |

## 使用方法

### 快速上传（扁平结构）
```bash
ghpush <file-or-dir> <user>/<repo> "commit message"
```

### 保留目录结构
```bash
CONTENT=$(base64 -w0 <file>)
gh api repos/<user>/<repo>/contents/<path> -X PUT -f message="msg" -f content="$CONTENT"
```

## 触发词

上传到github、推送到github、发布到github、github上传、上传仓库、创建github仓库

## 踩坑记录

1. ghpush 上传文件时不保留目录层级，只用文件名
2. 更新已有文件必须提供 sha 值
3. Windows 下 gh 可能需要完整路径 `/c/Program Files/GitHub CLI/gh.exe`
4. base64 在 Windows Git Bash 需要 `-w0` 参数

## 来源

从实际项目上传经验中提炼（2026-05-15）。
