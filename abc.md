***Task 2:
Description : The same company xyz has provided one of his developers an oracle based application
which runs on a web logic server. Somehow the developer while trying to deploy the application is
getting file related errors and he somehow concludes that there are way too many files open in the
server via some editor or other commands like tails etc. So DevOps needs to identify the issue of too
many open files and solve it.*


Findings:

The ulimit command allows you to control the user resource limits in the system such as process data size, process virtual memory, and process file size, number of process etc.

$ ulimit -a
	>	core file size          (blocks, -c) 0
	>	data seg size           (kbytes, -d) unlimited
	>	scheduling priority             (-e) 0
	>	file size               (blocks, -f) unlimited
	>	pending signals                 (-i) 3802
	>	max locked memory       (kbytes, -l) 16384
	>	max memory size         (kbytes, -m) unlimited
	>	open files                      (-n) 1030
	>	pipe size            (512 bytes, -p) 8
	>	POSIX message queues     (bytes, -q) 819200
	>	real-time priority              (-r) 0
	>	stack size              (kbytes, -s) 8192
	>	cpu time               (seconds, -t) unlimited
	>	max user processes              (-u) 3802
	>	virtual memory          (kbytes, -v) unlimited
	>	file locks                      (-x) unlimited


In linux , Socket connections are treated as files. So any socket connection created by any linux process will be consider one open file.
 
weblogic java process create lot of socket connections, it might create the maximum limit of open files which a process can open.
 
To find max open file limit: 

$ ulimit -n

ulimit further divided into soft limit and hard limit.
 
Soft Limit :- 
Soft limit means process will be allowed to go beyond this limit but it is warning that you are exceeding your resource consumption. And it will meet your hard limit soon.
 
$ ulimit -S -n
 
 
HardLimit :- 
Hard limit is a full stop for a process, Process will not be allowed to create more connection than this count. 

$ ulimit -H -n.
 

Solution:


In case of weblogic application running on linux server might creating so many connections like 3k - 4k connections. We have to increase the limit.
The maximum number of file descriptors is controlled two different ways:

a) Per-User Limit:

1. Explicitly set the number of file descriptors using the ulimit command
$ ulimit -n <open count>
 
ex: $ ulimit -n 8096
 
Note:
ulimit -n command show default soft limit , but when we set this using ulimit -n <open count> it set hard and soft. so if your hard limit is 8096 and you did ulimit -n 4096 , it will set your hard and soft limit to 4096 for that linux session.

2. Set below values in /etc/security/limits.conf
 
* soft nofile 65536
* hard nofile 65536
 
The new value can be set in /etc/security/limits.conf (need to logout and login again or requires OS restart to take effect) 
 
pam-limits
If above changes are not working for then add below value in /etc/pam.d/common-session

session required pam_limits.so


b) System-Wide Limit
Set this higher than user-limit set above /etc/sysctl.conf

fs.file-max = 2097152

$ sysctl -p

This will will increase “total” number of files that can remain open system-wide.

Verify New Limits

cat /proc/sys/fs/file-max

Hard Limit
$ ulimit -Hn

Soft Limit
$ ulimit -Sn


Check limit for other user

$ su - <user> -c 'ulimit -aHS' -s '/bin/bash'


