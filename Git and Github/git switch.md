`git switch` (Git 2.23+) does **one thing only**: it changes which branch you're on. That's it. No file restoration, no staging — just branch navigation.

### All commands at a glance

|   |   |
|---|---|
|Command|What it does|
|`git switch <branch>`|Switch to an existing branch|
|`git switch -c <branch>`|Create a new branch and switch to it|
|`git switch -C <branch>`|Force-create (overwrite) a branch and switch|
|`git switch -`|Go back to the **previous** branch|
|`git switch -f <branch>`|**Force** switch (discards uncommitted changes)|
|`git switch -t origin/<branch>`|Switch to a remote branch (creates tracking)|
|`git switch -c <branch> origin/<branch>`|Create local branch tracking a remote one|
|`git switch --detach <commit>`|Enter detached HEAD at a specific commit|
|`git switch --orphan <branch>`|Create a branch with **no history** (fresh start)|

### Industry scenarios

**1. Daily: Start working on a new feature**

```
git switch -c feature-dark-mode
```

**2. Daily: Jump back to main after checking something**

```
git switch main
# ... do something ...
git switch -          # back to feature-dark-mode
```

**3. You have uncommitted changes and need to switch urgently**

```
git stash
git switch main
# fix the urgent bug
git switch -
git stash pop
```

**4. Pick up a teammate's branch from remote**

```
git fetch origin
git switch -c hotfix-payment origin/hotfix-payment
```

**5. Inspect code at a specific commit (read-only)**

```
git switch --detach a1b2c3d
# explore the code...
git switch main   # get back to your branch
```

> ⚠️ **Detached HEAD:** You're not on any branch. Any commits you make here will be **lost** unless you create a branch first (`git switch -c save-my-work`).

