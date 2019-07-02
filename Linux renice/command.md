# Linux renice

- Description

renice alters the scheduling priority of one or more running processes.

A higher value of priority actually makes the process lower priority; it means that the process will demand fewer system resources (and therefore is a "nicer" process). A lower priority value means that the process will demand more resources, possibly denying those resources to processes that are "nicer".

The priority value of any given process can vary from -20 (highest priority, least "nice") to 20 (lowest priority, "nicest"). The default priority of new processes, by default, is 0.

renice'ing a process group causes all processes in the process group to have their scheduling priority altered.

renice'ing a user causes all processes owned by the user to have their scheduling priority altered.

By default, the processes to be affected are specified by their process ID's.
