This section explains the environment related settings for Ambari Server.

# Set Up Password less SSH
To have Ambari Server automatically install Ambari Agents on all your cluster hosts, you must set up password-less SSH connections between the Ambari Server host and all other hosts in the cluster. The Ambari Server host uses SSH public key authentication to remotely access and install the Ambari Agent.

**Note**: You can choose to manually install an Ambari Agent on each cluster host. In this case, you do not need to generate and distribute SSH keys.

1. Generate public and private SSH keys on the Ambari Server host.\
`ssh-keygen`
2. Copy the SSH Public Key (id_rsa.pub) to the root account on your target hosts.\
`.ssh/id_rsa` and `.ssh/id_rsa.pub`
3. Add the public key to the target host.\
`ssh-copy-id -i /root/.ssh/id_rsa.pub root@odp{1-4}-test.adsre.com`
4. Depending on your version of SSH, you may need to set permissions on the .ssh directory (to 700) and the authorized_keys file in that directory (to 600) on the target hosts.
`chmod 700 ~/.ssh`\
`chmod 600 ~/.ssh/authorized_keys`\
5. From the Ambari Server, make sure you can connect to each host in the cluster using SSH, without having to enter a password.
`ssh root@odp{1-4}-test.adsre.com`

# Set Up Service User Accounts
Each service requires a service user account. The Ambari Cluster Install wizard creates new and preserves any existing service user accounts, and uses these accounts when configuring Hadoop services. Service user account creation applies to service user accounts on the local operating system and to LDAP/AD accounts.

# Enable NTP/chrony on the Cluster and on the Browser Host
Install NTP and Chrony on RHEL/CentOS and Ubuntu.

## RHEL/CentOS:
**Install NTP**: Run the command `yum install ntp` and start the NTP service using the command `systemctl start ntpd`.\
or\
**Install Chrony**: Run the command `yum install chrony` and start the Chrony service using the command `systemctl start chronyd`.

## Ubuntu:
**Install NTP**: Run the command `sudo apt-get install ntp` and start the NTP service using the command `sudo systemctl start ntp`.
or
**Install Chrony**: Run the command sudo apt-get install chrony and start the Chrony service using the command `sudo systemctl start chrony`.

# Check DNS and NSCD

All hosts in your system must be configured for both forward and reverse DNS.\
\
If you are unable to configure DNS in this way, you should edit the `/etc/hosts` file on every host in your cluster to contain the IP address and Fully Qualified Domain Name of each of your hosts. The following instructions are provided as an overview and cover a basic network setup for generic Linux hosts. Different versions and flavors of Linux might require slightly different commands and procedures. Please refer to the documentation for the operating system(s) deployed in your environment.

Hadoop relies heavily on DNS, and as such performs many DNS lookups during normal operation. To reduce the load on your DNS infrastructure, it's highly recommended to use the Name Service Caching Daemon (NSCD) on cluster nodes running Linux. This daemon will cache host, user, and group lookups and provide better resolution performance, and reduced load on DNS infrastructure.

# Configuring iptables if enabled and Disable Firewalld service

For Ambari to communicate during setup with the hosts it deploys to and manages, certain ports must be open and available. The easiest way to do this is to temporarily disable iptables, as follows:

## RHEL/CentOS/Oracle/Amazon Linux
`systemctl disable firewalld`\
`service firewalld stop`

## SLES
`rcSuSEfirewall2 stop`\
`chkconfig SuSEfirewall2_setup off`

## Ubuntu

`sudo ufw disable`\
`sudo iptables -X`\
`sudo iptables -t nat -F`\
`sudo iptables -t nat -X`\
`sudo iptables -t mangle -F`\
`sudo iptables -t mangle -X`\
`sudo iptables -P INPUT ACCEPT`\
`sudo iptables -P FORWARD ACCEPT`\
`sudo iptables -P OUTPUT ACCEPT`

## Debian

`sudo iptables -X`\
`sudo iptables -t nat -F`\
`sudo iptables -t nat -X`\
`sudo iptables -t mangle -F`\
`sudo iptables -t mangle -X`\
`sudo iptables -P INPUT ACCEPT`\
`sudo iptables -P FORWARD ACCEPT`\
`sudo iptables -P OUTPUT ACCEPT`

You can restart iptables after setup is complete. If the security protocols in your environment prevent disabling iptables, you can proceed with iptables enabled, if all required ports are open and available.\
\
Ambari checks whether iptables is running during the Ambari Server setup process. If iptables is running, a warning displays, reminding you to check that required ports are open and available. The Host Confirm step in the Cluster Install Wizard also issues a warning for each host that has iptables running.

# Disable SELinux and PackageKit and check the umask Value
1. You must disable SELinux for the Ambari setup to function. On each host in your cluster, enter:\
`setenforce 0`

To permanently disable SELinux set `SELINUX=disabled` in `/etc/selinux/config`  This ensures that SELinux does not turn itself on after you reboot the machine.\
\
2. UMASK (User Mask or User file creation MASK) sets the default permissions or base permissions granted when a new file or folder is created on a Linux machine. Most Linux distros set 022 as the default umask value. A umask value of 022 grants read, write, execute permissions of 755 for new files or folders. A umask value of 027 grants read, write, execute permissions of 750 for new files or folders.\
\
Ambari, and ODP, support umask values of 022 (0022 is functionally equivalent), 027 (0027 is functionally equivalent). These values must be set on all hosts.

## UMASK Examples:
Setting the umask for your current login session:\
`umask 0022`

