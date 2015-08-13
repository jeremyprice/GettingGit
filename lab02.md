# Lab 2

In this lab you will do the following:
* Investigate branching and merging in Git

## Prerequisites
For this lab you will need:
* A computer with terminal access and Git installed
* Basic knowledge of the Git command line [See Lab 1](lab01.md)
* A willingness to dive in and try stuff

## Tasks

### Create and initialize a repository
Create a new directory named `lab02` to work in and initialize a repository there.  Add a file called `README` and commit it to the repository.

> [See Lab 1](lab01.md) if you need a refresher on the steps

```console
$ mkdir lab02 && cd lab02
$ git init .
$ touch README
$ git add README
$ git commit -m "initial repo creation and README addition"
```

### Work with branches
#### Create a branch
Make a branch in your new repo called `fancy_branch`.
```console
$ git branch fancy_branch
```

Notice that nothing much happened (Git was pretty quiet, right?).  Git created the branch, but didn't move you to that branch.  Your repo is still sitting on the `master` branch.  You can verify this by issuing a `git status` command and looking at the `On branch` output.

#### Change branches
Let's change to the `fancy_branch` so we can make some changes.
```console
$ git checkout fancy_branch
Switched to branch 'fancy_branch'
```
>Note: if you want to know what branch you are on at any time you can issue the `git status` command and it will tell you.

#### Make some changes
Let's make some changes to the files in `fancy_branch` and see how it affects the repository.  Change the contents of the existing `README` file and create a new file called `useful_info.txt` with some good info in it.
```console
$ echo "This file is redundant" >> README
$ echo "really critical information" > useful_info.txt
```

Stage the changes from both files and commit those to the repository.
```console
$ git add README useful_info.txt
$ git commit -m "committed multiple things in one pass - now with more useful information"
```

At this point your `git status` should return cleanly:
```console
$ git status
On branch fancy_branch
nothing to commit, working directory clean
```

#### Investigate differences
Look at the differences between your branch `fancy_branch` and the `master` branch.
```console
$ git diff master
```
```diff
diff --git a/README b/README
index e69de29..78784bd 100644
--- a/README
+++ b/README
@@ -0,0 +1 @@
+This file is redundant
diff --git a/useful_info.txt b/useful_info.txt
new file mode 100644
index 0000000..524d6b6
--- /dev/null
+++ b/useful_info.txt
@@ -0,0 +1 @@
+really critical information
```

Visualize the history.
```console
$ git log --graph
```

#### Merge branches
Since our diff looks good it is time for us to merge our `fancy_branch` branch into `master`.
```console
$ git checkout master
$ git merge fancy_branch
Updating 271e70d..835d39e
Fast-forward
 README          | 1 +
 useful_info.txt | 1 +
 2 files changed, 2 insertions(+)
 create mode 100644 useful_info.txt
```

If we are all done with our `fancy_branch` we can delete it.
```console
$ git branch -d fancy_branch
Deleted branch fancy_branch (was 835d39e).
```

### Work with conflicts
We are going to create some artificial conflicts in our repository so you can see how to  work through a conflict scenario.

Create a branch called `conflict` and make it the active branch (using the shortcut method).
```console
$ git checkout -b conflict
```

Make a change to the README file so that the contents are a the single line.  Stage and commit those changes.
```console
$ echo "These are some changes that will conflict.  Conflict is bad." > README
$ git add README
$ git commit -m "incoming conflicts"
[conflict 877d7d1] incoming conflicts
 1 file changed, 1 insertion(+), 1 deletion(-)
```

Switch to the `master` branch and change the README file so the contents are single line.  Stage and commit those changes.
```console
$ git checkout master
Switched to branch 'master'
$ echo "Seemingly mundane change." > README
$ git add README
$ git commit -m "master changes to README"
[master 30d0315] master changes to README
 1 file changed, 1 insertion(+), 1 deletion(-)
```

Our repository now has changes on the `conflict` branch that are different from, and in direct conflict with, the changes in the `master` branch.  Let's try to merge the changes from `conflict` into `master`.
```console
$ git merge conflict
Auto-merging README
CONFLICT (content): Merge conflict in README
Automatic merge failed; fix conflicts and then commit the result.
```

Git gave up on us.  It found the changes were in conflict and said, "It's your problem now buddy".  If you look at the README file you will see the conflicting changes inline with each other.
```diff
<<<<<<< HEAD
Seemingly mundane change.
=======
These are some changes that will conflict.  Conflict is bad.
>>>>>>> conflict
```

`HEAD` refers to the latest commit in `master` since it is the branch we are merging into.  The lines between `<<<<<<< HEAD` and `=======` represent the change from `master`.  The lines between `=======` and `>>>>>>> conflict` represent the changes from the `conflict` branch. You now have to choose the lines you want to keep, so edit the file to represent the text you want (remove all the lines inserted by Git to show you the conflict).  After editing, the file should contain a single line:
```
Seemingly mundane change.
```

Stage the properly merged file and commit the resolved conflict.
```console
$ git add README
$ git commit -m "resolved those nasty conflicts"
[master 24d9480] resolved those nasty conflicts
```


Now take a look at the history to see how it was affected by our conflict fun:
```console
*   commit 24d94801173d5455d605279a6757e5895e360638
|\  Merge: 30d0315 877d7d1
| | Author: Joe Racker <Joe.Racker@rackspace.com>
| | Date:   Thu Aug 13 16:55:52 2015 -0500
| |
| |     resolved those nasty conflicts
| |
| * commit 877d7d17faaf4c0269457ba3d2736a0e2ee53597
| | Author: Joe Racker <Joe.Racker@rackspace.com>
| | Date:   Thu Aug 13 16:42:09 2015 -0500
| |
| |     incoming conflicts
| |
* | commit 30d0315b541b54e7ea413dcb7780857127890f91
|/  Author: Joe Racker <Joe.Racker@rackspace.com>
|   Date:   Thu Aug 13 16:45:07 2015 -0500
|
|       master changes to README
|  
* commit 835d39ee0e416c991637b513a7d7c474805ba7e9
| Author: Joe Racker <Joe.Racker@rackspace.com>
| Date:   Thu Aug 13 16:25:54 2015 -0500
|
|     committed multiple things in one pass - now with more useful info
|  
* commit 271e70daa34a7fa91deb4765d42aa8be455d62fc
  Author: Joe Racker <Joe.Racker@rackspace.com>
  Date:   Thu Aug 13 16:24:33 2015 -0500

      added a readme
```

## Conclusions
In this lab you experimented with branching, merging, and resolving conflicts.  Feel free to try all those commands in other different ways and experiment in your new repository.
