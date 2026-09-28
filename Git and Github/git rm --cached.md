# Git rm --cached`

It removes a file **only from Git's index (staging area)** while **keeping the file on your local disk**. Git stops tracking it from the next commit onward, but the file itself is untouched in your working directory.

### Exact scenarios where you use it

|   |   |
|---|---|
|Scenario|Example|
|**Accidentally committed a file that should be in `.gitignore`** (e.g., `.env`, `node_modules/`, `logs/`)|`git rm --cached .env`|
|**Added a file to `.gitignore` but Git still tracks it** — `.gitignore` only affects _untracked_ files, so you must first remove it from the index|`git rm --cached config/database.yml`|
|**Remove a sensitive file** (API keys, passwords) from tracking while keeping your local copy|`git rm --cached secrets.json`|
|**Undo an accidental `git add .`** without losing local files|`git rm --cached -r .`|

### The typical workflow

```
# 1. Add the file/folder to .gitignore
echo ".env" >> .gitignore

# 2. Remove it from Git's index (file stays on disk)
git rm --cached .env

# 3. Commit the change
git commit -m "Stop tracking .env"
```

### Key distinction

|   |   |   |
|---|---|---|
|Command|File on disk?|File in Git index?|
|`git rm <file>`|❌ Deleted|❌ Removed|
|`git rm --cached <file>`|✅ Kept|❌ Removed|
|`git reset <file>`|✅ Kept|✅ Still tracked (just unstaged)|

**One important caveat:** `git rm --cached` does **not** remove the file from Git's _history_. It only stops tracking it going forward. If the file contained secrets and you need it purged from all past commits, you'd need `git filter-branch` or `git filter-repo` instead.

