# Introduction

Here are is the basic workflow for working with git

## Cloning a repository

The first command to learn is *git clone*. It allows you to clone a repository from a url to your local machine. From this point on we can refer to 
that repository as the 'origin' and your machine's repository as the 'local' repository. 

For example: 

```
$ git clone git@github.com:danielcaldwell/test_git.git
Cloning into 'test_git'...
remote: Enumerating objects: 40, done.
remote: Counting objects: 100% (40/40), done.
remote: Compressing objects: 100% (28/28), done.
remote: Total 40 (delta 6), reused 38 (delta 4), pack-reused 0
Receiving objects: 100% (40/40), done.
Resolving deltas: 100% (6/6), done.
Checking connectivity... done.
```

If you look into the directory that was downloaded you will see a hidden *.git* directory: 

```
$ cd test_git

$ ls -la
total 16
drwxr-xr-x   5 dcaldwel  staff  160 Dec 13 08:23 .
drwxr-xr-x  11 dcaldwel  staff  352 Dec 13 08:23 ..
drwxr-xr-x  13 dcaldwel  staff  416 Dec 13 08:23 .git
-rw-r--r--   1 dcaldwel  staff  135 Dec 13 08:23 test.txt
-rw-r--r--   1 dcaldwel  staff   12 Dec 13 08:23 test2.txt
```

Seeing a *.git* folder in folder is a good indication that it is a git repository. This is useful when 
you have to investigate an error with a web application you've never looked at before. You go to the server, see
where the web application is being run from, then look for .git folders to see if 
the web application's source code was pulled from git. This can help you find more information about it. 


## Verifying where a repository's 'origin' is

To check the repo to find where it came from use the *git remote* command. 

```
$ git remote -v
origin	git@github.com:danielcaldwell/test_git.git (fetch)
origin	git@github.com:danielcaldwell/test_git.git (push)
```

Here we can see that this repo was pulled from GitHub. Rather than GitLab, BitBucket, et cetera...


## origin vs upstream vs remote

There are times when we see various terms used to describe the same thing. A remote, is an upstream repository
for the local repository. You can create more upstream repositories using 'git remote add' but only one will be the 
origin repository. When you do command to pull/push from the remote repo, the 'origin' repository is used. 

# Adding and Committing a change

There are two "areas" that can be referred to when making changes. The Local repository, which can be referred to as the "working area", that
you can make changes too, and a "staging" area, where commits are recorded in order to prepare them to be pushed to the remote 'origin' 
repository. 

# Checking for changes 

You can use the *git status* command to check for changes between the repository and your working area. This will identify the files that 
you have changed, that need to be committed to the remote 'origin' repository. 

For example, here I changed a file named test.txt and added a file named test3.txt. When I use git status they show up. 

```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   test.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	test3.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Here we can see the modified files, and "untracked" files (files that are not part of the local repository). They have been altered in the
working area. To move the changes into the "staging" area, we need to use *git add* in order to do so. 

```
$ git add test.txt 
$ git add test3.txt 

$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   test.txt
	new file:   test3.txt
```

After adding the files, we can see the modifications in the "staging" area. Then we can use *git commit* to add them to the local repository. 


```
$ git log -3 --oneline 
c8943c0 master 11
255f948 master 10
9ed0920 master 9

$ git commit -m "updated test and added test3"
[master ae4868d] updated test and added test3
 2 files changed, 2 insertions(+)
 create mode 100644 test3.txt

$ git log -4 --oneline
ae4868d updated test and added test3
c8943c0 master 11
255f948 master 10
9ed0920 master 9

$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
nothing to commit, working directory clean
```

After committing, we can see that our commit is in the commit log, it is stored in the local repository's master branch. The "working area" is 
now clean with no differences between it and the local repository. 


