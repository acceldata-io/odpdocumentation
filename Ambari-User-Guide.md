#1. Getting Ready
This section describes the information and materials you should get ready to install a cluster using Ambari. Ambari provides an end-to-end management and monitoring solution for your cluster. Using the Ambari Web UI and REST APIs, you can deploy, operate, manage configuration changes, and monitor services for all nodes in your cluster from a central point.

##1.1 Product Interoperability
Ambari 2.7.6.0 currently supports only ODP 3.2.2.0. 

Below table provide component version and list for the corresponding Ambari release.

| Component Name | Apache Version | Distribution Version |
| --- | --- | --- |
| Ambari | 2.7.6.0 | 2.7.6.0-0 |
| Ambari-Infra-Solr | 2.7.6.0 | 2.7.6.0-0 |
| Ambari-Metrics | 2.7.6.0 | 2.7.6.0-0 |

Below table provide component version and list for the corresponding ODP release.

| Component Name | Apache Version | ODP Version |
| --- | --- | --- |
| Bigtop-Utils | 1.0.0 | 1.0.0.3.2.2.0-1 |
| Odp-Select | NA | 3.2.2.0-1 |
| Hadoop | 3.2.3 | 3.2.3.3.2.2.0-1 |
| HBase | 2.4.11 | 2.4.11.3.2.20-1 |
| Phoenix | 5.0.0 | 5.0.0.3.2.20-1 |
| Hive | 4.0.0-alpha-1 | 3.1.4.3.2.2.0-1 |
| Kafka | 2.8.1 | 2.8.1.3.2.2.0-1 |
| Livy | 0.7.1 | 0.7.1.3.2.2.0-1 |
| Ranger | 2.3.0 | 2.3.0.3.2.2.0-1 |
| Spark 2 | 2.4.8 | 2.4.8.3.2.2.0-1 |
| Tez | 0.10.1 | 0.10.1.3.2.2.0-1 |
| Sqoop | 1.4.7 | 1.4.7.3.2.2.0-1 |
| Zookeeper | 3.5.10 | 3.5.10.3.2.2.0-1 |
| Zeppelin | 0.10.1 | 0.10.1.3.2.2.0-1 |

Here are the list of available Ambari-Mpacks and their details supported by this version of Ambari.

| Component Name | Apache Version | ODP Version |
| --- | --- | --- |
| Hue | 4.10.0 | 4.10.0.3.2.2.0-1 |
| Impala | 4.1.0 | 4.1.0.3.2.2.0-1 |
| Spark 3 | 3.2.2 | 3.2.2.3.2.2.0-1 |
| NiFi | 1.19.1 | 1.19.1.3.2.2.0-1 |


###1.2 Meet Minimum System Requirements
Your system must meet the following minimum requirements:

####1.2.1. Software Requirements
On each host of the cluster:
- yum and rpm (RHEL/CentOS/Rocky Linux)
- apt (Ubuntu)
- scp, curl, unzip, tar, wget, and gcc*
- OpenSSL (v1.01, build 16 or later)
- Python 2.7.12 (with python-devel)

####1.2.2. Memory Requirements
The Ambari host should have at least 1 GB RAM, with 500 MB free.
To check available memory on any host, run:

  `free -m`

**Note** : Use these values as guidelines. Be sure to test them for your specific environment.

####1.2.3. Package Size and Inode Count Requirements

| Component | Size | INodes|
| --- | --- | --- |
| Ambari Server | 100MB	| 5,000|
| Ambari Agent | 8MB| 1,000 |
| After Ambari Server Setup| NA | 4,000 |

| Component | Size | INodes|
| --- | --- | --- |
| After Ambari Server Start | NA	| 500|
| After Ambari Agent Start | NA| 200 |

**Size and Inode values are approximate values, please tune based on cluster sizes.** 

####1.2.4. Maximum Open Files Requirements
The recommended maximum number of open file descriptors is **10000**, or more. 
To check the current value set for the maximum number of open file descriptors, execute the following shell commands on each host:

```
ulimit -Sn
ulimit -Hn
```

If the output is not greater than **10000**, run the following command to set it to a suitable default:

  `ulimit -n 10000`

###1.3. Collect Information
Before deploying a cluster, you should collect the following information:

