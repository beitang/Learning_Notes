# Chapter 1.1 Getting Started - About Version Control
- Version control is a system that records changes to a file or set of files over time so that you can recall specific versions later.
- Local Version Control Systems: A simple database that kept all the changes to files under revision control.
- Centralized Version Control Systems: Have a single server that contains all the versioned files, and a number of clients that check out files from that central place, such as CVS, Subversion.
-- Serious downsides: The most obvious is the single point of failure that the centralized server represents. If that server goes down for an hour, then during that hour nobody can collaborate at all or save versioned changes to anything they're working one. If the hard disck the central database is on becomes corrupted, and proper backups haven't been kept, you lose absolutely everything - the entire history of the project except whatever single snapshots people happen to have on their local machines.
- Distributed Version Control Systems: Clients don't just check out the latest snapshot of the files, they fully mirror the repository. Thus if any server dies, and these systems were collaborating via it, any of the client repositories can be copied back up to the server to retore it. Every clone is really a full backup of all the data.

---

# Chapter 1.3 Getting Started - Git Basics
- This is an important section to absorb, because if you understand what Git is and the fundamentals of how it works, then using Git effectively will probably be much easier for you.
- Snapshots, Not Differences
-- Conceptually, most other systems store information as a list of file-based changes. These systems think of the information they keep as a set of files and the changes made to each file over time.
-- Git thinks of its data more like a set of snapshots of a miniature filesystem. Every time you commit, or save the state of your project in Git, it basically takes a picture of what all your files look like at that moment and stores reference to that snapshot. To be efficient, if files have not changed, Git doesn't store the file again, just a like to the previous identical file it has already stored. Git thinks about its data more like a stream of snapshots.
- Nearly Every Operation Is Local
- Git Has Integrity
-- Everything in Git is check-summed before it is stored and is then referred to by that checksum. This means it's impossible to change the contents of any file or directory without Git knowing about it.
-- The mechanism that Git uses for this checksumming is called a SHA-1 hash. This is a 40-character string composed of hexadecimal charactoer and calculated based on the contents of a file or directory structure in Git.
-- You will see these hash values all over the place in Git because it uses them so much. In fact, Git stores everything in its database not by file name but by the hash value of its contents.
- Git Generally Only Adds Data
-- When you do actions in Git, nearly all of them only add data to the Git database. It is hard to get the system to do anything that is not undoable or to make it erase data in any way.
- The Three States
-- Git has three main states that your files can reside in: committed, modified, and staged. Committed means that the data is safely stored in your local database. Modified means that you have changed the file but have not committed it to your database yet. Staged means that you have marked a modified file in its current version to go into your next commit snapshot.
-- This leads us to the three main sections of a Git project: the Git directory, the working directory, and the staging area. The Git directory is where Git stores the metadata and object database for your project. This is the most important part of Git, and it is what is copied when you clone a repository from anther computer. The working directory is a single checkout of one version of the project. These files are pulled out of the compressed database in the Git directory and placed on disk for you to use or modify. The staging area is a file, generally contained in your Git directory, that stores information about what will go into your next commit.

---

# Chapter 1.6 Getting Started - First-Time Git Setup
