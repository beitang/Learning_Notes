# Automatic Variables
- http://www.gnu.org/software/make/manual/make.html#Automatic-Variables
- $@: The file name of the target of the rule. If the target is an archive member, then $@ is the name of the archive file.
- $%: The target member name, when the target is an archive member.
- $<: The name of the first prerequisite.
- $?: The names of all the prerequisites that are newer than the target, with spaces between them.
- $^: The names of all the prerequisites, with spaces between them.
- $+: This is like $^, but prerequisites listed more than once are duplicated in the order they were listed in the makefile.
- $|: The names of all the order-only prerequisites, with spaces between them.
- $*


