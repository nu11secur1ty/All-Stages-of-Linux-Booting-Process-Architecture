# Linux renice

- Description

renice alters the scheduling priority of one or more running processes.

A higher value of priority actually makes the process lower priority; it means that the process will demand fewer system resources (and therefore is a "nicer" process). A lower priority value means that the process will demand more resources, possibly denying those resources to processes that are "nicer".

The priority value of any given process can vary from -20 (highest priority, least "nice") to 20 (lowest priority, "nicest"). The default priority of new processes, by default, is 0.

renice'ing a process group causes all processes in the process group to have their scheduling priority altered.

renice'ing a user causes all processes owned by the user to have their scheduling priority altered.

By default, the processes to be affected are specified by their process ID's.


# Syntax

```bash
renice [-n] priority [[-p] pid who...] [[-g] pgrp who...] [[-u] user who...]
```
```bash
renice -h | -v
```
- Options
```table
-n, --priority 	The scheduling priority of the process, process group, or user.
-g, --pgrp 	Force who parameters to be interpreted as process group ID's.
-u, --user 	Force the who parameters to be interpreted as user names.
-p, --pid 	Resets the who interpretation to be (the default) process ID's.
-v, --version 	Display version information, and exit.
-h, --help 	Display a help message, and exit.
```
- more
```bash
renice --help

Usage:
 renice [-n] <priority> [-p|--pid] <pid>...
 renice [-n] <priority>  -g|--pgrp <pgid>...
 renice [-n] <priority>  -u|--user <user>...

Alter the priority of running processes.

Options:
 -n, --priority <num>   specify the nice increment value
 -p, --pid <id>         interpret argument as process ID (default)
 -g, --pgrp <id>        interpret argument as process group ID
 -u, --user <name>|<id> interpret argument as username or user ID

 -h, --help             display this help
 -V, --version          display version
```


- Priority

Users other than the superuser may only alter the priority of processes they own, and can only monotonically increase their "nice value" within the range 0 to PRIO_MAX (20). The superuser may alter the priority of any process and set the priority to any value in the range PRIO_MIN (-20) to PRIO_MAX.

Useful settings for priority are:

   - 20: the affected processes will run only when nothing else in the system needs the resources.
   - 0: the default.
   - any negative value: will make things go very fast, at the expense of other processes.


- Examples

```bash
renice +1 987 -u daemon root -p 32
```


Change the priority of process IDs 987 and 32, and all processes owned by users daemon and root, to be one greater (+1, one increment "nicer") than its current value.

- Related Commands
```table
kill — Send a signal to a process, affecting its behavior or killing it.
nice — Invoke a command with an altered scheduling priority.
ps — Report the status of a process or processes.
top — Display a sortable, continually-updated list of processes.
```


# Examples
How to decrease the priority of a running process? (Increase nice)

In the example below, an existing shell-script is running at nice value of 10. (6th column in the ps output)

```bash
$ ps axl | grep nice-test
0   509 13245 13216  30  10  5244  968 wait   SN   pts/1      0:00 /bin/bash ./nice-test.sh
```
To increase the nice value (thus reducing the priority), execute the renice command as shown below.

```bash
$ renice 16 -p 13245
13245: old priority 10, new priority 16

$ ps axl | grep nice-test
0   509 13245 13216  36  16  5244  968 wait   SN   pts/1      0:00 /bin/bash ./nice-test.sh
```

[Note: Now, the 6th column of the nice-test.sh (PID 13245) shows the new nice value of 16.]
How to increase the priority of a running process? (Decrease nice)

In the example below, an existing shell-script is running at a nice value of 10. (6th column in the ps output)

```bash
$ ps axl | grep nice-test
0   509 13254 13216  30  10  4412  968 wait   SN   pts/1      0:00 /bin/bash ./nice-test.sh
```
In increase the priority, give a lower nice value as shown below. However, only root can increase the priority of a running process, else you’ll get the following error message.

```bash
$ renice 5 -p 13254
renice: 13254: setpriority: Permission denied
Login as root to increase the priority of a running process

$ su -

# renice 5 -p 13254
13254: old priority 10, new priority 5

# ps axl | grep nice-test
0   509 13254 13216  25   5  4412  968 wait   SN   pts/1      0:00 /bin/bash ./nice-test.sh
```
[Note: The 6th column now shows a lower nice value of 5 (increased priority)]
















