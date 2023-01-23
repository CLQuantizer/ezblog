---
date: 2023-01-31
authors:
  - ezio
---
**#What is dumped when "core dumped"?**

**## A not so good explanation**

Adapted from [geekforgeeks](https://www.geeksforgeeks.org/core-dump-segmentation-fault-c-cpp/):

Core Dump/Segmentation fault is a specific kind of error caused by accessing memory that “does not belong to you.” In other words, when a piece of code tries to do write operation in a read only location in memory or freed block of memory, it is known as core dump.

Here is an example in C (isn't it easy to write bad code in C?)
N.b. do not try this on softboy **Mac**. Try this on alpha ubuntu to get the real toxic thang.

```
int main()
{
char *str;
str = "abc";	
*(str+1) = 'n';
return 0;
}
```

But this does not really explain what is being dumped. Something has to be dumped, thrown away into the dumpster right? What is it that is dumped?

The next bit is adapted from [wikipedia](https://en.wikipedia.org/wiki/Core_dump)

In computing, a core dump **consists of the recorded state of the working memory of a computer program at a specific time**, generally when the program has crashed.

In practice, the program counter and stack pointer, and operating system flags and information are dumped too. They can be used in diagnosing and debugging errors in computer programs.


**## Extra bit from wikipedia**
Magnetic-core memory was the mainstream random-access memory 1950-1970. The name has long outlived the technology.

Earliest core dumps were paper printouts of Strings representing the content of the memeory. Later they were written to tapes and disks.

Linux typically writes dump to "/var/lib/systemd/coredump" as file.
Mac is very different.

**## Man 5 core** 
Run ```man 5 core``` to see the following. It is crazy.
```
NAME
       core - core dump file

DESCRIPTION

The  default  action  of certain signals is to cause a process to terminate and produce a core dump file, a disk file containing an image of the process's memory at the time of termination.  This image can be used in a debugger (e.g., gdb(1)) to inspect the state of the program at the time that it terminated.

A  list  of  the signals which cause a process to dump core can be found in signal(7). A process  can set its soft RLIMIT_CORE resource limit to place an upper limit on the size of the core dump file that will be produced if it receives a "core dump"

There are various circumstances in which a core dump file is not produced:

-  The process does not have permission to write the core file.**

-  A (writable, regular) file with the same name as would be used for the core dump already exists, but there is more than one hard link to that file.

-  The filesystem where the core dump file would be created is full; or has run out of inodes; or is mounted read-only; or the user has reached their quota for the filesystem.

-  The directory in which the core dump file is to be created does not exist.

-  The  RLIMIT_CORE  (core  file  size)  or  RLIMIT_FSIZE (file size) resource limits for the process are set to zero; see getrlimit(2) and the documentation of the shell's ulimit command (limit in csh(1)).

-  The binary being executed by the process does not have read permission enabled.

-  The process is executing a set-user-ID (set-group-ID) program that is owned by a user (group) other than the real user (group) ID of the process, or the  process is  executing  a  program that has file capabilities (see capabilities(7)).  (However, see the description of the prctl(2) PR_SET_DUMPABLE operation, and the description of the /proc/sys/fs/suid_dumpable file in proc(5).)

-  /proc/sys/kernel/core_pattern is empty and /proc/sys/kernel/core_uses_pid contains the value 0.  (These files are described below.)  Note that if  /proc/sys/ker‐nel/core_pattern  is  empty  and /proc/sys/kernel/core_uses_pid contains the value 1, core dump files will have names of the form .pid, and such files are hidden unless one uses the ls(1) -a option.

-  (Since Linux 3.7) The kernel was configured without the CONFIG_COREDUMP option.

In addition, a core dump may exclude part of the address space of the process if the madvise(2) MADV_DONTDUMP flag was employed.

On systems that employ systemd(1) as the init framework, core dumps may instead be placed in a location determined by systemd(1).  See below for further details.
```