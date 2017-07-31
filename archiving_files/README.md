# Archiving Files
#### Matt Whitney



## Overview
-   [What is a backup](#what-is-a-backup)
-   [RPO/RTO](#rpo-rto)
-   [Types of Backup Medium](#types-of-backup-medium)
-   [Backup Types](#backup-types)
-   [Schedule](#schedule)
-   [What to Backup](#what-to-backup)
-   [Linux Backup Utilities](#linux-backup-utilities)


### What is a Backup?
-   Redundant copy of data
-   Stored on a different physical device
-   Many times stored in a different geographical region
-   Used when primary copy of data is unavailable/unusable

Notes: A backup is a secondary, or redundant, copy of data. When making a
backup, the copy is stored on a different physical device. This ensures that if
one device fails, the data will still be available. To provide even more
security, the backups should be stored at a different geographical location.
These backups are used when the primary data has become unavailable or for some
other reason is unusable.



### RPO/RTO
-   RPO
    -   Recovery Point Objective
    -   How much data loss can be tolerated
-   RTO
    -   Recovery Time Objective
    -   How quickly does the data need to be restored

Notes: Two of the most common terms when discussing backups are RPO and RTO.
RPO, or Recovery Point Objective, is the metric used to determine how much
data loss can be tolerated. For example, if the New York stock exchange loses
even a few seconds of data, it would be extremely catastrophic. RTO, or
Recovery Time Objective, determines the amount of time that an organization
can survive an outage of the service. Again, if the New Your stock exchange
were to have a service outage for more than a few seconds, it would also be
catastrophic.



### Types of Backup Medium
-   Tape
-   CD/DVD/Bluray
-   Removable Hard Drive
-   NAS/SAN
-   Cloud
-   Replication w/ Hot/Warm Standby

Notes: There are many different types of mediums to store backup data. One of
the most common backup mediums is tape. Backup tapes are a very stable medium
and can store up to 15 TB of data. Tapes are most commonly used in enterprise
organizations. Other backup mediums include optical mediums, CD/DVD/Bluray,
removable hard drives, Network Attached Storage or Storage Area Networks,
cloud storage or backup solutions, or replication to a hot or warm standby
server.



### Backup Types
-   Full
    -   Backs up every specified file
-   Incremental
    -   Backs up only changed files since last full/incremental backup
-   Differential
    -   Backs up only changed files since last full backup

Notes: There are three main types of backups. The first, a full backup, backs
up every file specified for the system. This method is the slowest to backup
but ensures all files are copied to the storage medium. Full backups are also
the quickest to restore. Incremental backups will back up all files that have
changed since the last full or incremental backup. Differential backups will
backup only changed files since the last full backup. Typically, both
incremental and differential backups are combined with a full backup.



### Schedule
-   Typically on a weekly rotation
-   Pick one day for full backup
-   Rest of the days should be incremental or differential
-   Mixing incremental and differential can cause confusion and possible data loss
-   Backups should occur during the least system load

Notes: The most common backup schedule is a weekly rotation. Pick one day for
the full backup and then use either an incremental or differential backup for
the rest of the week. When making backups, it should be done when the system is
under the least load.



### What to Backup
-   User data files
-   Configuration files
-   Log files
-   Potential locations
    -   /etc
    -   /home
    -   /opt
    -   /root
    -   /var
    -   /srv

Notes: Backups are extremely situation dependent. When deciding what to backup
on a system, you must take into account any user data files, configuration
files, log files or even application specific files. 



### Linux Backup Utilities
-   tar
    -   Tape Archive
-   cpio
    -   Copy Into or Out of an archive
-   dd
    -   Data Duplicator



### The tar Command
-   Packages a list of files into a single archive
-   If a tar archive is compressed, it's called a tarball
```Bash
tar -cvf /path/to/archive.tar list of files
tar -czvf /path/to/archive.tar.gz list of files
```
-   Files can be appended or updated in tar archive
-   Using the "-d" option, you can compare the files in the archive with system files



### Extract from tar
-   Extract from a compressed archive
    -   The "-z" option extracts from gzip files
    -   The "-j" option extracts from bzip2 files
-   Extracting from an archive will overwrite system files by default
```Bash
tar -xvf /path/to/archive.tar
```
-   Individual files from an archive can be extracted
```Bash
tar -xvf /path/to/archive.tar list of files
```



### The cpio Command
-   Creates an archive from a list of files passed on stdin
-   Does not descend into directories
-   Can accept the output of other commands
-   Use the "-o" option to create an archive
-   Use the "-i" option to extract from an archive



### The dd Command
-   Copies data using records
-   The "if" option is the source file
-   The "of" option is the destination file
-   Can be used to copy partitions or entire disk
-   Allows partial file copies
