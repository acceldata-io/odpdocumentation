You can download the Ambari and ODP repositories. The links for the same can be obtained by contacting the [Acceldata Support](https://acceldata.force.com/) team. 


# Setting up Local Repository

You must execute the following steps to setup local repository. 

1. You must install Httpd service by executing the following command. 

`yum install httpd -y`

2. Extract the Ambari and ODP repositories under (/var/www/html/repo) directory by executing the following commands.

```
cd /var/www/html/\
tar -xvzf AMBARI-2.7.6.0.0_15Feb23_latest_orig.tar.gz -C /var/www/html/\
tar -xvzf ODP-3.2.2.0-1_15Feb23_latest_orig.tar.gz -C /var/www/html/
```

3. Create Ambari and ODP repositories by executing the following commands. 
```
cat /etc/rum.repos.d/ambari.repo
[AMBARI-2.7.6.0.0]
baseurl=http://<repo-host>/repos/AMBARI-2.7.6.0.0/
gpgcheck=0
name=ambari
enable=1

[ODP-3.2.2.0-1]
baseurl=http://<repo-host>/repos/ODP-3.2.2.0-1/
gpgcheck=0
name=ODP
enable=1
```

4. Verify Ambari repository by executing the following commands. 
```
$ yum clean all\
$ yum repolistt\
\
repo id                repo name                          status
AMBARI-2.7.6.0.0        ambari                     	   35
ODP-3.2-repo-4          ODP-3.2-repo-4                     132
```

5. Place the **ambari.repo** file on the host you plan to use for the Ambari server by executing one of the following commands

* For RHEL/CentOS/Oracle/Amazon Linux execute the following command.

`/etc/yum.repos.d/ambari.repo`

* For SLES execute the following command. 

`/etc/zypp/repos.d/ambari.repo`

* For Debain/Ubuntu execute the following command.

`/etc/apt/sources.list.d/ambari.list`

