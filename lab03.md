# Lab 3

In this lab you will do the following:
* Interact with GitHub

## Prerequisites
For this lab you will need:
* A computer with terminal access and Git installed
* Basic knowledge of the Git command line [See Lab 1](lab01.md)
* Basic knowledge of branching and merging in Git [See Lab 2](lab02.md)
* A willingness to dive in and try stuff!

## Tasks

### Create an account on GitHub
If you don't have an account on GitHub, go [here](https://github.com/join) to create one.

Once you have an account on GitHub let me know your account username so I can add you to the collaborator list.  You can send it to me via Slack or tell me in class.

### Clone an existing repository from GitHub
Clone the class scratchpad repository from GitHub. In the command below replace "class" with your cohort name.
```console
$ git clone https://github.com/gocodeup/class_scratchpad
Cloning into 'class_scratchpad'...
remote: Counting objects: 184, done.
remote: Compressing objects: 100% (163/163), done.
remote: Total 184 (delta 36), reused 145 (delta 17), pack-reused 0
Receiving objects: 100% (184/184), 3.97 MiB | 3.25 MiB/s, done.
Resolving deltas: 100% (36/36), done.
Checking connectivity... done.
```
> Note: Git created a directory to match the name of the repository you cloned and put the repository in there.

### Branch, edit, and push
Create a new branch to make some changes (make up your own branch name).  Make some changes in your branch, stage and commit those changes on your branch.  Push those changes up to GitHub.
```console
$ cd class_scratchpad
$ git checkout -b {my_cool_branchname}
... make some changes ...
$ git add {all_the_changes}
$ git commit -m "description of the changes"
... make sure you add and commit some changes to your branch, otherwise there will be nothing to push to GitHub ...
$ git push origin {my_cool_branchname}
```
Now that your changes are up on GitHub, file a Pull Request based on your new branch.  Go to the scratchpad repo to file your Pull Request.  While you are there be sure to comment on the Pull Requests from your fellow classmates.

> Note: For more info on Pull Requests go to the [GitHub help page](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests)
## Conclusions
In this lab you experimented with collaborating with others in GitHub.  Feel free to try all those commands in other different ways and experiment in your new repository.
