This document explains the process to setup the ODP cluster. 

# Launch the Ambari Cluster Install Wizard

1. From the Ambari Welcome page, choose Launch Install Wizard.

![](https://github.com/acceldata-io/odpdocumentation/blob/main/assets/1.png)


# Name Your Cluster

1. In Name your cluster, type a name for the cluster you want to create.
Do no use white spaces or special characters in the name.\
**Note**: If you plan to Kerberize the cluster, consider limiting the cluster name (to 12 characters or less), to accommodate the fact that Kerberos principals will be appended to the cluster name string and that some identity providers impose a limit on the total principal name length.
2. Choose **Next**.

# Select Version

You must select the software version and method of delivery for your cluster. Using a Private Repository requires Internet connectivity. Using a Local Repository requires you have configured the software in a repository available in your network.
## Choosing Stack
When you select a TAB, Ambari attempts to discover what specific version of that Stack is available. That list is shown in a DROPDOWN.

![](https://github.com/acceldata-io/odpdocumentation/blob/main/assets/2.png)



# Choosing Repositories
Ambari gives you a choice to install the software from the Private Repositories (if you have Internet access) or Local Repositories. Regardless of your choice, you can edit the Base URL of the repositories. The available operating systems are displayed and you can add/remove operating systems from the list to fit your environment.

![](https://github.com/acceldata-io/odpdocumentation/blob/main/assets/3.png)

# Installation Options
To build up the cluster, the Cluster Install wizard prompts you for general information about how you want to set it up. You must supply the FQDN of each of your hosts.The wizard also needs to access the private key file you created when you set up password-less SSH.

## Steps

1. In Target Hosts, enter your list of host names, one per line.
You can use ranges inside brackets to indicate larger sets of hosts. For example, for host01.domain through host10.domain use host[01-10].domain
2. Enter the user name for the SSH key you have selected. If you do not want to use root, you must provide the user name for an account that can execute sudo without entering a password. If SSH on the hosts in your environment is configured for a port other than 22, you can change that also.
3. If you do not want Ambari to automatically install the Ambari Agents, select Perform manual registration.
4. Choose Register and Confirm to continue.
