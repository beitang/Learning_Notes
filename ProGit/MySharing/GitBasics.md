# Git Basics
> This is an important section to absorb, because if you understand what Git is and the fundamentals of how it works, then using Git effectively will probably be much easier for you.

## Snapshots, Not Differences
> Most other systems store information as a list of file-based changes. These systems think of the information they keep as a set of files and the changes made to each file over time.
>
> Figure 1-4
>
> Git thinks of its data more like a set of snapshots of a miniature filesystem. Every time you commit, or save the state of your project in Git, it basically takes a picture of what all your files look like at that moment and stores a reference to that snapshot. To be efficient, if files have not changed, Git does not store the file again, just a link to the previous identical file it has already stored. Git thinks about its data more like a stream of snapshots.
>
> Figure 1-5

## Nearly Every Operation Is Local
> Most operations in Git only need local files and resources to operate - generally no information is needed from another computer on your network. If you are used to a CVCS where most operations have that network latency overhead, this aspect of Git will make you think that the gods of speed have blessed Git with unworldly powers. Because you have the entire history of the project right there on your local disk, most operations seem almost instantaneous.

