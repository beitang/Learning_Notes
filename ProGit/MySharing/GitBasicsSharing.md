# Git Basics

## Snapshots, Not Differences
> Most other systems store information as a list of file-based changes. These systems think of the information they keep as a set of files and the changes made to each file over time.
>
> ![deltas](https://github.com/beitang/Learning_Notes/blob/master/ProGit/MySharing/Figure_1-4_deltas.png "deltas")
> 
> Figure 1-4. Storing data as changes to a base version of each file.
>
> Git thinks of its data more like a set of snapshots of a miniature filesystem. Every time you commit, or save the state of your project in Git, it basically takes a picture of what all your files look like at that moment and stores a reference to that snapshot. To be efficient, if files have not changed, Git does not store the file again, just a link to the previous identical file it has already stored. Git thinks about its data more like a stream of snapshots.
>
> ![snapshots](https://github.com/beitang/Learning_Notes/blob/master/ProGit/MySharing/Figure_1-5_snapshots.png "snapshots")
> 
> Figure 1-5. Storing data as snapshots of the project over time.

## Nearly Every Operation Is Local
> ![centralized](https://github.com/beitang/Learning_Notes/blob/master/ProGit/MySharing/Figure_1-2_centralized.png "centralized")
> 
> Figure 1-2. Centralized version control.
> 
> ![distributed](https://github.com/beitang/Learning_Notes/blob/master/ProGit/MySharing/Figure_1-3_distributed.png "distributed")
> 
> Figure 1-3. Distributed version control.
> 
> Most operations in Git only need local files and resources to operate - generally no information is needed from another computer on your network. If you are used to a CVCS where most operations have that network latency overhead, this aspect of Git will make you think that the gods of speed have blessed Git with unworldly powers. Because you have the entire history of the project right there on your local disk, most operations seem almost instantaneous.

Local Operation: maybe some commands supporting non-local operation by specific parameters
```
git log
git diff
git config
git help
git commit
git add
git rm
git mv
git reset
git status
git checkout
```

Non-local Operation
```
git clone
git pull
git push
```

Not-sure?
```
git branch
```

## Git Has Integrity
> Everything in Git is check-summed before it is stored and is then referred to by that checksum. This means it is impossible to change the contents of any file or directory without Git knowing about it. This functionality is built into Git at the lowest levels and is integral to its philosophy. You can not lose information in transit or get file corruption without Git being able to detect it.
> 
> The mechnism that Git uses for this checksumming is called a SHA-1 hash. This is a 40-character string composed of hexadecimal characters (0-9 and a-f) and calculated based on the contencts of a file or directory structure in Git.
> 
> In fact, Git stores everything in its database not by file name but by the hash value of its contents.

## Git Generally Only Adds Data
> When you do actions in Git, nearly all of them only add data to the Git database. It is hard to get the system to do anything that is not undoable or to make it erase data in any way. As in any VCS, you can lose or mess up changes you have not committed yet; but after you commit a snapshot into Git, it is very difficult to lose, especially if you regularly push your database to another repository.
> 
> This makes using Git a joy because we know we can experiment without the danger of severely screwing things up.

## The Three States
> This is the main thing to remember about Git if you want the rest of your learning process to go smoothly. Git has three main states that your files can reside in: committed, modified, and staged. Committed means that the data is safely stored in your local database. Modified means that you have changed the file but have not committed it to your database yet. Staged means that you have marked a modified file in its current version to go into your next commit snapshot.
> 
> This leads us to the three main sections of a Git project: the Git directory, the working directory, and the staging area.
> 
> ![areas](https://github.com/beitang/Learning_Notes/blob/master/ProGit/MySharing/Figure_1-6_areas.png "areas")
> 
> Figure 1-6. Working directory, staging area, and Git directory.
> 
> The Git directory is where Git stores the metadata and object database for your project. This is the most important part of Git, and it is what is copied when you clone a respository from another computer.
> 
> The working directory is a single checkout of one version of the project. These files are pulled out of the compressed database in the Git directory and placed on disk for you to use or modify.
> 
> The staging area is a file, generally contained in your Git directory, that stores information about what will go into your next commit.
> 
> The basic Git workflow goes something like this:
> 
> 1. You modify files in your working directory.
> 
> 2. You stage the files, adding snapshots of them to your staging area.
> 
> 3. You do a commit, which takes the files as they are in the staging area and stores that snapshot permanently to your Git directory.
> 
> If a particular version of a file is in the Git directory, it is considered committed. If it has been modified and was added to the staging area, it is staged. And if it was changed since it was checked out but has no been staged, it is modified.

# Getting Help
```
git help <verb>
git <verb> --help
man git-<verb>
```

# Recording Changes to the Repository
> Remember that each file in your working directory can be in one of two states: tracked or untracked. Tracked files are files that were in the last snapshot; they can be unmodified, modified, or staged. Untracked files are everything else - any files in your working directory that were not in your last snapshot and are not in your staging area. When you first clone a repository, all of your files will be tracked and unmodified because Git just checked them out and you have not edited anything.
> 
> As you edit files, Git sees them as modified, because you are changed them since your last commit. You stage these modified files and then commit all your staged changes, and the cycle repeats.
> 
> ![lifecycle](://github.com/beitang/Learning_Notes/blob/master/ProGit/MySharing/Figure_2-1_lifecycle.png "lifecycle")
> 
> Figure 2-1. The lifecycle of the status of your files.

## Checking the Status of Your Files
`git status`
> The command also tells you which branch you are on and informs you that it has not diverged from the same branch on the server.
> 
> Untracked basically means that Git sees a file you did not have in the previous snapshot (commit); Git will not start including it in your commit snapshots until you explicitly tell it to do so. It does this so you do not accidentally begin including generated binary files or other files that you did not mean to include.

## Tracking New Files
`git add README`

## Staging Modifed Files
> `git add` is a multipurpose command - you use it to begin tracking new files, to stage files, and to do other things like marking merge-conflicted files are resolved. It may be helpful to think of it more as "add this content to the next commit" rather than "add this file to the project".

## Viewing Your Staged and Unstaged Changes
```
git diff
git diff --staged
```

## Committing Your Changes
```
git commit
git commit -m "commit messages"
```

## Skipping the Staging Area
`git commit -a -m "commit messages"`
> `-a` flag includes all changes files. This is convenient, but be careful; sometimes this flag will cause you to include unwanted changes.

## Removing Files
`git rm`

## Moving Files
> Unlike many other VCS systems, Git does not explicitly track file movement. If you rename a file in Git, no metadata is stored in Git that tells it you renamed the file.

```
git mv file_from file_to

mv README.md README
git rm README.md
git add README
```

> Git figures out that it is a rename implicitly.

# Viewing the Commit History
```
git log
git log --since=2.weeks
git log file_name
git log --author=gitster
git log -p -2
```
`-p` which shows the difference introduced in each commit, `-2` which limits the output to only the last two entries.

# Undoing Things
> Be careful, because you can not always undo some of these undos. This is one of the few areas in Git where you may lose some work if you do it wrong.
> 
> One of the common undos takes place when you commit too early and possibly forget to add some files, or you mess up your commit message. If you want to try that commit again, you can run commit with `--amend` option: `git commit --amend`
>
> This command takes your staging area and uses it for the commit.

## Unstaging a Staged File
`git reset HEAD <file>...`
if with --hard, dangerous

## Unmodifying a Modified File
`git checkout -- <file>...` dangerous, will lose your local changes
> Remember, anything that is committed in Git can almost always be recovered. Even commits that were on branches that were deleted or commits that were overwritten with an --amend commit can be recovered. However, anything you lost that was never committed is likely never to be seen again.

# Questions and To Learn
* If `git commit --amend` to the wrong commit, hwo to deal with it?
* `git pull` and `git pull --rebase` difference
* Remote and branch
* How to fix conflicts?
