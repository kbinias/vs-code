## Configure SSH connection on Windows for remote development on Linux

1. Open Windows command prompt.
2. Generate a separate SSH key in file **id_rsa-remote-ssh**.
`ssh-keygen -t rsa -b 4096 -f %USERPROFILE%\.ssh\id_rsa-remote-ssh`
3. Add the contents of the local **id_rsa-remote-ssh.pub** file generated in step 2 to the appropriate authorized_keys file(s) on the SSH host.
`SET REMOTEHOST=name-of-ssh-host`
`SET PATHOFIDENTITYFILE=%USERPROFILE%\.ssh\id_rsa-remote-ssh.pub`
`scp %PATHOFIDENTITYFILE% %REMOTEHOST%:~/tmp.pub`
`ssh %REMOTEHOST% "mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat ~/tmp.pub >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys && rm -f ~/tmp.pub"`
4. In VS Code, run **Remote-SSH: Open Configuration File...** in the Command Palette **(F1)**, select an SSH config file, and add (or modify) a host entry as follows:
> Host name-of-ssh-host   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;User your-user-name-on-host   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;HostName host-fqdn-or-ip-goes-here   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;IdentityFile ~/.ssh/id_rsa-remote-ssh   

Example of config file:
> Host my_machine   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;User kbinias   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;HostName 192.168.12.34   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;IdentityFile ~/.ssh/id_rsa-remote-ssh
