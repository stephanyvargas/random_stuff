# Learning GIT 

## Learning GIT BRANCHING

Use this url of git branching https://learngitbranching.js.org/ to learn git online. 
I am keeping track of the lessons and some side material here =).

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

<img src="git_merge_fig.png" width="200" height="200" />
