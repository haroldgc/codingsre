---
layout: post
title: GIT Cheatsheet
date: 2023-03-05 19:37 +0100
---

# GIT command sheet
  
## Common commands

| Operation                                               | Command                                                               |
| ------------------------------------------------------- | --------------------------------------------------------------------- |
| Initialize project                                      | ```$ git init```                                                      |
| List of files to add                                    | ```$ git status```                                                    |
| Add files to staging, in this case the entire directory | ```$ git add```                                                       |
| Unstage a file                                          | ```$ git reset HEAD <file>```                                         |
| Commit staged files                                     | ```$ git commit -m "Initial commit" ```                               |
| Stage and commit at the same time                       | ```$ git commit -am "Edits support phone number throughout website``` |

## Branching

| Operation                                                       | Command                                                     |
| --------------------------------------------------------------- | ----------------------------------------------------------- |
| List branches                                                   | ```$ git branch```                                          |
| List remote branches                                            | ```$ git branch -r```                                       |
| List all remote and local branches                              | ```$ git branch -a```                                       |
| List only branches that are (or not) included in current branch | ```$ git branch --merged```                                 |
|                                                                 | ```$ git branch --no-merged```                              |
| Switch to a different branch                                    | ```$ git checkout <branch_name>```                          |
| Create a branch                                                 | ```$ git branch <branch_name>```                            |
|                                                                 | ```$ git checkout -b <branch_name>```                       |
|                                                                 | ```$ git checkout -b <new_branch_name> <org_branch_name>``` |
| Rename/Moving a branch                                          | ```$ git branch -m <new_branch_name>```                     |
|                                                                 | ```$ git branch -m <old_branch_name> <new_branch_name>```   |
| Delete a branch                                                 | ```$ git branch -d <branch_name>```                         |
| Reset a branch                                                  | ```$ git reset --soft tree-ish```                           |
|                                                                 | ```$ git reset --mixed tree-ish```                          |
|                                                                 | ```$ git reset --hard tree-ish```                           |
| Merge branche with current branch                               | ```$ git merge branch_to_merge```                           |


Reset a branch 

| Reset | HEAD | staging | working |
| ----- | ---- | ------- | ------- |
| soft  | X    |         |         |
| mixer | X    | X       |         |
| hard  | X    | X       | X       |

WARN: Previous commits will be discarded.

## Comparing with diff

| Operation                                                                                                            | Command                                                   |
| -------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| See differences between staged and working files                                                                     | ```$ git diff```                                          |
| See differences between staged and working files with colors                                                         | ```$ git diff --color-words```                            |
| See differences between staged and HEAD (commited changes)                                                           | ```$ git diff --staged```                                 |
| This is to view the changes between two arbitrary <commit>. (Use the "git log" command to see the commit ID to use). | ```$ git diff --color-words <oldest SHA>..<newest SHA>``` |

## Checking and filtering commit log

| Operation                | Command                                                                                                 |
| ------------------------ | ------------------------------------------------------------------------------------------------------- |
| Show the commit log      | ```$ git log```                                                                                         |
|                          | ```$ git log --oneline```                                                                               |
|                          | ```$ git log --graph --all --oneline --decorate```                                                      |
|                          | ```$ got log --format=[email format: full fuller mboxrd medium oneline raw reference short tformat:]``` |
| Filetering commit log    | ```$ git log```                                                                                         |
| Tail the log             | ```$ git log -3```                                                                                      |
| Other filetring examples | ```$ git log --grep="bug"```                                                                            |
|                          | ```$ git log --since=2020-01-30```                                                                      |
|                          | ```$ git log --until="3 days ago"```                                                                    |
|                          | ```$ git log --after=2.weeks --before=3.days```                                                         |
|                          | ```$ git log --author="Harold"```                                                                       |
|                          | ```$ git log <SHA>..<SHA>```                                                                            |
|                          | ```$ git log filename```                                                                                |
|                          | ```$ git log -p```                                                                                      |
|                          | ```$ git log stat```                                                                                    |


## Remote repositories

| Operation                                                     | Command                                                           |
| ------------------------------------------------------------- | ----------------------------------------------------------------- |
| Get remote information                                        | ```$ git remote show origin```                                    |
| List existing remotes                                         | ```$ git remote```                                                |
| List remote branches                                          | ```$ git branch -r```                                             |
| Push an existing repository to github                         | ```$ git remote add origin https://github.com/<user>/<repo>```    |
| Clone an existing remote repository                           | ```$ git clone https://github.com/<user>/<repo> <project_name>``` |
| Create a remote branch in remote (-u option track the branch) | ```$ git push -u origin master```                                 |
| Remove a remote                                               | ```$ git remote rm origin```                                      |

