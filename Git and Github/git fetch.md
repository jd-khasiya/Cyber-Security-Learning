git fetch used to get latest commit information all information's into system

but to apply that we need to do git pull : which does git fetch plus git merge

- just git fetch : all branch pointers will be in sync with the origin( remote ) location branches
- and if specify git fetch origin feature : then the feature branch will be in sync all information -- then to apply latest changes we do the git pull

if we do 
- git pull : then the remote default name goes and the current branch goes for fetch + merge with the origin / or rebase

| **`git fetch`** | Downloads new commits from the remote into your local repo (doesn't touch your working files yet) |
| --------------- | ------------------------------------------------------------------------------------------------- |
| **`git merge`** | Merges those downloaded commits into your current branch                                          |

usually we do --- `git fetch && git checkout branch` as git fetch already got information of all branches information in local but till we don,t do the checkout the data is not available in local of the other then default one branch

git push to update origin (remote) pointers 