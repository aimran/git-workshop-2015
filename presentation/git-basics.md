#Git Basics
**Asif Imran** January 27, 2015

## Three Essential Concepts
- Repository
- Commit
- Branch

We will cover all of them today! It was written by
the ultimate command-line nerd, Linus! Git is best served/used
from CLI. However, there exists a few GUI for git (including
[GitHub for Mac](https://mac.github.com/) and
[GitHub for Windows](https://windows.github.com/)).

We will do most of our work today from the command
line.

## Getting setup: `git config`
Your contributions via git is *loosely* tracked via
you Name and Email address. This becomes important/essential
when you start to collaborate with others.

Do the following:

    $ git config --global user.name "YOUR NAME"
    $ git config --global user.email "YOUR EMAIL"

I also like to setup some helpful aliases
for routine work:

    $ git config --global core.editor /usr/bin/vim
    $ git config --global color.ui always
    $ git config --global alias.df 'diff --color --color-words --abbrev'
    $ git config --global alias.lg 'log --color --graph --pretty --abbrev-commit'

There is no magic here. All we are doing is editing the
global config file, stored at `~/.gitconfig`.
Feel free to poke around later.

## Create a local repository: `git init`
A git repository is any regular directory with a special `.git` directory
sitting at the top of the directory structure. It contains all
the required repository file, index etc.

You have to do `git init` only once per repo

###:vertical_traffic_light: Ex 1: Create a local repository

    $ cd scratch
    $ git init jira-45
    Initialized empty Git repository in scratch/jira-45/.git/

Verify that there is a `.git` folder inside the newly-created repo

    $ cd jira-45
    $ ls -a
    $ cd .git
    $ ls

###:vertical_traffic_light: Ex 1a: (optional) Create a repository from existing directory

    $ cd scratch
    $ mkdir old_work
    $ cd old_work
    $ git init
    Initialized empty Git repository in scratch/old_work/.git/

## Git workflow:
You will find your typical git-related workflow to be similar to:
- Create new file
- Put new file under version control
- Make modifications
- Check your changes with `git status`, `git diff`, and `git log`
- Stage you changes to be saved with `git add`
- Commit or take a snapshot of the current version `git commit`

###:vertical_traffic_light: Ex 2: Add File to your repository

    $ cd scratch/jira-45
    $ vi README
    $ git status
    On branch master

    Initial commit

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

      README

    nothing added to commit but untracked files present (use "git add" to track)

Git has detected a new file. We need to tell Git to start tracking it

    $ git add README
    $ git status
    On branch master

    Initial commit

    Changes to be committed:
      (use "git rm --cached <file>..." to unstage)

    new file:   README

## Commit your changes: `git commit`

In order to take a snapshot of the current state of the repo,
we use the `commit` command. Committing changes to your
repository involves two steps:
 - indicating the changes to be committed with `git add`
 (known as "staging the changes", which we have just done), and
 - then actually *committing* those changes with `git commit`.

If you type just `git commit`, an editor will open for you to add a
comment describing the changes. Alternatively, use can use the `-m`
flag followed by the comment in quotes.

Its a good idea to keep your commits *atomic*! This loosely implies
that changes within a commit are related and serve a single purpose.

Commits can be thought of as the check points for the undo button.
So, how it is totally up to you as to how often you want to commit.
If you want to save an hour worth of work, you should commit once an
hour.

Always, write a succint but descriptive commit message. Make
it a habit to always write a one line commit message that is
meaningful. *Just* writing "Typo" is rather aggravating.

###:vertical_traffic_light: Ex 3: Commit File

    $ git commit -m "This is my initial commit"

*Note*: You *have* to tell which changes to stage for a commit. There is
a short cut to tell Git to add every changed file (that is also)
tracked to be staged.

    $ git add .

## The many ways to `diff`
Git provides various ways to examine your work for changes.
Here are the 3 that I find the most useful:

    $ git diff #show diff between staged work and working dir
    $ git diff HEAD #shows diff between HEAD and working dir
    $ git diff --cached #diff between staged dir and HEAD

###:vertical_traffic_light: Ex 4: Practice diff
- Edit README (try all 3 diffs)
- Stage your work (diff again)

## Viewing the history: `git log`

A log of the commit messages is kept by the repository and can be
reviewed with the log command.

    $ git log
    commit 663118b3e9b3cadbaadf0a59a50496deb1f90458
    Author: Asif Imran <asif.imran@adroll.com>
    Date:   Tue Jan 27 23:10:40 2015 -0800

        Initial commit

## Oh shit moments:

###1: Unstage file that you unintentionally staged
    $ git reset filename
###2: Revert back to *just working now* files
    $ git checkout -- filename


## Experiment with Git: `git branch`
Unlike most other VCS tools out there, it is amazingly easy to setup branches
on Git. You no longer need special permissions to commit your branches.

At the heart of it all, Git branches are commits with tags. This in turn allows
you to navigate easily between your named/tagged commits.

Branches are an awesome way to start and test out new features, attend
bug-fixes. Git tries to keep your experimental work organized and separate. Since
branches are merely labels on commits, they are cheap to create.

The common saying is:
> Branch early and branch often

###:vertical_traffic_light: Ex 4: Create a branch

First make sure that your current branch is clean. Otherwise, bad stuff can happen.

    $ git branch #this will list your branches. Asterisk denotes the active branch
    $ git branch feature  #Where feature is the name of the branch
    $ git branch  #Notice a new entry

You can move between branches using `git checkout`

    $ git checkout feature #You are now in the feature branch
    $ git branch #confirm that you are


###:vertical_traffic_light: Ex 4: Make modifications to new branch

    $ vi README
    $ vi newFile.txt # create a new file
    $ ...            # stage the file(s) and commit
    $ git status     # always check your status
    $                # git


## Merging branches: `git merge`

If you are satisfied with your experimental work on a particular branch, you may
want to merge this work with your master branch or some other branch.
[The master branch typically denotes the production version of your work.
You should try your best not to break you master branch.]

###:vertical_traffic_light: Ex 4a: Create a second branch and merge

    $ git branch experiment
    $ git checkout experiment

- Make changes to the new branch and commit them! Very important to commit your
work.

- Move to the branch where you want the new commits to appear. Say we want to move
our work in the 'experiment' branch to 'feature'.


    $ git checkout feature
    $ git merge experiment

    Updating 663118b..9c194b1
    Fast-forward
    newFile.txt | 1 +
    1 file changed, 1 insertion(+)
    create mode 100644 newFile.txt

## Resolving conflicts:
Now that you are simultaneously working on multiple branch, its highly likely that
some of your edits are conflicting. Git still lacks the `git read-mind` command!

Therefore, you have to be prepared to resolve merge conflicts.

###:vertical_traffic_light: Ex 5: Create conflicting edits to same file

    $ git checkout experiment
    $ vi README  #make changes on the first line, do the stage and commit dance
    $ git commit -am "change first line to be sad"

    $ git checkout feature
    $ vi README
    $ git commit -am "change first line to be happy"

    $ git merge experiment
    Auto-merging newFile.txt
    CONFLICT (content): Merge conflict in newFile.txt
    Automatic merge failed; fix conflicts and then commit the result.


Git stops during a conflict and edits the conflicting files like this:

    =====================
    <<<<<<< HEAD
    Happy
    =======
    Sad
    >>>>>>> experiment
    =====================

Edit the file to keep the Happy commit

    $ vi README
    $ git add README
    $ git commit -m "keep the happy line"

This completes the merge process
