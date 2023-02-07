# CODELAB: Init, Pushing and Pulling

# Create a GitHub account

GitHub is currently the most popular online service for hosting public and private Git repositories. Public repositories are completely free of charge.
While GitHub's main purpose is to host repositories, it has allowed coding to become a more social and fun experience. There are other (very great) alternatives such as GitLab and BitBucket.

## 1. Create an account on GitHub

> If you already have an account on a alternative of GitHub such as Bitbucket or GitLab, you can use that service instead of GitHub.

Go to [GitHub](https://github.com/) and create yourself a free account. 
Make sure to remember your account information since you will it during the complete remainder of the course.

## 2. Create a remote repository
Repositories are a core concept of version control (and thus Git). 
Simply put, it is a place where the history of your work is stored.

1. Login on GitHub/GitLab/... with your account and create a new repository.
2. Name it `switchfully-version-control-git`.
3. Keep the default options.
4. Finalize the creation.
    - By creating a 'repository' on a service like GitHub, you create a placeholder location on which a git repository can be stored.

# Initialize your local git repository

Create a new folder for this codelab in your working directory.

Initialize a local Git repository inside the newly created *codelab* folder.
- Check the slides for the command if you don't remember.

# Check the status and commit your first file

## 1. Git status
To see the current state of your working tree, type the following command into the CMD or Terminal:
```
git status
```
    
This should provide the following output:
```
On branch master
No commits yet
nothing to commit (create/copy files and use "git add" to track)
```

It tells us that we are on the master branch (the default branch created), 
that no previous commit has been made and that Git has nothing to commit. Let us give Git something to commit.

## 3. Create a new directory
Still inside your *codelab* folder, create a new folder / directory using the CMD, Terminal:
```
mkdir version-control
```

Navigate to this directory
```
cd version-control
```

## 3. Create a file
Inside your *version-control* folder, create a new file using the CMD, Terminal:
```
echo hello world > readme.txt
```

This will create a file *readme.txt* in your *version-control* folder. 

Again, check the status of your working tree:
```
git status
```

This should now provide the following output:
```
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        ./

nothing added to commit but untracked files present (use "git add" to track)
```

So, it's detecting there are untracked files present, however it's not showing the name...

1. Let's go one level up in the directory hierarchy.
2. Now, inside the *codelab* folder, again, get the status:
    ```
    On branch master
    
    No commits yet
    
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
    
            version-control/
    
    nothing added to commit but untracked files present (use "git add" to track)
    ```

Git will ignore the context of a directory if the directory doesn't already contain tracked files. 
However, you know by the presence of `version-control/` in `git status` that there are files in there! 

We can however aks Git to also show us the files that are included in the directories using the following command:
```
git status -uall
```

Which will result in:
    
```
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        version-control/readme.txt

nothing added to commit but untracked files present (use "git add" to track)
```

    
Git automatically detects newly created files, however it does not automatically track newly created files.
Git expects us to tell which files to track (and which not).

To make Git track our *readme.txt* file, insert the following command, when inside the *codelab* directory: 
`git add */readme.txt` or `git add *readme.txt` or `git add *` or `git add .`

You can also use the following command if you're inside the *version-control* directory: `git add readme.txt`

**Note:** all these commands will add our file to the stage (in this case: the file will be tracked).
    
After tracking the file, check the working tree status. This should provide the following output:
```
 On branch master
 No commits yet
 Changes to be committed:
   (use "git rm --cached <file>..." to unstage)
         new file:   readme.txt
```

(or `new file:   version-control/readme.txt` if you're not inside the *version-control* directory, but one level up)

Git is now tracking our *readme.txt* file, meaning that from now on Git will be able to keep a complete history of all modifications 
made to this file.
    
## 5. Commit files

Commit your changes, use option *–m* to provide a custom message describing what it is we’re committing:
```
git commit -m "Adding a simple readme file"
```
    
This should provide the following output:
```
[master (root-commit) 6858465] Adding a simple readme file
 1 file changed, 1 insertion(+)
 create mode 100644 readme.txt    
```

The last line of the output shows our file, which was created and now inserted into the local repository. 
The number from the first line, *6858465*, is the SHA-1 key (the shorter version): the unique identifier key for our commit 
that references the commit (object).

# Pushing

We have committed our changes to the local repository. 
However, we're still working completely locally. 
In order to send our changes to the repository we have created on GitHub, 
we have to *push* our changes to that remote repository. 

## 1. Inspect your (local) commits
Before pushing, let us inspect which local commits we have made so far:
```
git log
```

It will show all of our commits in the order we have made them. The last being at the top of the list.
    
This should provide the following output:
```
commit 68584654243a1b934d8d60c86096d802a820a5e7
Author: nielsde <niels@somemail.com>
Date:   Mon Aug 21 18:00:56 2017 +0200

    Adding a simple readme file
```
    
For now, we only have one commit.

For every commit we receive:

1. The SHA-1 unique key (the long version) of the commit. It references the snapshot.
2. The author.
3. The date the commit was made.
4. The commit message.

## 2. Push your commits
We are now ready to push to our remote GitHub repository. 

By doing so, we’ll have stored our complete project (and its entire history) on a remote server (so if our computer crashes, we will still have an online back-up).
Other developers will also be able to clone our work and contribute!

### Add the remote repository

Before adding the remote, check which remotes have already been configured using the following command
```
git remote -v
```
 
Now, let's add the remote GitHub repository, we will name it `origin`, which is the default name for your main remote.
As the remote address, use the url that is shown on the 'Quick Setup' page of your remote repository on GitHub:
```
git remote add origin https://github.com/<username>/switchfully-version-control-git.git
```

Now, again, check the remotes that have been configured:
```
git remote -v
```

Try the same command, leaving out the `-v` option. See how it's less informative.


**Note**: Adding your remote repository address is something you normally do only once for every local repository.

### Push (it real good)  
We can now *push*. By specifying the name of the remote (origin) and the branch name (master) 
we will push our changes from master branch on the local repository to the master branch on the remote repository. 
```
git push origin master
```
    
When your push is complete, go on GitHub and refresh your repository page. 
In the 'Code' tab, you should see your *readme.txt* file.

**Note**: Multiple local commits can be made before doing a single push to the remote repository.

# Pulling

With the *push* command we send our local changes to the remote repository. 
With *pull* we do the opposite, retrieving changes from the remote repository to our local repository.

## 1. Pull before push

Before *pushing*, your local repository should be up to date with the latest changes from the remote repository.
 
Imagine, after some time, another developer from its own computer *clones* the remote repository, edits the *readme.txt* file 
and *pushes* it back to the remote repository. From then on, the *readme.txt* file that is located on your computer is "outdated". 
It will remain outdated until you *pull* (update) changes from the remote repository.

## 2. Pull command

To pull changes from the remote repository:
```
git pull origin master
```
    
You will get the message `Already up-to-date`, since no one made any changes to your remote repository.
Your local repository has the exact same changes as the remote repository.

## 3. Pull changes

To mimic a situation where someone else did make changes to the *readme.txt* file on your remote repository:
- Go to the repository page on GitHub (GitLab,... will have a similar feature)
- Click on the *readme.txt* file
- When on the *readme.txt* page, click on the pencil icon (right side) to edit the file
- Change the text to *goodbye world* (yes, we're intentionally leaving out the *cruel* part. #NoDrama)
- Scroll down to the *commit changes* button and click it. 
- We now have an updated version of the *readme.txt* file on the remote repository

Open the *readme.txt* on your computer, validate that it still has the text *hello world*

Now, pull again from the remote repository:
```
  git pull origin master
```

- This should provide the following output:
```
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/<username>/switchfully-version-control-git
   6d5d88e..476eaff  master     -> origin/master
Updating 6d5d88e..476eaff
Fast-forward
 readme.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

- The most important thing to notice is that Git shows the total amount and names of the files changed (last 2 lines). 

**NOTE**: Since the local *readme.txt* was unmodified, Git had no problem with merging the local *readme.txt* with the new data 
from the remote *readme.txt* file. However, if both the local and the remote *readme.txt* would have been changed, 
this could have potentially led to merge conflicts.
We'll discuss merging later on.

## 4. You're done!

Feel free to experiment some more by adding and modifying files and pushing them to your remote repository.
When you're done, head over to the next codelab that will cover cloning an existing repository.
