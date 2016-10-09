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
