## Setup

|Command|Description|
|---|---|
|`git config --global user.name "Name"`|Set your name|
|`git config --global user.email "email"`|Set your email|
|`git config --list`|View settings|

## Basic Commands

|Command|Description|
|---|---|
|`git init`|Initialize repository|
|`git status`|Check file status|
|`git add filename`|Stage specific file|
|`git add .`|Stage all files|
|`git commit -m "message"`|Commit changes|
|`git log`|View history|
|`git log --oneline`|Compact history|
|`git diff`|See changes|

## Undoing Changes

|Command|Description|
|---|---|
|`git restore --staged file`|Unstage file|
|`git restore file`|Discard changes|
|`git reset HEAD~1`|Undo last commit|
|`git reset --hard HEAD~1`|Undo and delete changes|
|`git revert commit-id`|Safely undo commit|

## Branching

|Command|Description|
|---|---|
|`git branch`|List branches|
|`git branch name`|Create branch|
|`git checkout name`|Switch branch|
|`git checkout -b name`|Create and switch|
|`git merge branch-name`|Merge branch|
|`git branch -d name`|Delete branch|

## GitHub

|Command|Description|
|---|---|
|`git clone url`|Clone repository|
|`git remote add origin url`|Add remote|
|`git remote -v`|View remotes|
|`git push -u origin main`|First push|
|`git push`|Push changes|
|`git pull`|Pull changes|
|`git fetch`|Fetch without merge|

## Advanced

|Command|Description|
|---|---|
|`git stash`|Save changes temporarily|
|`git stash pop`|Apply stashed changes|
|`git stash list`|List stashes|
|`git rebase main`|Rebase onto main|

## Typical Workflow

```
git pull                    # Get latest code
git checkout -b feature    # Create feature branch
# ... make changes ...
git add .                  # Stage changes
git commit -m "message"    # Commit
git push -u origin feature # Push branch
# ... create Pull Request on GitHub ...
# ... after PR is merged ...
git checkout main          # Switch to main
git pull                    # Get merged code
git branch -d feature      # Delete feature branch
```