# Basic Git Commands

## git status

Used to get a list of the currently editied, and staged files, as well as your branches status compared to the GitHub version.

```
 1        On branch master
 2        Your branch is ahead of 'origin/master' by 1 commit.
 3          (use "git push" to publish your local commits)
 4        Changes to be committed:
 5          (use "git reset HEAD <file>..." to unstage)
 6
 7            new file:   file2.html
 8
 9        Untracked files:
10          (use "git add <file>..." to include in what will be committed)
11
12            file3.html
13
14        jassok@Kyles-MacBook-Pro gitTeaching (master) $ 
```

**Breakdown**
    
    LN 1: Tells you what branch you are currently on.
    
    LN 2: Tells you where your verion is in relation to the repository on github.com
    
    LN 4: This begins the list of files that have been added, or modified in your current commit, but have not recieved a a commit message. Files in here will show up as green in terminal. These files must be commited before they will be pushed to the server.
    
    LN 9: Files listed under here, are files that are newly added, or modified but have not yet been staged. These files will be inored on the next push unless you add, and commit them.
    
## git add

Adding, is how you will stage a file to be commited. Inorder to do this,  you can either add each file on its own, if you only want to push up specific files:

``` git add file3.html ```

Or you can add all modified files at one:

``` git add . ```

Files that have been added, will appear green upon doing a `git status` and are ready to have a message added to them.

## git commit

Once a file(s) have been staged, a message needs to be added to them. The message should be fairly descriptive, incase we need to revert to a previous version. A commit can be done with the following command:

``` git commit -m "adding two new files to the repo" ```

As soon as you commit the files, a record is created in git, so that we can return to this point at any time. 
