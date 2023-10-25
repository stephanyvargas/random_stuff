# Learning GIT 

## Learning GIT BRANCHING

Use this url of git branching https://learngitbranching.js.org/ to learn git online. 
I am keeping track of the lessons and some side material here =).

### GIT add 
If files that have been added but shouldn't check here https://www.freecodecamp.org/news/undo-git-add-how-to-remove-added-files-in-git/

### Git commit
A commit in a git repository records a snapshot of all the (tracked) files in your directory. It's like a giant copy and paste.
Git wants to keep commits as lightweight as possible though, so it doesn't just blindly copy the entire directory every time you commit. It can (when possible) compress a commit as a set of changes, or a "delta", from one version of the repository to the next.

Git also maintains a history of which commits were made when. That's why most commits have ancestor commits above them.
```shell
git commit 
```

### Branches in Git 
Are incredibly lightweight aand they are simply pointers to a specific commit.
Because there is no storage / memory overhead with making many branches, it's easier to logically divide up your work than have big beefy branches.

```shell
git checkout <name_of_branch>
git commit
```

**Shortcut:** if you want to create a new branch AND check it out at the same time, you can simply type 
```shell
git checkout -b <yourbranchname>.
```

**Note:** 
In Git version 2.23, a new command called git switch was introduced to eventually replace git checkout, which is somewhat overloaded (it does a bunch of different things depending on the arguments). The lessons here will still use checkout instead of switch because the switch command is still considered experimental and the syntax may change in the future. However you can still try out the new switch command in this application, and also learn more here https://git-scm.com/docs/git-switch.

### Merging in GIT
Now we need to learn some kind of way of combining the work from two different branches together. This will allow us to branch off, develop a new feature, and then combine it back in.

#### Merge
Merging in Git creates a special commit that has two unique parents. A commit with two parents essentially means "I want to include all the work from this parent over here and this one over here, and the set of all their parents."

<p align="center">
<img src="git_merge_fig.png" width="800" height="400" />
</p>

- Solution to 3rd exercise

```shell
git checkout -b bugFix
git commit 
git checkout main
git commit 
git merge bugFix
```

#### Rebase
The second way of combining work between branches is rebasing. Rebasing essentially takes a set of commits, "copies" them, and plops them down somewhere else.

While this sounds confusing, the advantage of rebasing is that it can be used to make a nice linear sequence of commits. 
The *commit log / history* of the repository will be a lot cleaner if only rebasing is allowed.

<p align="center">
<img src="git_rebase.png" width="800" height="400" />
</p>


- Solution to problem 4

We would like to move our work from bugFix directly onto the work from main. That way it would look like these two features were developed sequentially, when in reality they were developed in parallel.
```shell
git checkout -b bugFix
git commit 
git checkout main
git commit
git checkout bugFix
git rebase main
```

#### Moving around in GIT

1. **HEAD** 
	- HEAD is the symbolic name for the currently checked out commit -- it's essentially what commit you're working on top of. 
	- HEAD always points to the most recent commit which is reflected in the working tree. 
	- Most git commands which make changes to the working tree will start by changing HEAD. 
	- Normally HEAD points to a branch name (like bugFix). When you commit, the status of bugFix is altered and this change is visible through HEAD.
	- Detaching HEAD: Detaching HEAD just means attaching it to a commit instead of a branch. This is what it looks like beforehand: `HEAD -> main -> C1`
	- Detaching the head of `bugFix` and attaching it to the commit is achieved by using `git checkout C4`.


	- Way more information about HEAD here https://initialcommit.com/blog/what-is-git-head#:~:text=In%20Git%2C%20a%20head%20is,recent%20commit)%20of%20that%20branch.
	- In Git, a head is a ref that points to the tip (latest commit) of a branch. 
	- You can view your repository’s heads in the path `.git/refs/heads/`. In this path you will find one file for each branch, and the content in each file will be the commit ID of the tip (most recent commit) of that branch.
	- For example, there is literally a file called `master` in that path that contains the commit ID of the tip of the master branch. When you make a new commit on a branch or pull commits from a remote, the head file for that branch is always updated to reflect the commit ID of the tip of the branch. In this way, your branch name ref always stays in sync with the most recent commit at the tip of the branch.
	- So what is the difference between capitalized Git HEAD and lowercase Git head?