- The fully qualified domain name (FQDN) of each host in your system. The Ambari Cluster Install wizard supports using IP addresses. You can use the following command for the same.

  `hostname -f`

- A list of components you want to set up on each host.
- The base directories you want to use as mount points for storing:
- NameNode data {Standby Namenode data mount should be same as Namenode Data mount.}
- DataNodes data
- Secondary NameNode data
- Oozie data
- YARN data
- ZooKeeper data, if you install ZooKeeper
- Various log, pid, and db files, depending on your install type

**Important**

You must use base directories that provide persistent storage locations for your components and your Hadoop data. Installing components in locations that may be removed from a host may result in cluster failure or data loss. 
For example: Do _**Not**_ use _**/tmp**_ in a base directory path. 

###1.4. Prepare the Environment
To deploy your Hortonworks stack using Ambari, you need to prepare your deployment environment:

####1.4.1. Set Up Password-less SSH
**About This Task :**
To have Ambari Server automatically install Ambari Agents on all your cluster hosts, you must set up password-less SSH connections between the Ambari Server host and all other hosts in the cluster. The Ambari Server host uses SSH public key authentication to remotely access and install the Ambari Agent.
**Note : **
You can choose to manually install an Ambari Agent on each cluster host and register them with the target ambari server. In this case, you do not need to generate and distribute SSH keys.

**Steps :**
1. Generate public and private SSH keys on the Ambari Server host.

   `ssh-keygen`
2. Copy the SSH Public Key (`id_rsa.pub`) to the root account on your target hosts. 
   
```
   .ssh/id_rsa
   .ssh/id_rsa.pub
```
3. Add the SSH Public Key to the authorized_keys file on your target hosts.

   `cat id_rsa.pub >> authorized_keys`
4. Depending on your version of SSH, you may need to set permissions on the .ssh directory (to 700) and the authorized_keys file in that directory (to 600) on the target hosts.
```
   chmod 700 ~/.ssh
   chmod 600 ~/.ssh/authorized_keys
```
5. From the Ambari Server, make sure you can connect to each host in the cluster using SSH, without having to enter a password.

   `ssh root@<remote.target.host>` where `<remote.target.host>` has the value of each host name on the desired cluster.
6. If the following warning message displays during your first connection: `Are you sure you want to continue connecting (yes/no)? Enter Yes`.
7. Retain a copy of the SSH Private Key on the machine from which you will run the web based Ambari Install Wizard.

   **Note :**
   It is possible to use a non-root SSH account, if that account can execute sudo without entering a password.

####1.4.2. Set Up Service User Accounts
Each service requires a service user account. The Ambari Cluster Install wizard creates new and preserves any existing service user accounts, and uses these accounts when configuring Hadoop services. Service user account creation applies to service user accounts on the local operating system and to LDAP/AD accounts.

####1.4.3. Enable NTP on the Cluster and on the Browser Host
The clocks of all the nodes in your cluster and the machine that runs the browser through which you access the Ambari Web interface must be able to synchronize with each other.

To install the NTP service and ensure it's ensure it's started on boot, run the following commands on each host:

- RHEL/CentOS/RockyLinux 
```
 yum install -y ntp
 systemctl enable ntpd
```
- Ubuntu
```
 apt-get install ntp
 update-rc.d ntp defaults
```
####1.4.4. Check DNS and NSCD

All hosts in your system must be configured for both forward and and reverse DNS. 
If you are unable to configure DNS in this way, you should edit the `/etc/hosts` file on every host in your cluster to contain the IP address and Fully Qualified Domain Name of each of your hosts.

The following instructions are provided as an overview and cover a basic network setup for generic Linux hosts.
Different versions and flavors of Linux might require slightly different commands and procedures. 
Please refer to the documentation for the operating system(s) deployed in your environment.
Hadoop relies heavily on DNS, and as such performs many DNS lookups during normal operation.
To reduce the load on your DNS infrastructure, it's highly recommended to use the Name Service Caching Daemon (NSCD) on cluster nodes running Linux.
This daemon will cache host, user, and group lookups and provide better resolution performance, and reduced load on DNS infrastructure.
#####1.4.4.1. Edit the Host File

1. Using a text editor, open the hosts file on every host in your cluster. For example: `vi /etc/hosts`
2. Add a line for each host in your cluster. The line should consist of the IP address and the FQDN. For example:
   `1.2.3.4 <fully.qualified.domain.name>`

   **Important**
   Do not remove the following two lines from your hosts file. Removing or
   editing the following lines may cause various programs that require network functionality to fail.
