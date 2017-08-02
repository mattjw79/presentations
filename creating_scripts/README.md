# Creating Scripts
#### Matt Whitney



## Overview
-



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
    -   Directly, if the script is in a directory specified in the PATH



### Components of a Shell Script
-   The hash-bang #!
-   Comments - lines starting with "#"
-   Commands - simple or complex
-   Control Structures
-   Exit code



### The hash-bang
-   A.K.A. Shebang
-   Determines the interpreter to be used for the script
-   Is used when running the script directly
-   Specify any interpreter options



### Comments
-   Comments in Bash shell scripts start with a hash ("#")
-   Can be specified after commands
-   Should help explain
    -   What commands are attempting to Accomplish
    -   Why commands are being run



### Commands
-   Any commands that can be run on the command line
    -   Simple Commands
    -   Pipelines
    -   Lists of Commands
    -   Compound Commands
-   The stdout and stderr become part of stdout and stderr of the script