> In lowercase, "head" is a general term that means any commit that represents a branch tip. In uppercase, "HEAD" is a specific Git ref that always points to the commit currently checked out in the working directory.

	- Useful to check previous commits and files, example follows

```shell
➜  2023_10_24_learning_GIT git:(master) ✗ git log --oneline                                                                                                                                    [🐍 lewagon]
98a1060 (HEAD -> master, origin/master) add information about HEAD in git
f0a862b rebase schema
0dd7e9d add rebase info
76c6f38 add merge
fbe8939 changed figure
3210636 branching and merging figure
9448885 add a figure
6302aa6 add git branching
378830b first commit
➜  2023_10_24_learning_GIT git:(master) git checkout 378830b                                                                                                                                   [🐍 lewagon]
Note: checking out '378830b'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at 378830b first commit
➜  2023_10_24_learning_GIT git:((378830b...)) ls                                                                                                                                               [🐍 lewagon]
README.md
➜  2023_10_24_learning_GIT git:((378830b...)) nano README.md   
```

> This places Git into a detached HEAD state, which means that HEAD is not currently pointing to a branch head (branch tip). In this state, you can view and edit any files in your working directory, exactly as they were in that commit.

	- Head can also be used to see changes from files
```shell
➜  2023_10_24_learning_GIT git:(master) ✗ git show HEAD                                                                                                                                        [🐍 lewagon]
commit f25e8c9700470762f3e7ad775e87b6f8542eabd6 (HEAD -> master, origin/master)
Author: stephanyvargas <yostephy@hotmail.com>
Date:   Wed Oct 25 12:01:15 2023 +0900

    updated a webpage with more info about HEAD in git

diff --git a/2023_10_24_learning_GIT/README.md b/2023_10_24_learning_GIT/README.md
index 516a595..ec8c024 100644
--- a/2023_10_24_learning_GIT/README.md
+++ b/2023_10_24_learning_GIT/README.md
@@ -79,8 +79,21 @@ git rebase main
 
 #### Moving around in GIT
 
-1. **HEAD** HEAD is the symbolic name for the currently checked out commit -- it's essentially what commit you're working on top of. HEAD always points to the most recent commit which is reflected in the
-
+1. **HEAD** 
+       - HEAD is the symbolic name for the currently checked out commit -- it's essentially what commit you're working on top of. 
+       - HEAD always points to the most recent commit which is reflected in the working tree. 
+       - Most git commands which make changes to the working tree will start by changing HEAD. 
+       - Normally HEAD points to a branch name (like bugFix). When you commit, the status of bugFix is altered and this change is visible through HEAD.
        - Detaching HEAD: Detaching HEAD just means attaching it to a commit instead of a branch. This is what it looks like beforehand: `HEAD -> main -> C1`
        - Detaching the head of `bugFix` and attaching it to the commit is achieved by using `git checkout C4`.
+
+
        - Way more information about HEAD here https://initialcommit.com/blog/what-is-git-head#:~:text=In%20Git%2C%20a%20head%20is,recent%20commit)%20of%20that%20branch.
+       - In Git, a head is a ref that points to the tip (latest commit) of a branch. 
+       - You can view your repository’s heads in the path `.git/refs/heads/`. In this path you will find one file for each branch, and the content in each file will be the commit ID of the tip (most rece
+       - For example, there is literally a file called `master` in that path that contains the commit ID of the tip of the master branch. When you make a new commit on a branch or pull commits from a rem
+       - So what is the difference between capitalized Git HEAD and lowercase Git head?
+
+> In lowercase, "head" is a general term that means any commit that represents a branch tip. In uppercase, "HEAD" is a specific Git ref that always points to the commit currently checked out in the worki
+
+       - Useful to check previous commits and files 
```
