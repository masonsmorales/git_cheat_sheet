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
| `git add -u` | Only adds currently tracked files (which have been modified) to the staging area and also checks if they have been deleted (if yes, they are removed from staging area). Does not stage new files |
| `git fetch origin && git rebase origin/main` | Rebases a feature branch onto the latest version of the main branch  |
| `git restore <file> [options]` | Unstage and/or discard local changes to a file |
| `git checkout HEAD -- <file>` | Perform a hard reset of changes made to `file` back to `HEAD` |
| `git config --list --show-origin` | Show all global git configurations and the file path of each config setting |
| `git branch -D some_branch` | Delete some_branch locally |

# Useful Git Configurations
## Global gitignore file
1. Pull your favorite gitignore files from https://github.com/github/gitignore and concatenate them into a new file at ~/.gitignore
2. `git config --global core.excludesfile ~/.gitignore`
3. You now have a global gitignore file!
4. Note: You will probably still want to add a .gitignore file to the repos you are working on if multiple people are working on the repository.

## Use OSX Keychain for HTTPS Repo Auth
- `git config --global credential.helper osxkeychain`

## Reuse Tokens from Web Auth for Git CLI Auth
- https://github.com/git-ecosystem/git-credential-manager
- `git config --global credential.interactive always`
- `git config --global credential.useHttpPath true`

## Avoid Re-Entering GPG Key Passphrase for every Signed Commit (OSX)
Options:
- [GPG Suite](https://gpgtools.org/) (recommended by [Github](https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-commits)/easiest)
  - Note: [GnuPG](https://www.gnupg.org/download/) is also recommended by [GitHub](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key) but it doesn't have a way to access the OSX keychain
- pinentry-mac
  - https://gist.github.com/koshatul/2427643668d4e89c0086f297f9ed2130
  - https://unixb0y.de/blog/articles/2019-01/gpg-password-macos-keychain
- GitHub Doc: https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key
- More useful info: https://stackoverflow.com/questions/41502146/git-gpg-onto-mac-osx-error-gpg-failed-to-sign-the-data
- `git config --global commit.gpgsign=true`
- `git config --global gpg.program=gpg`
- `git config --global user.signingkey=<gpg key>`

## Configure Username and Email
- `git config --global user.name "first_name last_name"`
- `git config --global user.email "name@example.com"`

## Strip Python notebook output from git
Create a `.gitattributes` file and add the following line:
```
*.ipynb filter=strip-notebook-output`
```
# Useful Bash Aliases
gp - git push current branch to origin
```bash
alias gp='git push origin "$(git symbolic-ref --short HEAD)"'
```

## Other Tips & Tricks
### Count the number of lines of code in a git repo
```bash
git ls-files | xargs wc -l | sort
```
### Count the number of lines of Python code in a git repo
```bash
git ls-files | egrep '.py$' | xargs wc -l | sort
```
Or, to get the number of characters, use `wc -c`
### Create a function to find all instances of a string in git-tracked files
In `~/.bashrc`
```bash
# Create a function called "ggrep" (git grep)
ggrep() {
  if [ -z "$1" ]; then
    echo "Usage: ggrep <pattern>"
    echo 'Note: pattern supports Extended Regular Expressions (ERE)'
    echo 'To add egrep args, such as "-i" simply pass them with your pattern in double quotes,'
    echo '  e.g. ggrep "-i mypattern" or ggrep "mypattern -i" (order does not matter)'
  else
    git ls-files | xargs egrep -n --color=auto $1
  fi
}
```
