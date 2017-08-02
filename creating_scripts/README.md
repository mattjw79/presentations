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



### Executing Shell Scripts
-   Add the execute permission and run the script directly
-   Run the script as an argument to a interpreter
-   A script can be called with a
    -   Relative path
    -   Absolute path
-   Scripts can be called directly, if the script is in a directory specified
    in the PATH



### Components of a Shell Script
-   The hash-bang #!
-   Comments - lines starting with "#"
-   Commands - simple or complex
-   Exit Code



#### The hash-bang
-   A.K.A. Shebang
-   Determines the interpreter to be used for the script
-   Is used when running the script directly
-   Specify any interpreter options



#### Comments
-   Comments in Bash shell scripts start with a hash ("#")
-   Can be specified after commands
-   Should help explain
    -   What commands are attempting to accomplish
    -   Why commands are being run



#### Commands
-   Any commands that can be run on the command line
    -   Simple Commands
    -   Pipelines
    -   Lists of Commands
    -   Compound Commands
-   The stdout and stderr become part of stdout and stderr of the script



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



### Control Structures
-   Branching
    -   if/then/else
    -   case
-   Looping
    -   while
    -   until
    -   for



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



#### while
-   Run a block of commands as long as a condition is true
```Bash
COUNT=0
while [[ ${COUNT} -lt 10 ]]; do
  echo "Current count: ${COUNT}"
  COUNT=$((${COUNT}+1))  # Increment COUNT by one
done
```



#### until
-   Run a block of commands as long as a condition is false
```Bash
COUNT=10
until [[ ${COUNT} -lt 0 ]]; do
  echo "Current count: ${COUNT}"
  COUNT=$((${COUNT}-1))  # Decrement COUNT by one
done
```



#### for
-   Run a block of code for each element passed in
-   Passed in elements are space separated
```Bash
for i in one two three four; do
  echo ${i}
done
```
