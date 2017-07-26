# Managing Users and Groups

### What is a user account?
-   A persons
    -   Files
    -   Resources
    -   Information
-   Represented by
    -   Username
    -   Password



### Logging In
-   Prompt for
    -   Username (clear text)
    -   Password (not displayed)
-   Password is verified for the user
-   Environment is created
    -   User ID (UID)
    -   Group ID (GID)
    -   Variables (HOME, SHELL, PATH, LOGNAME, MAIL)
    -   ulimit
    -   umask
-   Start user's shell



### Passwd File
-   /etc/passwd
    -   Login name
    -   Optional password (no longer used)
    -   User ID
    -   Group ID
    -   Comment field (Full name)
    -   Home directory
    -   Command interpreter (Shell)



### Group File
-   /etc/group
    -   Group name
    -   Optional password
    -   Group ID
    -   User list



### Shadow File
-   /etc/shadow
    -   Login name
    -   Hashed password
    -   Date of last password change
    -   Minimum password age
    -   Maximum password age
    -   Password warning period
    -   Password inactivity period
    -   Account expiration date
    -   Reservered



### User Management Commands
-   useradd
-   passwd
-   usermod
-   userdel
-   groupadd
-   groupmod
-   groupdel



### Adding Users
-   useradd
    ```Bash
    useradd demouser
    ```
-   Gets default settings from /etc/default/useradd



### Modifying Users
-   usermod
    ```Bash
    usermod -s /bin/tcsh demouser
    usermod -L demouser
    ```
-   chfn
    ```Bash
    chfn -f \"Demo User\" demouser
    ```
-   chsh
    ```Bash
    chsh -s /bin/tcsh demouser
    ```
-   passwd
    ```Bash
    passwd demouser
    ```



### Deleting Users
-   userdel
