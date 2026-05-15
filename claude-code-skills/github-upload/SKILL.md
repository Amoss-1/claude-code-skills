# GitHub Upload Skill

## Description
Use this skill when uploading local files or projects to GitHub. Trigger phrases include: 上传到github, 推送到github, 发布到github, github上传, 上传仓库, 创建github仓库.

## Purpose
Automate the workflow of uploading files to GitHub when `git push` is unavailable (corporate network restrictions), using the gh CLI API or the ghpush mirror tool.

## Prerequisites
- `gh` CLI installed and authenticated (`gh auth login`)
- For ghpush: `~/projects/github-mirror-tool/ghpush` exists

## Workflow

### Step 1: Determine target repository
Check if repo exists:
```bash
gh repo view <user>/<repo> 2>/dev/null
```
If not, create it:
```bash
gh repo create <user>/<repo> --public --description "description"
```

### Step 2: Upload files

**Method A: ghpush (simple, for flat files)**
```bash
export PATH="/c/Program Files/GitHub CLI:$PATH"
cd <local-project-dir>
bash ~/projects/github-mirror-tool/ghpush <file-or-dir> <user>/<repo> "commit message"
```

**Limitation**: ghpush uses base filename only. A file at `subdir/SKILL.md` gets uploaded as `SKILL.md` at repo root, NOT `subdir/SKILL.md`.

**Method B: gh api (preserves directory structure)**
```bash
export PATH="/c/Program Files/GitHub CLI:$PATH"
CONTENT=$(base64 -w0 <file-path> 2>/dev/null || base64 <file-path> 2>/dev/null)
gh api repos/<user>/<repo>/contents/<target-path> -X PUT \
  -f message="commit message" \
  -f content="$CONTENT"
```
This preserves the full path. Use this when files must be in subdirectories.

**Method C: Update existing file (requires sha)**
```bash
SHA=$(gh api repos/<user>/<repo>/contents/<path> --jq '.sha')
CONTENT=$(base64 -w0 <file-path> 2>/dev/null || base64 <file-path> 2>/dev/null)
gh api repos/<user>/<repo>/contents/<path> -X PUT \
  -f message="update message" \
  -f content="$CONTENT" \
  -f sha="$SHA"
```

**Method D: Delete file (requires sha)**
```bash
SHA=$(gh api repos/<user>/<repo>/contents/<path> --jq '.sha')
gh api repos/<user>/<repo>/contents/<path> -X DELETE \
  -f message="delete message" \
  -f sha="$SHA"
```

### Step 3: Verify
```bash
gh api repos/<user>/<repo>/git/trees/main?recursive=1 --jq '.tree[].path'
```

## Decision Table

| Scenario | Method |
|----------|--------|
| Upload single file to root | ghpush |
| Upload entire directory (flat ok) | ghpush |
| Upload file to specific subdirectory | gh api PUT |
| Update existing file | gh api PUT (with sha) |
| Delete file | gh api DELETE (with sha) |
| Upload large directory with structure | Loop gh api PUT per file |

## Pitfalls

1. **ghpush flattens paths**: `ghpush subdir/file.txt repo` uploads as `file.txt`, not `subdir/file.txt`
2. **base64 -w0**: On Windows Git Bash, use `-w0` to disable line wrapping. If `base64 -w0` fails, try without `-w0`
3. **File size limit**: GitHub API limits files to 1MB via contents API
4. **Windows PATH**: `gh` may need full path: `/c/Program Files/GitHub CLI/gh.exe`
5. **Update requires sha**: To update an existing file, you MUST provide its current sha, otherwise API returns 422

## Example: Upload a Skill to a new repo

```bash
# 1. Create repo
gh repo create Amoss-1/claude-code-skills --public --description "Skills collection"

# 2. Upload root README
cd ~/my-skill-project
bash ~/projects/github-mirror-tool/ghpush README.md Amoss-1/claude-code-skills "init: add README"

# 3. Upload skill files with directory structure
CONTENT=$(base64 -w0 my-skill/SKILL.md)
gh api repos/Amoss-1/claude-code-skills/contents/my-skill/SKILL.md -X PUT \
  -f message="feat: add my-skill" -f content="$CONTENT"

# 4. Verify
gh api repos/Amoss-1/claude-code-skills/git/trees/main?recursive=1 --jq '.tree[].path'
```
