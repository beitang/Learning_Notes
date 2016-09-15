# Chapter 1 Getting Started
## 1.1 About Version Control
- Version control is a system that records changes to a file or set of files over time so that you can recall specific versions later.
- Local Version Control Systems: A simple database that kept all the changes to files under revision control.
- Centralized Version Control Systems: Have a single server that contains all the versioned files, and a number of clients that check out files from that central place, such as CVS, Subversion.
-- Serious downsides: The most obvious is the single point of failure that the centralized server represents. If that server goes down for an hour, then during that hour nobody can collaborate at all or save versioned changes to anything they are working one. If the hard disck the central database is on becomes corrupted, and proper backups have not been kept, you lose absolutely everything - the entire history of the project except whatever single snapshots people happen to have on their local machines.
- Distributed Version Control Systems: Clients do not just check out the latest snapshot of the files, they fully mirror the repository. Thus if any server dies, and these systems were collaborating via it, any of the client repositories can be copied back up to the server to retore it. Every clone is really a full backup of all the data.

## 1.3 Git Basics
- This is an important section to absorb, because if you understand what Git is and the fundamentals of how it works, then using Git effectively will probably be much easier for you.
- Snapshots, Not Differences
-- Conceptually, most other systems store information as a list of file-based changes. These systems think of the information they keep as a set of files and the changes made to each file over time.
-- Git thinks of its data more like a set of snapshots of a miniature filesystem. Every time you commit, or save the state of your project in Git, it basically takes a picture of what all your files look like at that moment and stores reference to that snapshot. To be efficient, if files have not changed, Git does not store the file again, just a like to the previous identical file it has already stored. Git thinks about its data more like a stream of snapshots.
- Nearly Every Operation Is Local
- Git Has Integrity
-- Everything in Git is check-summed before it is stored and is then referred to by that checksum. This means it is impossible to change the contents of any file or directory without Git knowing about it.
-- The mechanism that Git uses for this checksumming is called a SHA-1 hash. This is a 40-character string composed of hexadecimal charactoer and calculated based on the contents of a file or directory structure in Git.
-- You will see these hash values all over the place in Git because it uses them so much. In fact, Git stores everything in its database not by file name but by the hash value of its contents.
- Git Generally Only Adds Data
-- When you do actions in Git, nearly all of them only add data to the Git database. It is hard to get the system to do anything that is not undoable or to make it erase data in any way.
- The Three States
-- Git has three main states that your files can reside in: committed, modified, and staged. Committed means that the data is safely stored in your local database. Modified means that you have changed the file but have not committed it to your database yet. Staged means that you have marked a modified file in its current version to go into your next commit snapshot.
-- This leads us to the three main sections of a Git project: the Git directory, the working directory, and the staging area. The Git directory is where Git stores the metadata and object database for your project. This is the most important part of Git, and it is what is copied when you clone a repository from anther computer. The working directory is a single checkout of one version of the project. These files are pulled out of the compressed database in the Git directory and placed on disk for you to use or modify. The staging area is a file, generally contained in your Git directory, that stores information about what will go into your next commit.

## 1.6 First-Time Git Setup
－ git config files
-- /etc/gitconfig: Contains values for every user on the system and all their repositories. If you pass the option --system to git config, it reads and writes from this file specifically.
-- ~/.gitconfig or ~/.config/git/config: Specific to your user. You can make Git read and write to this file specifically by passing the --global option.
-- config file in the Git directory (that is, .git/config) of whatever repository you are currently using: Specific to that single repository.
- $ git config --global user.name "beitang"
- $ git config --global user.email beitang@example.com
- $ git config --global core.editor vim
- $ git config --list
- $ git config user.name

## 1.7 Getting Help
- $ git help <verb>
- $ git <verb> --help
- $ man git-<verb>

# Chapter 2 Git Basics
## 2.1 Getting a Git Repository
- Initializing a Repository in an Existing Directory: $ git init
-- This creates a new subdirectory named .git that contains all of your necessary repository files - a Git repository skeleton.
- Cloning an Existing Repository: $ git clone [url]

## 2.2 Recording Changes to the Repository
- Remember that each file in your working directory can be in one of two states: tracked or untracked. Tracked files are files that were in the last snapshot; they can be unmodified, modified, or staged. Untracked files are everything else - any files in your working directory that were not in your last snapshot and are not in your staging area.
- Checking the Status of Your Files: $ git status
- Tracking New Fiels: $ git add [file name]
- Staging Modifiled Files: $ git add [file name]
- Short Status: $ git status -s
- Ignoring Files: .gitignore
- Viewing Your Staged and Unstaged Changes
-- To see what you are changed but not yet staged: $ git diff
-- To see what you have staged that will go into your next commit: $ git diff --staged or $ git diff --cached
- Committing Your Changes: $ git commit or $ git commit -m "log"
- Skipping the Staging Area: $ git commit -a -m "log"
- Removing Files
-- $ git rm [file name]
-- Keep the file on your hard drive but not have Git track it anymore: $ git rm --cached [file name]
- Moving Files: $ git mv file_from file_to

