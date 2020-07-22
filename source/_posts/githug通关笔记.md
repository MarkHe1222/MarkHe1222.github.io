---
title: githug通关笔记
date: 2020-07-22 22:00:01
categories: Git
tags:

---

`Git`几乎是现在版本管理的标配。用了好几年的`Git`，但是有一些功能还是用的比较少，发现`Github`上有个叫`githug`的小游戏，对`Git`入门和复习有很大的帮助。这里附上通关的笔记。

`Githug`地址：`https://github.com/Gazler/githug`

#### Welcome

```powershell
[ecssync@ecssync ~]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
No githug directory found, do you wish to create one? [yn]  y
Welcome to Githug!
```

#### 1 - 10

##### 1: 

```powershell
Q:

Name: init
Level: 1
Difficulty: *

A new directory, `git_hug`, has been created; initialize an empty repository in it.

********************************************************************************
A:

ecssync@ecssync git_hug]$ git init
Initialized empty Git repository in /home/ecssync/git_hug/.git/

[ecssync@ecssync git_hug]$ githug play
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 2:

```powershell
Q:

Name: config
Level: 2
Difficulty: *

Set up your git name and email, this is important so that your commits can be identified.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git config user.name mark
[ecssync@ecssync git_hug]$ git config user.email mark.he.1314@gmail.com
[ecssync@ecssync git_hug]$ githug play
********************************************************************************
*                                    Githug                                    *
********************************************************************************
What is your name? mark
What is your email? mark.he.1314@gmail.com
Your config has the following name: mark
Your config has the following email: mark.he.1314@gmail.com
Congratulations, you have solved the level!
```

##### 3:

```powershell
Q:

Name: add
Level: 3
Difficulty: *

There is a file in your folder called `README`, you should add it to your staging area
Note: You start each level with a new repo. Don't look for files from the previous one.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git add README
[ecssync@ecssync git_hug]$ githug play
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 4:

```shell
Q:

Name: commit
Level: 4
Difficulty: *

The `README` file has been added to your staging area, now commit it.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git commit
[master (root-commit) 19c35e0] commit
 Committer: ecssync <ecssync@ecssync.local>

 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README
[ecssync@ecssync git_hug]$ githug play
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 5:

```powershell
Q:

Name: clone
Level: 5
Difficulty: *

Clone the repository at https://github.com/Gazler/cloneme.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git clone https://github.com/Gazler/cloneme.git
Cloning into 'cloneme'...
remote: Enumerating objects: 7, done.
remote: Total 7 (delta 0), reused 0 (delta 0), pack-reused 7
Unpacking objects: 100% (7/7), done.
[ecssync@ecssync git_hug]$ githug play
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 6:

```powershell
Q:

Name: clone_to_folder
Level: 6
Difficulty: *

Clone the repository at https://github.com/Gazler/cloneme to `my_cloned_repo`.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git clone https://github.com/Gazler/cloneme.git my_cloned_repo
Cloning into 'my_cloned_repo'...
remote: Enumerating objects: 7, done.
remote: Total 7 (delta 0), reused 0 (delta 0), pack-reused 7
Unpacking objects: 100% (7/7), done.

[ecssync@ecssync git_hug]$ githug play
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 7:

```powershell
Q:

Name: ignore
Level: 7
Difficulty: **

The text editor 'vim' creates files ending in `.swp` (swap files) for all files that are currently open.  We don't want them creeping into the repository.  Make this repository ignore those swap files which are ending in `.swp`.

********************************************************************************
A:

ecssync@ecssync git_hug]$ vim .gitignore
[ecssync@ecssync git_hug]$ cat .gitignore
.profile.yml
.gitignore
*.swp
[ecssync@ecssync git_hug]$ githug play
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 8:

```powershell
Q:

Name: include
Level: 8
Difficulty: **

Notice a few files with the '.a' extension.  We want git to ignore all but the 'lib.a' file.

********************************************************************************
A:


[ecssync@ecssync git_hug]$ vim .gitignore
[ecssync@ecssync git_hug]$ cat .gitignore
.profile.yml
.gitignore
*.a
!lib.a

[ecssync@ecssync git_hug]$ githug play
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 9:

```powershell
Q:

Name: status
Level: 9
Difficulty: *

There are some files in this repository, one of the files is untracked, which file is it?

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git status
# On branch master
#
# Initial commit
#
# Changes to be committed:
#   (use "git rm --cached <file>..." to unstage)
#
#       new file:   Guardfile
#       new file:   README
#       new file:   config.rb
#       new file:   deploy.rb
#       new file:   setup.rb
#
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#       database.yml
[ecssync@ecssync git_hug]$ githug play
********************************************************************************
*                                    Githug                                    *
********************************************************************************
What is the full file name of the untracked file? database.yml
Congratulations, you have solved the level!
```

##### 10:

```shell
Q:

Name: number_of_files_committed
Level: 10
Difficulty: *

There are some files in this repository, how many of the files will be committed?

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#       new file:   rubyfile1.rb
#       modified:   rubyfile4.rb
#
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#       modified:   rubyfile5.rb
#
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#       rubyfile6.rb
#       rubyfile7.rb

[ecssync@ecssync git_hug]$ githug play
********************************************************************************
*                                    Githug                                    *
********************************************************************************
How many changes are going to be committed? 2
Congratulations, you have solved the level!
```

#### 11 - 20:

##### 11:

```powershell
Q:

Name: rm
Level: 11
Difficulty: **