```
127.0.0.1 localhost.localdomain localhost
::1 localhost6.localdomain6 localhost6
```
#####1.4.4.2. Set the Hostname
1. Confirm that the hostname is set by running the following command:

   `hostname -f`

   This should return the <fully.qualified.domain.name> you just set.
2. Use the `hostname` command to set the hostname on each host in your cluster. For example:

   `hostname <fully.qualified.domain.name>`

#####1.4.4.3. Edit the Network Configuration File
1. Using a text editor, open the network configuration file on every host and set the desired network configuration for each host. For example:

   `vi /etc/sysconfig/network`

2. Modify the HOSTNAME property to set the fully qualified domain name.
```
 NETWORKING=yes
 HOSTNAME=<fully.qualified.domain.name>
```
####1.4.5. Configuring iptables
For Ambari to communicate during setup with the hosts it deploys to and manages, certain ports must be open and available. 
 The easiest way to do this is to temporarily disable iptables, as follows: 


- RHEL/CentOS/Rocky Linux
```
 service firewalld stop
 systemctl disable firewalld
```
- Ubuntu 
```
 sudo iptables -X
 sudo iptables -t nat -F
 sudo iptables -t nat -X
 sudo iptables -t mangle -F
 sudo iptables -t mangle -X
 sudo iptables -P INPUT ACCEPT
 sudo iptables -P FORWARD ACCEPT
 sudo iptables -P OUTPUT ACCEPT
```
You can restart iptables after setup is complete. 
If the security protocols in your environment prevent disabling iptables, you can proceed with iptables enabled, if all required ports are open and available.

Ambari checks whether iptables is running during the Ambari Server setup process. 
If iptables is running, a warning displays, reminding you to check that required ports are open and available. 
The Host Confirm step in the Cluster Install Wizard also issues a warning for each host that has iptables running.

####1.4.6. Disable SELinux and PackageKit and check the umask Value
1. We must disable SELinux for the Ambari setup to function. On each host of the cluster, enter:

   `setenforce 0`

   **Note :**
   To permanently disable SELinux set `SELINUX=disabled` in `/etc/selinux/`
   config This ensures that SELinux does not turn itself on after you reboot
   the machine .

2. On an installation host running RHEL/CentOS/RockyLinux with PackageKit installed, open `/etc/yum/pluginconf.d/refresh-packagekit.conf` using a text editor. Make the following change:
   
   `enabled=0`

   **Note :**
   PackageKit is not enabled by default on Ubuntu systems.
   Unless PackageKit is specifically enabled, skip this step for Ubuntu hosts.

3. **UMASK** (User Mask or User file creation MASK) sets the default permissions or base permissions granted when a new file or folder is created on a Linux machine. Most Linux distros set 022 as the default umask value. A umask value of 022 grants read, write, execute permissions of 755 for new files or folders. A umask value of 027 grants read, write, execute permissions of 750 for new files or folders.
   Ambari, and ODP support umask values of **022** (**0022** is functionally equivalent), **027** (0027 is functionally equivalent). These values must be set on all hosts.
   UMASK Examples:

   Setting the umask for current login session:

   `umask 0022`

   Checking current umask:
   `umask`

   Permanently changing the umask for all interactive users:

   `echo umask 0022 >> /etc/profile`

####1.4.7. Download and set up database connectors
   Components like  Hive, Ranger and Oozie require an operational backend database.
   During installation, there is an option to use an existing database or have Ambari install a new instance, in the case of Hive.
   For Ambari to connect to the database of choice, the necessary database drivers and connectors must be downloaded directly from the database vendor before installing the component.
   To better prepare for install or upgrade, set up the database connectors as while setting up the environment.

   Supported Databases and versions

   | Component | Supported Version |
   | --- | --- |
   | MySql / MariaDB | 5.7.x |
   | Postgres | 9.x |
   | Oracle | 11.x to 19.x |
   
#####1.4.7.1. Configuring a Database Instance for Ranger
   A MySQL, Oracle, PostgreSQL, or Amazon RDS database instance must be running and available to be used by Ranger.
   The Ranger installation will create two new users (default names: `rangeradmin` and `rangerlogger`) and two new databases (default names: `ranger` and `ranger_audit`).

