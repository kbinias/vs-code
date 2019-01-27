## Increase permanently max number of open files limit in Ubuntu 16.04

#### Maximum capability of system
$ `cat /proc/sys/fs/file-max`  
708444

#### Current available limit
$ `ulimit -n`  
1024

#### To increase the available limit to 2048
$ `sudo vim /etc/sysctl.conf`

#### Add the following line to file
`fs.file-max = 2048`

#### Run this to refresh with new config
$ `sudo sysctl -p`

#### Edit the following file
$ `sudo vim /etc/security/limits.conf`

#### Add following lines to file
`* soft  nofile  2048`  
`* hard  nofile  2048`  
`root soft nofile 2048`  
`root hard nofile 2048`

#### Edit the following file
$ `sudo vim /etc/pam.d/common-session`

#### Add this line to it
`session required pam_limits.so`

#### Logout and login and try the following command
$ `ulimit -n`  
2048
