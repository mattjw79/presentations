# Bash Essentials
#### Matt Whitney



## Overview
-   [What is Bash?](#what-is-bash)
-   [Shell Operation](#shell-operation)
-   [Special Characters and Quotes](#special-characters-and-quotes)
-   [Working in the Shell](#working-in-the-shell)
-   [Shortcuts](#shortcuts)
-   [References](#references)



## What is Bash?
-   Command line interpreter
-   Bourne-Again Shell
-   Executes commands
    -   Standard input or terminal
    -   Script file

Notes: Bash is an acronym for Bourne-Again Shell and it is a command line
interpreter. Bash provides a configurable environment to allow the user to
interact with the kernel to accomplish tasks. The Bash shell is an enhancement
to the Bourne Shell (sh) and commands that work with the Bourne Shell will
also work in the Bash shell.



## Shell Operation
1.  Reads input from terminal, arguments or file
2.  Breaks input into words and operators known as tokens
3.  Parses the tokens into simple and compound commands
4.  Performs shell expansions
5.  Performs necessary redirections
6.  Executes the command
7.  Optionally waits for the command to complete

Notes: This is a high level view of how the Bash shell executes the commands
given to it. At this point, you don't need to completely understand each of
the steps in depth. Just keep them in mind as we fill out the details in the
coming slides.



## Special Characters and Quotes
-   [Escape Character](#escape-character)
-   [Single Quotes](#single-quotes)
-   [Double Quotes](#double-quotes)
-   [Pound Sign (Hash)](#pound-sign-hash)



### Escape Character "\\" (backslash)
-   Prevents the shell from interpreting the next character
-   The "\\newline" sequence is effectively ignored
    -   Allows the command to be continued on more than one line
```Bash
./configure --prefix=/sw/pkg/apache \
  --enable-ldap=shared \
  --enable-lua=shared
```

Notes: The escape character is used to keep bash from using the special
operations of certain characters; such as "$", "!", "\`" and even "\\"
itself. The escape character can also be used to continue a command on more
than one line.



### Single Quotes
-   Prevents the shell from interpreting the characters between two single
    quotes
-   The backslash does not function as an escape character in a single
    quoted string

Notes: Single quoted strings are not interpreted by the shell, which means
there is no need to escape the special characters within the string. This also
means that the single quote character cannot be used within a single quoted
string.



### Double Quotes
-   Prevents the shell from interpreting most characters between two sets
    of double quotes
-   The special characters "$", "\`", "\\" and "!" retain their special
    meaning

Notes: Double quoted strings allow the "$", "\`", "\\" and "!" characters to
retain their special meanings. A double quoted string can contain the double
quote character within the string but it must be escaped.



### Pound Sign (Hash)
-   All characters after the "#" and before the newline are ignored by the
    shell
-   Effectively makes anything on the line after "#" a comment

Notes: The pound sign (or hash mark) is used to allow comments on the shell or
within shell scripts. The comments are not considered part of the command
string when executing but they are stored within the history. This is useful
for documenting why a command was run or what the command was expected to do.



## Shell Commands
-   [Simple Commands](#simple-commands)
-   [Pipelines](#pipelines)
-   [Lists of Commands](#lists-of-commands)
-   [Compound Commands](#compound-commands)



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
These are single command strings with a command followed by options and/or
arguments. These are usually designed to complete a specific task.



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
with another command. This allows the user to do things like search for a
specific string in the output of another command. When running commands in a
pipeline, each command is started at the same time and the shell waits for all
commands to complete.



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



## Working in the Shell
-   [Prompt](#prompt)
-   [Variables](#variables)
-   [Environment](#environment)
-   [Initialization Files](#initialization-files)



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



### Variables
-   variable: "apt or liable to vary or change; changeable" - dictionary.com
-   Named location to temporarily store information
-   Bash has several variables already defined
-   Names can contain a-z, A-Z, 0-9 and the underscore ("\_")
-   Names can NOT begin with 0-9
-   Setting/unsetting a variable will never include a "$"
-   Using a variable will always include a "$" before the name

Notes: Dictionary.com defines "variable" as something "apt or liable to vary or
change; changeable". A Bash shell variable is just a named location to store
temporary information. When creating a variable, the name can be upper or lower
case, can contain only letters, numbers and underscores but cannot start with
a number. When using variables a "$" will always precede the variable name but
when setting a variable's value, the "$" is not used.



### Variables (cont.)
-   Setting a variable takes the following form
```Bash
VAR_NAME="value or data"
```
-   Export variables to make them available to subprocesses
```Bash
export VAR_NAME="value or data"
```
-   An example of using a variable
```Bash
echo $HOME
echo ${HOME}
```

Notes: When setting a variable, use the form of variable name, an equals sign,
then the data to be stored in the variable. There should NOT be spaces around
the equals sign and if the data contains spaces it should be quoted. To make
the variable available to subprocesses of the shell, use the "export" keyword
and the variable name. This can be done when assigning a value to the variable
or after the value has been assigned. Lastly, to use a variable, the variable
name needs to be prefixed with the "$". Optionally, the variable name can be
enclosed in curly braces which signify the beginning and the end of the
variable name.



### Environment
-   Configured globally and on a per user basis
-   Consists of
    -   Shell options
    -   Variables
    -   Functions
    -   Aliases

Notes: The Bash environment allows for global and per user configuration. The
environment consists of preset shell options, variables, functions and aliases.
Each of these items can be configured independently.



### Environment - Shell Options
-   Shell options define the behavior of the Bash shell
-   Defined using the "set" command
-   Turn on an option using the "+" and off using the "-"
-   Examples
    -   Prevent overwriting of existing files
    ```Bash
    set +o noclobber
    ```
    -   Disable command history
    ```Bash
    set -o history
    ```
    -   Show full execution command
    ```Bash
    set +x
    set +o xtrace
    ```

Notes: The shell options help to define how the Bash shell behaves and can be
modified using the "set" command. When setting options, prefix the option with
a "+" to turn the option on and a "-" to turn the option off.



### Environment - Variables
-   Environment variables are essentially shell variables
-   Most can be displayed using the "env" command
-   Commonly modified
    -   PATH = List of paths to search for executables
    -   PS1 = Prompt definition
    -   HISTSIZE = Max number of commands to keep in the history list
    -   TERM = Terminal type and features

Notes: Environment variables are shell variables that are set on startup. They
work similarly to the shell options but are subject to change and/or be used
more often. Environment variables can be displayed using the "env" command.



### Environment - Functions
-   Shell functions are a grouping of commands under one name
-   May accept parameters (arguments)
-   Returns an exit code
-   Two ways to define
    ```Bash
    function MyFunction { commands; }

    MyFunction () { commands; }
    ```

Notes: Shell functions are a named grouping of commands to be run. These
functions can accept positional parameters and will return an exit code when
they complete. There are two ways to define a shell function but in either case
the grouped commands will be enclosed within the curly braces. Once defined,
functions can be executed just like a command.



### Environment - Aliases
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



## Shortcuts
-   [Key Combinations](#key-combinations)
-   [Shell Expansions](#shell-expansions)
-   History



### Key Combinations
-   TAB key
    -   Single press - attempt to complete depending on the starting character
        of the current token
    -   Double press - display all options for completion
-   Ctrl-c - cancel the current running process
-   Ctrl-a - Move to the beginning of the current line
-   Ctrl-e - Move to the end of the current line
-   Ctrl-f - Move the cursor forward one character
-   Ctrl-b - Move the cursor backward one character
-   Ctrl-l - Clear the screen
-   Ctrl-r - Search backward through history
-   Ctrl-s - Search forward through history
-   Ctrl-u - Clear the current line from the cursor to the beginning



### Shell Expansions
1.  [Brace Expansion](#brace-expansion)
2.  [Tilde Expansion](#tilde-expansion)
3.  [Shell Parameter and Variable Expansion](#shell-parameter-and-variable-expansion)
4.  [Command Substitution](#command-substitution)
5.  [Arithmetic Expansion](#arithmetic-expansion)
6.  [Process Substitution](#process-substitution)
7.  [Word Splitting](#word-splitting)
8.  [File Name Expansion](#file-name-expansion)

Notes: <http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_03_04.html>



### Brace Expansion
-   Brace expansions are the first expansion to be processed
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
brace expansions are not performed on the string(s) contained within.



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



## References
-   [Bash Reference](https://www.gnu.org/software/bash/manual/html_node/index.html#SEC_Contents)
-   [Bash Beginners Guide](http://tldp.org/LDP/Bash-Beginners-Guide/html/index.html)
-   [GitHub for this Presentation](https://github.com/mattjw79/bash_essentials)
