# Managing Users and Groups
#### Matt Whitney



## Overview
-   [What is a user account?](#what-is-a-user-account)
-   [Login Process and Files](#login-process-and-files)
-   [User Management](#user-and-group-management-commands)
-   [Group Management](#user-and-group-management-commands)
-   [Managing Root Account Security](#managing-root-account-security)
-   [Security Focused Log Files](#security-focused-log-files)



## What is a user account?
-   A persons
    -   Files
    -   Resources
    -   Information
-   Represented by
    -   Username
    -   Password

Notes: A user account is a collection of a person's files, resources and other
information. This collection is represented by a username and password.



## Login Process and Files
-   [Logging In](#logging-in)
-   [Passwd File](#passwd-file)
-   [Group File](#group-file)
-   [Shadow File](#shadow-file)



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

Notes: When logging into the Linux environment on a command console, the user
is prompted to input their username and their password (which is not
displayed). Once the username and password are verified correct, the user's
environment is created with the user's ID, group ID, variables, ulimit and
umask. Last, the shell that is defined for the user is started.



### Passwd File
-   /etc/passwd
    -   Login name
    -   Optional password (no longer used)
    -   User ID
    -   Group ID
    -   Comment field (Full name)
    -   Home directory
    -   Command interpreter (Shell)

Notes: The /etc/passwd file is a colon (":") separated file. It contains the
user's login name, a password field that is no longer used, the numerical user
ID and group ID. The last three fields are the comment field, the path to the
user's home directory and the path to the command interpreter. The comment
field can be further divided using commas (',').



### Group File
-   /etc/group
    -   Group name
    -   Optional password
    -   Group ID
    -   User list

Notes: The /etc/group file is also a colon (":") separated file. The field
order is group name, an optional password, a numerical group ID and finally,
a comma separated member list. Theoretically, there is no limit to the number
of users that can belong to one group. However, all users in that group must
exist on the same line.



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
    -   Reserved

Notes: As with the passwd and group files, the /etc/shadow file continues the
tradition of colon separated. After the login name, there's a hashed (NOT
encrypted) password. Along with that, the remaining data on each line deals
with when the password was last changed, the minimum and maximum password age,
how many days before the password expires to warn the user, how long after the
expiration date the password should be accepted, the expiration date of the
password, and the last field is reserved for future use.



## User Management
-   [Adding and Deleting Users](#adding-and-deleting-users)
-   [Modifying Users](#modifying-users)



### Adding and Deleting Users
-   Adding
    -   useradd - create a new user or update default new user information
        ```Bash
        useradd demouser
        ```
    -   Gets default settings from /etc/default/useradd
-   Deleting
    -   userdel - delete a user account and related files
        ```Bash
        userdel demouser
        ```
    -   Does not remove user's home directory by default

Notes: Adding a user is done with the "useradd" command. Using this command,
the /etc/passwd, /etc/shadow and sometimes the /etc/group files are modified.
The /etc/default/useradd file is used to provide default values to the useradd
command where needed. Removing a user is done with the "userdel" command. By
default, the userdel command does not remove the user's home directory. In
order to remove the user's directory as well, use the option "-r" or "--remove".



### Modifying Users
-   usermod - modify a user account
    ```Bash
    usermod -s /bin/tcsh demouser
    usermod -L demouser
    ```
-   chfn - change "finger" information
    ```Bash
    chfn -f \"Demo User\" demouser
    ```
-   chsh - change login shell
    ```Bash
    chsh -s /bin/tcsh demouser
    ```
-   passwd - update authentication tokens
    ```Bash
    passwd demouser
    ```

Notes: There are several commands to make changes to a user's account. The
"usermod" command covers most of the changes that need to be made. The other
commands allow changes to the "finger" information (comment data about the
user), changing the login shell and the passwd command to update the user's
password.



## Group Management
-   [Adding and Deleting Groups](#adding-and-deleting-groups)
-   [Modifying Groups](#modifying-groups)



### Adding and Deleting Groups
-   Adding
    -   groupadd - create a new group
    ```Bash
    groupadd demogroup
    ```
-   Deleting
    -   groupdel - delete a group
    ```Bash
    groupdel demogroup
    ```

Notes: The commands for adding and removing groups are similar to the user
management commands. Both the groupadd and groupdel commands modify the
/etc/group file.



### Modifying Groups
-   groupmod - modify a group definition on the system
```Bash
groupmod -g 7777 demogroup
```
-   gpasswd - administer /etc/group and /etc/gshadow
```Bash
gpasswd demogroup
gpasswd -a demouser demogroup
gpasswd -d demouser demogroup
```
-   usermod
```Bash
usermod -a -G demogroup demouser
```

Notes: When adding a user to a group, rather than a "group" command, the
usermod command is used.



## Managing Root Account Security
-   [Proper Use of Root Account](#proper-use-of-root-account)
-   [Substitute User](#substitute-user)
-   [Superuser Do](#superuser-do)



### Proper Use of Root Account
-   Root account has full access to everything
-   Should only be used when necessary
-   Should not be used for
    -   Web browsing
    -   Email
    -   Commands that are unknown/unfamiliar



### Substitute User
-   A.K.A. "su"
-   Switch to a target user account
    -   Defaults to the root account
    -   Requires the password of the target user
```Bash
    [duser@linux ~]$ su
    Password:
    [root@linux duser]#
```



### Superuser Do
-   A.K.A. "sudo"
-   Execute a command as another user
    -   Defaults to the root account
    -   Requires the password of the current user
-   Configured with visudo (/etc/sudoers)

![XKCD: Sandwich](https://imgs.xkcd.com/comics/sandwich.png)



## Security Focused Log Files
-   /var/log/wtmp (last)
-   /var/log/lastlog (lastlog)
-   /var/log/secure
-   who and w commands



### /var/log/wtmp
-   Binary file
-   Accessed with the "last" command
-   Show a history of user logins and system reboots

```Bash
[root@linux log]# last
root     pts/0        10.1.1.10        Wed Jul 26 09:10   still logged in
root     pts/0        10.1.1.10        Wed Jul 26 07:07 - 07:34  (00:27)
root     pts/0        10.1.1.10        Tue Jul 25 21:23 - 21:32  (00:08)
reboot   system boot  3.10.0-514.21.1. Tue Jul 25 21:04 - 21:04 (1+14:44)

wtmp begins Tue Jul 25 21:04:50 2017
[root@linux log]#
```



### /var/log/lastlog
-   Binary file
-   Accessed with the "lastlog" command
-   Shows the last login time for each user

```Bash
[root@linux log]#  lastlog
Username         Port     From             Latest
root             pts/0                     Wed Jul 26 10:53:57 -0400 2017
bin                                        **Never logged in**
daemon                                     **Never logged in**
adm                                        **Never logged in**
```



### /var/log/secure
-   Text file
-   Use tail/less/etc to access
-   Contains login related log messages

```Bash
[root@mattjw ~]# tail -f /var/log/secure
Jul 26 14:25:52 linux saslauthd[23915]: pam_unix(smtp:auth): check pass; user unknown
Jul 26 14:25:52 linux saslauthd[23915]: pam_unix(smtp:auth): authentication failure; logname= uid=0 euid=0 tty= ruser= rhost=
Jul 26 14:26:01 linux sshd[54734]: Connection closed by 10.1.1.10 [preauth]
Jul 26 14:26:02 linux sshd[54736]: Connection closed by 10.1.1.10 [preauth]
Jul 26 14:26:21 linux sshd[54708]: Received disconnect from 10.1.1.10: 11: disconnected by user
Jul 26 14:26:21 linux sshd[54708]: pam_unix(sshd:session): session closed for user root
Jul 26 14:27:46 linux sshd[54744]: Accepted publickey for root from 10.1.1.10 port 54423 ssh2: RSA fb:40:bc:d4:22:37:7a:1e:22:be:27:cc:c2:86:39
Jul 26 14:27:46 linux sshd[54744]: pam_unix(sshd:session): session opened for user root by (uid=0)
```



### who and w Commands
-   who
    -   Prints information about users currently logged in

```Bash
[root@linux ~]# who
root     pts/0        2017-07-26 14:27 (10.1.1.10)
[root@linux ~]#
```
-   w
    -   Prints who is logged in and what they are doing

```Bash
[root@mattjw ~]# w
 15:47:36 up 42 days,  7:08,  1 user,  load average: 0.00, 0.01, 0.05
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
root     pts/0    10.1.1.10        14:27    0.00s  0.00s  0.00s w
[root@mattjw ~]#
```