A file has been removed from the working tree, however the file was not removed from the repository.  Find out what this file was and remove it.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git status
# On branch master
# Changes not staged for commit:
#   (use "git add/rm <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#       deleted:    deleteme.rb
#
no changes added to commit (use "git add" and/or "git commit -a")
[ecssync@ecssync git_hug]$ git rm deleteme.rb
rm 'deleteme.rb'
[ecssync@ecssync git_hug]$ githug play
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 12:

```powershell
Q:

Name: rm_cached
Level: 12
Difficulty: **

A file has accidentally been added to your staging area, find out which file and remove it from the staging area.  *NOTE* Do not remove the file from the file system, only from git.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git status
# On branch master
#
# Initial commit
#
# Changes to be committed:
#   (use "git rm --cached <file>..." to unstage)
#
#       new file:   deleteme.rb
#
[ecssync@ecssync git_hug]$ git rm --cached deleteme.rb
rm 'deleteme.rb'
[ecssync@ecssync git_hug]$ git status
# On branch master
#
# Initial commit
#
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#       deleteme.rb
nothing added to commit but untracked files present (use "git add" to track)
[ecssync@ecssync git_hug]$ githug play
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 13:

```powershell
Q:

Name: stash
Level: 13
Difficulty: **

You've made some changes and want to work on them later. You should save them, but don't commit them.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git status
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#       modified:   lyrics.txt
#
no changes added to commit (use "git add" and/or "git commit -a")
[ecssync@ecssync git_hug]$ git stash
Saved working directory and index state WIP on master: 0206059 Add some lyrics
HEAD is now at 0206059 Add some lyrics
[ecssync@ecssync git_hug]$ githug play
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 14:

```powershell
Q:

Name: rename
Level: 14
Difficulty: ***

We have a file called `oldfile.txt`. We want to rename it to `newfile.txt` and stage this change.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ ls
oldfile.txt
[ecssync@ecssync git_hug]$ git mv oldfile.txt newfile.txt
[ecssync@ecssync git_hug]$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#       renamed:    oldfile.txt -> newfile.txt
#
[ecssync@ecssync git_hug]$ githug play
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 15:

```powershell
Q:

Name: restructure
Level: 15
Difficulty: ***

You added some files to your repository, but now realize that your project needs to be restructured.  Make a new folder named `src` and using Git move all of the .html files into this folder.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ ls
about.html  contact.html  index.html
[ecssync@ecssync git_hug]$ mkdir src
[ecssync@ecssync git_hug]$ git mv *.html src
[ecssync@ecssync git_hug]$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#       renamed:    about.html -> src/about.html
#       renamed:    contact.html -> src/contact.html
#       renamed:    index.html -> src/index.html
#
[ecssync@ecssync git_hug]$ githug play
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 16:

```shell
Q:

Name: log
Level: 16
Difficulty: **

You will be asked for the hash of most recent commit.  You will need to investigate the logs of the repository for this.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git log
commit c2e4b191f112fc2c3d5f8372dcf28dd8b2ae34b9
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 14:13:16 2020 +0800

    THIS IS THE COMMIT YOU ARE LOOKING FOR!
[ecssync@ecssync git_hug]$ githug play
********************************************************************************
*                                    Githug                                    *
********************************************************************************
What is the hash of the most recent commit? c2e4b191f112fc2c3d5f8372dcf28dd8b2ae34b9
Congratulations, you have solved the level!
```

##### 17:

```powershell
Q:

Name: tag
Level: 17
Difficulty: **

We have a git repo and we want to tag the current commit with `new_tag`.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git tag new_tag
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 18:

```powershell
Q:


Name: push_tags
Level: 18
Difficulty: **

There are tags in the repository that aren't pushed into remote repository. Push them now.


From /tmp/d20200721-9363-o8bjo9/
 * [new branch]      master     -> origin/master

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git tag
tag_to_be_pushed
[ecssync@ecssync git_hug]$ git push --tags
Total 0 (delta 0), reused 0 (delta 0)
To /tmp/d20200721-9363-o8bjo9/.git
 * [new tag]         tag_to_be_pushed -> tag_to_be_pushed
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 19:

```shell
Q:

Name: commit_amend
Level: 19
Difficulty: **

The `README` file has been committed, but it looks like the file `forgotten_file.rb` was missing from the commit.  Add the file and amend your previous commit to include it.

********************************************************************************
A:


[ecssync@ecssync git_hug]$ git status
# On branch master
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#       forgotten_file.rb
nothing added to commit but untracked files present (use "git add" to track)
[ecssync@ecssync git_hug]$ git log
commit 16fd6b783380c4588d9741d7d83bd009d2ecb79c
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 14:20:04 2020 +0800

    Initial commit
[ecssync@ecssync git_hug]$ git add forgotten_file.rb


[ecssync@ecssync git_hug]$ git commit --amend
[master a1903b5] Initial commit
 Committer: ecssync <ecssync@ecssync.local>

*****[commit with VIM]*****

 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README
 create mode 100644 forgotten_file.rb
[ecssync@ecssync git_hug]$ git status
# On branch master
nothing to commit, working directory clean

[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!

```

##### 20:

```powershell
Name: commit_in_future
Level: 20
Difficulty: **

Commit your changes with the future date (e.g. tomorrow).

********************************************************************************
A:

[ecssync@ecssync git_hug]$ date
Tue Jul 21 14:25:28 CST 2020
[ecssync@ecssync git_hug]$ git commit --date="Tue Jul 22 14:25:28 CST 2020"
[master (root-commit) c31abea] tomorrow
 Committer: ecssync <ecssync@ecssync.local>

*****[commit with VIM]*****

 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

#### 21 - 30:

##### 21:

```powershell
Q:

