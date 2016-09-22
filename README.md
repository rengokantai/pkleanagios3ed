## pkleanagios3ed
###Chapter 10. Monitoring Remote Hosts
####Monitoring over SSH
Once Nagios schedules an active check to be performed, the ```check_by_ssh``` plugin runs the ssh command to connect to the remote host's SSH server.

#####Configuring the SSH connection
on local machine
```
root@nagiosserver:~# su -s /bin/bash nagios
nagios@nagiosserver:~$ ssh-keygen
```

on remote machine
```
root@remotehost:~# groupadd nagios
root@remotehost:~# useradd -g nagios -d /opt/nagios nagios
root@remotehost:~# mkdir /opt/nagios
root@remotehost:~# chown nagios:nagios /opt/nagios
root@remotehost:~# chmod 0700 /opt/nagios
```

create .ssh folder
```
root@remotehost:~# mkdir /opt/nagios/.ssh
root@remotehost:~# echo 'ssh-rsa 12345678 nagios@nagiosserver' /opt/nagios/.ssh/authorized_keys 
root@remotehost:~# chown nagios:nagios /opt/nagios/.ssh /opt/nagios/.ssh/authorized_keys
root@remotehost:~# chmod 0700 /opt/nagios/.ssh /opt/nagios/.ssh/authorized_keys
```
test connection
```
ssh -v nagios@remoteip
nagios@nagiosserver:~$ /opt/nagios/plugins/check_by_ssh  -H remoteip -C "/opt/nagios/plugins/check_apt"
```
