# Git Commands Cheat Sheet
| Command        | Notes           | 
| ------------- |:-------------:| 
| `git switch some_branch` | If some_branch exists on remote but not local, it will pull it from the local repo and switch to it |
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
| `git reset --soft HEAD~3`| Remove the last 3 commits on the branch (does not lose changes, userful for squashing locally) |
| `git push -f origin my_branch` | Force push `my_branch` (overwrites remote branch; useful after a local squash when remote was pushed but not squashed; resolves "Updates were rejected because the tip of your current branch is behind its remote counterpart") |
| `git reset --hard origin/master && git pull -v --rebase origin master && git checkout master && git pull` | Discard all local changes and re-pull the master branch; useful in a `gitfix` bash alias |

# Useful Git Configurations
## Global gitignore file
1. Pull your favorite gitignore files from https://github.com/github/gitignore and concatenate them into a new file at ~/.gitignore
2. `git config --global core.excludesfile ~/.gitignore`
3. You now have a global gitignore file! 
4. Note: You will probably still want to add a .gitignore file to the repos you are working on if multiple people are working on the repository.

## Use OSX Keychain for HTTPS Repo Auth
`git config --global credential.helper osxkeychain`

## Reuse Tokens from Web Auth for Git CLI Auth
- https://github.com/git-ecosystem/git-credential-manager

## Avoid Re-Entering GPG Key Passphrase for every Signed Commit (OSX)
Options:
- [GPG Suite](https://gpgtools.org/) (recommended by [Github](https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-commits)/easiest)
  - Note: [GnuPG](https://www.gnupg.org/download/) is also recommended by [GitHub](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key) but it doesn't have a way to access the OSX keychain
- pinentry-mac
  - https://gist.github.com/koshatul/2427643668d4e89c0086f297f9ed2130
  - https://unixb0y.de/blog/articles/2019-01/gpg-password-macos-keychain
