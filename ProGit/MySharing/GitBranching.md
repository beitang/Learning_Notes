# Git Branching
> Branching means you diverge from the main line of development and continue to do work without messing with that main line.
> 
> Some people refer to Git branching model as its "killer feature, " and it certainly sets Git apart in the VCS community. Why is it so special? The way Git branches is incredibly lightweight making branching operations nearly instantaneous, and switching back and forth between branches generally just as fast.

## Branches in a Nutshell
> When you make a commit, Git stores a commit object that contains a pointer to the snapshot of the content you staged. This object also contains the author name and email, the message that you typed, and pointers to the commit or commits that directly came before this commit (its parent or parents): zero parents for the initial commit, one parent for a normal commit, and multiple parents for a commit that results from a merge of two or more branches.
> 
> When you create the commit by running `git commit`, Git checksums each subdirectory and stores those tree objects in the Git repository. Git then creates a commit object that has the metadata and a pointer to the root project tree so it can re-create that snapshot when needed.
> 
> Your Git repository now contains five objects: one blob for the contents of each of your three files, one tree that lists the contents of the directory and specifies which file names are stored as which blobs, and one commit with the pointer to that root tree and all the commit metadata.
> 
> Figure 3-1. A commit and its tree
> 
> If you make some changes and commit again, the next commit stores a pointer to the commit that came immediately before it.
> 
> Figure 3-2. Commits and their parents
> 
> A branch in Git is simply a lightweight movable pointer to one of these commits. The default branch name in Git is master.

### Creating a New Branch
> What happens if you create a new branch? Well, doing so creates a new pointer for you to mmove around.
> 
> `git branch testing`: This creates a new pointer to the same commit you are currently on.
> 
> How does Git know what branch you are currently on? It keeps a special pointer called `HEAD`.
> 
> The `git branch` command only created a new branch - it did not switch to that branch.
> 
> You can easily see this by running a simple `git log` command that shows you where the branch pointers are pointing. This option is called `--decorate`.
> 
> `git log --oneline --decorate`

### Switching Branches
> To switch to an existing branch, you run the `git checkout` command.
> 
> `git checkout testing` This moves `HEAD` to point to the testing branch.
> 
> Figure 3-7. The HEAD branch moves forwardd when a commit is made
> 
> Figure 3-8. HEAD moves when you checkout
> 
> That command did two things. It moves the HEAD pointer back to point to the master branch, and it reverted the files in your working directory back to the snapshot that master points to. This also means the changes you make from this point forward will diverge from an older version of the project. It essentially rewinds the work you are done in your testing branch so you can go in a different direction.
> 
> If you run `git log --oneline --decorate --graph --all` it will print out the history of your commits, showing where your branch pointers are and how your history has diverged.
> 
> Because a branch in Git is in actually a simple file that contains the 40 character SHA-1 checksum of the commit it points to, branches are cheap to create and destroy. Creating a new branch is as quick and simple as writing 41 bytes to a file (40 characters and a newline).

## Basic Branching and Merging
### Basic Branching
> To create a branch and switch to it at the same time, you can run the `git checkout` command with the `-b` switch
> 
> Note that if your working directory or staging area has uncommitted changes that conflict with the branch you are checking out, Git will not let you switch branches. It is best to have a clean working state when you switch branches.
> 
> Merge it back into your master branch to deploy to production. You do this with the `git merge` command. `git checkout master`, `git merge hotfix`
> 
> You will notice the phrase "fast-forward" in that merge. Because the commit C4 pointed to by the branch hotfix you merged in was directly ahead of the commit C2 you are on, Git simply moves the pointer forward. To phrase that another way, when you try to merge one commit with a commit that can be reached by following the first commit history, Git simplifies things by moving the pointer forward because there is no divergent work to merge together -- this is called a "fast-forward."
> 
> You can delete the branch with the `-d` option to `git branch`: `git branch -d hotfix`

