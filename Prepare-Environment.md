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
Install NTP and Chrony on RHEL/CentOS and Ubuntu

RHEL/CentOS:
Install NTP: Run the command yum install ntp and start the NTP service using "systemctl start ntpd".
or
Install Chrony: Run the command yum install chrony and start the Chrony service using "systemctl start chronyd".\

Ubuntu:
Install NTP: Run the command sudo apt-get install ntp and start the NTP service using "sudo systemctl start ntp".
or
Install Chrony: Run the command sudo apt-get install chrony and start the Chrony service using "sudo systemctl start chrony".

