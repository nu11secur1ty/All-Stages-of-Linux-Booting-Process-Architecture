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









