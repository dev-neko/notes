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

## Git Real 2 : Level 1

### Interactive rebase

Interactive rebaseの際のコミットの順番は古い方が一番上に来る。（git logでは新しい方が一番上に来る）

```
# noop
$ git rebase -i HEAD

# 1 commit before
$ git rebase -i HEAD^

# 3 commits before
$ git rebase -i HEAD^3

```

Interactive rebaseで行うことが出来る操作

- pick : そのままコミットを採用する場合。コミットの順番を変えたい場合は、pickのまま順番だけ入れ替える。
- reword : コミットメッセージを変更する場合
- edit : コミットを分割する場合。編集したファイルはステージングへ追加、コミットして、git rebase --continueを行う。
- squash : コミットをまとめる場合


## Git Real 2 : Level 2

### Stash

変更途中のファイルをコミットせずに、一時的に退避しておく機能。

```

# Save changes to a temporary area and reset to HEAD
$ git stash save
$ git stash # alias

# There is no diff
$ git diff
$ git status

# Retrieve changes from a temporary ares and apply it.
$ git stash apply

# Show list of stash
$ git stash list

# Apply specific stash (default is stash@{0})
$ git stash apply stash@{1}

# Discard a stash
$ git stash drop

# Alias. Apply and drop in the same time
$ git stash pop

# Stash only unstaged files. So you can commit staged files.
$ git stash save --keep-index

# Stash even untracked files.
$ git stash save --include--untracked

# Show stash content
$ git stash show
$ git stash show stash@{1}

# You can use list options the same as "git log" options.
$ git stash list --stat
$ git stash list --patch

# You can save a message like as a commit message.
$ git stash save "Hogehoge..."

# Create a new branch using a stash and pop it automatically.
$ git stash branch hogehoge stash@{0}

# Clear all stashes
$ git stash clear

```


## Git Real 2 : Level 3

### 履歴の廃棄

```
# Remove the password.txt file from all previous commits.
# ファイルが無いとでも実行失敗しないように-fをつけること。
$ git filter-branch --tree-filter "rm -f password.txt" -- --all

# Remove from current commit.
$ git filter-branch --tree-filter "rm -f password.txt" -- HEAD

# Remove all video files.
$ git filter-branch --tree-filter 'find  -name "*.mp4" -exec rm {} ¥;'

# Remove from files without checking it out. Command will be executed against staging area.
# ファイルが無いとでも実行失敗しないように--ignore-unmatchをつけること。
$ git filter-branch --index-filter 'git rm --cached --ignore-unmatch password.txt'


# Force. Remove even backup.
$ git filter-branch -f --tree-filter 'rm -f password.txt'

# Drop empty commits.
$ git filter-branch -f --prune-empty -- --all

$ git filter-branch --tree-filter 'rm -f password.txt' --prune-empty -- --all

```

## Git Real 2 : Level 4

### 改行コードの設定

```
# On Unix-like systems (Linux, OSX, etc). Changes CR/LF to LF on commit.
git config --global core.autocrlf input

# On Windows systems. Changes LF to CR/LF on chckeout.
git config --global core.autocrlf true

# On Windows-only projects. Does no conversion.
git config --global core.autocrlf false

```

### gitattribute

ファイル種別の設定

```
* text=auto

*.html text
*.css text

*.bat eol=crlf
*.sh eol=lf

*.jpg binary
*.png binary

```

### cherry-picking

あるブランチの特定のコミットのみを、マスターにコミットしたい場合に使用する。

```
# まずリリースブランチをチェックアウト
git checkout production

# リリースブランチに適用したいコミットのハッシュを指定する。
git cherry-pick <hash>

# 適用するコミットのメッセージを変えたい時
git cherry-pick --edit <hash>

# 複数のコミットを適用したい時。このコマンドだけではコミットされないので、手動でコミットすること。
git cherry-pick --no-commit <hash> <hash2>

# コミット元を追跡したい時。しかし、これはパブリックのブランチからコミットを適用する時にしか使えないので注意。
# （ローカルブランチは他の人から見えないので）
git cherry-pick -x <hash>

# 元々コミットした人をログ上で維持したい時
# Authorは保持され、Signed-off-byのところに、現在のユーザ名が記載される。
git cherry-pick -signoff <hash>

```


## Git Real 2 : Level 5

### Submodule

```
# サブモジュールを追加
git submodule add git@example.com:css.git
cat .gitmodules

# プロジェクトをクローン（この時点でサブモジュールディレクトリは空っぽ）
git clone <レポジトリ>

# サブモジュールを取得
git submodule init
git submodule update

# もしなんのブランチも持っていない状態でコミットしてしまったら、マージする。
git checkout master
git merge <hash>
git log --oneline

# 1. まずはサブモジュールで変更、コミット、プッシュする。
# 2. その後、親プロジェクトに移動し、サブモジュールをコミット、プッシュする必要がある。
cd css
git add styles.css
git commit -m "hoge"

cd ..
git add css
git commit -m "foo"

# サブモジュールをプッシュし忘れると、他の人がプルした場合にエラーが起きてしまう。
# 防止策1 : サブモジュールがプッシュされてなかったら、親プロジェクトのプッシュを中断する。
git push --recurse-submodules=check

# 防止策2 : 親プロジェクトをプッシュする際に、サブモジュールも含めてプッシュする。
git push --recurse-submodules=on-demand

# 防止策2のエイリアスを作っておくと楽。
git config --global alias.pushall "push --recurse-submodules=on-demand"
git pushall

```
