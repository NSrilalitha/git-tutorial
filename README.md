# git-tutorial

https://www.atlassian.com/git/tutorials/learn-git-with-bitbucket-cloud

https://git-scm.com/docs/gittutorial

Git cheatsheet: https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf

A Git project can be thought of as having three parts:

1.A Working Directory: where you'll be doing all the work: creating, editing, deleting and organizing files

2.A Staging Area: where you'll list changes you make to the working directory

3.A Repository: where Git permanently stores those changes as different versions of the project

Git commands
------------
1. To know the version of git installed use below command

        git --version


2. configure your name and email

        git config --global user.name "Srilalitha Nittala"

        git config --global user.email "srilalitha.nittala@gmail.com"

these details needs to be updated in .gitconfig file as well.

---------------
repositories:
1. local repository : The repository which you work in your local machine is called local repository. We can get local repository either by cloning it from remote repository
    or we can initialize the repository using git init command.
2. remote repository : The repository which is available in GitHub/BitBucket is called remote repository. The default remote repository is called origin. The default branch
   is called master.
----------------


3. inorder to track changes using git, we have initialize that specific project folder with below command

        git init

this creates .git folder which stores information about this repository. git init initializes the repository as a new Git repository

Clone repository
----------------
Inorder to clone any repository for the first time, we need SSH or HTTPS url

lets say i have angular5-tutorial repository in GitHub

the https url for this repository is
https://github.com/NSrilalitha/angular5-tutorial.git

the SSH to clone this repository is
we need to create one public SSH key in GitHub account and then we can use
git@github.com:NSrilalitha/angular5-tutorial.git

eg:
        git clone https://github.com/NSrilalitha/angular5-tutorial.git
        (or)
        git clone git@github.com:NSrilalitha/angular5-tutorial.git

for the first time it will give a prompt to enter password

After cloning repository from GitHub to local system, repository will be local repository.
GitHub repository is called remote repository by default name will be origin


4. to know the status of the files in the repository use below command

        git status
        
   there is another command which gives brief information on any changes that you have made. git status inspects the contents of the working directory and staging area
   
        git diff
        
   git diff shows the difference between the working directory and the staging area

Adding another remote repository to your local repository
---------------------------------------------------------
A remote is a Git repository that lives outside your Git project folder. Remotes can live on the web, on a shared network or even in a separate folder on your local computer. 

The Git Collaborative Workflow are steps that enable smooth project development when multiple collaborators are working on the same Git project. 

1.git clone: Creates a local copy of a remote.

2.git remote -v: Lists a Git project's remotes. 

3.git fetch: Fetches work from the remote into the local copy.

4.git merge origin/master: Merges origin/master into your local branch.

5.git push origin <branch_name>: Pushes a local branch to the origin remote.

To add another remote repository other than origin, we can use git remote add command as shown below.

        git remote add staging git://git.kernel.org/.../gregkh/staging.git
        
        here staging -> remote repository name
        git://git.kernel.org/.../gregkh/staging.git -> remote repository url
        
        to access this remote repository instead of url each time we can use given name 'staging'
        
 To fetch changes from this remote repository we can use fetch command as shown below
 
        git fetch staging
        
Adding files to staging area
----------------------------
5. inorder to add files to staging area use below command

        git add filename

    eg: git add index.html

to add all files to the staging area use below command

        git add .

git add adds files from the working directory to the staging area

now do git status
staged files shown in green color and it tells changes to be committed or 
use git rm --cached <file> to unstage the file

Committing changes
--------------
6. committing changes

        git commit -m "commit message"

git commit permanently stores file changes from the staging area in the repository
In order to view details about particular commit we can use show command

        git show <commit-hash>

log history
-----------
to know the history of commits use below commands

        git log
        
If you want complete diff at each step use below command

        git log -p


7. go back to previous commit/any commit we wanted
To go back to state of previous commit, use below command

        git checkout <commit-hash>

Branches
--------
main branch -> called as master

8. to get the list of branches use below command

        git branch

here star(*) indicates active branch that we are working on

9. to create a new branch use below command

        git branch <new-branch-name>
        eg: git branch crazycolors
  