## Save changes in the stash

| Operation                                             | Command                                        |
| ----------------------------------------------------- | ---------------------------------------------- |
| Save changes in a stash                               | ```$ git stash save "Give the stash a name"``` |
| List available stash entries                          | ```$ git stash list```                         |
| Show the changes recorded in a stash                  | ```$ git stash show <stash_entrie>```          |
|                                                       | ```$ git stash show -p <stash_entrie>```       |
| Retrieve changes with pop the stash entrie is removed | ```$ git stash pop <stash_entrie>```           |
| With apply don't remove the stash from the stash list | ```$ git stash apply <stash_entries>```        |
| Delete a stashs                                       | ```$ git stash drop stash@{0}```               |
| Delete all entries in the stash list                  | ```$ git stash clear```                        |

## List, retrieve and revert changes to files in a commit==

| Operation                                                                          | Command                                                                    |
| ---------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| Show changes in a commit. (Use the "git log" command to see the commit ID to use). | ```$ git show --color-words <SHA>```                                       |
| List files in a commit                                                             | ```$ git ls-tree HEAD```                                                   |
|                                                                                    | ```$ git ls-tree HEAD <directory>/```                                      |
| Retrieve old version of a file                                                     | ```$ git checkout <SHA> -- <file name>```                                  |
| Move or rename a file, directory or symlink.                                       | ```$ git mv <source> <destination>```                                      |
| Discard changes in the working directory.                                          | ```$ git restore <file>```                                                 |
|                                                                                    | ```$ git checkout -- <file>```                                             |
| Amend the last commit.                                                             | ```$ git commit --amend -m "Reorder recommended items for outdoor trip"``` |
| Revert changes made in a commit                                                    | ```$ git revert <SHA>```                                                   |
| Remove untracked files (*USE WITH CAUTION!*)                                       | ```$ git clean -n```                                                       |
|                                                                                    | ```$ git clean -f```                                                       |

# Configuration

List configuration:
```
$ git config --list
```

Set git configuration parameter:
```
$ git config --global user.name "Harold Gutierrez"
$ git config --global user.email "harold.gutierrez@nutanix.com"
$ git config --global core.editor "emacs"
```

+ ```--global``` is for _user_ configuration, 
+ ```--system``` is for _system_ wide configuration,
+ ```none``` is for _project_ configuration.

Configuration file:
```
~/.gitconfig
```

## Configure authentication

To configure access such that password are not required when pushing code to remote.

1. Add to ```.gitconfig``` file.
```
[credential "https://github.com/fooUser"]
        username = fooUser
	helper = store --file ~/.git-access

[credential "https://github.com/barUser"]
        username = barUser
	helper = store --file ~/.git-access
```

2. Create access file
```
❯ cat ~/.git-access
https://fooUser:<GIT Token>@github.com/fooUser
https://barUser:<GIT Token>@github.com/barUser
```

Source: [https://git-scm.com/docs/gitcredentials]

## Ignore files
Ignore files in a project
```
.gitignore
```

To ignore files so these are not tracked by GIT create the file ~.gitignore~ in the project directory and specify which files don't want to be tracked. You can use regular expresions like:
```
*?[aeiou][0-9]
logs/*.txt

# ignore php files but not index.php
*.php
!index.php
```

Check on https://github.com/github/gitignore for useful templates.


Ignore files globally
```
$ git config --global core.excludesfile ~/.gitignore_global
```

Ignore tracked files. If a file is part of the repository and we just want to ignore new changes, we need to add it to ```.gitignore``` file but also run a ```git rm --cached <file>``` for git to ignore new changes.
```
$ git rm --cached <file>
```

## Tracking empty folders

GIT doesn't track empty folder, to achive this just create a ```.gitkeep``` file inside the empty folder.

# Commands to overwrite master with another branch

```
git checkout seotweaks
git merge -s ours master
git checkout master
git merge seotweaks
```

Source: https://stackoverflow.com/questions/2862590/how-to-replace-master-branch-in-git-entirely-from-another-branch

# Miscellaneous  

## Remote .DS_Store from repo

```ß
> git rm --cached .DS_Store
> git commit -m "Remove .DS_Store"
```

## Useful links

+ Git Credential Manager
https://github.com/GitCredentialManager/git-credential-manager/blob/main/README.md
