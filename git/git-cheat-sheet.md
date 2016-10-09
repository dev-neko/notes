# Git cheat sheet

Code schoolの"Git Real" コースで学んだ内容です。

## Git Real 1

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
