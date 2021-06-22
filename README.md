
## 15.7.1. Getting Ready: Code Together

Coding together allows you to work as a team so you can build bigger projects faster.

In this studio, we will practice the common Git commands used when multiple people work on the same code base.

You and a partner will begin by coding in tag-team shifts. By the end of the task you should have a good idea about how to have two people work on the same code at the same time. You will learn how to:

1.  Quickly add code in pull + push cycles  _(Important! This is the fundamental process!)_
2.  Add a collaborator to a GitHub Project
3.  Share  _repositories_  on GitHub
4.  Create a  _branch_  in Git
5.  Create a  _pull request_  in GitHub
6.  Resolve merge conflicts (which are not as scary as they sound)

This lesson will reinforce the following:

1.  Creating repositories
2.  Cloning repositories
3.  Working with Git concepts: Staging, Commits, and Status

## 15.7.2. Overview

We are going to simulate a radio conversation between the shuttle pilot and mission control.

First, find a new friend to share the activity. Students 
*must* pair off for this exercise

You and your partner will alternate tasks, so designate one of you as **Pilot** and the other as **Control**. Even when it is not your turn to complete a task, read and observe what your partner is doing to complete theirs. The steps here mimic how a real-world collaborative Git workflow can be used within a project.

***Warning***:
*As you go through these steps, you’ll be working with branches. It’s very likely you will make changes to the code only to realize that you did so in the wrong branch. When this happens (and it happens to all of us) you can use  `git  stash`  to cleanly move your changes to another branch. Read about how to do so in our  [Git Stash](https://education.launchcode.org/intro-to-programming-csharp/appendices/git/stash.html#git-stash)  tutorial.*


## 15.7.3.1. Step 1: Create a New Repository

**Control:** Create a new git repository with the following commands (please note that the '$' symbol is just used to represent prompts in the terminal).

    $ mkdir communication-log
    $ cd communication-log
    $ git init

This will initialize the repository, next navigate to visual studio and create a new project inside the folder you just created with the following information:

[Project Setup](https://drive.google.com/file/d/1Gj7Eh4pWbf-2jabe7BhvHd4o3dS0xnLt/view?usp=sharing)


Let’s check that our project works by running it.

You can continue to use your terminal, or you can use the terminal that is part of Visual Studio. If you want to use the Visual Studio terminal, it can be found under the  **View**  tab.

**Note**
*If your console window does not stay open long enough for you to see your code, try adding the  `Console.Read()`  below the  `WriteLine`. This is a piece of code that will keep your terminal window open so you can read what it contains.*

If you can read your terminal window just fine and you haven’t added anything, then ignore this tip.

Now, navigate back to your terminal, and inside your new git repository add a `.gitignore` file with `touch .gitignore`, and edit it so that it contains the following information:

    communication-log/communication-log/bin/*
    communication-log/communication-log/obj/*
    communication-log/.vs/*
    communication-log/Backup/*
    communication-log/UpgradeLog.htm

What this `.gitignore` files does, is it tells git what files and folders we want it to well... ignore (surprise). Some of these folders are really not needed for anything but for our local machines, and it can make the remote repository look very bloated. However, If you get stuck, keep moving on and do not stress too much on this for now.

Once you’ve done this and checked that your visual studio code runs, let’s stage and commit these files


1.  First, check the  status with `git status`.  You will likely see something akin to this:
    
```
	    $ git status
	    On branch main
    
	    No commits yet.
    
	    Untracked files:
	    (use "Git add <file>..." to include in what will be committed)
	    
	    .gitignore
		communication-log/communication-log.sln
		communication-log/communication-log/Program.cs
		communication-log/communication-log/communication-log.csproj
	    
	    nothing added to commit but untracked files present (use "git add" to track)    
```
    
2.  This output shows us that we have four new files that have not been staged yet. We want to add them, So let’s  `add`  them, then check the  `status`  again.

```$ git add .
$ git status
On branch main

    No commits yet

    Changes to be committed:
    (use "git rm --cached <file>..." to unstage)
    
   new file:  .gitignore
   new file:  communication-log/communication-log.sln
   new file:  communication-log/communication-log/Program.cs
   new file:  communication-log/communication-log/communication-log.csproj
```



4.  The output tells us that the files are staged. Now let’s  `commit`. After that, we can see a record of our progress by using  `git  log`.
    
  
```
  $ git commit -m 'Started communication log.'
    [main (root-commit) e1c1719] Started communication log.
    4 files changed, 451 insertions(+)
    create mode 100644 .gitignore
    create mode 100644 communication-log.sln
    create mode 100644 communication-log/Program.cs
    create mode 100644 communication-log/communication-log.csproj
  
  ```
  ```  
   $ git log
   commit 679de772612099c77891d2a3fab12af8db08b651
   Author: Cheryl <chrisbay@gmail.com>
   Date:   Wed Apr 5 10:55:56 2017 -0500
    
       Started communication log.
 ```

Great! We’ve got our project going locally, but we’re going to need to make it accessible for  **Pilot**  also. Let’s push this project up to GitHub.

### 15.7.3.2. Step 2: Share Your Repository On GitHub[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#step-2-share-your-repository-on-github "Permalink to this headline")

**Control**: Go to your GitHub profile in a web browser. Click on the “+” button to add a new repository (called a  _repo_  for short).

![The New Repository link in the dropdown menu at top right on GitHub.](https://education.launchcode.org/intro-to-programming-csharp/_images/new-repo-button.png)

The  _New Repository_  link is in the dropdown menu at top right on GitHub.[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#id2 "Permalink to this image")

To create a new repository:

1.  Fill in the name and description.
2.  Uncheck  _Initialize this repository with a README_  and click  _Create Repository_.

![Creating a new repository in GitHub by filling out the form](https://education.launchcode.org/intro-to-programming-csharp/_images/create-repo.png)

Create a new repository in GitHub[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#id3 "Permalink to this image")

**Note**
*If you initialize with a README, in the next step Git will refuse to merge this repo with the local repo. There are ways around that, but it’s faster and easier to just create an empty repo here.*

After clicking, you should see something similar to:

![The page you see after creating an empty repository, with several options.](https://education.launchcode.org/intro-to-programming-csharp/_images/new-repo-push.png)

Now go back to your terminal and copy/paste the commands shown in the GitHub instructions. These should be very similar to (if github gives a different list of commands, follow those commands):

    $ git remote add origin https://github.com:chrisbay/communication-log.git
    $ git push origin main

**Note**:
 *The first time you push up to GitHub, you will be prompted in the    terminal to enter your account username and password. Do this.*

You will then see a large amount of output that you can safely ignore. The final few lines will confirm a successful push. They will look something like this:

    To github.com:chrisbay/communication-log.git    c7f97814..54993de3  main -> main

***Warning***
*Unless you’ve set up an SSH key with GitHub, make sure you’ve selected the HTTPS clone URL. If you’re not sure whether you have an SSH key, you probably don’t.*

Now you should be able to confirm that GitHub has the same version as your local project. (File contents in browser match those in terminal). Click around and see what is there. You can read all your code through GitHub’s web interface.

![A repository with one commit in GitHub](https://education.launchcode.org/intro-to-programming-csharp/_images/repo-first-commit.png)

A repository with one commit in GitHub[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#id5 "Permalink to this image")

### 15.7.3.3. Step 3: Clone a Project from GitHub[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#step-3-clone-a-project-from-github "Permalink to this headline")

**Pilot**: Go to Control’s GitHub profile and find the communication-log repo. Click on the green  _Clone or download_  button. Use HTTPS (not SSH). Copy the url to your clipboard.

![The clone button is on the right-hand side of a project's main page](https://education.launchcode.org/intro-to-programming-csharp/_images/clone-button.png)

Cloning a repository in GitHub[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#id6 "Permalink to this image")

In your terminal, navigate to your development folder and clone down the repo. The command should look something like this.

    $ git clone https://github.com/chrisbay/communication-log.git

Now you can respond to Control! Open the  `communication-log.sln`  file in your editor and add your response to mission control. Be creative, the communication can go anywhere! Just don’t ask your partner what you should write. After you finish, commit your change.

**Note**
*When you open the project folder, you might not be in the same directory as the solution. You want to open the solution or  `.sln`  file. A quick way to do that from the terminal is to  `cd`  into the folder that is holding the solution and then type  `open  .sln`.*
```
$ git status
On branch main
Your branch is up-to-date with 'origin/main'.
nothing to commit, working directory clean
$ git add .
$ git commit -m 'Added second line to log.'
```
Now we need to push up your changes so Control can use them as well.
```
    $ git push origin main ERROR: Permission to chrisbay/communication-log.git denied to pilot. fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```
Great error message! It let us know exactly what went wrong: Pilot does not have security permissions to write to Control’s repo. Let’s fix that.

### 15.7.3.4. Step 4: Add A Collaborator To A GitHub Project[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#step-4-add-a-collaborator-to-a-github-project "Permalink to this headline")

**Control**: In your web browser, go to your  `communication-log`  repo. Click the  _Settings_  button then click on  _Collaborators_. Enter in Pilot’s GitHub username and click  _Add Collaborator_.

![Add a collaborator by typing their user name into the input on the Add Collaborator page.](https://education.launchcode.org/intro-to-programming-csharp/_images/add-collaborator.png)

Add a collaborator to your repo in GitHub[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#id7 "Permalink to this image")

### 15.7.3.5. Step 5: Join the Project and Push[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#step-5-join-the-project-and-push "Permalink to this headline")

**Pilot**: You should receive an email invitation to join this repository. View and accept the invitation.

**Note**
*If you don’t see an email (it may take a few minutes to arrive in your inbox), check your Spam folder. If you still don’t have an email, visit the repository page for the repo that Control created (ask them for the link), and you’ll see a notification at the top of the page.*

[![The email invite to join a GitHub repository](https://education.launchcode.org/intro-to-programming-csharp/_images/repo-invite.png)](https://education.launchcode.org/intro-to-programming-csharp/_images/repo-invite.png)

Invited to collaborate email in GitHub[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#id8 "Permalink to this image")

Now let’s go enter that command again to push up our code.
```
$ git push origin main
Counting objects: 9, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (9/9), done.
Writing objects: 100% (9/9), 1.01 KiB | 0 bytes/s, done.
Total 9 (delta 8), reused 0 (delta 0)
remote: Resolving deltas: 100% (8/8), completed with 8 local objects.
To git@github.com:chrisbay/communication-log.git
   511239a..679de77  main -> main
```
Anyone reading the code through GitHub’s browser interface should now see the new second line.

### 15.7.3.6. Step 6: Pull Pilot’s Line and Add Another Line[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#step-6-pull-pilot-s-line-and-add-another-line "Permalink to this headline")

**Control**: You might notice you don’t have the second line of code in your copy of the project on your computer. Let’s fix that. Go to the terminal and enter this command to pull down the updated code into your local git repository.
```
$ git pull origin main
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0
Unpacking objects: 100% (3/3), done.
From github.com:chrisbay/communication-log
   e0de62d..e851b7e  main     -> origin/main
Updating e0de62d..e851b7e
Fast-forward
communication-log.sln | 1 +
1 file changed, 1 insertion(+)
```
Now, in your editor, add a third line to the communication. Then add, commit, and push it up.

You can have your story go anywhere! Try to tie it in with what the pilot wrote, without discussing with them any plans on where the story will go.

### 15.7.3.7. Step 7: Do It Again: Pull, Change, and Push![](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#step-7-do-it-again-pull-change-and-push "Permalink to this headline")

**Pilot**: You might notice now  _you_  don’t have the third line on your computer. Go to the terminal and enter this command to pull in the changes that Control just made.

    $ git pull origin main remote: Counting objects: 3, done. remote: Compressing objects: 100% (2/2), done. remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0 Unpacking objects: 100% (3/3), done. From github.com:chrisbay/communication-log    e851b7e..167684c  main
    -> origin/main Updating e851b7e..167684c Fast-forward communication-log.sln | 1 + 1 file changed, 1 insertion(+)

Now add a fourth line to the log. Again, be creative, but no planning!

Then add, commit, and push your change.

You can both play like this for a while! Feel free to repeat this cycle a few times to add to the story.

### 15.7.3.8. Step 8: Create a Branch In Git[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#step-8-create-a-branch-in-git "Permalink to this headline")

This workflow is a common one in team development situations. You might wonder, however, if professional developers sit around waiting for their teammates to commit and push a change before embarking on additional work on their own. That would be a drag, and thankfully, there is a nice addition to this workflow that will allow for simultaneous work to be carried out in a reasonable way.

**Pilot**: While Control is working on an addition to the story, let’s make another change simultaneously. In order to do that, we’ll create a new branch. Recall that a branch is a separate “copy” of the codebase that you can commit to without affecting code in the  `main`  branch.
```
$ git checkout -b open-mic
Switched to a new branch 'open-mic'
```
This command creates a new branch named  `open-mic`, and switches your local repository to use that branch.

Update the  [background color of the console](https://docs.microsoft.com/en-us/dotnet/api/system.console.backgroundcolor?view=net-5.0), and update the  `Hello  World!`  statement to something more exciting.:

    Console.BackgroundColor = ConsoleColor.Your-Choice-Here

Now stage and commit these changes.
```
$ git add .
$ git commit -m 'Changed background color'
$ git push origin open-mic
```
Note that the last command is a bit different than what we’ve used before (`git  push  origin  open-mic`). The final piece of this command is the name of the branch that we want to push to GitHub.

You and your partner should both now see a second branch present on the GitHub project page. To view branches on GitHub, select  _Branches_  from the navigation section just below the repository title.

![../../_images/two-branches.png](https://education.launchcode.org/intro-to-programming-csharp/_images/two-branches.png)


In your terminal, you can type this command to see a list of the available branches:
```
$ git branch
* open-mic
main
```
Note that creating and being able to see a branch in your local repository via this command does NOT mean that the branch is on GitHub. You’ll need to push the branch for it to appear on GitHub.

**Note**
*The * to the left of  `open-mic`  indicates that this is the active branch.*

Great! Now let’s show the other player your work in GitHub and ask them to merge it in to the main branch.

### 15.7.3.9. Create a Pull Request In GitHub[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#create-a-pull-request-in-github "Permalink to this headline")

**Pilot**: If you haven’t already, in your browser, go to the GitHub project and click on  _Branches_  and make sure you see the new branch name,  _open-mic_.

[![The Branches page of a repo, with a button to open a new pull request to the right of each feature branch.](https://education.launchcode.org/intro-to-programming-csharp/_images/new-pr-button1.png)](https://education.launchcode.org/intro-to-programming-csharp/_images/new-pr-button1.png)

Branches Page in GitHub[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#id10 "Permalink to this image")

Click  _New Pull Request_  to begin the process of requesting that your changes in the  `open-mic`  branch be incorporated into the  `main`  branch. Add some text in the description box to let Control know what you did and why.

Note that the branch selected in the  _base_  dropdown is the one you want to merge  _into_, while the selected branch in the  _compare_  dropdown is the one you want to merge  _from_.

[![The form for creating a new pull request.](https://education.launchcode.org/intro-to-programming-csharp/_images/create-pr1.png)](https://education.launchcode.org/intro-to-programming-csharp/_images/create-pr1.png)

Open a PR in GitHub[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#id11 "Permalink to this image")

This is what an opened pull request looks like:

[![An open pull request.](https://education.launchcode.org/intro-to-programming-csharp/_images/open-pr1.png)](https://education.launchcode.org/intro-to-programming-csharp/_images/open-pr1.png)

An open PR in GitHub[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#id12 "Permalink to this image")

### 15.7.3.10. Step 10: Make a Change in the New Branch[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#step-10-make-a-change-in-the-new-branch "Permalink to this headline")

**Control**: You will notice that you do not see the new console colors. Type this command to see what branches are on your local computer:
```
$ git branch
* main
```
If you want to work with the branch before merging it in, you can do so by typing these commands:
```
$ git fetch origin open-mic
...
$ git branch
open-mic
* main
```
```
$ git checkout open-mic
Switched to branch 'open-mic'
Your branch is up-to-date with 'origin/open-mic'.
```
Make a change, commit, and push this branch–you will see that the pull request in GitHub is updated to reflect the changes you added. The context in the description box is NOT updated, however, so be sure to add comments to the pull request to explain what you did and why.

Now switch back to the  `main`  branch:
```
$ git checkout main
Switched to branch 'main'
Your branch is up-to-date with 'origin/main'.
```
You will see your files no longer have the changes made in the  `open-mic`  branch. Let’s go merge those changes in, so that the  `main`  branch adopts all the changes in the  `open-mic`  branch.

### 15.7.3.11. Step 11: Merge the Pull Request[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#step-11-merge-the-pull-request "Permalink to this headline")

**Control**: Go to the repo in GitHub. Click on  _Pull Requests_.

![../../_images/pr-link.png](https://education.launchcode.org/intro-to-programming-csharp/_images/pr-link.png)

PR Open in GitHub[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#id13 "Permalink to this image")

Explore this page to see all the information GitHub shows you about the pull request.

[![A pull request ready to merge](https://education.launchcode.org/intro-to-programming-csharp/_images/open-pr1.png)](https://education.launchcode.org/intro-to-programming-csharp/_images/open-pr1.png)

Merge a Pull Request in GitHub[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#id14 "Permalink to this image")

When you’re happy with the changes, merge them in. Click  _Merge Pull Request_  then  _Confirm Merge_.

[![Confirming a merge](https://education.launchcode.org/intro-to-programming-csharp/_images/confirm-merge-pr.png)](https://education.launchcode.org/intro-to-programming-csharp/_images/confirm-merge-pr.png)

Confirm PR Merge in GitHub[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#id15 "Permalink to this image")

Upon a successful merge, you should see a screen similar to the following:

[![The screen displayed after a PR is merged](https://education.launchcode.org/intro-to-programming-csharp/_images/pr-merged1.png)](https://education.launchcode.org/intro-to-programming-csharp/_images/pr-merged1.png)

PR Merged in GitHub[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#id16 "Permalink to this image")

The changes from  `open-mic`  are now in the  `main`  branch, but only in the remote repository on GitHub. You will need to pull the updates to your  `main`  for them to be present locally.
```
$ git checkout main
$ git pull origin main
```
Git is able to merge these files on its own.

### 15.7.3.12. Step 12: Merge Conflicts![](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#step-12-merge-conflicts "Permalink to this headline")

When collaborating on a project, things won’t always go smoothly. It’s common for two people to make changes to the same line(s) of code, at roughly the same time, which will prevent Git from being able to merge the changes together.

![An animated GIF file showing two opposing armies colliding in a mess](https://education.launchcode.org/intro-to-programming-csharp/_images/git-merge.gif)

Git Merge Conflicts[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#id17 "Permalink to this image")

This isn’t such a big deal. In fact, it’s very common. To see how we can handle such a situation, we’ll intentionally create a merge conflict and then resolve it.

**Pilot**: Let’s change something about the style file. Our Console is looking pretty plain, so let’s change the color and maybe share a joke or something to liven this up.

First, switch back to the  `main`  branch.
```
$ git checkout main
```
Stage and commit your changes and push them up to GitHub. If you don’t remember how to do this, follow the instructions above. Make sure you’re back in the  `main`  branch! If you’re still in  `open-mic`, then your changes will be isolated, and you won’t get the merge conflict you need to learn about.

Meanwhile…

**Control**: Let’s change something about the style file that Pilot just edited. Change the color again. Update your current Console.WriteLine statement to make an observation about the weather or something.

Commit your changes to branch  `main`.

### 15.7.3.13. Step 13: Resolving Merge Conflicts[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#step-13-resolving-merge-conflicts "Permalink to this headline")

**Control**: Try to push your changes up to GitHub. You should get an error message. How exciting!
```
$ git push origin main

To git@github.com:chrisbay/communication-log.git
! [rejected]        main-> main (fetch first)
error: failed to push some refs to 'git@github.com:chrisbay/communication-log.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
There’s a lot of jargon in that message, including some terminology we haven’t encountered. However, the core of the message is indeed understandable to us: “Updates were rejected because the remote contains work that you do not have locally.” In other words, somebody (Pilot, in this case), pushed changes to the same branch, and you don’t have those changes on your computer. Git will not let you push to a branch in another repository unless you have incorporated all of the work present in that branch.

Let’s pull these outstanding changes into our branch and resolve the errors.
```
$ git pull
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 4 (delta 1), reused 4 (delta 1), pack-reused 0
Unpacking objects: 100% (4/4), done.
From github.com:chrisbay/communication-log
   7d7e42e..0c21659  main     -> origin/main
Auto-merging communication-log.sln
CONFLICT (content): Merge conflict in communication-log.sln
Auto-merging communication-log.sln
CONFLICT (content): Merge conflict in communication-log.sln
Automatic merge failed; fix conflicts and then commit the result.
```
Since Pilot made changes to some of the same lines you did, Git was unable to automatically merge the changes.

The specific locations where Git could not automatically merge files are indicated by the lines that begin with  `CONFLICT`. You will have to edit these files yourself to incorporate Pilot’s changes.

![VS shows merge conflicts in the editor window](https://education.launchcode.org/intro-to-programming-csharp/_images/conflict-workspace.png)

Merge conflicts in  `main`  branch of communication-log, viewed in VS on a Mac. Windows users, you will see a differnt screen, but the  `<<<<<<<`,  `=======`  and  `>>>>>>>`  symbols will be the same.[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#id18 "Permalink to this image")

At the top and bottom, there is some code that could be merged without issue.

Between the  `<<<<<<<  HEAD`  and  `=======`  symbols is the version of the code that exists locally. These are  _your_  changes.

Between  `=======`  and  `>>>>>>>  open-mic...`  are the changes that Pilot made (the hash  `open-mic...`  will be unique to the commit, so you’ll see something slightly different on your screen).

Let’s unify our code. Select which changes you would like to keep, or if possible select all of them. It’s up to you and your partner.

Tip

Like many other editors, VS provides fancy buttons to allow you to resolve individual merge conflicts with a single click. There’s nothing magic about these buttons; they do the same thing that you can do by directly editing the file.

Don’t forget to stage and commit.

### 15.7.3.14. Step 14: Pulling the Merged Code[](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#step-14-pulling-the-merged-code "Permalink to this headline")

**Pilot**: Meanwhile, Pilot is sitting at home, minding their own business. A random  `git  status`  seems reassuring:
```
$ git status
On branch main
Your branch is up-to-date with 'origin/main'.
nothing to commit, working directory clean
```
Your local Git thinks the status is quo. Little does it know that up at GitHub, the status is not quo. We’d find this out by doing either a  `git  fetch`, or if we just want the latest version of this branch,  `git  pull`:
```
$ git pull
remote: Counting objects: 13, done.
remote: Compressing objects: 100% (8/8), done.
remote: Total 13 (delta 4), reused 13 (delta 4), pack-reused 0
Unpacking objects: 100% (13/13), done.
From Github.com:chrisbay/communication-log
   0c21659..e0de62d  main     -> origin/main
Updating 0c21659..e0de62d
Fast-forward
communication-log.sln | 3 ++-
1 file changed, 4 insertions(+), 3 deletions(-)
```
Great Scott! Looks like Control changed the  `communication-log`. Note that  _Pilot_  didn’t have to deal with the hassle of resolving merge conflicts. Since Control intervened, Git assumes that the team is okay with the way they resolved it, and  _fast forwards_  our local repo to be in sync with the remote one. Let’s look at  `communication-log.sln`  to make sure. What do you see? What color is the text now? Oh my!

### 15.7.3.15. Step 15: More Merge Conflicts ![](https://education.launchcode.org/intro-to-programming-csharp/chapters/git/studio.html#step-15-more-merge-conflicts "Permalink to this headline")

Let’s turn the tables on the steps we just carried out, so Pilot can practice resolving merge conflicts.

1.  **Control and Pilot**: Confer to determine the particular lines in the code that you will both change. Make different changes in those places.
2.  **Control**: Stage, commit, and push your changes.
3.  **Pilot**: Try to pull in Control’s changes, and notice that there are merge conflicts. Resolve these conflicts as we did above (ask Control for help, if you’re uncertain about the process). Then stage, commit, and push your changes.
4.  **Control**: Pull in the changes that Pilot pushed, including the resolved merge conflicts.

Merge conflicts are a part of the process of team development. Resolve them carefully in order to avoid bugs in your code.






























