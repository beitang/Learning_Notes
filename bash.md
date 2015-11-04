# Bash learning notes

## Debugging Bash scripts
### Debugging on the entire script
- `bash -x script.sh`: run the entire script in debug mode. Traces of each command plus its arguments are printed to standard output after the commands have been expanded but before they are executed.
- `#!/bin/bash -xv`

### Debugging on part(s) of the script
- Using the set Bash built-in
```
set -x
date
set +x
```
- Add `echo` to print wanted information

### Overview of set debugging options
Short notation | Long notation | Result
-------------- | ------------- | ------
set -f | set -o noglob | Disable file name generation using metacharacters (globbing).
set -v | set -o verbose | Prints shell input lines as they are read.
set -x | set -o xtrace | Print command traces before executing command.


## Shell initialization files
- System-wide configuration files
  - > /etc/profile
  - > /etc/bashrc
- Individual user configuration files
  - > ~/.bash_profile
  - > ~/.bash_login
  - > ~/.profile
  - > ~/.bashrc
  - > ~/.bash_logout

## Three types of built-in commands
- Bourne Shell built-ins: `:, ., break, cd, continue, eval, exec, exit, export, getopts, bash, pwd, readonly, return, set, shift, test, [, times, trap, umask, unset`
- Bash built-in commands: `alias, bind, builtin, command, declare, echo, enable, help, let, local, logout, printf, read, shopt, type, typeset, ulimit, unalias`
- Special built-in commands

## Shell building blocks
- Shell syntax
- Shell commands
- Shell functions
- Shell parameters
- Shell expansions
- Redirections
- Executing commands
- Shell scripts

## Overview of programming terms
- Command control: Testing exit status of a command in order to determine whether a portion of the program should be executed.
- Conditional branch: Logical point in the program when a condition determines what happens next.
- Logic flow: The overall design of the program. Determines logical sequence of tasks so that the result is successful and controlled.
- Loop: Part of the program that is performed zero or more times.
- User input: Information provided by an external source while the program is running, can be stored and recalled when needed.

## Special variables
- `export PS1="\u@\h -w> "`


## Variables
- Global variables: available in all shells. The `env` or `printing` commands can be used to display environment variables.
- Local variables: only available in the current shell. Using the `set` built-in command without any options will display a list of all variables (including environment variables) and functions.
- Variables by content: string variables, integer variables, constant variables, array variables
- Creating variables: case sensitive, `VARNMAE=“value”`, putting spaces around the equal sign will cause errors. It is a good habit to quote content strings when assigning values to variables.
- Exporting variables: pass variables to a subshell, `export VARNAME=“value"`

### Bourne shell reserved variables
- CDPATH: A colon-separated list of directories used as a search path for the `cd` built-in command.
- HOME: The current user’s home directory; the default for the `cd` built-in. The value of this variable is also used by tilde expansion.
- IFS: A list of characters that separates fields; used when the shell splits words as part of a expansion.
- MAIL: If this parameter is set to a file name and the MAILPATH variable is not set, Bash informs the user of the arrival of mail in the specified file
- MAILPATH: A colon-separated list of file names which the shell periodically checks for new mail.
- OPTARG: The value of the last option argument processed by the getopts built-in.
- OPTIND: The index of the last option argument processed by the getopts built-in.
- PATH: A colon-separated list of directories in which the shell looks for commands.
- PS1: The primary prompt string. The default value is “‘\s-\v\$ ‘".
- PS2: The secondary prompt string. The default value is “‘> ‘".

### Bash reserved variables
- auto_resume
- BASH
- BASH_ENV
- BASH_VERSION
- BASH_VERSINFO
- COLUMNS
- COMP_CWORD
- COMP_LINE
- COMP_POINT
- COMP_WORDS
- COMPREPLY
- DIRSTACK
- EUID
- FCEDIT
- FIGNORE
- FUNCNAME
- GLOBIGNORE
- GROUPS
- histchars
- HISTCMD
- HISTCONTROL
- HISTFILE
- HISTFILESIZE
- HISTIGNORE
- HISTSIZE
- HOSTFILE
- HOSTTYPE
- IGNOREEOF
- INPUTRC
- LANG
- LC_ALL
- LC_COLLATE
- LC_CTYPE
- LC_MESSAGES
- LC_NUMERIC
- LINENO
- LINES
- MACHTYPE
- MAILCHECK
- OLDPWD
- OPTERR
- OSTYPE
- PIPESTATUS
- POSIXLY_CORRECT
- PPID
- PROMPT_COMMAND
- PS3
- PS4
- PWD
- RANDOM
- REPLY
- SECONDS
- SHELLOPTS
- SHLVL
- TIMEFORMAT
- TMOUT
- UID
Check the Bash man, info or doc pages for extended information. Some variables are read-only, some are set automatically and some lose their meaning when set to a different value than the default.

