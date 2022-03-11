# Intro-Git-and-Github
## List of references:
1. [Getting Started with Git and GitHub](https://www.coursera.org/learn/getting-started-with-git-and-github)

The version control system helps to keep track of the changes made in your documents or the projects. So, it becomes easier for you to recover the older version of your work, if you make a mistake in the newer version of the documents. This also makes the Collaboration with others much easier.

Go to this [github website](https://docs.github.com/en/get-started/quickstart/set-up-git), and follow the steps to connect your local git to your github account using the SSH protocal. Using SSH to clone the repo is easier and doesn't require password in the future to make any changes and push it to remote (which saves lots of time and pain). It requires giving the private key to the SSH-agent. Please carefully setup your account!

## SHORT Glossary of Terms
- **SSH protocal** -> A method for secure remote login from one computer to another
- **Repository** -> The folders of your project that are set up for version control
- **Fork** -> A copy of a repository
- **Pull request** -> The process you use to request that someone reviews and approves your changes before they become final
- **Working directory** -> A directory on your file system, including its files and subdirectories, that is associated with a git repository 

## Basic Git Commands
When starting out initially, you either start making directory locally and pushing it to Github or cloning the existing repository (done only once).
- **git init** -> starts the current working directory ready as github repo
- **git add** -> moves the changes from the working directory to the staging area
- **git status** -> helps to see the state of the working directory and or any changes in your staging area
- **git commit** -> takes the changes of staging and commits into the project
- **git reset** -> undoes the changes to the files in working directory
- **git log** -> helps to browse and see the previous changes to the files in the project
- **git branch** -> creates an isolated area within the repo to make new changes to the project
- **git checkout** -> lets you see and make changes to the existing branches or switch to different branches
- **git merge** -> lets you put everything back together again (merge the branches)
- **git revert** -> revert changes

## Github Branches
All codes and files created in git repo is in the branches, Master branch is by the default, and this master branch is deployable to create other branches to create and make changes to the codes.

## What is a Pull Request?
- A pull request makes the proposed (commited) changes available for others to review and use
- A pull can follow any commits, even if code is unfinished
- Pull requests can target specific users
- Github automatically makes a pull request if you make a change on a branch you do not own
- Log file record the approval of the merge

The master branch should be the only deployed code. Every other branches that has changes to the files should be merged to this master branch!

## Hands-on Lab: Getting started with branches using git commands on a local repository
```console
$ mkdir myrepo        // make directory for our local repository
$ cd myrepo
$ git init            // create a new local repository; creates .git file (which houses the local repo.)
$ ls -al              // to see (verify) .git file
$ touch newfile       // create new file
$ git add newfile     // add this file to local git repo.
$ git status          // see if stage is ready to commit
$ git commit -m "added newfile"   // saving the changes locally
$ git branch my1stbranch      // make new branch now to make other changes to master one
$ git branch        // to see in which branch you are; the asterisk * means that you are active in this branch
$ git checkout my1stbranch    // to change into this new branch
$ git branch    // verify, indeed that is the case; notice * is now on this branch
$ git checkout -b my1stbranch   // the shortcut you could have used to do above two steps
$ echo "make changes to the newfile" >> newfile   // adds this line to the file (in new branch)
$ cat newfile   // verify if the file is written
$ touch readme.md   // create anothe new file
$ git add readme.md   // add readme.md file to the repo. stage
$ git status      // verify that in our new branch we have edited newfile and added readme.md file
$ git add newfile   // add this file also to the staging area, after modification
$ git add *     // period or asterisk adds all the changes into the staging area, ready to be committed
$ git commit -m "added readme.md modified newfile"
$ git log   // to get a history of recent commits (shows commits history of all branches including master)
$ git revert HEAD --no-edit   // you might want to revert back, you can also use id of the commit
$ touch goodfile
$ git add goodfile
$ git commit -m "added goodfile"
$ git log
$ git checkout master   // before we merge the my1stbranch changes into the master, we need to move to master first
$ git merge my1stbranch   // merge the branch
$ git log   // you will see (HEAD-> master, my1stbranch) to confirm your action
$ git branch -d my1stbranch   // now that changes have been merged into the master, delete this branch
$ git branch  // to see now you only have *master
```

Let's say we have one master repository in GitHub.com; from there multiple developers **fork** and make there own copy of the repository in each of their's github.com. This own version of repo in github.com is called **local repo**. Finally, each developer can now **clone** to their own version of repo from their own github.com repo.The master repo is the **remote repo**.

**Clone**

Let's say a new developer now joins the team to collaborate on the project. This developer can create a identical copy of the **remote repo** using the **git clone** operation. The remote repo from which the project is originally cloned from is also referred to as the **origin**.

## Creating Branches and Sync Changes
After cloning the repo to the local machine, a developer can start making changes to the codebase.This could be for tasks like adding features and enhancements or fixing bugs. Normally, developer are asked to use **git branch** to create a branch e.g. *feature1-branch*, make that branch active using **git checkout** and make necessary changes within that branch - such as adding or editing files. The developer saves their changes often within the branch by using **git add** followed by **git commit**. Once all the code changes and developments are complete or looks okay, rather than merging to the main branch directly, it is often a good practice to **push** the new branch with changes to **origin** where other developers/reviewers can test/review the changes before merging the branch to main.

> NOTE: Since in this scenario the *feature1-branch* was developed by a new developer on the project, that developer may not have the access to merge their branch with main in **origin**. In fact, in many projects, only the project maintainers or admins are allowed to merge to the main branch, or in some sames a peer review may be required. In order to request that your changes be reviewed and merged with the main branch, many projects require that a **Pull Request (PR)** be submitted. Whereas, in some cases, e.g. if you are a lone developer on the project, this PR step may be omitted and you could merge and push your changes directly if you have write access to the origin repo.

Every once in a while, a developer may want to get the latest copy of the repo from **origin** to serve as the base for making changes or reviewing changes by others. For example, this may be the case after the changes in *feature1-branch* have been pushed to **origin** and the peer developer wants to review the code. The **git fetch** command can be used for this purpose. The **git diff** command can help others reviewing your code to identify and compare the changes. Once a peer reviewer or project maintainer has reviewed the changes, and is satisfied, the reviewer will **git checkout** the main branch and then **git merge** the new *feature1-branch*, which can then be deleted. After the branch is merged locally, the reviewer can **git push** the updated main branch back to **origin**.

> NOTE: **git-remote -v** command can be used to check which remote repos you are synchronizing push and fetch changes with.

Another option for getting the latest copy of the repo is to use the **git pull** command. The **pull** command in effect is a combination of **fetch** and **merge**. That is, using this single command, you can both fetch and merge the changes into your local repo. For example, another developer who wants to use the updated codebase with the *feature1* changes that have been merged to main branch in origin, can use the **git pull** command to **fetch** the updated codebase from the origin and **merge** with his/her local codebase before starting development on a new feature.

This **clone->branch->merge** workflow is how things are done Please see the flow diagram of this task in below:



## Cloning and Forking Github Projects
Cloning creates a copy of a repository on your local machine (via terminal). Forking modifies or extends a project (via github) without affecting the original project. Frequently, this is done to start out for your project from already developed codes (or projects) and building from there!

**Forking** - takes a copy of a GitHub project/repository and use it as the base for a new project. You can also submit changes back to the original repository. Independently make changes to a project and when you are satisfied; you can submit a **pull request** to the original owner. Then, it remains on the owner's right whether to change the original files or not.

You can clone the repository from the github to your local machine using https option (SSH is better) `git clone https:://web.url/to/github/repo`.

To sync changes from local to GitHub:
- git add <files>  // takes changed files to the staging area
- git commit -m "message"
- git push // to push all changes to remote repo
  
Use `git push` to push any changes from local repo to remote repo; and `git fetch` to sync changes from remote repo to your local repo. This action doesn't make any changes to the branch you are working on (you can manually merge changes to the branch). Some terminology people use-> **origin** generally refers to the repo of our local fork; and **upstream** refers to the original work.
  
## Forking a Project
* Forking
  * Takes a copy of GitHub repository to use it as the base for a new project
  * Submit changes back to the original repository
* Independently make changes to a project
  * Submit a **pull** request to the orginial project owner
  * Owner decides whether to accept updates
  
## Steps in Forking a Project
* Navigate to the repository that you want to fork
* Top right corner, click **Fork**

## Syncing a Fork of a Project
To keep a fork in sync with the original work from a local clone:
* Create a local clone of the project
* Configure Git to sync your fork
  * Open the Terminal and change to the directory containing the clone
  * To access the remote repository, type **git remote -v**
  * Type **git remote add upstream** \<clone directory\>
  * To see the change, type **git remote -v**
  
## Commands for Managing Forks
* To grab upstream branches
  * **git fetch upstream**  // to grab upstream branches
* To merge changes into the master branch
  * **git merge upstream/master**   // merges changes to the master branch
  
  
  
  
  
  
