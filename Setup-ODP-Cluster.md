This document explains the process to setup the ODP cluster. 

# Launch the Ambari Cluster Install Wizard

1. From the Ambari Welcome page, choose Launch Install Wizard.




# Name Your Cluster

1. In Name your cluster, type a name for the cluster you want to create.
Do no use white spaces or special characters in the name.\
**Note**: If you plan to Kerberize the cluster, consider limiting the cluster name (to 12 characters or less), to accommodate the fact that Kerberos principals will be appended to the cluster name string and that some identity providers impose a limit on the total principal name length.
2. Choose **Next**.

# Select Version

You must select the software version and method of delivery for your cluster. Using a Private Repository requires Internet connectivity. Using a Local Repository requires you have configured the software in a repository available in your network.
## Choosing Stack
When you select a TAB, Ambari attempts to discover what specific version of that Stack is available. That list is shown in a DROPDOWN.



# Choosing Repositories
Ambari gives you a choice to install the software from the Private Repositories (if you have Internet access) or Local Repositories. Regardless of your choice, you can edit the Base URL of the repositories. The available operating systems are displayed and you can add/remove operating systems from the list to fit your environment.