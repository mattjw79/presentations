# Creating Scripts
#### Matt Whitney



## Overview
-   [What is a Shell Script](#what-is-a-shell-script)
-   [Executing Shell Scripts](#executing-shell-scripts)
-   [Components of a Shell Script](#components-of-a-shell-script)
-   [Reading Input from Users](#reading-input-from-users)
-   [Control Structures](#control-structures)



### What is a Shell Script?
-   Collection of Commands
-   Accomplishes a specific task
-   Used for automation
    -   Mundane
    -   Complex
    -   Repetitive

Notes: A shell script is a collection of commands that accomplish a specific
task. They can be used for automating mundane, complex and/or repetitive tasks.
Once a script is written, it can be used to complete that same task as many
times as needed.



### Executing Shell Scripts
-   Run the script as an argument to a interpreter
-   Add the execute permission and run the script directly
-   A script can be called with a
    -   Relative path
    -   Absolute path
-   Scripts can be called directly if the script is in a directory specified
    in the PATH

Notes: When executing a shell script, if the script file does not have the
execute permission assigned, it can be run as an argument to the interpreter.
For example, "bash /path/to/script.file" would run the script using the Bash
interpreter. If the script file is given the execute permission, that same
example could be run as "/path/to/script.file" without having to specify the
interpreter. Likewise, if the script is stored in a directory that is part of
the PATH and has the execute permission, the script can be run by typing in
just "script.file".



### Components of a Shell Script
-   The hash-bang "#!""
-   Comments - lines starting with "#"
-   Commands - simple or complex
-   Exit Code

Notes: Proper shell scripts always start with the hash-bang, then have any
number of comments and/or commands. Then end with an exit code.



#### The hash-bang
-   A.K.A. Shebang
-   Determines the interpreter to be used for the script
-   Is used when running the script directly
-   Specify any interpreter options

Notes: The hash-bang, also known as "shebang", describes the interpreter to be
used and any options that should apply to that interpreter. The hash-bang is
only used when the script is not an argument to an interpreter.



#### Comments
-   Comments in Bash shell scripts start with a hash ("#")
-   Can be specified after commands
-   Should help explain
    -   What commands are attempting to accomplish
    -   Why commands are being run

Notes: Comments do not affect how a script runs. The interpreter ignores any
text on the same line which occurs after the hash sign. Comments can be used
for many reasons but typically the most helpful comments are those that
describe what a command or commands are attempting to accomplish, or, why
the commands are being run.



#### Commands
-   Any commands that can be run on the command line
    -   Simple Commands
    -   Pipelines
    -   Lists of Commands
    -   Compound Commands
-   The stdout and stderr become part of stdout and stderr of the script

Notes: A script can contain any command that can be run on the command line,
including complex commands. When commands are run within a script, the
standard output and standard error become part of the standard output and/or
error of the script.



#### Variables
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



#### Exit Code
-   Numerical indicator of a command or script success
-   Valid values are 0 through 255
-   Exit code of zero is success
-   Non-zero exit codes are failures
-   Previous command's exit code is stored in the "?" variable
-   Set using "exit \<code\>" at the end of a script

Notes: All scripts and programs return a numerical status code. A code of zero
indicates that the command completed successfully and any other code indicates
the script failed. When a command exits, the status code is stored in the ?
variable until another command completes. To specify the exit status code for
a script, use the exit command. By default, the exit status of the script is
zero, or success.



### Reading Input from Users
-   Use the "read" command to get input from users
    -   Reads up to the first newline character by default
    -   Stores the input in the named variable
```Bash
[duser@linux ~]$ read MyNewVar      # read the next typed input
string to capture
[duser@linux ~]$ echo ${MyNewVar}   # print out the contents of the variable
string to capture
```

Notes: When scripts need user intervention to make a decision, we can use the
"read" command to prompt the user for input. The read command stores the input
in a specified variable for retrieval later on. By default, read will read the
users input up to the first newline character.



### Control Structures
-   Branching
    -   if/then/else
    -   case
-   Looping
    -   while
    -   until
    -   for

Notes: Simple automation can be done with a script that just runs commands
sequentially. However, for more complex automation, scripts will need to be
able to make decisions and be able to repeat blocks of commands.



#### if/then/else
-   If a condition is true, then run the first block of commands
-   If the condition is false, run the second block of commands
```Bash
if [[ 2 -gt 1 ]]; then
  echo "Two IS greater than one."
else
  echo "Are you nuts? What kind of math are you using?"
fi
```

Notes: With the if/then/else statement, the block of commands directly after
the "then" will be executed providing the condition is true. Optionally, when
the condition is false, the block of commands after the "else" will be executed
instead. To close the if statement, use the word "fi".



#### case
-   Check if an expression matches certain cases
```Bash
CURRDATE=$(date '+%m')
case ${CURRDATE} in
  10|11|12|01|02|03)
    echo 'Probably best to have a jacket.'
    ;;
  04|05|08|09)
    echo 'The jacket is probably optional.'
    ;;
  06|07)
    echo 'No jacket needed.'
    ;;
  *)
    echo 'What kind of calendar are you using...'
    ;;
esac
```

Notes: The "case" statement is similar to an if/then/else statement but it can
decide between multiple items. In the example, the script would advise having
a jacket between the months of Oct. through March.



#### while
-   Run a block of commands as long as a condition is true
```Bash
COUNT=0
while [[ ${COUNT} -lt 10 ]]; do
  echo "Current count: ${COUNT}"
  COUNT=$((${COUNT}+1))  # Increment COUNT by one
done
```

Notes: A while loop can run through a block of commands multiple times. It
will run the block of commands as long as the condition is true. Be aware that
if the condition never changes to false, then the loop will run forever.



#### until
-   Run a block of commands as long as a condition is false
```Bash
COUNT=10
until [[ ${COUNT} -lt 0 ]]; do
  echo "Current count: ${COUNT}"
  COUNT=$((${COUNT}-1))  # Decrement COUNT by one
done
```

Notes: Similar to the while loop, the until loop will also run through a block
of commands multiple times. However, for the until command to run through the
block of commands, the condition must be false. Once the condition turns to
true, the loop will no longer run. In this case, if the condition never changes
to true, the loop will run forever.



#### for
-   Run a block of code for each element passed in
-   Passed in elements are space separated
```Bash
for i in one two three four; do
  echo "Howdy"
  echo ${i}
done
```

Notes: The for loop is similar to the while and until loops only in that it
will also run through a block of commands multiple times. However, with the
for loop, it runs through those commands once for each of the items passed into
the loop.