10. to move to specific branch use below command

        git checkout <branch-name>

now move to new branch and make changes in that branch
git checkout crazycolors

Merge branches
---------------
inorder to merge the new branch to master first move to master and then merge new branch

    step1: move to master

    git checkout master

    step2: merge new branch

    git merge crazycolors

this will merge all changes in crazycolors branch to master branch

11. to delete a branch use -d flag with below command

        git branch -d crazycolors


Push the changes from local repository to remote repository
-----------------------------------------------------------
12. Inorder to push changes from your local repository to your github remote repository (origin)
    use push command as shown below

        git push origin master

here origin -> remote repository
master -> branch name


Pull changes from remote repository (i.e., from GitHub)
--------------------------------------
suppose the remote repository has latest changes which u dont have in your local
repository. Inorder to update your local repository with latest changes take pull

    git pull --all

The git pull command merges the file from your remote repository (GitHub) into your local repository with a single command.
The "pull" command thus performs two operations: it fetches changes from a remote branch, then merges them into the current branch.
 
 If you have uncommitted changes in your local repository, then when you try to pull you may end up with conflicts if the same file is modified in your local and in remote
 repository. In such cases, instead of directly pulling the changes we can use fecth. git fetch will show the changes in remote repository without merging it to local files
 
        git fetch
 
Resolving merge conflicts
--------------------------
When a merge isn’t resolved automatically, Git leaves the index and the working tree in a special state that gives you all the information you need to help resolve the merge.

Also, git-status will list those files as "unmerged", and the files with conflicts will have conflict markers added, like this:

        <<<<<<< HEAD:file.txt
        Hello world
        =======
        Goodbye
        >>>>>>> 77976da35a11db4580b80ae27e8d65caf5208086:file.txt
        
All you need to do is edit the files to resolve the conflicts, and then

        $ git add file.txt
        $ git commit
        
This will resolve the simple merge conflicts.

All of the changes that Git was able to merge automatically are already added to the index file, so git-diff shows only the conflicts. It uses an unusual syntax:

        $ git diff
        diff --cc file.txt
        index 802992c,2b60207..0000000
        --- a/file.txt
        +++ b/file.txt
        @@@ -1,1 -1,1 +1,5 @@@
        ++<<<<<<< HEAD:file.txt
        +Hello world
        ++=======
        + Goodbye
        ++>>>>>>> 77976da35a11db4580b80ae27e8d65caf5208086:file.txt
        
Stash your changes
-------------------
Whenever you want to take pull, inorder to avoid conflicts, first stash your changes. Stash will save all your local uncommitted changes to some temporary location. Then take pull and update your branch with remote repository latest changes. After taking new changes then apply your stash changes so that the branch gets updated with remote repository latest changes and your latest changes. Then you can commit your changes.

        Step1: stash your local uncommitted changes
                git stash
                
        Step2: Take updates from remote repository either origin or any other remote repository
                git pull 
                
        Step3: Apply your stashed changes
                git stash apply
                
        Step4: To see all files that needs to be committed, and file modifications either use git status or git diff commands
        
        Step5: Commit your changes
                git add .
                git commit -m "committing latest changes"
                
        Step6:  Push the changes to remote repository
                git push origin master
                (or)
                git push staging master
                
git reset
-----------
With git add command we can add all our changes to staging area. Git reset command will remove the changes from staging area and show those files as untracked. Suppose by mistake if we some files to staging area. If we dont want those files to be committed, then you can remove those changes from staging area.

        git reset
        
This does opposite of git add command



The Git workflow consists of editing files in the working directory, adding files to the staging area, and saving changes to a Git repository. In Git, we save changes with a commit

1. git checkout HEAD filename: Discards changes in the working directory.It will restore the file in your working directory to look exactly as it did when you last made a commit.

2. git reset HEAD filename: Unstages file changes in the staging area.This command resets the file in the staging area to be the same as the HEAD commit. It does not discard file changes from the working directory, it just removes them from the staging area.

3. git reset SHA: Can be used to reset to a previous commit in your commit history. 

4. way to add multiple files to the staging area with a single command: git add filename_1 filename_2


