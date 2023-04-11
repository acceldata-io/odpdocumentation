RHEL/CentOS/Oracle Linux 7

1. Login to the host where you want to install the Ambari Server.
1. Download the Ambari repository file to a directory on your installation host.
1. Confirm that the repository is configured by checking the repo list. You can execute the following command to check the repo list.\
`$ yum repolist`

**Note**: ​​By default, Ambari Server uses an embedded PostgreSQL database. When you install the Ambari Server, the PostgreSQL packages and dependencies must be available for installation. These packages are typically available as part of your Operating System repositories. You must ensure that you have the appropriate repositories available for the **postgresql-server** packages by executing the following commands. 

`$ yum install ambari-server`