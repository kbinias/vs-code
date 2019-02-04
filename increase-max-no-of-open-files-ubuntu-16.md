## Increase permanently max number of open files limit in Ubuntu 16.04

#### Increase the available limit (system-wide limit)
$ `sudo vim /etc/sysctl.conf`

#### Add the following line to file
`fs.file-max = 2097152`

#### Run this to increase total number of files that can remain open system-wide
$ `sudo sysctl -p`

#### Edit the following file (per-user limit)
$ `sudo vim /etc/security/limits.conf`

#### Add following lines to file
`* soft  nofile  600000`
`* hard  nofile  600000`
`root soft nofile 600000`
`root hard nofile 600000`

#### Edit the following file
$ `sudo vim /etc/pam.d/common-session`

#### Add this line to it
`session required pam_limits.so`

#### Logout and login

#### Check new limits
Hard limit `ulimit -Hn`
Soft limit `ulimit -Sn`
Max limit `cat /proc/sys/fs/file-max`