### Basic Merging
> In this case, your development history has diverged from some older point. Because the commit on the branch you are on is not a direct ancestor of the branch you are merging in, Git has to do some work. In this case, Git does a simple three-way merge, using the two snapshots pointed to by the branch tips and the common ancestor of the two.
> 
> Figure 3-16. Three snapshots used in a typical merge
> 
> Instead of just moving the branch pointer forward, Git creates a new snapshot that results from this three-way merge and automatically creates a new commit that points to it. This is referred to as a merge commit, and is special in that it has more than one parent.
> 
> Figure 3-17. A merge commit
> 
> It is worth pointing out that Git determines the best common ancestor to use for its merge base.

### Basic Merge Conflicts
> If you changed the same part of the same file differently in the two branches you are merging together, Git will not be able to merge them cleanly.
> 
> Git has not automatically created a new merge commit. It has paused the process while you resolve the conflict. If you want to see which files are unmerged at any point after a merge conflict, you can run `git status`.
> 
> Anything that has merge conflicts and has not been resolved is listed as unmerged. Git adds standard conflict-resolution markers to the files that have conflicts, so you can open them manually and resolve those conflicts.
> 
> After you have resolved each of these sections in each conflicted files, run `git add` on each file to mark it as resolved. Staging the file marks it as resolved in Git.
> 
> If you are happy with that, and you verify that everything that had conflicts has been staged, you can type `git commit` to finalize the merge commit.

## Branch Management
> `git branch`: a simple listing of your current branches, the * indicates the branch that you currently have checked out.
> 
> `git branch -v`: see the last commit on each branch
> 
> `git branch --merged`: see which branches are already merged into the branch you are on, branches on this list without the * in the front of them are generally find to delete with `git branch -d`
> 
> `git branch --no-merged`: see all the branches that contain work you have not yet merged in, trying to delete it with `git branch -d` will fail. If you really do want to delete the branch and lose that work, you can force it with `-D`, as the helpful message points out.

## Branching Workflows
### Long-Running Branches
> Such as having only code that is entirely stable in their `master` branch - possibly only code that has been or will be released. They have another parallel branch named `develop` or `next` that they work from or use to test stability - it is not necessarily always stable, but whenever it gets to a stable state, it can be merged into `master`. It is used to pull in topic branches when they are ready, to make sure they pass all the tests and do not introduce bugs.
> 
> You can keep doing this for several levels of stability.
> 
> The idea is that your branches are at various levles of stability; when they reach a more stable level, they are merged into the branch above them. Again, having multiple long-running branches is not necessary, but it is often helpful, especially when you are dealing with very large or complex projects. 

### Topic Branches
> Topic branches, however, are useful in projects of any size. A topic branch is a short-lived branch that you create and use for a single particular feature or related work.
> 
> It is important to remember when you are doing all this that these branches are completely local. When you are branching and merging, everything is being done only in your Git repository - no server communication is happening.

## Remote Branches
> Remote references are references (pointers) in your remote repositories, including branches, tags, and so on. You can get a full list of remote references explicitly with `git ls-remmote [remote]`, or `git remote show [remote]` for remote branches as well as more information. Nevertheless, a more common way is to take advantage of remote-tracking branches.
> 
> Remote-tracking branches are references to the state of remote branches. They are local references that you can not move; they are moved automatically for you whenever you do any network communication. Remote-tracking branches act as bookmarks to remind you where the branches in your remote repositories were the last time you connected to them.
> 
> They take the for (remote)/(branch).
> 
> If you clone from this, Git `clone` command automatically names it `origin` for you, pulls down all its data, creates a pointer to where its `master` branch is, and names it `origin/master` locally. Git also gives you your own local `master` branch starting at the same place as origin `master` branch, so you have somethign to work from.
> 
> "origin" is not special: While "master" is the default name for a starting branch when you run `git init` which is the only reason it is widely used, "origin" is the default name for a remote when you run `git clone`.
> 
> Figure 3-22. Server and local repositories after cloning
> 
> If you do some work on your local `master` branch, and, in the meantime, someone else pushes to `git.ourcompany.com` and updates its `master` branch, then your histories move forward differently. Also, as long as you stay out of contact with your origin server, your `origin/master` pointer does not move.
> 
> Figure 3-23. Local and remote work can diverge
> 
> To synchronize your work, you run a `git fetch origin` command. This command looks up which server `origin` is, fetches any data from it that you do not yet have, and updates your local database, moving your `origin/master` pointer to its new, more up-to-date position.
> 
> Figure 3-24. `git fetch` updates your remote references

