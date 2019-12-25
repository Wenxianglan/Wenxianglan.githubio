---
layout: post
title:  "An Intro to Git and GitHub for Beginners"
date:   2019-12-25
author: Wen Xianglan
categories: Dummy
---

 

# Product

·         [Home](https://product.hubspot.com/)

·         [Jobs](https://www.hubspot.com/jobs/departments/product-and-engineering)

·         [Blog](https://product.hubspot.com/blog)

·         [Open Source](http://github.hubspot.com/?__hstc=90302427.97218259c08d7f8fb8677b6ba30fa505.1567409182088.1567409182088.1567409182088.1&__hssc=90302427.1.1567409182089&__hsfp=1189399445)

# [HubSpot Product and Engineering Blog](https://product.hubspot.com/blog) 

# An Intro to Git and GitHub for Beginners (Tutorial)

Oct 1, 2015 / by [Meghan Nelson](https://product.hubspot.com/blog/author/meghan-nelson) 

·          

·         Share 

·          

In August, we hosted a [Women Who Code meetup](http://www.meetup.com/Women-Who-Code-Boston/events/224072838/) at HubSpot and led a workshop for beginners on using git and GitHub. I first walked through a [slide presentation](https://www.slideshare.net/HubSpot/git-101-git-and-github-for-beginners) on the basics and background of git and then we broke out into groups to run through a tutorial I created to simulate working on a large, collaborative project. We got feedback after the event that it was a helpful, hands-on introduction. So if you're new to git, too, follow the steps below to get comfortable making changes to the code base, opening up a pull request (PR), and merging code into the master branch. Any important git and GitHub terms are in bold with links to the official git reference materials. 

 

### Step 0: Install git and create a GitHub account 

The first two things you'll want to do are install git and create a free GitHub account.

Follow the instructions [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) to install git (if it's not already installed). Note that for this tutorial we will be using git on the command line only. While there are some great git GUIs (graphical user interfaces), I think it's easier to learn git using git-specific commands first and then to try out a git GUI once you're more comfortable with the command. 

Once you've done that, create a GitHub account [here](https://github.com/join).  (Accounts are free for public repositories, but there's a charge for private repositories.)

 

### Step 1: Create a local git repository 

When creating a new project on your local machine using git, you'll first create a new [repository](https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository) (or often, '**repo**', for short). 

To use git we'll be using the terminal. If you don't have much experience with the terminal and basic commands, check out [this tutorial](http://mac.appstorm.net/how-to/utilities-how-to/how-to-use-terminal-the-basics/) (especially the 'Navigating the Filesystem' and 'Moving Around' sections).

To begin, open up a terminal and move to where you want to place the project on your local machine using the `cd` (change directory) command. For example, if you have a 'projects' folder on your desktop, you'd do something like:

```
mnelson:Desktop mnelson$ cd ~/Desktop
```

```
mnelson:Desktop mnelson$ mkdir myproject
```

```
mnelson:Desktop mnelson$ cd myproject/
```

[view raw](https://gist.github.com/cubeton/67a84eb876984f0b5785/raw/d4560016d742865c1fd68d97fcff1feb557d5e19/terminalcd.md) [terminalcd.md](https://gist.github.com/cubeton/67a84eb876984f0b5785#file-terminalcd-md) hosted with ❤ by [GitHub](https://github.com/) 

 

To initialize a git repository in the root of the folder, run the [git init](http://git-scm.com/docs/git-init) command:  

```
mnelson:myproject mnelson$ git init
```

```
Initialized empty Git repository in /Users/mnelson/Desktop/myproject/.git/
```

[view raw](https://gist.github.com/cubeton/89793ba1bc947f64658e/raw/f3dba1dd72fda5eeb98b761338aedfc310d29d54/gitinit.md) [gitinit.md](https://gist.github.com/cubeton/89793ba1bc947f64658e#file-gitinit-md) hosted with ❤ by [GitHub](https://github.com/) 

###  

### Step 2: Add a new file to the repo

Go ahead and add a new file to the project, using any text editor you like or running a [touch](http://linux.die.net/man/1/touch) command.

Once you've added or modified files in a folder containing a git repo, git will notice that changes have been made inside the repo. But, git won't officially keep track of the file (that is, put it in a commit - we'll talk more about commits next) unless you explicitly tell it to.

```
mnelson:myproject mnelson$ touch mnelson.txt
```

```
mnelson:myproject mnelson$ ls
```

```
mnelson.txt
```

[view raw](https://gist.github.com/cubeton/2d8f224bede4c2dde86b/raw/b865e27cc4715b3a3a4a5839e77ab232ff1b31f9/addfile.md) [addfile.md](https://gist.github.com/cubeton/2d8f224bede4c2dde86b#file-addfile-md) hosted with ❤ by [GitHub](https://github.com/) 

 邬媛截止

After creating the new file, you can use the [`**git status**`](http://git-scm.com/docs/git-status) command to see which files git knows exist.

```
mnelson:myproject mnelson$ git status
```

```
On branch master
```

```
 
```

```
Initial commit
```

```
 
```

```
Untracked files:
```

```
  (use "git add <file>..." to include in what will be committed)
```

```
 
```

```
               mnelson.txt
```

```
 
```

```
nothing added to commit but untracked files present (use "git add" to track)
```

[view raw](https://gist.github.com/cubeton/02e849bbffcbea1e9a61/raw/71c93139666a8a4e06795f53c9aec5db95e6019a/gitstatus.md) [gitstatus.md](https://gist.github.com/cubeton/02e849bbffcbea1e9a61#file-gitstatus-md) hosted with ❤ by [GitHub](https://github.com/) 

What this basically says is, "Hey, we noticed you created a new file called mnelson.txt, but unless you use the '`git add' `command we aren't going to do anything with it."

 

### An interlude: The staging environment, the commit, and you

One of the most confusing parts when you're first learning git is the concept of the staging environment and how it relates to a commit.

A [commit](http://git-scm.com/docs/git-commit) is a record of what files you have changed since the last time you made a commit. Essentially, you make changes to your repo (for example, adding a file or modifying one) and then tell git to put those files into a commit.

Commits make up the essence of your project and allow you to go back to the state of a project at any point.

So, how do you tell git which files to put into a commit? This is where the [**staging environment** or **index**](https://git-scm.com/book/en/v2/Getting-Started-Git-Basics) come in. As seen in Step 2, when you make changes to your repo, git notices that a file has changed but won't do anything with it (like adding it in a commit).

To add a file to a commit, you first need to add it to the staging environment. To do this, you can use the [git add](http://git-scm.com/docs/git-add) **<filename>** command (see Step 3 below).

Once you've used the git add command to add all the files you want to the staging environment, you can then tell git to package them into a commit using the [**git commit** ](http://git-scm.com/docs/git-commit)command. 

Note: The staging environment, also called 'staging', is the new preferred term for this, but you can also see it referred to as the 'index'.

 

### Step 3: Add a file to the staging environment

Add a file to the staging environment using the **git add** command. 

If you rerun the git status command, you'll see that git has added the file to the staging environment (notice the "Changes to be committed" line).  

```
mnelson:myproject mnelson$ git status
```

```
On branch master
```

```
 
```

```
Initial commit
```

```
 
```

```
Changes to be committed:
```

```
  (use "git rm --cached <file>..." to unstage)
```

```
 
```

```
               new file:   mnelson.txt
```

[view raw](https://gist.github.com/cubeton/28f7bea3b232f67e031c/raw/875157cd78d75c23f3f0e29bf0c97989e3d52937/addtostaging.md) [addtostaging.md](https://gist.github.com/cubeton/28f7bea3b232f67e031c#file-addtostaging-md) hosted with ❤ by [GitHub](https://github.com/) 

 To reiterate, the file has **not** yet been added to a commit, but it's about to be.

 赵小蕊

### Step 4: Create a commit

It's time to create your first commit!

Run the command `git commit -m "Your message about the commit"`

```
mnelson:myproject mnelson$ git commit -m "This is my first commit!"
```

```
[master (root-commit) b345d9a] This is my first commit!
```

```
 1 file changed, 1 insertion(+)
```

```
 create mode 100644 mnelson.txt
```

[view raw](https://gist.github.com/cubeton/1068d965d147b4039e4d/raw/5c3262c3f6e3c28328ba57ea33c512dbab149fcf/commit.md) [commit.md](https://gist.github.com/cubeton/1068d965d147b4039e4d#file-commit-md) hosted with ❤ by [GitHub](https://github.com/) 

The message at the end of the commit should be something related to what the commit contains - maybe it's a new feature, maybe it's a bug fix, maybe it's just fixing a typo. Don't put a message like "asdfadsf" or "foobar". That makes the other people who see your commit sad. Very, very, sad.

 

### Step 5: Create a new branch

Now that you've made a new commit, let's try something a little more advanced.

Say you want to make a new feature but are worried about making changes to the main project while developing the feature. This is where [git branches](https://git-scm.com/book/en/v1/Git-Branching-What-a-Branch-Is) come in. 

Branches allow you to move back and forth between 'states' of a project. For instance, if you want to add a new page to your website you can create a new branch just for that page without affecting the main part of the project. Once you're done with the page, you can [**merge**](http://git-scm.com/docs/git-merge) your changes from your branch into the master branch. When you create a new branch, Git keeps track of which commit your branch 'branched' off of, so it knows the history behind all the files. 

Let's say you are on the master branch and want to create a new branch to develop your web page. Here's what you'll do: Run [`**git checkout -b **`](http://git-scm.com/docs/git-checkout). This command will automatically create a new branch and then 'check you out' on it, meaning git will move you to that branch, off of the master branch.

After running the above command, you can use the [`**git branch**`](http://git-scm.com/docs/git-branch) command to confirm that your branch was created:

```
mnelson:myproject mnelson$ git branch
```

```
  master
```

```
* my-new-branch
```

[view raw](https://gist.github.com/cubeton/fa25a25f322a2cd5f405/raw/81033788d288adeffe260bd724ab2699b29e3e35/gitbranch.md) [gitbranch.md](https://gist.github.com/cubeton/fa25a25f322a2cd5f405#file-gitbranch-md) hosted with ❤ by [GitHub](https://github.com/) 

The branch name with the asterisk next to it indicates which branch you're pointed to at that given time. 

Now, if you switch back to the master branch and make some more commits, your new branch won't see any of those changes until you [**merge**](http://git-scm.com/docs/git-merge) those changes onto your new branch.

 

### Step 6: Create a new repository on GitHub

If you only want to keep track of your code locally, you don't need to use GitHub. But if you want to work with a team, you can use GitHub to collaboratively modify the project's code.

 

To create a new repo on GitHub, log in and go to the GitHub home page. You should see a green '+ New repository' button: 

After clicking the button, GitHub will ask you to name your repo and provide a brief description:

When you're done filling out the information, press the 'Create repository' button to make your new repo.

文香兰

GitHub will ask if you want to create a new repo from scratch or if you want to add a repo you have created locally. In this case, since we've already created a new repo locally, we want to push that onto GitHub so follow the **'....or push an existing repository from the command line'** section: 

```
mnelson:myproject mnelson$ git remote add origin https://github.com/cubeton/mynewrepository.git
```

```
mnelson:myproject mnelson$ git push -u origin master
```

```
Counting objects: 3, done.
```

```
Writing objects: 100% (3/3), 263 bytes | 0 bytes/s, done.
```

```
Total 3 (delta 0), reused 0 (delta 0)
```

```
To https://github.com/cubeton/mynewrepository.git
```

```
 * [new branch]      master -> master
```

```
Branch master set up to track remote branch master from origin.
```

### [view raw](https://gist.github.com/cubeton/3a2616c44e35ca68a6b0/raw/41e5758cfdbd7db8a1659c1adaba9346680097f9/addgithub.md) [addgithub.md](https://gist.github.com/cubeton/3a2616c44e35ca68a6b0#file-addgithub-md) hosted with ❤ by [GitHub](https://github.com/) 

 (You'll want to change the URL in the first command line to what GitHub lists in this section since your GitHub username and repo name are different.)

 

### Step 7: Push a branch to GitHub

Now we'll **push** the commit in your branch to your new GitHub repo. This allows other people to see the changes you've made. If they're approved by the repository's owner, the changes can then be merged into the master branch.

To push changes onto a new branch on GitHub, you'll want to run [git push](http://git-scm.com/docs/git-push) **origin yourbranchname**`. `GitHub will automatically create the branch for you on the remote repository: 

```
mnelson:myproject mnelson$ git push origin my-new-branch
```

```
Counting objects: 3, done.
```

```
Delta compression using up to 8 threads.
```

```
Compressing objects: 100% (2/2), done.
```

```
Writing objects: 100% (3/3), 313 bytes | 0 bytes/s, done.
```

```
Total 3 (delta 0), reused 0 (delta 0)
```

```
To https://github.com/cubeton/mynewrepository.git
```

```
 * [new branch]      my-new-branch -> my-new-branch
```

[view raw](https://gist.github.com/cubeton/bf8274609c344b6d0e70/raw/4764e740cac9a48eefad341d9e34ceb09f89b73f/addnewbranchgithub.md) [addnewbranchgithub.md](https://gist.github.com/cubeton/bf8274609c344b6d0e70#file-addnewbranchgithub-md) hosted with ❤ by [GitHub](https://github.com/) 

 You might be wondering what that "origin" word means in the command above. What happens is that when you clone a remote repository to your local machine, git creates an **alias** for you. In nearly all cases this alias is called "[**origin**](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes)." It's essentially shorthand for the remote repository's URL. So, to push your changes to the remote repository, you could've used either the command: `**git push git@github.com:git/git.git yourbranchname**` or `**git push origin yourbranchname**`

(If this is your first time using GitHub locally, it might prompt you to log in with your GitHub username and password.)

If you refresh the GitHub page, you'll see note saying a branch with your name has just been pushed into the repository. You can also click the 'branches' link to see your branch listed there.

 

Now click the green button in the screenshot above. We're going to make a **pull request**!

 秦秋凤

### Step 8: Create a Pull Request (PR)

A pull request (or PR) is a way to alert a repo's owners that you want to make some changes to their code. It allows them to review the code and make sure it looks good before putting your changes on the master branch.

This is what the PR page looks like before you've submitted it:

And this is what it looks like once you've submitted the PR request: 

You might see a big green button at the bottom that says 'Merge pull request'. Clicking this means you'll merge your changes into the master branch.

Note that this button won't always be green. In some cases it'll be grey, which means you're faced with a **merge conflict**. This is when there is a change in one file that conflicts with a change in another file and git can't figure out which version to use. You'll have to manually go in and tell git which version to use.

Sometimes you'll be a co-owner or the sole owner of a repo, in which case you may not need to create a PR to merge your changes. However, it's still a good idea to make one so you can keep a more complete history of your updates and to make sure you always create a new branch when making changes.

 

### Step 9: Merge a PR

Go ahead and click the green 'Merge pull request' button. This will merge your changes into the master branch.

 

 

When you're done, I recommend deleting your branch (too many branches can become messy), so hit that grey 'Delete branch' button as well.

You can double check that your commits were merged by clicking on the 'Commits' link on the first page of your new repo.

 

 

This will show you a list of all the commits in that branch. You can see the one I just merged right up top (Merge pull request #2).

 

You can also see the [**hash code**](https://git-scm.com/docs/git-hash-object) of the commit on the right hand side. A hash code is a unique identifier for that specific commit. It's useful for referring to specific commits and when undoing changes (use the [git revert](http://git-scm.com/docs/git-revert)` <hash code number>` command to backtrack).

 

### Step 10: Get changes on GitHub back to your computer

Right now, the repo on GitHub looks a little different than what you have on your local machine. For example, the commit you made in your branch and merged into the master branch doesn't exist in the master branch on your local machine.

In order to get the most recent changes that you or others have merged on GitHub, use the **git pull origin master** command (when working on the master branch).

谢婷

```
mnelson:myproject mnelson$ git pull origin master
```

```
remote: Counting objects: 1, done.
```

```
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
```

```
Unpacking objects: 100% (1/1), done.
```

```
From https://github.com/cubeton/mynewrepository
```

```
 * branch            master     -> FETCH_HEAD
```

```
   b345d9a..5381b7c  master     -> origin/master
```

```
Merge made by the 'recursive' strategy.
```

```
 mnelson.txt | 1 +
```

```
 1 file changed, 1 insertion(+)
```

[view raw](https://gist.github.com/cubeton/48b5c726b496d50c3975/raw/fe2c68e0988c467fd218587e2397552076355b52/pulloriginmaster.md) [pulloriginmaster.md](https://gist.github.com/cubeton/48b5c726b496d50c3975#file-pulloriginmaster-md) hosted with ❤ by [GitHub](https://github.com/) 

 

This shows you all the files that have changed and how they've changed.

Now we can use the [`**git log**`](http://git-scm.com/docs/git-log) command again to see all new commits.

(You may need to switch branches back to the master branch. You can do that using the **git checkout master**` `command.)

```
mnelson:myproject mnelson$ git log
```

```
commit 3e270876db0e5ffd3e9bfc5edede89b64b83812c
```

```
Merge: 4f1cb17 5381b7c
```

```
Author: Meghan Nelson <mnelson@hubspot.com>
```

```
Date:   Fri Sep 11 17:48:11 2015 -0400
```

```
 
```

```
    Merge branch 'master' of https://github.com/cubeton/mynewrepository
```

```
 
```

```
commit 4f1cb1798b6e6890da797f98383e6337df577c2a
```

```
Author: Meghan Nelson <mnelson@hubspot.com>
```

```
Date:   Fri Sep 11 17:48:00 2015 -0400
```

```
 
```

```
    added a new file
```

```
 
```

```
commit 5381b7c53212ca92151c743b4ed7dde07d9be3ce
```

```
Merge: b345d9a 1e8dc08
```

```
Author: Meghan Nelson <meghan@meghan.net>
```

```
Date:   Fri Sep 11 17:43:22 2015 -0400
```

```
 
```

```
    Merge pull request #2 from cubeton/my-newbranch
```

```
    
```

```
    Added some more text to my file
```

```
 
```

```
commit 1e8dc0830b4db8c93efd80479ea886264768520c
```

```
Author: Meghan Nelson <mnelson@hubspot.com>
```

```
Date:   Fri Sep 11 17:06:05 2015 -0400
```

```
 
```

```
    Added some more text to my file
```

```
 
```

```
commit b345d9a25353037afdeaa9fcaf9f330effd157f1
```

```
Author: Meghan Nelson <mnelson@hubspot.com>
```

```
Date:   Thu Sep 10 17:42:15 2015 -0400
```

```
 
```

```
    This is my first commit!
```

[view raw](https://gist.github.com/cubeton/48f55c5a237cd8e1a238/raw/3e31113a073b9bdec16800407d718b631dd0f587/gitlogaftermerge.md) [gitlogaftermerge.md](https://gist.github.com/cubeton/48f55c5a237cd8e1a238#file-gitlogaftermerge-md) hosted with ❤ by [GitHub](https://github.com/) 

### Step 11: Bask in your git glory

You've successfully made a PR and merged your code to the master branch. Congratulations! If you'd like to dive a little deeper, check out the files in [this Git101 folder](https://github.com/cubeton/git101/tree/master/TurtorialInfo) for even more tips and tricks on using git and GitHub. 

I also recommend finding some time to work with your team on simulating a smaller group project like we did here. Have your team make a new folder with your team name, and add some files with text to it. Then, try pushing those changes to this remote repo. That way, your team can start making changes to files they didn't originally create and practice using the PR feature. And, use the git blame and git history tools on GitHub to get familiar with tracking which changes have been made in a file and who made those changes. 

The more you use git, the more comfortable you'll... git with it. (I couldn't resist.)

 

### Written by [Meghan Nelson](https://product.hubspot.com/blog/author/meghan-nelson)

### Subscribe for updates

  \*  Lifecycle Stage    HubSpot Product Blog Email Subscription    HubSpot Product needs the contact information you provide to us to contact you about our products and services. You may unsubscribe from these communications at anytime. For information on how to unsubscribe, as well as our privacy practices and commitment to protecting your privacy, check out our Privacy Policy.      

### Topics

·         [Product](https://product.hubspot.com/blog/topic/product) 

·         [Engineering](https://product.hubspot.com/blog/topic/engineering) 

·         [Design](https://product.hubspot.com/blog/topic/design) 

·         [Product Management](https://product.hubspot.com/blog/topic/product-management) 

·         [UX](https://product.hubspot.com/blog/topic/ux) 

·         [Culture](https://product.hubspot.com/blog/topic/culture) 

·         [Career Growth](https://product.hubspot.com/blog/topic/career-growth) 

 

[What is HubSpot](https://www.hubspot.com/what-is-hubspot)|[Our Story](https://www.hubspot.com/internet-marketing-company)|[Our Products](https://www.hubspot.com/products)|[Culture Code](https://blog.hubspot.com/blog/tabid/6307/bid/34234/The-HubSpot-Culture-Code-Creating-A-Company-We-Love.aspx)

[Facebook](https://www.facebook.com/HubSpotDevelopment?fref=ts)|[Twitter](https://twitter.com/HubSpotDev)|[Instagram](https://instagram.com/hubspotdev/) 

 