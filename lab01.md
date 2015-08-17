# Lab 1

In this lab you will do the following:
* Install Git
* Configure Git
* Learn the basic command line usage for Git

## Prerequisites
For this lab you will need:
* A computer with terminal access
* A willingness to dive in and try stuff

## Tasks

### Install Git

#### Determine if Git is installed
First, determine if you have Git installed.  Issue the following command at a terminal prompt:

```console
$ git --version
```

You can skip the install step and continue to the [Configure Git](#configure-git) section if you get a response like the following:

`git version 2.5.0`
> Note: The version identifier returned by your system will be system-dependent.  Any version of `git` is acceptable to accomplish this lab, and you do not need a specific version.

#### Installing Git

Make sure you have the Git command line binaries installed on your machine.  Find on your flavor of Linux below and issue the proper commands.

If you need more detailed instructions, or your OS isn't listed here, have a look at http://git-scm.com/download

#### Install on Ubuntu
```console
$ sudo apt-get -y install git
```

#### Install on CentOS
```console
$ sudo yum -y install git
```

### Configure Git
Git requires that a few config items are set in order for us to use it.  It needs to know who you are so it can tack that information onto all your work.

#### Set your email address
Git requires that you set an email address in order to commit your work.  It won't verify that it is a correct email address, nor will it verify that it is your email address.  This information will be sent with your repo to anyone who collaborates with you on this repository.

```console
$ git config --global user.email "joe.racker@rackspace.com"
```
#### Set your real name
Like your email address, Git wants to know your real name.  You can put whatever you want in here, but if you collaborate with others it is useful to have your real name.

```console
$ git config --global user.name "Joe Racker"
```

### Create your first Repository
The first step in working with Git and having it keep track of your changes is to create a repository.  The repository is where Git stores all its information about the history and working contents of your directory.
> Note: we will learn later about collaborating with others and will learn how to grab their repository rather than creating your own.

Create a directory for your repository and change to that directory:

```console
$ mkdir my_first_repo
$ cd my_first_repo
```

Create and initialize the Git repository in your new directory:
```console
$ git init .
Initialized empty Git repository in my_first_repo/.git
```

Now you have a repository ready to accept all your changes and keep track of your work.  You will notice that there is a `.git` directory in the current directory.  This is where Git stores all of its brains with respect to this repository.

### Add a file to the repository
First, let's create a file to add to our repository:
```console
$ echo "Hello World" > hello_world.txt
```

Now, add it to the repository (stage those changes):
```console
$ git add hello_world.txt
```

Finally, we commit the addition of the file:
```console
$ git commit -m "Added a very informative first file"
[master (root-commit) 5df0615] Added a very informative first file
 1 file changed, 1 insertion(+)
 create mode 100644 hello_world.txt
```

### Take a look at the history of the repository
Now that we have some history in Git, let's take a look:
```console
$ git log
commit 5df0615895e593a7c2b29f0dd802ca053fb72993
Author: Joe Racker <Joe.Racker@rackspace.com>
Date:   Thu Aug 13 11:47:00 2015 -0500

    Added a very informative first file
```

### Check the status of things
Since Git is managing the state of our directory for us we can ask it for a status at any time.
```console
$ git status
On branch master
nothing to commit, working directory clean
```

Let's add a file and see what Git tells us about the status.
```console
$ echo "Goodbye world" > goodbye_world.txt
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	goodbye_world.txt

nothing added to commit but untracked files present (use "git add" to track)
```

Add our new file and check the status.
```console
$ git add goodbye_world
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   goodbye_world.txt
```

Now commit the file and check status.
```console
$ git commit -m "added a morbid file"
[master 38ef982] added a morbid file
 1 file changed, 1 insertion(+)
 create mode 100644 goodbye_world.txt

$ git status
On branch master
nothing to commit, working directory clean
```
Life is back to normal again!

### Change an existing file
Let's say we want to change the contents of an existing file in our repository.  Change the contents of the `hello_world.txt` file.
```console
$ echo "Changed my mind" > hello_world.txt
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   hello_world.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Add those changes to our staged changes and commit.
```console
$ git add hello_world.txt
$ git commit -m "more insight to the world added"
[master 62e75d3] more insight to the world added
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### Look at a useful history
Now that we've done some things in our repository let's look at a more interesting log of history.
```console
$ git log
commit 62e75d3a7e0a253a7ad71aa2e1581be04ae226a3
Author: Joe Racker <Joe.Racker@rackspace.com>
Date:   Thu Aug 13 13:03:23 2015 -0500

    more insight to the world added

commit 38ef98238b4f35d85d1ea6a7333437723b21c7d0
Author: Joe Racker <Joe.Racker@rackspace.com>
Date:   Thu Aug 13 12:56:10 2015 -0500

    added a morbid file

commit 5df0615895e593a7c2b29f0dd802ca053fb72993
Author: Joe Racker <Joe.Racker@rackspace.com>
Date:   Thu Aug 13 11:47:00 2015 -0500

    Added a very informative first file
```

### Check out the differences
It is useful to be able to see what you've changed in a repository in order to select the proper changes for staging and committing.  Create a new file called `new_file`, stage `new_file`, commit the initial file.  Add another line to the file and ask Git for the differences.
```console
$ echo "see me in the diff" > new_file
$ git add new_file
$ git commit -m "added new file for diffing"
$ echo "new line" >> new_file
$ git diff .
```
```diff
diff --git a/new_file b/new_file
index bf3322c..a31eb3c 100644
--- a/new_file
+++ b/new_file
@@ -1 +1,2 @@
 see me in the diff
+new line
```

## Conclusions
In this lab you created your own repository, added files, changed files, looked at history, checked status, and committed changes using Git.  Feel free to try all those commands in other different ways and experiment in your new repository.
