# git_cheat_sheet
| Command        | Notes           | 
| ------------- |:-------------:| 
| `git switch some_branch` | If some_branch exists on remote but not local, it will pull it from the local repo |
| `git reset HEAD~1` | Undo the previous commit but not the changes | 
| `git stash` | Stash current uncommitted changes |
| `git reset --hard origin/some_branch` | Destructive command to remove any uncommitted changes |
| `git stash pop` | Apply your last stash |
| `git stash list` | List stashes |
| `git branch -m new_branch` | Rename current branch to new_branch |
| `git format patch commit_hash` | Creates a patch files with the changes from that commit |
| `git apply filename.patch` | Applies a patch file to the current branch |
| `git clone --single-branch --branch=master --bare clone_url` | Clones down a .git/ folder containing only the master branch |
| `git clone url` | Clones a repo |
| `git checkout -b branch_name` | Creates a new branch and switches to it |
| `git status` | List changed files |
| `git add --all` | Add all files that are not in .gitignore |
| `git commit -m "commit message"` | Create a new commit |
| `git log` | Log file of all commits |
