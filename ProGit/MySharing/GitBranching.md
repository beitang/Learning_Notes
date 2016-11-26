# Git Branching
> Branching means you diverge from the main line of development and continue to do work without messing with that main line.
> Some people refer to Git branching model as its "killer feature, " and it certainly sets Git apart in the VCS community. Why is it so special? The way Git branches is incredibly lightweight making branching operations nearly instantaneous, and switching back and forth between branches generally just as fast.

## Branches in a Nutshell
> When you make a commit, Git stores a commit object that contains a pointer to the snapshot of the content you staged. This object also contains the author name and email, the message that you typed, and pointers to the commit or commits that directly came before this commit (its parent or parents): zero parents for the initial commit, one parent for a normal commit, and multiple parents for a commit that results from a merge of two or more branches.
> When you create the commit by running `git commit`, Git checksums each subdirectory and stores those tree objects in the Git repository. Git then creates a commit object that has the metadata and a pointer to the root project tree so it can re-create that snapshot when needed.
> Your Git repository now contains five objects: one blob for the contents of each of your three files, one tree that lists the contents of the directory and specifies which file names are stored as which blobs, and one commit with the pointer to that root tree and all the commit metadata.
> Figure 3-1. A commit and its tree
> If you make some changes and commit again, the next commit stores a pointer to the commit that came immediately before it.
> Figure 3-2. Commits and their parents
> A branch in Git is simply a lightweight movable pointer to one of these commits. The default branch name in Git is master.

### Creating a New Branch
> What happens if you create a new branch? Well, doing so creates a new pointer for you to mmove around.
> `git branch testing`: This creates a new pointer to the same commit you are currently on.
> How does Git know what branch you are currently on? It keeps a special pointer called `HEAD`.
> The `git branch` command only created a new branch - it did not switch to that branch.
> You can easily see this by running a simple `git log` command that shows you where the branch pointers are pointing. This option is called `--decorate`.
> `git log --oneline --decorate`

### Switching Branches
> To switch to an existing branch, you run the `git checkout` command.
> `git checkout testing` This moves `HEAD` to point to the testing branch.
> Figure 3-7. The HEAD branch moves forwardd when a commit is made
> Figure 3-8. HEAD moves when you checkout
> That command did two things. It moves the HEAD pointer back to point to the master branch, and it reverted the files in your working directory back to the snapshot that master points to. This also means the changes you make from this point forward will diverge from an older version of the project. It essentially rewinds the work you are done in your testing branch so you can go in a different direction.
> If you run `git log --oneline --decorate --graph --all` it will print out the history of your commits, showing where your branch pointers are and how your history has diverged.
> Because a branch in Git is in actually a simple file that contains the 40 character SHA-1 checksum of the commit it points to, branches are cheap to create and destroy. Creating a new branch is as quick and simple as writing 41 bytes to a file (40 characters and a newline).

## Basic Branching and Merging
### Basic Branching
> To create a branch and switch to it at the same time, you can run the `git checkout` command with the `-b` switch
> Note that if your working directory or staging area has uncommitted changes that conflict with the branch you are checking out, Git will not let you switch branches. It is best to have a clean working state when you switch branches.
> Merge it back into your master branch to deploy to production. You do this with the `git merge` command. `git checkout master`, `git merge hotfix`
> You will notice the phrase "fast-forward" in that merge. Because the commit C4 pointed to by the branch hotfix you merged in was directly ahead of the commit C2 you are on, Git simply moves the pointer forward. To phrase that another way, when you try to merge one commit with a commit that can be reached by following the first commit history, Git simplifies things by moving the pointer forward because there is no divergent work to merge together -- this is called a "fast-forward."
> You can delete the branch with the `-d` option to `git branch`: `git branch -d hotfix`

### Basic Merging
> In this case, your development history has diverged from some older point. Because the commit on the branch you are on is not a direct ancestor of the branch you are merging in, Git has to do some work. In this case, Git does a simple three-way merge, using the two snapshots pointed to by the branch tips and the common ancestor of the two.
> Figure 3-16. Three snapshots used in a typical merge
> Instead of just moving the branch pointer forward, Git creates a new snapshot that results from this three-way merge and automatically creates a new commit that points to it. This is referred to as a merge commit, and is special in that it has more than one parent.
> Figure 3-17. A merge commit
> It is worth pointing out that Git determines the best common ancestor to use for its merge base.

### Basic Merge Conflicts
> If you changed the same part of the same file differently in the two branches you are merging together, Git will not be able to merge them cleanly.
> Git has not automatically created a new merge commit. It has paused the process while you resolve the conflict. If you want to see which files are unmerged at any point after a merge conflict, you can run `git status`.
> Anything that has merge conflicts and has not been resolved is listed as unmerged. Git adds standard conflict-resolution markers to the files that have conflicts, so you can open them manually and resolve those conflicts.
> After you have resolved each of these sections in each conflicted files, run `git add` on each file to mark it as resolved. Staging the file marks it as resolved in Git.
> If you are happy with that, and you verify that everything that had conflicts has been staged, you can type `git commit` to finalize the merge commit.

## Branch Management