### Special parameters
These parameters may only be referenced; assignment to them is not allowed.
- $*: Expands to the positional parameters, starting from one. When the expansion occurs within double quotes, it expands to a single word with the value of each parameter separated by the first character of the IFS special variable.
- $@: Expands to the positional parameters, starting from one. When the expansion occurs within double quotes, each parameter expands to a separate word.
- $#: Expands to the number of positional parameters in decimal.
- $?: Expands to the exit status of the most recently executed foreground pipeline.
- $-: A hyphen expands to the current option flags as specified upon invocation, by the `set` built-in command, or those set by the shell itself.
- $$: Expands to the process ID of the shell.
- $1: Expands to the process ID of the most recently executed background command.
- $0: Expands to the name of the shell or shell script.
- $_: The underscore variable is set at the shell startup and contains the absolute file name of the shell or script being executed as passed in the argument list. Subsequently, it expands to the last argument to the previous command, after expansion. It is also set to the full pathname of each command executed and placed in the environment exported to that command. When checking mail, this parameter holds the name of the mail file.

The positional parameters are the words following the name of a shell script. They are put into the variable $1, $2, $3, and so on.

## Quoting characters
- Quoting is used to remove the special meaning of characters or words: quotes can disable special treatment for special characters, they can prevent reserved words from being recognized as such and they can disable parameter expansion.
- Escape characters: used to remove the special meaning from a single character. A non-quoted backslash, \, is used as an escape character in Bash.
- Single quotes: used to preserve the literal value of each character enclosed within the quotes. A single quote may not occur between single quotes, even when preceded by a backslash.
- Double quotes: Using double quotes the literal value of all characters enclosed is preserved, except for the dollar sign, the backticks (backward single quotes, ``) and the backslash. The dollar sign and the backticks retain their special meaning within the double quotes. The backslash retains its meaning only when followed by dollar, backticks, double quote, backlash or newline. A double quote may be quoted within double quotes by preceding it with a backslash.

## Shell expansion
- After the command has been split into tokens, these tokens or words are expanded or resolved. There are eight kinds of expansion performed, which we will discuss in the next section, in the order that they are expanded. After all expansions, quote removal is performed.

### Brach expansion
- A mechanism by which arbitrary strings may be generated.
- Brace expansion is performed before any other expansions, and any characters special to other expansions are preserved in the result.
```
franky -> echo sp{el,il,al}l
spell spill spall
```

### Tilde expansion
- if a word begins with an unquoted tilde character (“~”), all of the characters up to the first unquoted slash are considered a tilde-prefix. If none of the characters in the tilde-prefix are quoted, the characters in the tilde-prefix following the tilde are treated as a possible login name. If this login name is the null string, the tilde is replaced with the value of the HOME shell variable If HOME is unset, the home directory of the user executing the shell is substituted instead. Otherwise, the tilde-prefix is replaced with the home directory associated with the special login name.
- If the tilde-prefix is “~+”, the value of the shell variable PWD replaces the tilde-prefix.
- If the tilde-prefix is “~-“, the value of the shell variable OLDPWD, if it is set, is substituted.

### Shell parameter and variable expansion
- The “$” character introduces parameter expansion, command substitution, or arithmetic expansion. The parameter name or symbol to be expanded may be enclosed in braces, which are optional but serve to protect the variable to be expanded from characters immediately following it which could be interpreted as part of the name.
- The following construct allows for creation of the named variable if it does not yet exist: `${VAR:=value}`
- ??

### Command substitution
- allows the output of a command to replace the command itself.
- occurs when a command is enclosed like this: $command, or `command`

### Arithmetic expansion
- allows the evaluation of an arithmetic expression and the substitution of the result.
- The format for arithmetic expansion is: $(( EXPRESSION ))
- The expression is treated as if it were within double quotes, but a double quote inside the parentheses is not treated specially. All tokens in the expression undergo parameter expansion, command substitution, and quote removal. Arithmetic substitutions may be nested.

Arithmetic operators in order of decreasing precedence
Operator | Meaning
---------- | ----------
VAR++ and VAR-- | variable post-increment and post-decrement
++VAR and --VAR | variable pre-increment and pre-decrement
- and + |
! and ~ |
** |
*, / and % |
<< and >> |
<=, >=, < and > |
== and != |
& |
^ |
| |
&& |
|| |
expr ? expr : expr |
=, *=, /=, %=, +=, -=, <<=, >>=, &=, ^= and != |
, | separator between expression.

- Shell variables are allowed as operands; parameter expansion is performed before the expression is evaluated.
- When possible, Bash users should try to use the syntax with square brackets: $[ EXPRESSION ]. However, this will only calculate the result of EXPRESSION, and do not tests.

### Process substitution
- Is supported on systems that support named pipes (FIFOs) or the /dev/fd method of naming open files. It takes the form of <(LIST) or (LIST)

### Word splitting
?

### File name expansion
?

## Aliase
- `alias`
- `alias dh='df -h'`
- `unalias dh`

## More Bash options
### Displaying options
- `set -o`
### Changing options

### Bash help
- man bash
- bash info

# References
- http://www.tldp.org/LDP/Bash-Beginners-Guide/html/index.html
- `man bash`
- `info bash`
