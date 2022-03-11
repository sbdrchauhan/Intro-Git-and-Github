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

![alt text](https://github.com/sbdrchauhan/Intro-Git-and-Github/blob/main/git-flow-digram.PNG)

## Fork
If a developer wants to create a derivative project with another project as the starting point, or work on a project using a separate or independent clone, the developer can choose to **fork** a project. You can fork any public project.

> NOTE: The fork option is only available using the web interface and there is no git command to create fork. You can however use a **git clone** workaround - see below for more.

Once the project has been forked, the developer with access to the fork can work on updating and making changes to the fork using the same workflow as already described previously i.e. the forked copy of the project now becomes the **origin** and developers with access to **origin** can create clones of it on their local machines, where they can create and merge branches, and synch changes with the origin using pull and push.

However it is important to note that the synch of changes using merge and push can only be done with repos that the developers have write access to i.e. in this case their fork of the project i.e. the **origin** from which they create their local clones. But what if a developer wants to contribute their changes back to the **upstream** project that they do not have access to? In this case they can submit **pull request** or PR with their proposed changes. A **pull request** can be opened by going to the project's homepage, navigating to the Pull Requests tab, and then clicking New Pull Request.

> NOTE: the term **Pull Request** should not be confused with the **git pull** command that you use to **fetch** and **merge** the latest codebase into your local repo. A **Pull Request**, as the name implies, is merely a request to review and **pull** your proposed changes. As part of the PR, you provide details of the proposed changes and your implementation.

The maintainers of the **upstream** project can review the changes in the PR and decide to merge them or not. In some cases, they may provide feedback (by commenting in the PR) or ask the submitter of the PR to perform some confict resolution such as applying their changes to the latest codebase and resubmitting the PR.

This **fork->clone->PR** workflow is summarized as follows:

![alt text](https://github.com/sbdrchauhan/Intro-Git-and-Github/blob/main/fork.clone.pr.PNG)

## When to Fork or Clone?
By now you should be familiar with the difference between fork and clone. So let's summarize when you should clone vs. fork. Typically if you have access to a project repo e.g. as part of a team developing a codebase collaboratively, you can clone the repo and synchronize changes from your local copy of the repo using pull and push.

If however there is a public project that you want to contribute to but do not have write access to, or use a public project as a starting point for your own project, you can fork the project. Then work with the forked codebase by cloning it to your machine and collaborating with your development team working on the fork using the pull-push synchronization with your fork of the project. But if you want to contribute your changes back to the upstream project (the original project that you forked from), you can submit your changes using a pull request.

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
  
## Summary
* **clone**
  * A clone is a copy of the project that you can make changes and work on
  * The project from which you clone from is called the **origin**
  * You can **pull** updates from the **origin** and **push** your changes back to it
* **fork**
  * A fork is a separate copy of a project that you can make changes independently of the original project
  * The project that you fork from is referred to as the **upstream** project
  * You can suggest changes back to the upstream project by submitting a **pull request** (PR)
  
> FYI: Although the usual workflow to start with the codebase of another project is to first fork it and then clone the fork, you may be tempted to simply clone the upstream project since it is quite convenient to do so from your local machine using the git clone command. If you do so, you will note that the project you clone from will by default become the origin repo. But since you likely don't have write access to the upstream repo that you cloned from, you will not be able to push your changes to it. Don't worry. You can easily rename the origin to upstream using the command git remote rename origin upstream and then add a new origin using git remote add origin <url> to point to the URL of a new GitHub repo that you have created or have access to, and use that repo for making your changes to the fork's code.
  
  
## Managing GitHub projects

A GitHub developer communicates with other using these commands:
  * **git-clone** from the upstream to prime the local repository
  * **git-pull** and **git-fetch** from "origin" to keep up-to-date with the upstream
  * **git-push** to shared repository
  * **git-format-patch** to prepare e-mail submission
  * **git-send-email** to send your e-mail submission w/o corruption by your MUA
  * **git-request-pull** to create a summary of changes for your upstream to pull
  
## Hands-On Lab: Cloning and Forking GitHub Projects
* The first step is to **fork** any public repository or the project that you want to work on.
* After forking and obtaining the copy of the **upstream**, as one of your own repo (this is your **origin**), clone it using either (https, ssh)

```console
$ export ORIGIN=<your (forked) repo HTTPS URL>    // just for the sake of simplicity
$ echo $ORIGIN    // to see if the origin variable has the correct https link
$ git clone $ORIGIN   // clone the repo
$ ls    // to see that you got the dir of the repo (given you are in your desired place to clone the repo)
```
  
