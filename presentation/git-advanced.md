#Git Advanced Topics
**Asif Imran** January 27, 2015

## Topics
- Clone
- Push and Pull
- Fork

##Following exercises are best done in pairs.

## Cloning a repo: `git clone`
A wonderful and vital feature of git whereby you can create an exact replica of
a git-controlled repo.

All you need is a git URL. The flavors are:

  - git: `git://host/xz[:port]/path/to/repo.git`

  e.g. git@github.com:aimran/iptools.git

  - ssh: ssh://[user@]host.xz[:port]/path/to/repo.git

  e.g., ssh://rserver.internal.adroll.com:/path/to/repo.git

  - http: `http[s]://host.xz[:port]/path/to/repo.hit`

  e.g., https://github.com/aimran/iptools.git

  - file: file:///full/path/to/reponame

We will stick to the first two.

## Github.com
A popular collaborative platform that provides a centralized
version control hub built on top of Git. It provides an easy interface for
browsing, collaborating on and storing your code. There are other sites that
provide similar experiences like [bitbucket](https://bitbucket.org),
[googlecode](http://code.google.com) etc. Much of the open source libraries are
hosted on Github.

<a id='ex1'></a>
###:vertical_traffic_light: Ex 1: Create a brand new repo on Github

Create a brand new repo on Github. Add a README file.


<a id='ex2'></a>
###:vertical_traffic_light: Ex 2: Clone your partner's  repo
Clone your partner's repo that she just created.

    $ git clone git@github.com:your-partner/putput.git

## Forking a Repository: `git remote`

Forking means creating a copy of an existing repository [super easy if repos
are hosted on Github]. Afterwards, you can commit changes to *your* repo and
even submit pull requests to have your changes committed to the original
repository.

In order to get started, you will need to add the original (online) repository
as a remote repository. This allows you to fetch updates and push out new commits.

The **git remote** command allows you to add, name, rename, list, and
delete repositories such as the original one **upstream** from your
fork, others that may be **parallel** to your fork, and so on.

<a id='ex3'></a>
###:vertical_traffic_light: Ex 3: Fork you partner's GitHub Repository
Step 1: You will make a copy "fork" of the repository github.  Now you
have a copy of the repo that you are free to do whatever you
want with it :neckbeard:

Step 2: Make a clone of your fork on your local machine

    $ git clone git@github.com:yourname/putput.git
    $ git remote -v # list the current remotes. All cloned repos have a remote branch called origin


Step 3: Add the "source" repo as an upstream branch

    $ git remote add upstream git@github.com:your-partner/putput.git

There is no magic here. All you are doing is giving an alias or shorthand to
the remote locations so that you can refer to them later for pulling in updates
or pushing out your own changes.

##Pushing out updates to personal repo: `git push`

Once you have made your commits that you would like to share with your team (or
the world!), you will *push* out your updates to the remote repo. However, keep
in mind that you may OR may *not* have permissions to push to the remote repo.

By default, on Github you have push access to all your own repos.

###:vertical_traffic_light: Ex 4: Makes changes to your personal repo and push out

Here you will make small changes to the repo you created in [Ex 1](#ex1)

    $ vi README
    $ git commit -am "commit for the world"
    $ git push origin master  #note how you specify the remote (origin) and branch name (master)


## Fetch contents from a remote repo: `git fetch`

Once you have defined your remotes (original and upstream in this case), you can
pull in updates from those repositories so that they are in sync (aka tracking!).

Note that the fetch command simply pulls down information/new changes but does
not alter your working directory. If you wish to update your local branch, the
fetch command has to be folllowed with a merge.


###:vertical_traffic_light: Ex 3: Fetch updates and merge into your master

Move to the directory containing the clone of your partners repo from [Ex 2](#ex2).

    $ git checkout master

    $ git fetch upstream
    $ git merge upstream/master

There is a short cut for the above using `git pull` which will combine the fetch
and pull move into one. I typically dont do it since I like to be able to compare
what has changed.

    $ git fetch upstream
    $ git diff master upstream/master

You still may have to worry about merge conflicts.


## Pushing out updates to team repo: Pull requests

We will make use of Github to push out updates to team. Subsequently, you will
make changes to your local fork of your partners repo from [Ex 3](#ex3)

Here is nice link from Github showing you how it is done:

https://help.github.com/articles/using-pull-requests/#reviewing-the-pull-request


##Further resources:
[1] https://help.github.com  (Really good with lots of screen shots)
[2] http://git-scm.com/book/en/v2/Getting-Started-Git-Basics (the bible)
[3] http://onlywei.github.io/explain-git-with-d3/ (Visual learners)  
