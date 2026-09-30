for unstaging a file `git restore --staged file` and then 

- `git restore file` for discarding the changes done in working directory and makes it sync with the last commit state
- but keep in mind if no file was therre in last commit state then the file will be deleted

-  `git restore --staged --worktree .` use for getting everything to last commit state and the same applies for `git restore .` so be carefull

- `git restore --source=commit_hash file` for checking a file's status at a specific commit state and . for files -- so it reverts changes and shows the state as a past commit and if you want the old part then you can create a new commit for applying and keeping that old changes with a new commit

Running **git checkout .** (or `git checkout -- .`) restores all tracked files in the current directory to their state in the **HEAD** commit, effectively discarding all uncommitted local changes.

This command operates on the **working directory** and **index** (staging area), but it **does not** remove untracked files (new files not yet added to Git). It is primarily used to **undo local modifications** or revert accidental changes without affecting the repository's history or remote state.