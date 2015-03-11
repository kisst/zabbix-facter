# Zabbix-facter

## Basics
With the [facter]( https://github.com/puppetlabs/facter) you can collect general information about the server, and then use it as an inventory field. This is used in the puppet project to gather information about the platform and compile the code for it, but as an independent project it's still useful.
This userparameter need facter to be installed, but does not depend on puppet itself.

## Preparation 
to install facter run:

on debian flavor os
```shell
sudo apt-get install facter
```
on RedHat flavor OS
```shell
yum install facter
```


## Installation 
Installation is simple place the userparameter_facter.conf into the /etc/zabbix/zabbix_agentd.d folder, make sure you refer to that folder in the main conf and reload the agent.

```shell
echo "UserParameter=facter[*],/usr/bin/facter $1"> /etc/zabbix/zabbix_agentd.d/userparameter_facter.conf
augtool -s set /files/etc/zabbix/zabbix_agentd.conf/Include "/etc/zabbix/zabbix_agentd.conf.d/"
service zabbix-agent restart
```

and then just add the template on the web interface and assign the template to a host.
The template contains only basic facts, but could be extended with any, ( custom facts, aws specific etc )

## Notes
No sudo added so fact require root privileges like productname or serialnumber  will fail, if you need those setup a sudo line for facter, and change the conf.

PR's are welcome
