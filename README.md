# Basic Git Commands

## git status

Used to get a list of the currently editied, and staged files, as well as your branches status compared to the GitHub version.

```bash
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

```bash 
git add file3.html 
```

Or you can add all modified files at one:

``` git add . ```

Files that have been added, will appear green upon doing a `git status` and are ready to have a message added to them.

## git commit

Once a file(s) have been staged, a message needs to be added to them. The message should be fairly descriptive, incase we need to revert to a previous version. A commit can be done with the following command:

``` git commit -m "adding two new files to the repo" ```

As soon as you commit the files, a record is created in git, so that we can return to this point at any time. 

## git push

After you've staged all your changes, and commited them, you're ready to push them up to github with the command `git push`. This can, however, return an error. Generally, the error that occours is because the repo on github, has information you don't. In that case, the error message will look something like this:

```bash
To git@github.com:jassok/gitTeaching.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'git@github.com:jassok/gitTeaching.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

In the following case, git tells us that the push failed, and gives us a suggestion as to what we should do next. If you don't receive an error, you will see something along the lines of this:

```bash
Counting objects: 7, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (7/7), 807 bytes | 0 bytes/s, done.
Total 7 (delta 1), reused 0 (delta 0)
To git@github.com:jassok/gitTeaching.git
   6bc21eb..9794593  master -> master
jassok@Kyles-MacBook-Pro gitTeaching (master) $ 
```

Which simply tells you how many files were modified, and how long it took.

## git pull

In the event that your push fails, because you need to pull, or, you're coming back to a project after more than two hours break. It is generally a good idea to do a `git pull` to insure that you have th emost up-to-date files.

When performing a pull, you may run into an error if your files are not commited. Which would look something like this:

```bash
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From github.com:jassok/gitTeaching
   eb46fc8..6bc21eb  master     -> origin/master
error: Your local changes to the following files would be overwritten by merge:
	file2.html
Please, commit your changes or stash them before you can merge.
Aborting
```

This occours, when you have modified a file(s), or staged a file(s) without commiting the changes. Github prevents the pull, to prevent work from being overwritten. In this case, we simply need to `git add` and `git commit -m " "` our changes, then re-perform our git pull.

Upon completing a success full pull, we will recieve a message similar to the following, which will list all the files that have been modified.

```bash
jassok@Kyles-MacBook-Pro gitTeaching (master) $ git pull
Merge made by the 'recursive' strategy.
 README.md | 53 ++++++++++++++++++++++++++++++++++++++++++++++++++++-
 1 file changed, 52 insertions(+), 1 deletion(-)
```

From here, you are free to push, or continue to work as necessary.

Additionally, a pull may run into conflicts, which look somthing like this:

```bash
jassok@Kyles-MacBook-Pro MLCS (master) $ git pull -f
Auto-merging style.css
CONFLICT (content): Merge conflict in style.css
Auto-merging sass/_global.scss
Auto-merging blog/wp-content/themes/lev-html5Blank/header.php
CONFLICT (content): Merge conflict in blog/wp-content/themes/lev-html5Blank/header.php
Automatic merge failed; fix conflicts and then commit the result.
```

If this is the case, you will need to look at each of the files that have a CONFLICT (content) followed by the message "Automatic merge failed" in this case, style.css, and blog/.../header.php from here, proceed with your normal conflict resolution.

After the conflicts have been resolved, you will need to go back through the process of `git add`, `git commit -m " "`, and `git push`

## The -f

You may have noticed, in the previous message, where conflicts were listed the pull command had a `-f` attached to it. This command is similar to the -m in the git commit in that we're telling the command to do something additional. In this case **f**orce. Adding the -f to your `git push -f` or `git pull -f` will tell git that you want you're changes to take precident over whats coming in, or going out. 

It's important to know this option is there, but for the most part you should never use it.

## git log

If you ever need to go back, and check a list of commits to see what was done, you can do so with the command `git log --one-line` which will return something like the following:

```bash
jassok@Kyles-MacBook-Pro gitTeaching (master) $ git log --oneline
9794593 Merge branch 'master' of github.com:jassok/gitTeaching
a9a86c5 added file two
6bc21eb readme part
e8c4033 staging file
eb46fc8 new file
d6ea75a Initial commit
```

The ID keys listed here (random characters at the start) become important for resetting.

## git reset

If a commit is made, that needs to be undone, because it broke things for some reason, you can do so with a `git reset [id]` to sent the project back to a previous version. For example, if adding file two, broke the project, I could reset to the version before it with the following command:

```bash
git rest 6bc21eb
```

This would revert my files, to the state they were at this commit. Again, this is one of those commands that can mess with a lot of things, so be very careful when doing so. Also not, that following a reset, you should be sure to examine the files that were changed. Often times if you add a new file, it wont delete that file from the folder, but the file will no longer be in the repo.

## git branch

Branching, is very important when working with production projects. We typically use 2 branches, master, and development. But in some cases, it's important to have additional branches, if what you're going to work on will potentially break things, or take a long time to complete.

In these cases, you will want to do `git checkout -b branchname` to make a new branch. Its important to note, that whatever branch you are currently on (you can figured that out by running `git branch`) is the branch that will be copied.

## git merge

After completeing work on a particular branch, either development, or another branch. You will need to merge that branch, into its base. For example, if you make a feature branch from development, you should merge it back into development. If if the changes made on development, are ready to go into master, you will do the following:

```bash
git checkout branch-to-merge-into
git merge --no-ff branch-to-merge-in
```

Again, this will return a message similar to a `git pull` with either conflicts, or a success. Once the merge is successful, you can `git push` the changes up to the server.
