`git checkout` historically did **two unrelated things** in one command, which made it confusing:

|   |   |   |
|---|---|---|
|Job|Example|Modern replacement|
|**Switch branches**|`git checkout feature-x`|`git switch feature-x`|
|**Restore files**|`git checkout -- file.txt`|`git restore file.txt`|

### Branch switching (now `git switch`)

```
# Switch to existing branch
git checkout feature-x        # old
git switch feature-x           # new (preferred)

# Create + switch to new branch
git checkout -b new-branch     # old
git switch -c new-branch       # new (preferred)

# Go back to previous branch
git checkout -                 # old
git switch -                   # new
```

### File restoration (now `git restore`)

```
# Discard changes in a file
git checkout -- file.txt       # old
git restore file.txt           # new (preferred)

# Restore a file from a specific commit
git checkout HEAD~2 -- file.txt  # old
git restore --source=HEAD~2 file.txt  # new
```

### Is `git checkout` deprecated?

**No.** The Git project explicitly stated (in Git 2.46 docs) that `git checkout` will **stay for the foreseeable future**. It's not deprecated — but the community consensus is:

- **Branch operations** → use `git switch`
    
- **File operations** → use `git restore`
    

Most teams in 2025+ are migrating new developers to `switch`/`restore`, while `checkout` persists in legacy scripts and muscle memory.

---

## Industry decision flowchart

```
Need to undo something?
│
├─ Uncommitted changes in files?
│   → git restore <file>          (discard)
│   → git restore --staged <file> (unstage)
│
├─ Local commits you haven't pushed?
│   → git reset --soft/mixed/hard HEAD~N
│
├─ Pushed commits on a shared branch?
│   → git revert <commit-hash>
│
├─ Switch to another branch?
│   → git switch <branch>
│
└─ View code at an old commit (read-only)?
    → git switch -d <commit-hash>   (detached HEAD)
```

### What teams actually do day-to-day

|   |   |
|---|---|
|Frequency|Command|
|🔥 Every day|`git switch`, `git restore`, `git add`, `git commit`, `git push`|
|📅 Weekly|`git reset --soft HEAD~1` (fix commit), `git revert` (undo a bad push)|
|📉 Rarely|`git reset --hard` (nuclear option), `git checkout <commit> -- <file>` (legacy)|

The key takeaway: **`git reset` rewrites history, `git checkout`/`switch` navigates, `git restore` touches files only.** Modern Git separates these concerns cleanly.