## Checking your current umask:
umask
Permanently changing the umask for all interactive users:\
`echo umask 0022 >> /etc/profile`

# Download and set up Database Connectors

Components like Hive, Ranger, Oozie, and Hue require an operational database. During installation, you have the option to use an existing database or have Ambari install a new instance, in the case of Hive. For Ambari to connect to the database of your choice, you must download the necessary database drivers and connectors directly from the database vendor before installing the component. To better prepare for your install, set up the database connectors as you set up your environment.

## Using Ambari with MySQL or MariaDB

Before setting up Ambari Server with an existing MySQL or MariaDB database; obtain the appropriate connectors and .jar files, create an Ambari user with sufficient permissions, and load the Ambari database schema.

### Before you Begin
Determine the appropriate database version and obtain the release drivers and .jar file.
* On the Ambari Server host, stage the appropriate connector/JDBC driver file for later deployment.
    - On the Ambari Server host, [Download the MySQL Connector/JDBC driver from MySQL](https://dev.mysql.com/downloads/connector/j/)
    - Run ambari-server setup `--jdbc-db=mysql --jdbc-driver=/path/to/mysql/mysql-connector-java.jar`
    - Confirm that .jar is in the Java share directory.\
       `ls /usr/share/java/mysql-connector-java.jar`\
    - Make sure the .jar file has the appropriate permissions - 644.
* Create a user for Ambari and grant it permissions.
using the MySQL database admin utility:

```mySQL
$ mysql -u root -p 
CREATE USER '[AMBARI_USER]'@'%' IDENTIFIED BY '[AMBARI_PASSWORD]';
GRANT ALL PRIVILEGES ON *.* TO '[AMBARI_USER]'@'%';
CREATE USER '[AMBARI_USER]'@'localhost' IDENTIFIED BY '[AMBARI_PASSWORD]';
GRANT ALL PRIVILEGES ON *.* TO '[AMBARI_USER]'@'localhost';
CREATE USER '[AMBARI_USER]'@'[AMBARI_SERVER_FQDN]' IDENTIFIED BY '[AMBARI_PASSWORD]';
GRANT ALL PRIVILEGES ON *.* TO '[AMBARI_USER]'@'[AMBARI_SERVER_FQDN]';
FLUSH PRIVILEGES;
```

Where `[AMBARI_USER]` is the Ambari user name, `[AMBARI_PASSWORD]` is the Ambari user password and `[AMBARI_SERVER_FQDN]` is the Fully Qualified Domain Name of the Ambari Server host.

* **Load the Ambari Server database schema.**

You must pre-load the Ambari database schema into your MySQL/MariaDB database using the schema script. Run the script in the same location where you find the Ambari-DDL-MySQL-CREATE.sql file. You should find the _Ambari-DDL-MySQL-CREATE.sql_ file in the _/var/lib/ambari-server/resources/_ directory of the Ambari Server host, after you have installed Ambari Server.

```mysql
mysql -u [AMBARI_USER] -p
CREATE DATABASE [AMBARI_DATABASE];
USE [AMBARI_DATABASE];
SOURCE Ambari-DDL-MySQL-CREATE.sql;
```
Where `[AMBARI_USER]` is the Ambari user name and` [AMBARI_DATABASE]` is the Ambari database name.

### After you finish

When you set up the Ambari Server, you must execute the following steps.  
1. Select **Advanced Database Configuration**.
2. Select Option [3] **MySQL/MariaDB**.
3. Enter the credentials you defined in Step 2. for user name, password and database name.
* Configuring a Database Instance for Ranger
* Install Databases for Ambari and ODP services

## Configure your MySQL database instance for Hive

Create a user for Hive and grant it permissions.
using the MySQL database admin utility:

```mysql
# mysql -u root -p
CREATE DATABASE [HIVE_DATABASE]
CREATE USER '[HIVE_USER]'@'localhost' IDENTIFIED BY '[HIVE_PASSWORD]';
GRANT ALL PRIVILEGES ON *.* TO '[HIVE_USER]'@'localhost';
CREATE USER '[HIVE_USER]'@'%' IDENTIFIED BY '[HIVE_PASSWORD]';
GRANT ALL PRIVILEGES ON *.* TO '[HIVE_USER]'@'%';
CREATE USER '[HIVE_USER]'@'[HIVE_METASTORE_FQDN]' IDENTIFIED BY '[HIVE_PASSWORD]';
GRANT ALL PRIVILEGES ON *.* TO '[HIVE_USER]'@'[HIVE_METASTORE_FQDN]';
FLUSH PRIVILEGES;
```
Where` [HIVE_USER]` is the Hive username, `[HIVE_PASSWORD]` is the Hive user password and `[HIVE_METASTORE_FQDN]` is the Fully Qualified Domain Name of the Hive Metastore host.

## Configure your MySQL database instance for Ranger

Before you begin

A MySQL/Oracle/PostgreSQL/Amazon RDS database instance must be running and available to be used by Ranger.
When using MySQL, the storage engine used for the Ranger admin policy store tables MUST support transactions. InnoDB is an example of an engine that supports transactions. A storage engine that does not support transactions is not suitable as a policy store.

**Procedure**

1. The MySQL database administrator should be used to create the Ranger databases. The following series of commands could be used to create the [RANGER_USER] user with password [RANGER_PASSWORD].
    - Log in as the root user, then use the following commands to create the  [RANGER_USER] user and grant it adequate privileges.


