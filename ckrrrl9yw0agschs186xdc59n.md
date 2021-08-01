## Important GIT commands you'll need to know 🔥 [Part 1] (for the major part of your work)

👆***NOTE:*** *This blog will be a bit longer as I will be explaining all the commands. Thus I will divide the blog into **two parts** (this being the first one). I will update this part with a link to part 2 once I publish it. Both parts will also contain a **summary** which will contain a list of all the commands mentioned in the blog for a quick revision. *

# 📋 Summary
- `git init`: To initialise a local directory with git.
- `git status`: To check the status of your repo i.e. to see if any file has been edited/ deleted/ added. It also shows all the tracked and untracked files. Stashed changes will not be reflected in `git status`.
- `git add <file name>`/ `git add .`: Adds changes in a particular file/ all changes in the staging area.
- `git commit -m "commit message describing in short what changes are made"`: To commit the changes.
- `git remote add origin <remote repo url>`: Connects local repo to a remote repo.
- `git push -u origin <Local repo name>`: Pushes all the committed changes from the local repo to the remote repo.
- `git remote -v`: Will list down all the remote repos that are linked to the local repo.
- `git branch -a`: To see all the branches in your repo **(local + remote)**.
- `git checkout <branch name>`: To checkout/ see the code in a branch.
- `git checkout -b <branch name>`: Create a new branch with the name `<branch name>` and check out the same branch.


GIT is a very powerful tool or shall I say a very elegant solution ever built to tackle a very complex challenge of version control. As one of my friends once said that the idea of multiple people working on the same product (and that too remotely) is in itself a very complicated job. GIT helps us to ease just that. And that is why it becomes so important to know GIT and all its useful commands.

# What this blog is not about and what it rather actually is about? 👨‍💻
To get this straight this blog is not to introduce you to GIT or what it is meant to do. Rather I assume that you know what is GIT and its basic and thus I'll jump right into the main point of this blog i.e ***what are the most common and important GIT commands that will help you sail through more than 99% of your daily job***.

Now there are mainly two possibilities that we should discuss here before moving forward. 

- One possibility is that **you might want to start a new project**. *This case mainly arises when a developer starts thinking of starting a side project/ or want to do a POC/ or simply follow along with some tutorial. *
- The second possibility is that **you want to contribute to an existing codebase**. *This case can arise when you either want to contribute to an open-source project or you are in a team that is developing an application* *(many folks working in a tech company can relate to this use-case)*. 

![Picture15.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627726905444/Br4qlZsml.png)

## What to do when you want to start a new project. 🤔

- Create a folder for your project.
- Navigate to that folder *(initially the folder will be empty)* and open the git bash terminal in that same location and type `git init`. You will notice that a **.git** folder got created in that directory. This way you can initialise the directory with git and it will now track any changes like file viz. edit/ delete/ add happening in that directory and all its direct children.

