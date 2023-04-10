This section explains the environment related settings for Ambari Server.\

# Set Up Password less SSH
To have Ambari Server automatically install Ambari Agents on all your cluster hosts, you must set up password-less SSH connections between the Ambari Server host and all other hosts in the cluster. The Ambari Server host uses SSH public key authentication to remotely access and install the Ambari Agent.

**Note**: You can choose to manually install an Ambari Agent on each cluster host. In this case, you do not need to generate and distribute SSH keys.

1. Generate public and private SSH keys on the Ambari Server host.\
`ssh-keygen`\
2. Copy the SSH Public Key (id_rsa.pub) to the root account on your target hosts.\
`.ssh/id_rsa` and `.ssh/id_rsa.pub`\
3. Add the public key to the target host.\
`ssh-copy-id -i /root/.ssh/id_rsa.pub root@odp{1-4}-test.adsre.com`\
4. Depending on your version of SSH, you may need to set permissions on the .ssh directory (to 700) and the authorized_keys file in that directory (to 600) on the target hosts.\
`chmod 700 ~/.ssh`\
`chmod 600 ~/.ssh/authorized_keys`
5. From the Ambari Server, make sure you can connect to each host in the cluster using SSH, without having to enter a password.\
`ssh root@odp{1-4}-test.adsre.com`

# Set Up Service User Accounts
Each service requires a service user account. The Ambari Cluster Install wizard creates new and preserves any existing service user accounts, and uses these accounts when configuring Hadoop services. Service user account creation applies to service user accounts on the local operating system and to LDAP/AD accounts.

# Enable NTP/chrony on the Cluster and on the Browser Host
Install NTP and Chrony on RHEL/CentOS and Ubuntu.

## RHEL/CentOS:
**Install NTP**: Run the command `yum install ntp` and start the NTP service using the command `systemctl start ntpd`.\
or\
**Install Chrony**: Run the command `yum install chrony` and start the Chrony service using the command `systemctl start chronyd`.\

## Ubuntu:
**Install NTP**: Run the command `sudo apt-get install ntp` and start the NTP service using the command `sudo systemctl start ntp`.
or
**Install Chrony**: Run the command sudo apt-get install chrony and start the Chrony service using the command `sudo systemctl start chrony`.

# Check DNS and NSCD

All hosts in your system must be configured for both forward and reverse DNS.\
\
If you are unable to configure DNS in this way, you should edit the `/etc/hosts` file on every host in your cluster to contain the IP address and Fully Qualified Domain Name of each of your hosts. The following instructions are provided as an overview and cover a basic network setup for generic Linux hosts. Different versions and flavors of Linux might require slightly different commands and procedures. Please refer to the documentation for the operating system(s) deployed in your environment.\
\
Hadoop relies heavily on DNS, and as such performs many DNS lookups during normal operation. To reduce the load on your DNS infrastructure, it's highly recommended to use the Name Service Caching Daemon (NSCD) on cluster nodes running Linux. This daemon will cache host, user, and group lookups and provide better resolution performance, and reduced load on DNS infrastructure.


