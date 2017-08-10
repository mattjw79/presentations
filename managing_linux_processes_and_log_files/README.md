# Managing Linux Processes and Log Files
#### Matt Whitney



## Overview
-   [What is a Process?](#what-is-a-process)
-   [Process Ancestry](#process-ancestry)
-   [Process IDs](#process-ids)
-   [Viewing Processes](#viewing-processes)
-   [Process Priority](#process-priority)
-   [Foreground and Background Processes](#foreground-and-background-processes)
-   [Signals](#signals)
-   [Sending Signals](#sending-signals)
-   [Managing Linux Log Files](#managing-linux-log-files)



### What is a Process?
-   A program in execution
    -   Binary executables
    -   Internal shell commands
    -   Shell scripts
-   Destroyed when the command exits
-   Created by human interaction or another process

Notes:  A process is a program that is currently in execution. It could be a
binary executable, internal shell command or a shell script. Processes are
created by another process (parent) or by human interaction and are destroyed
when the command exits.



### Process Ancestry
-   All processes have
    -   A process ID number, known as the PID
    -   A parent PID, known as the PPID
-   Can have child processes
-   Kernel is the first process, PID 0
-   The "init" or "systemd" process is PID 1

Notes: Every process that's created on a Linux system has a process ID number,
or PID, and also a parent PID, or PPID. A process can spawn other processes and
these spawned processes are called children. When Linux starts, the kernel gets
the PID number 0 and the "init" or "systemd" process is always PID number 1.



### Process IDs
-   Assigned sequentially
-   Default range is 0 to 32768
-   Wraps when the highest number is reached
-   Skips any already assigned numbers

Notes: Process IDs are assigned sequentially. PID numbers range from 0 to 32768
but as previously stated, 0 and 1 are used for the kernel and init processes.
When the PID numbers reach 32768, the system wraps back around to the lowest
number available. If it reaches a PID that is currently in use, it skips that
PID number and continues on with the next.



### Viewing Processes
-   top
    -   Displays Linux processes
-   ps
    -   Snapshot of the current processes
-   free
    -   Displays free and used memory

Notes: The main tools for managing processes are "top" and "ps". The top
command will show several pieces of information that will help in managing a
Linux system. The first line shows the system's uptime and load average, the
next line shows the task states of all the tasks on the system. After that are
CPU and memory statistics. The rest of the top display shows some of the
current processes running on the system, sorted by highest CPU usage by
default. The ps command shows a snapshot of the current processes in the
kernel's process table. By default, ps will only show the processes in the
current session but given the proper options, will be able to show all
processes on the system. The last command, free, will print the available and
used memory.



### Process Priority
-   Every process has a priority
    -   Larger numbers are a lower priority
    -   Smaller numbers are a higher priority
-   Child processes inherit their priority from their parent
-   Higher priority processes receive larger portions of CPU time
-   Priorities are set/changed with nice and renice commands

Notes: Not all processes are created equal, each process has a priority. Higher
numbers indicate a lower priority and will receive less system resources than
processes with lower numbers. When a child process is started, it receives the
same priority as the parent. A normal user can use the priorities of 0
through 20 but a super-user can assign priorities between 0 and -20.



### Foreground and Background Processes
-   Processes run in the foreground by default
-   Add an "&" at the end of the command to run it in the background
-   List processes in the background using "jobs"
    -   Use "fg" with the job number to bring it to the foreground
    -   Use "bg" with the job number to send it to the background

Notes: When working on the command line, processes typically run in the
foreground. Using the "&", the command will then be run in the background. To
list the jobs running in the background, use the "jobs" command. A process can
be moved from the background to the foreground, and back again using the "fg"
and "bg" commands.



### Signals
-   Signals
    -   SIGHUP (1)
        -   Sends a "hangup" to a process
        -   Typically restarts a process
    -   SIGINT (2)
        -   Send an "interrupt" to a process
    -   SIGKILL (9)
        -   Forcefully stops a process
        -   Process cannot ignore
    -   SIGTERM (15)
        -   Sends a "terminate" signal
        -   Process can ignore

Notes: There are many signals (or notifications) that can be sent to a process.
Of these signals, the SIGHUP, SIGINT, SIGKILL and SIGTERM are the most common
signals that a systems administrator will use. The SIGHUP signal can cause a
system process to restart or reload it's configuration files. SIGINT is the
same signal that is sent when a CTRL-C key combination is sent. SIGTERM is a
polite way of asking a process to exit but the process can "catch" or ignore
this signal. The SIGKILL will forcefully stop a process from running and
cannot be ignored.



### Sending Signals
-   Use the "kill" command to send a signal to a process
-   The default signal for the kill command is SIGTERM (15)
-   The SIGKILL (9) and SIGSTOP (19) cannot be ignored
-   Use "kill -9 \[pid\]" to forcefully terminate a process
    -   Use sparingly as the process is not allowed to cleanup resources

Notes: The "kill" command is used to send a signal to a process. It can be
used to send a SIGHUP, which in the case of most system processes is like
asking it to restart or reload it's configuration. The default signal that the
kill command sends is the SIGTERM, which asks the process to exit gracefully.
The SIGKILL and SIGSTOP are the only two signals that a process cannot ignore.
Use of the SIGKILL should be limited to a last resort as this forcefully stops
the process and does not allow it to clean up resources.



### Managing Linux Log Files
-   Logs are stored in /var/log
-   Syslog
    -   Configured with /etc/syslog.conf
    -   Facility - subsystem providing log message
    -   Priority - determines the importance of the message
    -   Destination - which file in which to store the log messages
-   Rotated with "logrotate"
    -   Configured with /etc/logrotate.conf

Notes: Log files are almost always stored in the /var/log directory. The
writing of logs is typically handled by the Syslog daemon (Syslog-NG or RSyslog
are more configurable alternatives that modern distributions use). With Syslog,
the configuration file is /etc/syslog.conf and contains lines that define the
facility, priority and destination file. The log files that Syslog creates can
become very large and cumbersome if enough data is written to them. To help
manage the log files and keep them useable, the logrotate daemon is configured
to move old logs and make way for new log files.
