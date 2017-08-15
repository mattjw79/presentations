# Bash Essentials
#### Matt Whitney



## Overview
-   [What is Bash?](#what-is-bash)
-   [Using a Shell](#using-a-shell)
-   [Quoting and Escaping](#quoting-and-escaping)
-   [Expansions](#expansions)
-   [Redirections](#redirections)
-   [Shortcuts](#shortcuts)



### What is Bash?
-   Bourne-Again Shell
-   Command line interpreter
-   Executes commands
    -   Terminal or standard input
    -   Script file

Notes: Bash is an acronym for Bourne-Again Shell. It is a command line
interpreter that provides a configurable environment to allow the user to
interact with the kernel to accomplish tasks. This interaction can be
accomplished through manual interaction such as typing in commands and waiting
for output or through a shell script that automates running multiple commands.



## Using a Shell
-   [Prompt](#prompt)
-   [Syntax](#syntax)
-   [Simple Commands](simple-commands)
-   [Pipelines](#pipelines)
-   [Lists of Commands](#lists-of-commands)
-   [Compound Commands](#compound-commands)



### Prompt
-   Default prompt contains
    -   Username
    -   Hostname
    -   Base name of current directory
    -   User level indication
-   Normal user
```Bash
[user1@example ~]$
```
-   Super user
```Bash
[root@example ~]#
```

Notes: The default prompt contains multiple useful pieces of information. It
shows the username of the current user, the hostname, the base name of the
current directory and also has a user level indicator. The user level indicator
is found at the end of the prompt as either a "$" for a normal user or as a "#"
for a super user (or root user).



### Syntax
-   Commands are white-space separated
-   When running a command, the shell
    1.  Reads input from terminal, arguments or file
    2.  Breaks input into words and operators known as tokens
    3.  Parses the tokens into simple and compound commands
    4.  Performs shell expansions
    5.  Performs necessary redirections
    6.  Executes the command(s)
    7.  Optionally waits for the command(s) to complete

Notes: When commands are entered in the Bash shell, there are several steps
that those commands must go through before they are actually executed. The
input is first read in from the terminal, then broken into words and operators.
Then the shell parses the tokens into simple and compound commands, performs
any shell expansions and redirections. Lastly, the shell executes the command or
commands and optionally waits for the commands to complete. When entering
commands into the shell, the different parts of the command are white space
separated.



### Simple Commands
-   Sequence of words separated by spaces
-   First word is the command
-   Every other word
    -   Options
    -   Arguments
-   Examples
```Bash
ls -alh /usr/local/bin
cp file1.txt file2.txt
mount /dev/cdrom /mnt
```

Notes: Simple commands are the most common for an interactive shell session.
These are single command strings that contain a command followed by options
and/or arguments. These simple commands are usually designed to complete a very
specific task such as copying a file or creating a directory.



### Pipelines
-   Sequence of simple commands separated by either "|" or "|&"
-   The pipe ("|") operator redirects only stdout to the next command
-   The pipe and ampersand ("|&") operator redirects both stdout and stderr to
    the next command
-   Examples
```Bash
command1 | command2 [ | commandx ]
command1 |& command2 [ |& commandx ]
```

Notes: Pipelines give the user the ability to process the output of one command
with another command. For example, this allows a user search for a specific
string in the output of another command. When running commands in a pipeline,
each command is started at the same time and the shell waits for all commands
to complete before returning to the prompt.



### Lists of Commands
-   Sequence of one or more pipelines separated by operators ";", "&", "&&" or
    "||"
-   The ";" operator is used to run commands in serial, the shell waits for
    each command to finish before executing the next
-   The "&" operator is used to run commands in the background, the shell does
    not wait for the command to finish
-   The "&&" operator runs the next command only when the previous command
    finishes successfully
-   The "||" operator runs the next command only when the previous command
    fails

Notes: Lists of commands can be executed in serial, the ";" operator, or in
the background using the "&" operator. Using the semicolon (";") operator, the
commands are treated as if you execute each one on a separate line. The shell
waits for each command to complete before moving on to the next command. Using
the ampersand ("&") operator runs the command in the background. In this case,
the shell does not wait for the command to finish. The "&&" and "||" operators
are used as simple conditional. The "&&" operator will run the second command
only if the first command exits successfully and the "||" operator will run the
second command only if the first command exits with a failure.



### Compound Commands
-   Shell programming constructs
-   Begins and ends with reserved words
-   Includes
    -   Looping constructs (while, for, until)
    -   Conditional constructs (if, case, select, etc.)
    -   Grouping of commands (parens, curly braces)

Notes: Compound commands are ways to add some logic and looping into the
commands that are run. They can be used on an interactive shell as well as
within a shell script. The looping constructs will run the same set of commands
multiple times while the conditional constructs allow branching to different
parts of code depending on certain circumstances. The grouping operators allow
multiple commands, and their output, to be acted upon as you would with a single
command. The parentheses causes the commands to be executed in a separate
subshell while the curly braces causes the commands to be executed in the
current shell context.



## Quoting and Escaping
-   [Escape Character](#escape-character)
-   [Double Quotes](#double-quotes)
-   [Single Quotes](#single-quotes)
-   [Comment Character](#comment-character)



### Escape Character
-   Backslash ("\\")
-   Prevents the shell from interpreting the next character
-   The "\\newline" sequence is effectively ignored
    -   Allows the command to be continued on more than one line
```Bash
./configure --prefix=/sw/pkg/apache \
  --enable-ldap=shared \
  --enable-lua=shared
```

Notes: The escape character is used to keep bash from using the special
meaning of certain characters; such as "$", "!", "\`" and even "\\"
itself. The escape character can also be used to continue a command on more
than one line.



### Double Quotes
-   Prevents the shell from interpreting most characters between two sets
    of double quotes
-   The special characters "$", "\`", "\\" and "!" retain their special
    meaning

Notes: Double quoted strings allow the "$", "\`", "\\" and "!" characters to
retain their special meanings. The escape character can be used to escape any
of these characters so that they are not interpreted. The escape character can
be used with a double quote to include a double quote within a double quoted
string.



### Single Quotes
-   Prevents the shell from interpreting the characters between two single
    quotes
-   The backslash does not function as an escape character in a single
    quoted string

Notes: Single quoted strings are not interpreted by the shell, which means
there is no need to escape the special characters within the string. This also
means that the single quote character cannot be used within a single quoted
string.



### Comment Character
-   All characters after the "#" and before the newline are ignored by the
    shell
-   Effectively makes anything on the line after "#" a comment

Notes: The pound sign (or hash mark) is used to allow comments on the shell or
within shell scripts. The comments are not considered part of the command
string when executing but they are stored within the history. This is useful
for documenting why a command was run or what the command was expected to do.



## Expansions
1.  [Brace Expansion](#brace-expansion)
2.  [Tilde Expansion](#tilde-expansion)
3.  [Shell Parameter Expansion](#shell-parameter-expansion)
4.  [Command Substitution](#command-substitution)
5.  [Arithmetic Expansion](#arithmetic-expansion)
6.  [Process Substitution](#process-substitution)
7.  [Word Splitting](#word-splitting)
8.  [Filename Expansion](#filename-expansion)

Notes: There are eight different kinds of expansions that the Bash shell
performs. After the shell breaks the command into tokens, each of the expansions
are performed in order. Once all expansions have been completed, quote removal
is performed and the command is executed.



### Brace Expansion
-   Allow the generation of an arbitrary number of strings
-   Strings to be expanded are comma separated
    ```Bash
    [user@example ~]$ echo {one,two,three}
    one two three
    [user@example ~]$ echo {one,two,three}_potato
    one_potato two_potato three_potato
    [user@example ~]$ echo a_{one,two,three}_potato
    a_one_potato a_two_potato a_three_potato
    ```
-   Special characters that trigger other shell expansions are not interpreted
    at this stage
-   Caveat: If the opening brace has a dollar sign directly preceding it, the
    string(s) contained in the braces are NOT expanded. Ex: "${"

Notes: Brace expansions are processed before all other expansions. Because of
this, special characters contained within the braces are not interpreted with
their special meanings at this stage. To avoid conflicts with a later shell
expansion, if a curly brace is immediately preceded with a dollar sign, the
brace expansions are not performed on the string contained within.



### Tilde Expansion
-   Typically used to expand a user's home directory
    ```Bash
    [user@example ~]$ echo ~
    /home/user
    [user@example ~]$ echo ~user2
    /home/user2
    ```
-   If the tilde is followed by the plus sign "~+" then it is expanded to the
    contents of the PWD variable (usually the current directory)
-   If the tilde is followed by the minus sign "~-" then it is expanded to the
    contents of the OLDPWD variable

Notes: The tilde expansion is typically used as a shortcut to a users home
directory. Used by itself, it expands to the current users home directory. If
paired with either the plus or minus sign it expands to the contents of the
PWD or OLDPWD variable respectively.



### Shell Parameter Expansion
-   The "$" character starts
    -   Parameter expansion (variables)
    -   Command substitution
    -   Arithmetic expansion
-   Simple form or direct expansion is $PARAMETER or ${PARAMETER}
    -   Value of $PARAMETER is substituted
    -   Braces are optional but denote start and end of parameter string
-   Indirect expansion is ${!B*}
    ```Bash
    [user@example ~]$ echo ${!B*}
    BASH BASHOPTS BASHPID BASH_ALIASES BASH_ARGC BASH_ARGV BASH_CMDS
    BASH_COMMAND BASH_COMPLETION_COMPAT_DIR BASH_LINENO BASH_REMATCH
    BASH_SOURCE BASH_SUBSHELL BASH_VERSINFO BASH_VERSION
    ```
-   Creation of named variable if it does not already exist
    ```Bash
    [user@example ~]$ echo ${COUNT}

    [user@example ~]$ echo ${COUNT:=0}
    0
    ```

Notes: Shell parameter expansions, or possibly better known as shell variables,
act as a named storage for data. Using the simplest form, the parameter is
replaced with it's contents in the command line. Indirect expansion is signaled
by using the exclamation point before the parameter pattern. By default, if a
parameter has not bee previously set, it will contain a null value. To override
this behavior, specify ":=" and the value to be used after the parameter name.



### Command Substitution
-   Two formats
    -   Dollar-parens(preferred): $(command)
    -   Backticks: \`command\`
-   Can be nested (inner backticks must be escaped when nested)
```Bash
[user@example ~]$ echo "Today is" $(date)
Today is Mon Aug 14 10:33:00 EDT 2017
[user@example ~]$ echo "Today is" \`date\`
Today is Mon Aug 14 10:33:00 EDT 2017
[user@example ~]$ echo "Today is $(date $(echo "+%A")), hooray!"
Today is Monday, hooray!
[user@example ~]$ echo "Today is \`date \\\`echo "+%A"\\\`\`, hooray!"
Today is Monday, hooray!
```

Notes: Command substitution allows the output of a command or commands to be
used in it's place. Of the two formats that are accepted for command
substitution, the dollar-parens format is preferred over backticks due to
easier readability and nesting.



### Arithmetic Expansion
-   Two formats
    -   dollar-square-bracket format (preferred): $\[expression\]
    -   dollar-double-parens format: $((expression))
-   Operators are similar to the C programming language
```Bash
[user@example ~]$ COUNT=5; echo $[ ++COUNT ]  # pre-increment
6
[user@example ~]$ echo $[ 3 + 4 ]             # simple addition
7
[user@example ~]$ echo $[ $[ 5 + 3 ] * 7 ]    # compound
56
[user@example ~]$ echo $[ 4 ** 2 ]            # exponents
16
[user@example ~]$ echo $[ 4 > 5 ? 2 : 1 ]     # conditional eval
1
```

Notes: Arithmetic expansion allows for the evaluation of an arithmetic
expression and substitutes the result. The operators allowed are similar to the
operators available in the C programming language. Of the two formats allowed,
the dollar-square-bracket format is preferred.



### Process Substitution
-   Creates an anonymous pipe for the output or input of a command
-   May be easiest with an example
    ```Bash
    [user@example ~]$ diff file1 <(sort file2)
    ```
    1.  Creates an anonymous pipe for "sort file2"
    2.  Sorts the contents of "file2" and the output is available as a file
        descriptor
    3.  The diff command compares the contents of file1 and the file descriptor
        representing the output for the command "sort file2"

Notes: Process substitution creates an anonymous pipe for the stdout or stdin
of a command so that it may be accessed like a file. In the example given,
assume that "file1" is a sorted list of names and "file2" is an unsorted list
of names. Without process substitution, "file2" would need to be sorted and
saved as another file before being able to (sanely) compare the two files. With
process substitution, the output of the sort command can be used to compare
with "file1".



### Word Splitting
-   Similar to when a command is split into tokens
-   Results or expansions are split on the contents of $IFS (Internal Field Separator)
    -   Parameter expansion
    -   Command substitution
    -   Arithmetic expansion
-   Null arguments are passed to commands as empty strings
-   If no expansion occurs, no word splitting is performed

Notes: Once the parameter expansions, command substitutions and arithmetic
expansions have completed, the expanded text is split into tokens based on the
characters contained in the IFS variable. Any null arguments are passed to the
commands as empty strings. This step will only be executed if an expansion has
occurred, otherwise, it is an unneeded step.



### File Name Expansion
-   Happens after all word splitting is complete
-   Bash looks for any of the following:
    -   "*" - expands to zero or more characters
    -   "?" - expands to exactly one character
    -   "[" - expands once to any of the characters between brackets
-   All matches are included in expansion
```Bash
[user@example ~]$ ls
dir1      dir2      file1       file2     file3
[user@example ~]$ echo file?
file1 file2 file3
[user@example ~]$ echo file[13]
file1 file3
```

Notes: The last step before the command is executed is to expand file names.
This step looks for special characters and expands them to file names that
match. The asterisk matches zero or more characters, the question mark matches
exactly one character and the open and close square brackets list possible
matches for a single character. All file names that match the pattern will be
listed in the expansion, so if a pattern matches five file (or directory) names
then all five file names will be included.



## Redirections
-   Redirecting output
    -   Sends stdout or stderr to a file
    -   The ">" redirects stdout and overwrites or creates a file
    -   The ">>" redirects stdout and appends to or creates a file
    -   Redirect stderr using "2>" or "2>>"
    -   Redirect both stdout and stderr to the same file using "&>" or "&>>"
-   Redirecting input
    -   Sends data to a command's stdin
    -   The "<" redirects the contents of a file
    -   The "<<" (or here document) reads input up to a delimiter specified

Notes: Redirections are used for changing the output or input of a command to a
specified file or string. When redirecting stdout or stderr, a single
greater-than will create a new file or, if the file already exists, truncate
the existing file effectively overwriting what was there. Using a double
greater-than will create a new file or append to an existing file.



## Shortcuts
-   [Aliases](#aliases)
-   [Initialization Files](#initialization-files)
-   [History](#history)
-   [Key Combinations](#key-combinations)



### Aliases
-   alias: "a false name used to conceal one's identity; an assumed name" - dictionary.com
-   A way to name a longer command string
    ```Bash
    alias df='df -h'
    alias ext_du='date; time du -sh *'
    ```
-   Aliases are expanded when a command is read, not when executed
-   Will NOT work as expected:
    ```Bash
    alias bad_alias='alias df="df -h"; df'
    ```
-   Remove an alias with the built-in command "unalias"

Notes: An alias in Bash is a way to give a name to another command string. To
do so, use the built-in command "alias", then the name of the new alias
followed by an equals sign and the command string (quoted) that should be run.
Because aliases are expanded when the command is read and not when executed,
when defining a new alias within another alias or function, the new alias will
not be available within that same alias or function.



### Initialization Files
-   Used to extend the default Bash startup behavior
-   Custom variables, aliases and functions are typically defined here
-   When executed as an interactive login shell (typical usage), reads the
    following files (in order)
    1.  /etc/profile
    2.  ~/.bash_profile
    3.  ~/.bash_login
    4.  ~/.profile
-   Read as a script
-   RedHat based distributions and Mac tend to use ~/.bash_profile
-   Debian based distributions tend to use ~/.profile

Notes: The Bash initialization files are used to extend the startup behavior of
the shell. They can contain custom variables, aliases, functions and any other
commands that may need to run upon the shell startup. When the Bash shell is
started as an interactive login shell, the initialization files are read, in
order, and the commands inside are executed.



### History
-   Bash, by default, keeps a list of commands previously typed
-   Uses multiple variables to define settings
-   Usually stored in the ~/.bash_history file, which is defined by HISTFILE
-   Loaded from HISTFILE when Bash is started
-   Saved back to HISTFILE when Bash is closed
-   Use the "history" command to print out the list of commands previously used
-   History shortcuts
    -   !! - Specifies the most recent command in history
    -   !n - Where "n" is a number, specifies the command in position "n"
    -   !s - Where "s" is a string, specifies the more recent command starting
        with the string

Notes: The Bash history is extremely useful when needing to recall commands
previously executed. Typically, the history data is stored in the user's home
directory under the name .bash_history and is loaded into memory when the shell
is started and saved to the file when bash is exited. To configure the Bash
history, there are several variables involved. The most commonly modified
variables are HISTSIZE and HISTCONTROL. The command "history" will print the
list of commands previously typed along with the command number. To access a
specific command by number, use the "!n" history shortcut where the "n" is the
number of the command displayed.



### Key Combinations
-   TAB key
    -   Single press - attempt to complete depending on the starting character
        of the current token
    -   Double press - display all options for completion
-   Up/Down arrows - scroll through previous commands
-   CTRL-c - cancel the current running process
-   CTRL-a - Move to the beginning of the current line
-   CTRL-e - Move to the end of the current line
-   CTRL-f - Move the cursor forward one character
-   CTRL-b - Move the cursor backward one character
-   CTRL-l - Clear the screen
-   CTRL-r - Search backward through history
-   CTRL-s - Search forward through history
-   CTRL-u - Clear the current line from the cursor to the beginning

Notes: Bash includes a plethora of key combination shortcuts. Of these, the most
common is the TAB key, which will attempt to complete a token (command or file
name) or display the options for completion of the token. The CTRL key
combinations allow breaking out of running processes, searching through the Bash
history, clearing the current line or screen, and cursor movements.



## References
-   [Bash Reference](https://www.gnu.org/software/bash/manual/html_node/index.html#SEC_Contents)
-   [Bash Beginners Guide](http://tldp.org/LDP/Bash-Beginners-Guide/html/index.html)
-   [Process Substitution (Wikipedia)](https://en.wikipedia.org/wiki/Process_substitution)
-   [Link to presentation on GitHub](https://github.com/mattjw79/presentations/tree/master/bash_essentials)
