# Git cheat sheet

Code schoolの"Git Real" コースで学んだ内容です。

## Git Real : Level 1

### 基本操作

```
# Show help
$ git help

# Set username and e-mail.
$ git config --global user.name hoge
$ git config --global user.email hoge@example.com

# Create git repository at local.
$ mkdir project
$ cd project
$ git init
$ echo "# This is My project!!" >> README.md
$ git add .
$ git commit -m "Initial commit"

```

### 様々なファイルの追加方法

```

# Add the list of files
$ git add <list of files>

# Adds all new or modified files.
$ git add --all

# Add all txt files in current directory
$ git add docs/*.txt

# Add all files in docs directory
$ git add docs/

# Add all txt files in the whole project
# git add "*.txt"

```


## Git Real : Level 2

### ステージング関連

```

# View unstaged diff
$ git diff

# View staged diff
$ git diff --staged

# Unstaged files (but still modifed)
$ git reset HEAD README.md

# Revert all changes
$ git checkout -- README.md

# Skip staging and commit
$ git commit -a -m "Modify README.md"

```

### コミットミス関連

**履歴を書き換える行為なので、これらはPushした後には使わないこと！！**

```

# Undo last commit, put changes into staging.
$ git reset --soft HEAD^

# Change the last commit
$ git add todo.txt
$ git commit --amend -m "Mofify readme & add todo.txt"

# Undo last commit and all changes
$ git reset --hard HEAD^

# Undo last 2 commits and all changes
$ git reset --hard HEAD^^

```

### リモート関連

```

# Add remote
$ git remote add origin https://github.com/dev-neko/notes.git

# Show remote repos
$ git remote -v

# Push repo (<remote repo name>, <local branch to push>)
$ git push -u origin master

# Pull, add, remove, push
$ git pull
$ git remote add <name> <address>
$ git remote rm <name>
$ git push -u <name> <branch>

# About Heroku

$ heroku create

# You can confirm 'heroku' is added as remote.
$ git remote -v

# To push to heroku
$ git push heroku master

```


## Git Real : Level 3

### クローン、ブランチ関連

```

# Clone a repo.
$ git clone http://..../git-repo.git
$ git clone http://..../git-repo.git git-demo

# Create a branch and checkout it.
$ git branch cat
$ git checkout cat

# Create and checkout a branch one time.
$ git checkout -b cat

$ git add catlist.txt
$ git commit -m "add catlist.txt"

# Merge changes from cat branch to master.
$ git checkout master
$ git merge cat

# Delete a branch
$ git branch -d cat

```

## Git Real : Level 4

### Fetch, Pull, Conflicts関連

```
# Get remote codes and update local ones.
$ git pull
$ git push

# Fetch doesn't update local codes. So merge after fetch.
$ git fetch
$ git merge origin/master

# When a conflict occurred, edit a conflicted file manually.
$ git commit -a index.html
$ git push
```


## Git Real : Level 5

### Branch関連

リモートのブランチを削除した時の動きがまだよくわかってない。

```
# Create a local branch and push it to remote.
$ git checkout -b shopping_cart
$ git push origin shopping_cart

# Add a file and push it.
$ git add cart.rb
$ git commit -a -m "Add basic cart ability"
$ git push

# When a co-worker pull that branch.
$ git pull
$ git branch # But stille you can't see that branch
$ git branch -r # List all remote branches. Now you can see that branch!!

$ git checkout shopping_cart

# You can check the details of remote.
$ git remote show origin

# Remove a branch from remote
$ git push origin :shopping_cart

# The local branch is still left. So remove it.
$ git branch -d shopping_cart

# Even if there are commits you don't merge yet, remove the branch forcibly.
$ git branch -D shopping_cart

# When a co-worker remove a remote branch you have referred
# Confirm the details of remote and remove a reference.
$ git remote show origin
$ git remote prune origin

```

### Tag関連

```
# List all tags
$ git tag

# Checkout code at commit
$ git checkout v0.0.1

# Add a new tag
$ git tag -a v0.0.3 -m "version 0.0.3"

# To push new tags
$ git push --tags

```

## Git Real : Level 6

### Rebase関連

```
# Fetch a co-worker fix.
$ git fetch

$ git rebase

# 'rebase' does 3 things
# 1. Move all changes to master which are not in origin/master to a temporary area.
# 2. Run all origin/master commits.
# 3. Run all commits in the temporary area, one at a time.
# => No merge commit!!

# Move to admin branch and rebase at there.
# Admin commits put above master commits.
$ git checkout admin
$ git rebase master

# Back to master and merge.
$ git checkout master
$ git merge admin


# When a conflict occurred
$ git fetch
$ git rebase # Woops, there is a conflict on README.txt!!

# After edit README.txt manually
$ git add README.txt
$ git rebase --continue

# Anothter option
$ git rebase --skip
$ git rebase --abort


```

## Git Real : Level 7

### log, config, alias関連

```
$ git config --global color.ui true

$ git log --pretty=oneline

$ git log --pretty=format "%h %ad %s [%an]"

$ git log --oneline -p

$ git log --oneline --stat

$ git log --oneline --graph

$ git log --until=1.minute.ago

$ git log --since=1.day.ago

$ git diff
$ git diff HEAD
$ git diff HEAD^
$ git diff HEAD^^
$ git diff HEAD~5
$ git diff HEAD^..HEAD

# Diff between 2 commits
$ git diff <HASH1> <HASH2>

# Diff between branches
$ git diff master bird

# time-based diff
$ git diff --since=1.week.ago --until=1.minute.ago

# Blame
$ git blame index.html --date short

# Remove
$ git rm README.txt
$ git commit -m "Remove README.txt"

# Stop tracking
$ git rm --cached hoge.txt

# Config
$ git config --list

# Alias
$ git config --global alias.mylog "log --pretty=format: '%h %s [%an]' --graph"
$ git config --global alias.lol "log --graph --decorate --pretty=oneline --abbrev-commit --all"

$ git config --global alias.st status
$ git config --global alias.co checkout
$ git config --global alias.br branch
$ git config --global alias.ci commit


```