######1.4.7.1.1. Configuring MySQL for Ranger
   **Prerequisites**

   When using MySQL, the storage engine used for the Ranger admin policy store tables MUST support transactions.
   **InnoDB** is an example of engine that supports transactions. A storage engine that does not support transactions is not suitable as a policy store.

   **Steps**
   - The MySQL database administrator should be used to create the Ranger databases.
   The following series of commands could be used to create the `rangerdba` user with password `rangerdba`. 
   - Log in as the `root` user, then use the following commands to create the `rangerdba` user and grant it adequate privileges.

   ```
   CREATE USER 'rangerdba'@'localhost' IDENTIFIED BY 'rangerdba';
   GRANT ALL PRIVILEGES ON *.* TO 'rangerdba'@'localhost';
   CREATE USER 'rangerdba'@'%' IDENTIFIED BY 'rangerdba';
   GRANT ALL PRIVILEGES ON *.* TO 'rangerdba'@'%';
   GRANT ALL PRIVILEGES ON *.* TO 'rangerdba'@'localhost' WITH GRANT OPTION; 
   GRANT ALL PRIVILEGES ON *.* TO 'rangerdba'@'%' WITH GRANT OPTION; FLUSH PRIVILEGES;
   ```
   - Use the exit command to exit MySQL. 
   - Validate connectivity to the database as rangerdba using the following command.

      `mysql -u rangerdba -p rangerdba`

     After testing the rangerdba login, use the exit command to exit MySQL.
   - Use the following command to confirm that the mysql-connector-java.jar file is in the Java share directory. This command must be run on the server where Ambari server is installed.

     `ls /usr/share/java/mysql-connector-java.jar`

      If the file is not in the Java share directory, use the following command to install the MySQL connector .jar file.
      RHEL/CentOS/Rocky Linux : `yum install mysql-connector-java`

   - Use the following command format to set the jdbc/driver/path based on the location of the MySQL JDBC driver .jar file.This command must be run on the server where Ambari server is installed.

      `ambari-server setup --jdbc-db={database-type} --jdbc-driver={/jdbc/driver/path}`

      For example:

      `ambari-server setup --jdbc-db=mysql --jdbc-driver=/usr/share/java/mysql connector-java.jar`

######1.4.7.1.2. Configuring PostgreSQL for Ranger
   - On the PostgreSQL host, install the applicable PostgreSQL connector.

      RHEL/CentOS/Rocky Linux : `yum install postgresql-jdbc*`

   - Confirm that the .jar file is in the Java share directory.

      `ls /usr/share/java/postgresql-jdbc.jar`

   - Change the access mode of the .jar file to 644.

      `chmod 644 /usr/share/java/postgresql-jdbc.jar`

   - The PostgreSQL database administrator should be used to create the Ranger databases. The following series of commands could be used to create the `rangerdba` user and grant it adequate privileges.

     ```
     echo "CREATE DATABASE $dbname;" | \ 
     sudo -u $postgres psql -U postgres echo "CREATE USER $rangerdba WITH PASSWORD '$passwd';" | \
     sudo -u $postgres  psql -U postgres \
     echo "GRANT ALL PRIVILEGES ON DATABASE $dbname TO $rangerdba;" | \
     sudo -u  $postgres psql -U postgres
     ```
     Where:
     - `$postgres` is the Postgres user.
     - `$dbname `is the name of your PostgreSQL database
   - Use the following command format to set the jdbc/driver/path based on the location of the PostgreSQL JDBC driver .jar file. This command must be run on the server where Ambari server is installed.

     `ambari-server setup --jdbc-db={database-type} --jdbc-driver={/jdbc/driver/path}`

      For example:

      `ambari-server setup --jdbc-db=postgres --jdbc-driver=/usr/share/java/ postgresql-jdbc.jar`
   - Run the following command:

           `export HADOOP_CLASSPATH=${HADOOP_CLASSPATH}:${JAVA_JDBC_LIBS}:/<connector_jar_path>`
   - Add Allow Access details for Ranger users:
     - change `listen_addresses='localhost'` to `listen_addresses='*'` (`'*' = any`) to listen from all IPs in `postgresql.conf`.
     - Add the following for the Ranger db user and Ranger audit db user in the `pg_hba.conf` file.
     
     `host  all  postgres,rangeradmin,rangerlogger  ::/0  trust`
   - After editing the `pg_hba.conf` file, run the following command to refresh the PostgreSQL database configuration:

     `sudo -u postgres /usr/bin/pg_ctl -D $PGDATA reload`

     For example, if the `pg_hba.conf` file is located in the `/var/lib/pgsql/data directory`, the value of `$PGDATA` is `/var/lib/pgsql/data`. 

