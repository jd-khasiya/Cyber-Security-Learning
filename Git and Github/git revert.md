`git revert` does **one thing**: it creates a **new commit** that is the exact **opposite** of a target commit. The original commit stays in history — nothing is deleted or rewritten.

### Why this matters

```
Before:  A → B → C (buggy)
After:   A → B → C → C' (revert of C)
```

History is **linear and intact**. Everyone who `git pull`s sees the original commit AND the fix. No force-push needed.

### All commands at a glance

|   |   |
|---|---|
|Command|What it does|
|`git revert <hash>`|Revert a specific commit|
|`git revert HEAD`|Revert the last commit|
|`git revert HEAD~1`|Revert the second-to-last commit|
|`git revert HEAD~3..HEAD`|Revert the last 3 commits|
|`git revert <hash1> <hash2>`|Revert multiple specific commits|
|`git revert --no-edit <hash>`|Revert without opening editor|
|`git revert -n <hash>`|Revert but **don't commit** (stage changes only)|
|`git revert -m 1 <merge-hash>`|Revert a **merge commit** (keep 1st parent)|
|`git revert --continue`|Continue after resolving conflicts|
|`git revert --abort`|Cancel the revert entirely|

### Industry scenarios

**1. A bug got merged to main and deployed (most common)**

```
# Find the bad commit
git log --oneline
# 3a7f2c1  "Add payment gateway integration"

# Revert it
git revert 3a7f2c1
git push
```

No force-push. No team disruption. The fix is a new commit.

**2. Revert multiple commits (a bad PR with 5 commits)**

```
git revert a1b2c3..f9e8d7
```

Creates individual revert commits for each, in reverse order.

**3. Revert a merge commit**

```
# You merged feature-x into main, and it broke things
git revert -m 1 <merge-commit-hash>
```

`-m 1` = "treat the first parent (main) as the base, undo everything from the second parent (feature-x)."

**4. Revert a revert (you reverted too aggressively)**

```
# You reverted commit C, but now you realize it was fine
git revert <revert-commit-hash>
```

This re-applies the original changes. Commit messages become:

```
Revert "Revert 'Add payment gateway integration'"
```

**5. Revert without committing (batch multiple reverts)**

```
git revert -n commit1
git revert -n commit2
git commit -m "Revert bad changes from hotfix"
```

### Conflict handling

```
git revert <hash>
# CONFLICT in file.js — resolve manually
# Edit the file, then:
git add file.js
git revert --continue
```

If it's too messy:

```
git revert --abort   # back to where you started
```

---

## `git switch` vs `git revert` — When to use which

|   |   |
|---|---|
|Situation|Command|
|I want to work on a different branch|`git switch`|
|I want to undo a **pushed** commit safely|`git revert`|
|I want to undo a **local, unpushed** commit|`git reset` (not revert)|
|I want to inspect old code without changing my branch|`git switch --detach <commit>`|
|I want to undo a merge that broke production|`git revert -m 1 <merge-hash>`|

### The decision rule (industry standard)

```
Did the commit go to a shared/remote branch?
│
├─ YES → git revert (safe, no history rewrite)
│
└─ NO (local only) → git reset (cleaner history)
```

### What teams actually do

|   |   |
|---|---|
|Frequency|Command|
|🔥 Every single day|`git switch`, `git switch -c`|
|📅 Weekly|`git revert HEAD` (undo a bad merge to main)|
|📉 Rarely|`git revert -m 1` (undo a bad merge), `git switch --detach` (inspect old code)|