Name: reset
Level: 21
Difficulty: **

There are two files to be committed.  The goal was to add each file as a separate commit, however both were added by accident.  Unstage the file `to_commit_second.rb` using the reset command (don't commit anything).

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#       new file:   to_commit_first.rb
#       new file:   to_commit_second.rb
#
[ecssync@ecssync git_hug]$ git reset to_commit_second.rb
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 22:

```powershell
Q:

Name: reset_soft
Level: 22
Difficulty: **

You committed too soon. Now you want to undo the last commit, while keeping the index.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git status
# On branch master
nothing to commit, working directory clean
[ecssync@ecssync git_hug]$ git log
commit 5dfd6a61b26fc982515684782de6794dd9d23412
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 14:27:25 2020 +0800

    Premature commit

commit 1f3668c9fe9c22bacd703d46485d6329ffa1fc41
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 14:27:25 2020 +0800

    Initial commit
[ecssync@ecssync git_hug]$ git reset -h
usage: git reset [--mixed | --soft | --hard | --merge | --keep] [-q] [<commit>]
   or: git reset [-q] <tree-ish> [--] <paths>...
   or: git reset --patch [<tree-ish>] [--] [<paths>...]

    -q, --quiet           be quiet, only report errors
    --mixed               reset HEAD and index
    --soft                reset only HEAD
    --hard                reset HEAD, index and working tree
    --merge               reset HEAD, index and working tree
    --keep                reset HEAD but keep local changes
    -p, --patch           select hunks interactively

[ecssync@ecssync git_hug]$ git reset --soft HEAD^1
[ecssync@ecssync git_hug]$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#       new file:   newfile.rb
#
[ecssync@ecssync git_hug]$ git log
commit 1f3668c9fe9c22bacd703d46485d6329ffa1fc41
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 14:27:25 2020 +0800

    Initial commit
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 23:

``` powershell
Q:

Name: checkout_file
Level: 23
Difficulty: ***

A file has been modified, but you don't want to keep the modification.  Checkout the `config.rb` file from the last commit.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git status
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#       modified:   config.rb
#
no changes added to commit (use "git add" and/or "git commit -a")
[ecssync@ecssync git_hug]$ git checkout -- config.rb
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 24:

```powershell
Q:

Name: remote
Level: 24
Difficulty: **

This project has a remote repository.  Identify it.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git remote
my_remote_repo
[ecssync@ecssync git_hug]$ git remote -v
my_remote_repo  https://github.com/Gazler/githug (fetch)
my_remote_repo  https://github.com/Gazler/githug (push)
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
What is the name of the remote repository? my_remote_repo
Congratulations, you have solved the level!
```

##### 25:

```powershell
Q:

Name: remote_url
Level: 25
Difficulty: **

The remote repositories have a url associated to them.  Please enter the url of remote_location.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git remote -v
my_remote_repo  https://github.com/Gazler/githug (fetch)
my_remote_repo  https://github.com/Gazler/githug (push)
remote_location https://github.com/githug/not_a_repo (fetch)
remote_location https://github.com/githug/not_a_repo (push)
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
What is the url of the remote repository? https://github.com/githug/not_a_repo
Congratulations, you have solved the level!
```

##### 26:

```powershell
Q:

Name: pull
Level: 26
Difficulty: **

You need to pull changes from your origin repository.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git pull -h
usage: git pull [-n | --no-stat] [--[no-]commit] [--[no-]squash] [--[no-]ff] [-s strategy]... [<fetch-options>] <repo> <head>...

Fetch one or more remote refs and merge it/them into the current HEAD.
[ecssync@ecssync git_hug]$ git pull origin master
From https://github.com/pull-this/thing-to-pull
 * branch            master     -> FETCH_HEAD
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 27:

```powershell
Q:

Name: remote_add
Level: 27
Difficulty: **

Add a remote repository called `origin` with the url https://github.com/githug/githug

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git remote add origin https://github.com/githug/githug
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 28:

```powershell
Q:

Name: push
Level: 28
Difficulty: ***

Your local master branch has diverged from the remote origin/master branch. Rebase your commit onto origin/master and push it to remote.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git rebase origin/master
First, rewinding head to replay your work on top of it...
Applying: First commit
Applying: Second commit
Applying: Third commit
[ecssync@ecssync git_hug]$ git status
# On branch master
# Your branch is ahead of 'origin/master' by 3 commits.
#   (use "git push" to publish your local commits)
#
nothing to commit, working directory clean
[ecssync@ecssync git_hug]$ git push origin master
Counting objects: 7, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 575 bytes | 0 bytes/s, done.
Total 6 (delta 2), reused 0 (delta 0)
To /tmp/d20200721-10098-1wufgfl/.git
   95ea39b..34ef860  master -> master
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 29:

```powershell
Q:

Name: diff
Level: 29
Difficulty: **

There have been modifications to the `app.rb` file since your last commit.  Find out which line has changed.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git status
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#       modified:   app.rb
#
no changes added to commit (use "git add" and/or "git commit -a")
[ecssync@ecssync git_hug]$ git diff app.rb
diff --git a/app.rb b/app.rb
index 4f703ca..3bfa839 100644
--- a/app.rb
+++ b/app.rb
@@ -23,7 +23,7 @@ get '/yet_another' do
   erb :success
 end
 get '/another_page' do
-  @message = get_response('data.json')
+  @message = get_response('server.json')
   erb :another
 end

[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
What is the number of the line which has changed? 26
Congratulations, you have solved the level!
```

##### 30:

```powershell
Q:

Name: blame
Level: 30
Difficulty: **

Someone has put a password inside the file `config.rb` find out who it was.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git status
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#       modified:   config.rb
#
no changes added to commit (use "git add" and/or "git commit -a")
[ecssync@ecssync git_hug]$ git blame config.rb
^5e8863d (Gary Rennie       2012-03-08 23:05:24 +0000  1) class Config
70d00535 (Bruce Banner      2012-03-08 23:07:41 +0000  2)   attr_accessor :name, :password
97bdd0cc (Spider Man        2012-03-08 23:08:15 +0000  3)   def initialize(name, password = nil, options = {})
^5e8863d (Gary Rennie       2012-03-08 23:05:24 +0000  4)     @name = name
97bdd0cc (Spider Man        2012-03-08 23:08:15 +0000  5)     @password = password || "i<3evil"
00000000 (Not Committed Yet 2020-07-21 14:42:38 +0800  6)
09409480 (Spider Man        2012-03-08 23:06:18 +0000  7)     if options[:downcase]
09409480 (Spider Man        2012-03-08 23:06:18 +0000  8)       @name.downcase!
09409480 (Spider Man        2012-03-08 23:06:18 +0000  9)     end
70d00535 (Bruce Banner      2012-03-08 23:07:41 +0000 10)
ffd39c2d (Gary Rennie       2012-03-08 23:08:58 +0000 11)     if options[:upcase]
ffd39c2d (Gary Rennie       2012-03-08 23:08:58 +0000 12)       @name.upcase!
ffd39c2d (Gary Rennie       2012-03-08 23:08:58 +0000 13)     end
ffd39c2d (Gary Rennie       2012-03-08 23:08:58 +0000 14)
^5e8863d (Gary Rennie       2012-03-08 23:05:24 +0000 15)   end
^5e8863d (Gary Rennie       2012-03-08 23:05:24 +0000 16) end
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Who made the commit with the password? Spider Man
Congratulations, you have solved the level!
```

#### 31 - 40:

##### 31:

```powershell
Q:

Name: branch
Level: 31
Difficulty: *

You want to work on a piece of code that has the potential to break things, create the branch test_code.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git status
# On branch master
nothing to commit, working directory clean
[ecssync@ecssync git_hug]$ git checkout -b test_code
Switched to a new branch 'test_code'
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 32:

```powershell
Q:

Name: checkout
Level: 32
Difficulty: **

Create and switch to a new branch called my_branch.  You will need to create a branch like you did in the previous level.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git checkout -b my_branch
Switched to a new branch 'my_branch'
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 33:

```powershell
Q:

Name: checkout_tag
Level: 33
Difficulty: **

You need to fix a bug in the version 1.2 of your app. Checkout the tag `v1.2`.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git tag
v1.0
v1.2
v1.5

[ecssync@ecssync git_hug]$ git checkout v1.2
Note: checking out 'v1.2'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b new_branch_name

HEAD is now at 6844746... Some more changes

[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 34:

```powershell
Q:

Name: checkout_tag_over_branch
Level: 34
Difficulty: **

You need to fix a bug in the version 1.2 of your app. Checkout the tag `v1.2` (Note: There is also a branch named `v1.2`).

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git branch
* master
  v1.2
[ecssync@ecssync git_hug]$ git tag
v1.0
v1.2
v1.5
[ecssync@ecssync git_hug]$ git checkout tags/v1.2
Note: checking out 'tags/v1.2'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b new_branch_name

HEAD is now at 4cc8649... Some more changes
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 35:

```shell
Q:

Name: branch_at
Level: 35
Difficulty: ***

You forgot to branch at the previous commit and made a commit on top of it. Create branch test_branch at the commit before the last.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git status
# On branch master
nothing to commit, working directory clean
[ecssync@ecssync git_hug]$ git branch
* master
[ecssync@ecssync git_hug]$ git log
commit 33da42e002d4b7fdf3f77865a957b947652d7fda
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 14:47:51 2020 +0800

    Updating file1 again

commit 580d1a83c099498c4f92b494edc86646931365b5
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 14:47:50 2020 +0800

    Updating file1

commit df106ed800fd05f171152f92cd40268b7eb933b0
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 14:47:50 2020 +0800

    Adding file1




[ecssync@ecssync git_hug]$ git branch test_branch HEAD^1
[ecssync@ecssync git_hug]$ git branch
* master
  test_branch
[ecssync@ecssync git_hug]$ git log
commit 33da42e002d4b7fdf3f77865a957b947652d7fda
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 14:47:51 2020 +0800

    Updating file1 again

commit 580d1a83c099498c4f92b494edc86646931365b5
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 14:47:50 2020 +0800

    Updating file1

commit df106ed800fd05f171152f92cd40268b7eb933b0
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 14:47:50 2020 +0800

    Adding file1
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!

```

##### 36:

```powershell
Q:

Name: delete_branch
Level: 36
Difficulty: **

You have created too many branches for your project. There is an old branch in your repo called 'delete_me', you should delete it.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git branch
  delete_me
* master
[ecssync@ecssync git_hug]$ git branch -d delete_me
Deleted branch delete_me (was b60afe2).
[ecssync@ecssync git_hug]$ git branch
* master
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 37:

```powershell
Q:

Name: push_branch
Level: 37
Difficulty: **

You've made some changes to a local branch and want to share it, but aren't yet ready to merge it with the 'master' branch.  Push only 'test_branch' to the remote repository

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git branch
* master
  other_branch
  test_branch
[ecssync@ecssync git_hug]$ git status
# On branch master
# Your branch is ahead of 'origin/master' by 1 commit.
#   (use "git push" to publish your local commits)
#
nothing to commit, working directory clean
[ecssync@ecssync git_hug]$ git push origin test_branch
Counting objects: 7, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 562 bytes | 0 bytes/s, done.
Total 6 (delta 3), reused 0 (delta 0)
To /tmp/d20200721-10878-18gcglj/.git
 * [new branch]      test_branch -> test_branch
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 38:

```powershell
Q:

Name: merge
Level: 38
Difficulty: **

We have a file in the branch 'feature'; Let's merge it to the master branch.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git merge feature
Updating e12277f..cc8ea5a
Fast-forward
 file2 | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file2
[ecssync@ecssync git_hug]$ git status
# On branch master
nothing to commit, working directory clean
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 39:

```powershell
Q:

Name: fetch
Level: 39
Difficulty: **

Looks like a new branch was pushed into our remote repository. Get the changes without merging them with the local repository

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git fetch origin
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 2 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (2/2), done.
From /tmp/d20200721-10967-4l6fg4/
 * [new branch]      new_branch -> origin/new_branch
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 40:

````powershell
Q:

Name: rebase
Level: 40
Difficulty: **

We are using a git rebase workflow and the feature branch is ready to go into master. Let's rebase the feature branch onto our master branch.

********************************************************************************
A:


[ecssync@ecssync git_hug]$ git branch
  feature
* master
[ecssync@ecssync git_hug]$ git checkout feature
Switched to branch 'feature'
[ecssync@ecssync git_hug]$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: add feature
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
````

#### 41 - 50:

##### 41:

```powershell
Q:

Name: rebase_onto
Level: 41
Difficulty: **

You have created your branch from `wrong_branch` and already made some commits, and you realise that you needed to create your branch from `master`. Rebase your commits onto `master` branch so that you don't have `wrong_branch` commits.

********************************************************************************
A:


[ecssync@ecssync git_hug]$ git branch
  master
* readme-update
  wrong_branch
[ecssync@ecssync git_hug]$ git log
commit ed867debbb0cbf7ce83112f7f72a43744c407cd7
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 15:01:12 2020 +0800

    Add `Install` header in readme

commit 385b5fb15c9e65e9c85aa910cf21ec71a78d43c2
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 15:01:12 2020 +0800

    Add `About` header in readme

commit 6cf72f834392c2d061d0580d6c70614d78b77713
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 15:01:12 2020 +0800

    Add app name in readme

commit b0cacccc9ed0a9b46d7b463533035354d3275196
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 15:01:12 2020 +0800

    Wrong changes

commit a7bfef30ddb70443802f742f219cc492a0bbddb0
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 15:01:12 2020 +0800

    Create authors file

[ecssync@ecssync git_hug]$ git rebase --onto master wrong_branch readme-update
First, rewinding head to replay your work on top of it...
Applying: Add app name in readme
Applying: Add `About` header in readme
Applying: Add `Install` header in readme

[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 42:

```powershell
Q:

Name: repack
Level: 42
Difficulty: **

Optimise how your repository is packaged ensuring that redundant packs are removed.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git gc
Counting objects: 3, done.
Writing objects: 100% (3/3), done.
Total 3 (delta 0), reused 0 (delta 0)
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 43:

```powershell
Q:

Name: cherry-pick
Level: 43
Difficulty: ***

Your new feature isn't worth the time and you're going to delete it. But it has one commit that fills in `README` file, and you want this commit to be on the master as well.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git branch
* master
  new-feature
[ecssync@ecssync git_hug]$ git checkout new-feature
Switched to branch 'new-feature'
[ecssync@ecssync git_hug]$ git log
commit ea2a47c19b85fc321e2737ddc49db3deeba3a1b5
Author: Andrey <aslushnikov@gmail.com>
Date:   Wed Mar 28 02:28:35 2012 +0400

    some small fixes

commit 4a1961bce62840eaef9c4392fe5cc799e38c9b7b
Author: Andrey <aslushnikov@gmail.com>
Date:   Wed Mar 28 02:27:18 2012 +0400

    Fixed feature

commit ca32a6dac7b6f97975edbe19a4296c2ee7682f68
Author: Andrey <aslushnikov@gmail.com>
Date:   Wed Mar 28 02:25:51 2012 +0400

    Filled in README.md with proper input

commit 58a8c8edcfdd00c6d8cce9aada8f987a1677571f
Author: Andrey <aslushnikov@gmail.com>
Date:   Wed Mar 28 02:24:41 2012 +0400

    Added a stub for the feature

commit ea3dbcc5e2d2359698c3606b0ec44af9f76def54
Author: Andrey <aslushnikov@gmail.com>
Date:   Wed Mar 28 02:20:32 2012 +0400

    Initial commit
[ecssync@ecssync git_hug]$ git checkout master
Switched to branch 'master'
[ecssync@ecssync git_hug]$ git cherry-pick ca32a6dac7b6f97975edbe19a4296c2ee7682f68
[master 5c78d26] Filled in README.md with proper input
 Author: Andrey <aslushnikov@gmail.com>
...
 1 file changed, 1 insertion(+), 2 deletions(-)
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 44:

```powershell
Q:

Name: grep
Level: 44
Difficulty: **

Your project's deadline approaches, you should evaluate how many TODOs are left in your code

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git grep 'TODO' | wc -l
4
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
How many items are there in your todolist? 4
Congratulations, you have solved the level!
```

##### 45:

```powershell
Q:

Name: rename_commit
Level: 45
Difficulty: ***

Correct the typo in the message of your first (non-root) commit.

********************************************************************************
A:
[ecssync@ecssync git_hug]$ git log
commit ae9e2f844acb4388bf45d6ee614a22678e5efc61
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 15:24:49 2020 +0800

    Second commit

commit ccb0fabfe03aeba0035a0f39e93f1fe17c94edb0
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 15:24:49 2020 +0800

    First coommit

commit 240aa55faa57f8d626a3bc68398d6c8ac2216977
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 15:24:49 2020 +0800

    Initial commit
[ecssync@ecssync git_hug]$ git rebase -i HEAD~2
[detached HEAD f845aac] First commit

 "reword"

 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file1
Successfully rebased and updated refs/heads/master.
[ecssync@ecssync git_hug]$ git log
commit 372dd8f04d9997d96e36d4c9eb67ae2867ca6b2d
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 15:24:49 2020 +0800

    Second commit

commit f845aac2ddf901e1fabfe13086f89046e8724fa5
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 15:24:49 2020 +0800

    First commit

commit 240aa55faa57f8d626a3bc68398d6c8ac2216977
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 15:24:49 2020 +0800

    Initial commit
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 46:

```powershell
Q:

Name: squash
Level: 46
Difficulty: ****

You have committed several times but would like all those changes to be one commit.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git rebase -i HEAD~4
[detached HEAD 3d3b91a] Adding README
 Committer: ecssync <ecssync@ecssync.local>
... ...
 1 file changed, 3 insertions(+)
 create mode 100644 README
Successfully rebased and updated refs/heads/master.

##############################vim editor##############################
pick c4fef0e Adding README
squash 5caa017 Updating README (squash this commit into Adding README)
squash 7bc5942 Updating README (squash this commit into Adding README)
squash 9100103 Updating README (squash this commit into Adding README)

# Rebase a7aa916..9100103 onto a7aa916
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
##############################vim editor##############################
[ecssync@ecssync git_hug]$ git log
commit 3d3b91a9e2d2186f6f416bf536e014cbdcec457c
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 15:53:21 2020 +0800

    Adding README

    Updating README (squash this commit into Adding README)

    Updating README (squash this commit into Adding README)

    Updating README (squash this commit into Adding README)

commit a7aa9161d36432580de6548d854f79a1116d2f32
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 15:53:21 2020 +0800

    Initial Commit
    
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 47: 

````powershell
Q:

Name: merge_squash
Level: 47
Difficulty: ***

Merge all commits from the long-feature-branch as a single commit.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git branch
  long-feature-branch
* master
[ecssync@ecssync git_hug]$ git merge --squash long-feature-branch
Squash commit -- not updating HEAD
Automatic merge went well; stopped before committing as requested
[ecssync@ecssync git_hug]$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#       new file:   file3
#
[ecssync@ecssync git_hug]$ git commit -m "X"
[master 77ceea7] X
 Committer: ecssync <ecssync@ecssync.local>


 1 file changed, 3 insertions(+)
 create mode 100644 file3
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!

````

##### 48:

```powershell
Q:

Name: reorder
Level: 48
Difficulty: ****

You have committed several times but in the wrong order. Please reorder your commits.

********************************************************************************
A:

#############################vim editor##############################
#
pick 15176e9 First commit
pick 676c1a4 Third commit
pick de1362e Second commit
      ⬇️
pick 15176e9 First commit
pick de1362e Second commit   
pick 676c1a4 Third commit
##############################vim editor##############################

[ecssync@ecssync git_hug]$ git log
commit 4d61dc7ea9f0717626a0169b135a7461a8a4e388
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 15:56:34 2020 +0800

    Third commit

commit f5ef4d3b972f3317fe5ef530d0b2114955cea0ed
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 15:56:34 2020 +0800

    Second commit

commit 15176e90ef0de866d9c89795ccc225a119998258
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 15:56:34 2020 +0800

    First commit

commit 8ee2035dfaf0814aaa1517a904ffc82163f2b313
Author: ecssync <ecssync@ecssync.local>
Date:   Tue Jul 21 15:56:34 2020 +0800

    Initial Setup

[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!

```

##### 49:

```powershell
Q:

Name: bisect
Level: 49
Difficulty: ***

A bug was introduced somewhere along the way.  You know that running `ruby prog.rb 5` should output 15.  You can also run `make test`.  What are the first 7 chars of the hash of the commit that introduced the bug.

********************************************************************************
A:


[ecssync@ecssync git_hug]$ git log --pretty=oneline
12628f463f4c722695bf0e9d603c9411287885db Another Commit
979576184c5ec9667cf7593cf550c420378e960f Another Commit
028763b396121e035f672ef5af75d2dcb1cc8146 Another Commit
888386c77c957dc52f3113f2483663e3132559d4 Another Commit
bb736ddd9b83d6296d23444a2ab3b0d2fa6dfb81 Another Commit
18ed2ac1522a014412d4303ce7c8db39becab076 Another Commit
5db7a7cb90e745e2c9dbdd84810ccc7d91d92e72 Another Commit
7c03a99ba384572c216769f0273b5baf3ba83694 Another Commit
9f54462abbb991b167532929b34118113aa6c52e Another Commit
5d1eb75377072c5c6e5a1b0ac4159181ecc4edff Another Commit
fdbfc0d403e5ac0b2659cbfa2cbb061fcca0dc2a Another Commit
a530e7ed25173d0800cfe33cc8915e5929209b8e Another Commit
ccddb96f824a0e929f5fecf55c0f4479552246f3 Another Commit
2e1735d5bef6db0f3e325051a179af280f05573a Another Commit
ffb097e3edfa828afa565eeceee6b506b3f2a131 Another Commit
e060c0d789288fda946f91254672295230b2de9d Another Commit
49774ea84ae3723cc4fac75521435cc04d56b657 Another Commit
8c992afff5e16c97f4ef82d58671a3403d734086 Another Commit
80a9b3d94237f982b6c9052e6d56b930f18a4ef5 Another Commit
f608824888b83bbedc1f658be7496ffea467a8fb First commit
[ecssync@ecssync git_hug]$ git bisect HEAD f608824888b83bbedc1f658be7496ffea467a8fb
usage: git bisect [help|start|bad|good|skip|next|reset|visualize|replay|log|run]
[ecssync@ecssync git_hug]$ git bisect start  HEAD f608824888b83bbedc1f658be7496ffea467a8fb
Bisecting: 9 revisions left to test after this (roughly 3 steps)
[fdbfc0d403e5ac0b2659cbfa2cbb061fcca0dc2a] Another Commit
[ecssync@ecssync git_hug]$ make test
ruby prog.rb 5 | ruby test.rb
[ecssync@ecssync git_hug]$ git bisect good fdbfc0d403e5ac0b2659cbfa2cbb061fcca0dc2a
Bisecting: 4 revisions left to test after this (roughly 2 steps)
[18ed2ac1522a014412d4303ce7c8db39becab076] Another Commit
[ecssync@ecssync git_hug]$ git bisect run make test
running make test
ruby prog.rb 5 | ruby test.rb
make: *** [test] Error 1
Bisecting: 2 revisions left to test after this (roughly 1 step)
[9f54462abbb991b167532929b34118113aa6c52e] Another Commit
running make test
ruby prog.rb 5 | ruby test.rb
Bisecting: 0 revisions left to test after this (roughly 1 step)
[5db7a7cb90e745e2c9dbdd84810ccc7d91d92e72] Another Commit
running make test
ruby prog.rb 5 | ruby test.rb
18ed2ac1522a014412d4303ce7c8db39becab076 is the first bad commit
commit 18ed2ac1522a014412d4303ce7c8db39becab076
Author: Robert Bittle <guywithnose@gmail.com>
Date:   Mon Apr 23 06:52:10 2012 -0400

    Another Commit

:100644 100644 917e70054c8f4a4a79a8e805c0e1601b455ad236 7562257b8e6446686ffc43a2386c50c254365020 M      prog.rb
bisect run success
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
What are the first 7 characters of the hash of the commit that introduced the bug? 18ed2ac1522a014412d4303ce7c8db39becab076
Congratulations, you have solved the level!
```

##### 50:

```powershell
Q:

Name: stage_lines
Level: 50
Difficulty: ****

You've made changes within a single file that belong to two different features, but neither of the changes are yet staged. Stage only the changes belonging to the first feature.

********************************************************************************
A:


[ecssync@ecssync git_hug]$ git diff
diff --git a/feature.rb b/feature.rb
index 1a271e9..4a80dda 100644
--- a/feature.rb
+++ b/feature.rb
@@ -1 +1,3 @@
 this is the class of my feature
+This change belongs to the first feature
+This change belongs to the second feature   ----------> remove
[ecssync@ecssync git_hug]$
[ecssync@ecssync git_hug]$
[ecssync@ecssync git_hug]$ git add -e feature.rb
[ecssync@ecssync git_hug]$ git diff
diff --git a/feature.rb b/feature.rb
index 3bccd0e..4a80dda 100644
--- a/feature.rb
+++ b/feature.rb
@@ -1,2 +1,3 @@
 this is the class of my feature
 This change belongs to the first feature
+This change belongs to the second feature
[ecssync@ecssync git_hug]$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#       modified:   feature.rb
#
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#       modified:   feature.rb
#
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

#### 51 - 56:

##### 51:

```powershell
Q:

Name: find_old_branch
Level: 51
Difficulty: ****

You have been working on a branch but got distracted by a major issue and forgot the name of it. Switch back to that branch.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git branch
  blowup_sun_for_ransom
  cure_common_cold
* kill_the_batman
  solve_world_hunger
[ecssync@ecssync git_hug]$ git reflog
894a16d HEAD@{0}: commit: commit another todo
6876e5b HEAD@{1}: checkout: moving from solve_world_hunger to kill_the_batman
324336a HEAD@{2}: commit: commit todo
6876e5b HEAD@{3}: checkout: moving from blowup_sun_for_ransom to solve_world_hunger
6876e5b HEAD@{4}: checkout: moving from kill_the_batman to blowup_sun_for_ransom
6876e5b HEAD@{5}: checkout: moving from cure_common_cold to kill_the_batman
6876e5b HEAD@{6}: commit (initial): initial commit
[ecssync@ecssync git_hug]$ git checkout solve_world_hunger
Switched to branch 'solve_world_hunger'
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 52:

```powershell
Q:

Name: revert
Level: 52
Difficulty: ****

You have committed several times but want to undo the middle commit.
All commits have been pushed, so you can't change existing history.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git log --pretty=oneline
b2803390aa23abd6ff45faf62b117f002b612218 Second commit
1d140556c1ca8af6e70a8e98abc5e83491dc9f80 Bad commit
46445b467625aac78ef3ab499d79f7b7229c199f First commit
[ecssync@ecssync git_hug]$ git revert 1d140556c1ca8af6e70a8e98abc5e83491dc9f80 --no-edit
[master a77bae5] Revert "Bad commit"

 delete mode 100644 file3
[ecssync@ecssync git_hug]$ git log --pretty=oneline
a77bae5a86c856cbb8f417b6c6f8c9f7ddf8c538 Revert "Bad commit"
b2803390aa23abd6ff45faf62b117f002b612218 Second commit
1d140556c1ca8af6e70a8e98abc5e83491dc9f80 Bad commit
46445b467625aac78ef3ab499d79f7b7229c199f First commit
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 53:

```powershell
Q:

Name: restore
Level: 53
Difficulty: ****

You decided to delete your latest commit by running `git reset --hard HEAD^`.  (Not a smart thing to do.)  You then change your mind, and want that commit back.  Restore the deleted commit.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git log --pretty=oneline
5d4f0fe4f22a0b4fa72084b16bce2accab6b5ce4 First commit
70fec1926947443bd760b8e8c79fbb86d3b462fe Initial commit
[ecssync@ecssync git_hug]$ git reflog
5d4f0fe HEAD@{0}: reset: moving to HEAD^
d7de144 HEAD@{1}: commit: Restore this commit
5d4f0fe HEAD@{2}: commit: First commit
70fec19 HEAD@{3}: commit (initial): Initial commit
[ecssync@ecssync git_hug]$ git reset --hard d7de144
HEAD is now at d7de144 Restore this commit

[ecssync@ecssync git_hug]$ git log --pretty=oneline
d7de144da5c4f506ab085a7a34e8a21c0b5c0db3 Restore this commit
5d4f0fe4f22a0b4fa72084b16bce2accab6b5ce4 First commit
70fec1926947443bd760b8e8c79fbb86d3b462fe Initial commit
[ecssync@ecssync git_hug]$ git reflog
d7de144 HEAD@{0}: reset: moving to d7de144
5d4f0fe HEAD@{1}: reset: moving to HEAD^
d7de144 HEAD@{2}: commit: Restore this commit
5d4f0fe HEAD@{3}: commit: First commit
70fec19 HEAD@{4}: commit (initial): Initial commit
[ecssync@ecssync git_hug]$

[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 54:

```powershell
Q:

Name: conflict
Level: 54
Difficulty: ****

You need to merge mybranch into the current branch (master). But there may be some incorrect changes in mybranch which may cause conflicts. Solve any merge-conflicts you come across and finish the merge.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git branch
* master
  mybranch
[ecssync@ecssync git_hug]$ git merge mybranch
Auto-merging poem.txt
CONFLICT (content): Merge conflict in poem.txt
Automatic merge failed; fix conflicts and then commit the result.
[ecssync@ecssync git_hug]$ git status
# On branch master
# You have unmerged paths.
#   (fix conflicts and run "git commit")
#
# Unmerged paths:
#   (use "git add <file>..." to mark resolution)
#
#       both modified:      poem.txt
#
no changes added to commit (use "git add" and/or "git commit -a")
[ecssync@ecssync git_hug]$ git diff
diff --cc poem.txt
index 3cb65be,1db9aa5..0000000
--- a/poem.txt
+++ b/poem.txt
@@@ -1,5 -1,4 +1,8 @@@
  Humpty dumpty
++<<<<<<< HEAD
 +Categorized shoes by color
++=======
+ Sat on a wall
++>>>>>>> mybranch
  Humpty dumpty
  Had a great fall
-
[ecssync@ecssync git_hug]$ vim poem.txt

[ecssync@ecssync git_hug]$ git status -s
UU poem.txt
[ecssync@ecssync git_hug]$ git add .
[ecssync@ecssync git_hug]$ git commit -m "Merge from mybranch"
[master f9adf97] Merge from mybranch
 Committer: ecssync <ecssync@ecssync.local>
 ... ...

[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 55:

```powershell
Q:

Name: submodule
Level: 55
Difficulty: **

You want to include the files from the following repo: `https://github.com/jackmaney/githug-include-me` into a the folder `./githug-include-me`. Do this without manually cloning the repo or copying the files from the repo into this repo.

********************************************************************************
A:

[ecssync@ecssync git_hug]$ git submodule add https://github.com/jackmaney/githug-include-me
Cloning into 'githug-include-me'...
remote: Enumerating objects: 9, done.
remote: Total 9 (delta 0), reused 0 (delta 0), pack-reused 9
Unpacking objects: 100% (9/9), done.
[ecssync@ecssync git_hug]$ githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!
```

##### 56:

```powershell
Name: contribute
Level: 56
Difficulty: ***

This is the final level, the goal is to contribute to this repository by making a pull request on GitHub.  Please note that this level is designed to encourage you to add a valid contribution to Githug, not testing your ability to create a pull request.  Contributions that are likely to be accepted are levels, bug fixes and improved documentation.
```

#### 参考

> https://wiki.jikexueyuan.com/project/githug-walkthrough/levels.html 









