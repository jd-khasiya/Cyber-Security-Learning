`git reset` does **one core job**: it moves your **branch pointer (HEAD)** to a different commit. Depending on the mode, it also affects the staging area and working directory.

### Three modes

|   |   |   |   |   |
|---|---|---|---|---|
|Mode|Branch pointer|Staging area|Working directory|When to use|
|`--soft`|Moved ✅|**Kept** (changes stay staged)|**Kept**|Fix a commit message, or squash commits before pushing|
|`--mixed` _(default)_|Moved ✅|**Reset** (changes become unstaged)|**Kept**|Redo a commit with different files staged|
|`--hard`|Moved ✅|**Wiped**|**Wiped**|Completely discard local commits + changes|

### Industry scenarios

**1. Fix the last commit message (most common daily use)**

```
git reset --soft HEAD~1
git commit -m "Corrected message"
```

**2. Accidentally committed the wrong files**

```
git reset --soft HEAD~1   # undo commit, keep files staged
git reset --staged wrong-file.txt  # unstage just that file
git commit -m "Correct commit"
```

**3. You pushed a bad commit to a _private_ branch**

```
git reset --hard HEAD~1
git push --force
```

> ⚠️ **Never do this on a shared branch.** Use `git revert` instead.

**4. Sync your local branch with remote after a rebase**

```
git fetch origin
git reset --hard origin/main
```

**5. Unstage a file (file-level reset)**

```
git reset HEAD myfile.txt
# Modern equivalent:
git restore --staged myfile.txt
```

### The golden rule

> **Local, unpushed commits → `git reset`**  
> **Pushed / shared commits → `git revert`**

---

# Git Hard reset

A **hard reset** (`git reset --hard <commit>`) moves the branch pointer back to the specified commit, effectively **erasing all commits that occurred after that point** from the current branch's history. It simultaneously **deletes all uncommitted changes** in both the staging area and the working directory, making the local state match the target commit exactly.

The extent of the history rollback depends on the target specified:

- **`git reset --hard HEAD~1`**: Moves back **one commit**. The last commit is removed from history, and all its changes are discarded.
    
- **`git reset --hard <commit-hash>`**: Moves back to that **specific commit**. All commits made after that hash are removed from the branch history.
    
- **`git reset --hard origin/main`**: Moves back to match the **remote branch exactly**, discarding any local commits or changes that differ from the remote.
    

**Important Safety Note**: This operation is **permanent** and rewrites history. It should only be used on **local, unpublished commits**. For shared branches, use `git revert` instead to avoid disrupting collaborators. If you accidentally reset, you can often recover lost commits using `git reflog`.