### Pushing
> When you want to share a branch with the world, you need to push it up to a remote that you have write access to. Your local branches are not automatically synchronized to the remotes you write to - you have to explicitly push the branches you want to share.
> 
> `git push <remote> <branch>`
> 
> `git push origin serverfix`: This is a bit of a shortcut. Git automatically expands the `serverfix` branchname out to `refs/heads/serverfix:refs/heads/serverfix`, which means, "Take my serverfix local branch and push it to update the remote serverfix branch."
> 
> Do not type your password every time. `git config --global credential.helper cache`
> 
> `git merge origin/serverfix`
> 
> `git checkout -b serverfix origin/serverfix`

### Tracking Branches
> Checking out a local branch from a remote-tracking branch automatically creates what is called a "tracking branch" (and the branch it tracks is called an "upstream branch"). Tracking branches are local branches that have a direct relationship to a remote branch. If you are on a tracking branch and type `git pull`, Git automatically knows which server to fetch from and branch to merge into.
> 
> When you clone a repository, it generally automatically creates a `master` branch that tracks `origin/master`. However, you can set up other tracking branches if you wish.
> 
> The simple case is the example you just saw, running `git checkout -b [branch] [remotename]/[branch]`. This is a common enough operation that git provides the `--track` shorthand: `git checkout --track origin/serverfix`
> 
> In fact, this is so common that there is even a shortcut for that shortcut. If the branch name you are trying to checkout does not exist and exactly matches a name on only one remote, Git will create a tracking branch for you: `git checkout serverfix`
> 
> To set up a local branch with a different name than the remote branch: `git checkout -b sf origin/serverfix`
> 
> If you want to see what tracking branches you have set up: `git branch -vv`, this will list out your local branches with more information including what each branch is tracking and if your local branch is ahead, behind or both.
> 
> It is important to note that these numbers are only since the last time you fetched from each server. This command does not reach out to the servers, it is telling you about what it has cached from these servers locally.

### Pulling
> While the `git fetch` command will fetch down all the changes on the server that you do not have yet, it will not modify your working directory at all. It will simply get the data for you and let you merge it yourself. However, there is a command called `git pull` which is essentially a `git fetch` immediately followed by a `git merge` in most cases.

### Delete Remote Branches
> `git push origin --delete serverfix`
> 
> Basically all this does is remove the poinster from the server. The Git server will generally keep the data there for a while until a garbage collection runs, so if it was accidently deleted, it is often easy to recover.

## Rebasing
> In Git, there are two main ways to integrate changes from one branch into another: the `merge` and the `rebase`. In this section you will learn what rebasing is, how to do it, why it is a pretty amazing tool, and in what cases you will not want to use it.

### The Basic Rebase
> You can take the patch of the change that was introduced in C4 and reapply it on top of C3. In Git, this is called rebasing. With the `rebase` command, you can take all the changes that were committed on one branch and replay them on another one.
> 
> Figure 3-29. Rebasing the change introduced in C4 onto C3
> 
> There is no difference in the end product of the integration, but rebasing makes for a cleaner history. If you examine the log of a rebased branch, it looks like a linear history; it appears that all the work happened in series, even when it originally happened in parallel.
> 
> Note that the snapshot pointed to by the final commit you end up with, whether it is the last of the rebased commits for a rebase or the final merge commit after a merge, is the same snapshot - it is only the history that is different. Rebasing replays changes from one line of work onto another in the order they were introduced, whereas merging takes the endpoints and merges them together.

### More Interesting Rebases
> `git rebase --onto master server client`: This basically says, "Check out the client branch, figure out the patches from the common ancestor of the client and server branches, and then replay them onto master." It is a bit complex, but the result is pretty cool.
> 
> Figure 3-31. A history with a topic branch off another topic branch
> 
> Figure 3-32. Rebasing a topic branch off another topic branch
> 
> You can rebase the server branch onto the master branch: `git rebase master server`, this replays your server work on top of your master work.

### The Perils of Rebasing
> Do not rebase commits that exist outside your repository.

### Rebase When You Rebase
> ?
> 
> `git pull --rebase`

### Rebase vs. Merge
> ?


