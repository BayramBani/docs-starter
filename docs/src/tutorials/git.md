# Git

> version control system

## commands

* Initializing repository

  ````bash
  git init
  ````

* add changes (to a staging area)

  ````
  git add [file1.ext]
  git add [file2.ext]
  ````

  or add all :

  ````
  git add .
  ````

- discard changes in working directory or the staging area

  ````shell
  git reset --hard
  ````

- committing changes

  ````shell
  git commit -m "commit message"
  ````

- branches

  - show

    ````shell
    git branch
    ````

  - create

    ````shell
    git branch [branch.name]
    ````

  - merge

  ````shell
  git merge master [branch.name]
  ````

- compare changes

  - working directory / staging area

    ````shell
    git diff
    ````

  - staging area / repository (commit)

    ````shell
    git diff --staged
    ````

  - between commits

    ````shell
    git diff [commit1.id] [commit2.id]
    ````

* show commits

  ````bash
  git log
  git log --stat
  git log --oneline
  git log --graph
  git log --graph --oneline [branch1] [branch2]
  ````

* change version (working directory)

  ````bash
  git checkout [commit.id]
  git checkout [branch.name]
  git checkout master
  ````

* show status

  ````bash
  git status
  ````

* adding a remote

  * show

    ````shell
    git remote
    ````

  * add

    ````shell
    git remote add origin [repository.url]
    ````

  * sync remote from local repository

    ````shell
    git push origin [branch.name]
    git push origin master

    #update all branches
    git push -u --all origin
    ````

  * sync local repository from remote

    ````shell
    git fetch
    git merge master origin/master

    # or
    git pull origin master
    ````

* tag

  ````
  git tag [tag.name]
  git push origin --tags
  ````

## configuration

- change default text editor

  ````bash
  git config --global core.editor "C:\Microsoft VS Code\Code.exe -n -w"
  ````

## useful link

[Git cheat sheet](https://github.com/github/training-kit/blob/master/downloads/github-git-cheat-sheet.pdf)