######1.4.7.1.3. Configuring Oracle for Ranger

- On the Oracle host, install the appropriate JDBC .jar file.
  - Download the Oracle JDBC (OJDBC) driver from [http://www.oracle.com/technetwork/database/features/jdbc/index-091264.html](http://www.oracle.com/technetwork/database/features/jdbc/index-091264.html).
  - For Oracle Database 11g: select Oracle Database 11g Release 2 drivers > `ojdbc6.jar`. 
  - For Oracle Database 12c: select Oracle Database 12c Release 1 driver > `ojdbc7.jar`. 
  - For Oracle Database 19c: select Oracle Database 19c JDBC Driver & UCP Downloads - Long Term Release > Oracle JDBC Driver > `ojdbc8.jar`. 
  - Copy the .jar file to the Java share directory. For example:
  
   `cp <odbc_jar> > /usr/share/java/`

   **Note**
   1. Make sure the .jar file has the appropriate permissions. For example: `chmod 644 /usr/share/java/ojdbc7.jar`
   2. Make sure the .jar downloaded is compatible for `JDK8`.
   
- The Oracle database administrator should be used to create the Ranger databases. The following series of commands could be used to create the `RANGERDBA` user and grant it permissions using `SQLPlus`, the Oracle database administration utility:
   - sqlplus `sys/root` as `sysdba`
   ```
    CREATE USER $RANGERDBA IDENTIFIED BY $RANGERDBAPASSWORD;
    GRANT SELECT_CATALOG_ROLE TO $RANGERDBA;
    GRANT CONNECT, RESOURCE TO $RANGERDBA;
    QUIT;
  ```
- Use the following command format to set the `jdbc/driver/path` based on the location of the Oracle JDBC driver .jar file. This command must be run on the server where Ambari server is installed.

   `ambari-server setup --jdbc-db={database-type} --jdbc-driver={/jdbc/driver/path}`

   For example:

   `ambari-server setup --jdbc-db=oracle --jdbc-driver=/usr/share/java/ojdbc6. jar`

#2. Using a Local Repository
If your enterprise clusters have limited outbound Internet access, you should consider using a local repository, which enables you to benefit from more governance and better installation performance. You can also use a local repository for routine post installation cluster operations such as service start and restart operations. Using a local repository includes obtaining public repositories, setting up the repository using either no internet access or limited internet access, and preparing the Apache Ambari repository configuration file to use your new local repository. 
##2.1. Setting Up a Local Repository
   Based on your Internet access, choose one of the following options:
   - No Internet Access :
   This option involves downloading the repository tarball, moving the tarball to the selected mirror server in your cluster, and extracting the tarball to create the repository.
   - Temporary Internet Access : 
   This option involves using your temporary Internet access to synchronize (using reposync) the software packages to your selected mirror server to create the repository.
   
Both options proceed in a similar, straightforward way. Setting up for each option presents some key differences, as described in the following sections.

###2.1.1. Preparing to Set Up a Local Repository
Before setting up your local repository, you must have met certain requirements.
- Selected an existing server, in or accessible to the cluster, that runs a supported operating system.
- Enabled network access from all hosts in your cluster to the mirror server.
- Ensured that the mirror server has a package manager installed such as yum (for RHEL, CentOS or Rocky Linux) or apt-get (for Ubuntu).

**Optional**: If your repository has temporary Internet access, and you are using RHEL, CentOS or Rocky Linux as your OS, installed yum utilities:

`yum install yum-utils createrepo`

After meeting these requirements, you can take steps to prepare to set up your local repository.

**Steps**
- Create an HTTP server:
   - On the mirror server, install an HTTP server (such as Apache httpd) using the instructions provided on the Apache community website.
   - Activate the server.
   - Ensure that any firewall settings allow inbound HTTP access from your cluster nodes to your mirror server.
  
   **Note**
   Make sure that SELinux is disabled.

- On your mirror server, create a directory for your web server.
   - For example, from a shell window, type:
  
     For RHEL/CentOS/Rocky Linux: `mkdir -p /var/www/html/`
  
     For Debian/Ubuntu: `mkdir -p /var/www/html/`
  
- If you are using a symlink, enable the follow symlinks on your web server. 
- You next must set up your local repository, either with no Internet access or with temporary Internet access.

###2.1.2. Setting up a Local Repository with Temporary Internet Access
**Prerequisites**

You must have completed the Getting Started Setting up a Local Repository procedure.
To finish setting up your local repository, complete the following:

**Steps**
- Install the repository configuration files for Ambari and the Stack on the host. 
- Confirm repository availability

For RHEL, CentOS or Rocky Linux: `yum repolist`

For Ubuntu: `dpkg-list` 

- Synchronize the repository contents to your mirror server: 
  - Browse to the web server directory:

For RHEL, CentOS  or Rocky Linux: `cd /var/www/html`


For Ubuntu: `cd /var/www/html`

- For Ambari, create the ambari directory and reposync:
```
mkdir -p ambari/<OS>
cd ambari/<OS>
reposync -r ambari-2.7.6.0
```
In this syntax, the value of `<OS>` is centos7, ubuntu18, or ubuntu20.

- For Open source Data Platform (ODP) stack repositories, create the odp directory and reposync:
```
mkdir -p hdp/<OS>
cd hdp/<OS>
reposync -r ODP-<latest.version>
reposync -r ODP-UTILS-<version>
```

- Generate the repository metadata:

   - For Ambari:

   `createrepo <web.server.directory>/ambari/<OS>/ambari-2.7.6.0`

   - For ODP Stack Repositories:
   ```
   createrepo <web.server.directory>/odp/<OS>/ODP-<latest.version>
   createrepo <web.server.directory>/odp/<OS>/ODP-UTILS-<version>
   ```
- Confirm that you can browse to the newly created repository:
```
Ambari Base URL - http://<web.server>/ambari/<OS>/ambari-2.7.6.0 
ODP Base URL - http://<web.server>/odp/<OS>/ODP-<latest.version> 
ODP-UTILS Base URL - http://<web.server>/odp/<OS>/ODP-UTILS-<version>

Where:
   <web.server> – The FQDN of the web server host
   <version> – The ODP stack version number
   <OS> – centos7, ubuntu 18 or ubuntu20.
```
   **Important**

   Be sure to record these Base URLs. You will need them when installing Ambari and the Cluster.

**Optional**: If you have multiple repositories configured in your environment, deploy the following plug-in on all the nodes in your cluster.
   - Install the plug-in.

   For RHEL/CentOS : `yum install yum-plugin-priorities`
   - Edit the `/etc/yum/pluginconf.d/priorities.conf` file to add the following:
     ```
     [main]
     enabled=1
     gpgcheck=0
     ```

###2.1.3. Setting Up a Local Repository with No Internet Access Prerequisites
You must have completed the Getting Started Setting up a Local Repository procedure. 
To finish setting up your local repository, complete the following:

**Steps**:
- Obtain the compressed tape archive file (tarball) for the repository you want to create.
- Copy the repository tarball to the web server directory and uncompress (untar) the archive:
   - Browse to the web server directory you created.

     For RHEL/CentOS/Rocky Linux: `cd /var/www/html/`

     For Ubuntu: `cd /var/www/html/`

- Untar the repository tarballs and move the files to the following locations, where `<web.server>`, `<web.server.directory>`, `<OS>`, `<version>`, and `<latest.version>` represent the `name`, `home directory`, `operating system type`, `version`, and `most recent release version`, respectively:
```
Ambari Repository Untar under <web.server.directory>.
ODP Stack Repositories Create a directory and untar it under <web.server.directory>/odp.
```
- Confirm that you can browse to the newly created local repositories, where `<web.server>`, `<web.server.directory>`, `<OS>`, `<version>`, and `<latest.version>` represent the `name`, `home directory`, `operating system type`, `version`, and `most recent release version`, respectively:
```
   Ambari Base URL http://<web.server>/Ambari-2.7.6.0/<OS>
   ODP Base URL http://<web.server>/odp/ODP/<OS>/3.2.3.3.2.2.0-1/ <latest.version>
   ODP-UTILS Base URL http://<web.server>/odp/ODP-UTILS-<version>/repos/<OS> 
```   
   **Important**: 
   Be sure to record these Base URLs. You will need them when installing Ambari and the cluster.
- _Optional_: If you have multiple repositories configured in your environment, deploy the following plug-in on all the nodes in your cluster.
   - For RHEL/CentOS 7: `yum install yum-plugin-priorities`
   - Edit the `/etc/yum/pluginconf.d/priorities.conf` file to add the following values:
  ```
   [main]
   enabled=1
   gpgcheck=0
  ```

##2.2. Preparing the Ambari Repository
Configuration File to Use the Local Repository 

**Steps**
- Download the ambari.repo file from the public repository:
   <<<Insert Link to the ambari.repo file hosted on AWS S3 >>>

- Edit the ambari.repo file and replace the Ambari Base URL baseurl obtained when setting up your local repository.
```
   [ambari-2.7.6.0]
   name=ambari-2.7.6.0
   baseurl=<<<INSERT-BASE-URL>>>
   gpgcheck=1
   gpgkey=<<<Insert_GPG_Key_URL>>>
   enabled=1
   priority=1
```
   **Note**:
   You can disable the GPG check by setting `gpgcheck=0`. 
   Alternatively, you can keep the check enabled but replace gpgkey with the URL to GPG-KEY in your local repository. 
   Place the ambari.repo file on the host you plan to use for the Ambari server:

   For RHEL/CentOS/Oracle/ Amazon Linux:`/etc/yum.repos.d/ambari.repo`

   For Ubuntu: `/etc/apt/sources.list.d/ambari.list`
   Edit the `/etc/yum/pluginconf.d/priorities.conf` file to add the following values:
   ```
      [main]
      enabled=1
      gpgcheck=0
   ```
#3. Accessing Acceldata ODP Repositories

These sections describe how to obtain:
   - Ambari Repositories 
   - ODP Stack Repositories

**Note**

   Accessing Ambari repositories requiries authentication. For more information, see Section 4.1, “Accessing Ambari Repositories”

##3.1. Ambari Repositories
   Use the link appropriate for your OS family to download a tar file that contains the software for setting up Ambari.

| OS | Component | Version | URL |
   | --- | --- | --- | --- |
| RHEL/CentOs 7 | Ambari | 2.7.6.0-0 |  |
| RHEL/RockyLinux 8 | Ambari | 2.7.6.0-0 |  |
| Ubuntu 18/20 | Ambari | 2.7.6.0-0 |  |

##3.2. ODP Stack Repositories
Use the link appropriate for your OS family to download a tar file that contains the software for setting up the Stack.

###3.2.1. Accessing ODP Repositories

| OS | Component | Version | URL |
   | --- | --- | --- | --- |
| RHEL/CentOs 7 | ODP | 3.2.2.0-1 |  |
| RHEL/RockyLinux 8 | ODP | 3.2.2.0-1 |  |
| Ubuntu 18/20 | ODP | 3.2.2.0-1|  |

##3.3. ODP Ambari-MPack Repositories
Use the link appropriate for your OS family to download a tar file that contains the software for setting up the desired Mpacks.

###3.3.1. Accessing Impala Ambari-Mpack 

| Component | Version | URL |
   | --- | --- | --- |
| Ambari-Impala-Mpack | 4.1.2.3.2.2.0-1 |  |

###3.3.2. Accessing Hue Ambari-Mpack

| Component | Version | URL |
   | --- | --- | --- |
| Ambari-Hue-Mpack | 4.10.0.3.2.2.0-1 |  |

###3.3.3. Accessing Spark3 Ambari-Mpack

| Component | Version | URL |
   | --- | --- | --- |
| Ambari-Spark3-Mpack | 3.2.2.3.2.2.0-1 |  |

###3.3.4. Accessing NiFi Ambari-Mpack

| Component | Version | URL |
   | --- | --- | --- |
| Ambari-NiFi-Mpack | 1.19.1.3.2.2.0-1 |  |

#4. Installing Ambari 

To install Ambari server on a single host in your cluster, complete the following.

##4.1. Accessing Ambari Repositories 
Ensure that Ambari repositories are accessible on the ambari-server and ambari-agent nodes of the cluster.