### How to track any change in files (new file added/ edited/ deleted), add it to stage and commit it? 🤔
Now that you have initialized a directory with git, it will create a default **master branch** (or **main **branch as it's called in current versions) for you. We will learn about how to make other branches later. For the time being, let's make some changes in the master branch itself.

- To check what is the current status of your local git repo execute the command `git status`. Initially, if there is no change to show, then the following message should be displayed.
![Picture2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627724167366/Neaqx-31JY.png)
- Create a new file in the project root directory by using the command `touch new.txt`. You can also create a file by the normal method of right-clicking in the directory and creating the desired file.
- Now execute `git status` and it will show you that a new file has been added to the directory. It will be shown in red as the change is still not in the staging area of git. 
- To add any new change in the staging area execute the command `git add <file name>`. You can also do `git add .` to add all the changes in the staging area. Once added, if you run `git status`, it will show the change in a green colour denoting that the change is now in the staging area.
- To commit any change to the branch you have to execute the command `git commit -m "your commit message describing in short what changes are made"`. Doing a `git status` at this point (after committing) will show that there is no more change to commit (provided that you have added all the changes to staging are and then committed them) and the working tree (master branch in this case) is clean.

Please note 👆 that staging is a way of us saying to git to **keep a track** of a particular file. So in case, a completely new file is added we **HAVE **to add it to the staging area at least once using `git add <filename>` or by `git add .`. Before we add the file in the staging area `git status` will show the file in the **"Untracked file"** section as shown in the image below. 

But once the file has been added to the staging area at least once, any further change in the file will make it show in the **"Changes not staged for commit"** section, but the file is being tracked. So to commit any subsequent change of the file in the working tree, we can directly run the command `git commit -am "Commit message"`. For eg. if I edit the previous file (new.txt) and also create a new file say "newfile.txt" in the root then `git status` will show the following. 

![Picture4.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627724689499/ILu4vLmM1.png)
As you can see that "new.txt" is in the "Changes not staged for commit" section as I had already `git add` this file previously and have just edited it now, whereas, on the other hand, I added a completely new file which is now showing in the **"Untracked file"** section. Running `git commit -am "Commit message"` command will only commit the changes in the tracked file "new.txt" and will NOT commit the "newfile.txt" as that is not tracked. We need to add it using `git add newfile.txt` first and then commit it.

## How do I connect a remote repository (repo) to my local git repo? 🤔
In collaborative teamwork, chances are that more than one person is working on a project. In that case, you have to connect your local repo to a remote repo so that everyone can access it. Currently, our repo is in our local and no one can access it. Let connect it to a remote Github repo.

- Create a new Github repo and copy the repo URL as shown in the image below. 

![Picture6.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627725123027/e6w-qHVEN.png)
- In the git bash terminal run the command `git remote add origin <url>`. This will now connect our local repo to the remote repo. Here `origin` is the shortcut name that we assign to the remote Github URL. Thus `origin` = `<remote Github url>`. It is not compulsory though but advised to name the base repo as `origin`. 

### How to push all the changes from local to remote. 🤔
- Run the command `git push -u origin <Local repo name>` i.e in this case `git push -u origin master`. This will push all the committed changes from the local repo to the remote repo. The changes will now get reflected in the remote Github repo as shown below.

![Picture8.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627725476727/i6zXvV-Sh.png)
- Thus `git push -u origin repo-example-name-1` will create a new branch in the remote repo with a name **repo-example-name-1** *(if it is not present already)* and **push all the committed changes** from the **local** branch you ran the command to the **remote branch**. 
- Please note 👆 that in a subsequent execution of `git push -u origin repo-example-name-1` a new branch in the remote repo (with name repo-example-name-1) is not created as it is already present in the remote repo.
- It also sets the **local branch to track the remote branch at the origin**.

Another handy command to keep in your toolbox is the following
### What are all the remote repo you have linked to your local repo? 🤔
- Run the command `git remote -v` and it will list down all the remote repos that are linked to the local repo as shown in the image below. 

![Picture10.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627725850899/GKj85tVDt.png)
It denotes that for all the **push** and **fetch**commands with **origin** git will use the URL **"https://github.com/sohamderoy/demo-repo.git"**


## How to create a new branch? And why should I create a new branch? 🤔
Branches in git is an elegant way for a user to switch between different kinds of tasks. Let's say I have to add two new features in my application viz. a login/ signup screen and a dark mode feature. For both the features let's say I need to work with different sets of files and might have to add totally different sets of logic. In that case, it is advised to create two new branches out of the main branch and work on both the feature separately. If there is a third new feature to add, create another branch for that. Later once the feature is developed, merge that sub-branch into the main branch *(or the branch where your team prefers to keep the latest code like a **develop** or **release** branch for many companies)* 

- `git branch -a`: Run this command to see all the branches in your repo **(local + remote)** . The branches shown in the form `<branch name>` is/ are the **local branch(es)** in the local repo. Similarly, the branches shown in the form `remotes/origin/<branch name>` is/ are the **remote branch(s)** from the remote repo **origin** connected to the local repo. 
- `git checkout <branch name>`: Use this command to checkout/ see the code in a branch.
- `git checkout -b <branch name>`: Create a new branch with the name `<branch name>` and check out the same branch.

![Picture12.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627726255798/KZbaaV33y.png)
As seen in the image above, initially there were only two branches **master** *(local branch)* and **remotes/origin/master** *(remote branch)*. After running the command `git checkout -b new-branch` a new local branch with the name **new-branch** is created. To get this branch on the remote branch run command `git push -u origin new-branch`. 

![Picture14.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1627726586257/rBRHGd-Lo.png)
👆 **NOTE**: 

1. It is advised to keep the name of the local and remote branches the same so that both can be recognised and linked easily.
2. Keep the name of your branch short and descriptive so that anyone can get an idea of what that branch was created for without even looking at the code just by looking at the name.
3. Always create a separate branch for different feature implementation.

*puff!!! that's a lot of branches. don't worry read the section again and I am sure you'll catch the drift.* 🙂

# To be continued...

I'll end Part 1 of this blog here. I hope that the content provided in this part will be helpful to all the readers. In the next part, I'll cover the rest of the git commands which are worth keeping in your toolbelt so stay tuned in. 

*Thanks for reading! If you like this blog and feel it's useful, do consider hitting the link button and share it with your friends, I'd really appreciate that. Stay tuned! * 🖖