## 2.3 Viewing the Commit History
- $ git log
- One of the more helpful options is -p, which shows the difference introduced in each commit. You can also use -2, which limits the output to only the last two entries: $ git log -p -2
- To see some abbreviated stats for each commit: $ git log --stat
- The option --pretty changes the log output to formats other than the default:
-- $ git log --pretty=oneline
-- $ git log --pretty=format:"%h - %an, %ar : %s"
- The option --graph adds a nice little ASCII graph showing your branch and merge history: $ git log --pretty=format:"%h %s" --graph
- Limiting Log Output
-- $ git log --since=2.weeks
-- Another really helpful filter is the -S option which takes a string and only shows the commits that introduced a change to the code that added or removed that string. For instance, if you wanted to find the last commit that added or removed a reference to a specific function, you could call: $ git log -Sfunction_name
- $ git log --pretty="%h - %s" --author=gitster --since="2008-10-01" --before="2008-11-01" --no-merges

## 2.4 Undoing Things
- One of the common undos takes place when you commit too early and possibly forget to add some files, or you mess up your commit message. If you want to try that commit again: $ git commit --amend
- Unstaging a Staging File: $ git reset HEAD [file name]
- Unmodifying a Modified File: $ git checkout -- [file name]

## 2.5 Working with Remotes
- Showing Your Remotes
-- $ git remote
-- $ git remote -v
- Adding Remote Repositories
-- $ git remote add [shortname] [url]
- Fetching and Pulling from Your Remotes
-- $ git fetch [remote-name]
-- $ git pull: generally fetches data from the server you originally cloned from and automatically tries to merge it into the code you are currently working on.
- Pushing to Your Remotes
-- $ git push origin master
- Inspecting a Remote
-- $ git remote show origin
- Removing and Renaming Remotes
-- $ git remote rename pb paul
-- $ git remote rm paul

## 2.6 Tagging

## 2.7 Git Aliases
- $ git config --global alias.co checkout -- then can use $ git co
- $ git config --global alias.unstage 'reset HEAD --'
- $ git config --global alias.last 'log -1 HEAD'
- $ git config --global alias.visual "!gitk"

# Chapter 3 Git Branching
## 3.1 Branches in a Nutshell
- When you make a commit, Git stores a commit object that contains a pointer to the snapshot of the content you staged. This object also contains the author name and email, the message that you typed, and pointers to the commit or commits that directly came before this commit (its parent or parents): zero parents for the initial commit, one parent for a normal commit, and multiple parents for a commit that results from a merge of two or more branches.
- A branch in Git is simply a lightweight movable pointer to one of these commits. The default branch name in Git is master. As you starting making commits, you are given a master branch that points to the last commit you made. Every time you commit, it moves forward automatically.
- Creating a New Branch: $ git branch testing
-- Creating a new branch creates a new pointer for you to move around.
-- How does Git know what branch you are currently on? It keeps a special pointer called HEAD. This is a pointer to the local branch you are currently on.
-- A simple git log command with option --decorate that shows you where the branch pointers are pointing: $ git log --oneline --decorate
- Switching Branches: $ git checkout testing
- $ git log --oneline --decorate --graph --all
- Good picture to understand HEAD and branch: http://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell

# Chapter 7 Git Tools
## 7.1 Revision Selection
- Git allows you to specify specific commits or a range of commits in several ways.
- Single Revisions
-- Short SHA-1: Git can figure out a short, unique abbreviation for your SHA-1 values.
--- $ git show 1c002d
--- $ git log --abbrev-commit --pretty=oneline
-- Branch References: The most straightforward way to specify a commit requires that it has a branch reference pointed at it. You can use a branch name in any Git command that expects a commit object for SHA-1 value.
--- $ git show branch_name
--- If you want to see which specific SHA-1 a branch points to: $ git rev-parse branch_name
-- RefLog Shortnames: A log of where your HEAD and branch references have been for the last few months.
--- $ git reflog
--- $ git show HEAD@{5}
--- $ git show master@{yesterday}
--- $ git log -g master
--- It is important to note that the reflog information is strictly local - it is a log of what you have done in your repository.
-- Ancestry References
--- If you place a ^ at the end of a reference, Git resolves it to mean the parent of that commit: $ git show HEAD^
--- $ git show d921970^2: means "the second parent of d921970", this syntax is only useful for merge commits, which have more than one parent.
--- HEAD~ is equal to HEAD^, but HEAD~2 means the first parent of the first parent
--- "$ git show HEAD~3" equal to "$ git show HEAD^^^"
- Commit Ranges
-- Double Dot: this basically asks Git to resolve a range of commits that are reachable from one commit but aren't reachable from another.
--- $ git log master..experiment
--- $ git log experiment..master
--- $ git log origin/master..HEAD: see what you're about to push to a remote
-- Multiple Points
-- Triple Dot

## 7.3 Stashing and Cleaning
- Cleaning your Working Directory
-- To remove all the untracked files in your working directory: $ git clean -f -d
-- If you ever want to see what it would do, you can run the command with -n: $ git clean -d -n
-- If you want to remove ignored files, you can add -x: $ git clean -n -d -x
-- Interactive mode: $ git clean -x -i

## 7.6 Rewriting History
- Changing the Last Commit: $ git commit --amend
- Changing Multiple Commit Messages: $ git rebase -i HEAD~3
- The Nuclear Option: filter-branch, if you need to rewrite a larger number of commits in some scriptable way.

## 7.7 Reset Demystified
- Good to know reset

