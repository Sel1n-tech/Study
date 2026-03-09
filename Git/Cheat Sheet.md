1. Git configuration

git config --global user.name "Your name"
git config --global user.email "you@example"
git config --global color.ui auto

2. Starting a project

git init [project name]
git clone <project url>

4. Day-to-day work

git status
git add [file]
git diff [file]
git diff --staged [file]
git checkout -- [file]
git reset [<path>...]
git commit
git rm [file]

6. Storing your work

git stash
git stash pop
git stach drop

5. Git branchong model

git branch [-a]
git branch [branch_name]
git rebase [branch_name]
git checkout [-b] [branch_name]
git merge [branch_name]
git branch -d [branch_name]

6. Inspect history
git log [-n count]
git log --oneline --graph --decorate
git log ref ..
git log ..ref
git reflog

7. Tagging commits
git tag 
git tag [name] [commit sha]
git tag -a [name] [commit sha]
git tag -d [name]

8. Reverting changes
git reset [--hard] [target reference]
git revert [commit sha]

9. Synchronizing repositories
git fetch [remote]
git fetch --prune [remote]
git pull [remote]
git push [--tags] [remote]
git push -u [remote] [branch]



