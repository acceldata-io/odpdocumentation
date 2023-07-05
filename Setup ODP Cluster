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
You can use ranges inside brackets to indicate larger sets of hosts. For example, for host01.domain through host10.domain use **host[01-10].domain**
2. Enter the user name for the SSH key you have selected. If you do not want to use **root**, you must provide the user name for an account that can execute **sudo** without entering a password. If SSH on the hosts in your environment is configured for a port other than 22, you can change it.
3. If you do not want Ambari to automatically install the Ambari Agents, select **Perform manual registration**.
4. Choose **Register** and Confirm to continue.

# Confirm Hosts

Confirm Hosts prompts you to confirm that Ambari has located the correct hosts for your cluster and to check those hosts to make sure they have the correct directories, packages, and processes required to continue the install.

At the bottom of the screen, you may notice a yellow box that indicates some warnings were encountered during the check process. Choose Click here to see the warnings to see a list of what was checked and what caused the warning.

Also please make sure that all the WARNINGS are taken care of else this may cause the problem in future.

# Choose Services

Based on the Stack chosen during the Select Stack step, you are presented with the choice of Services to install into the cluster. A Stack comprises many services. You may choose to install any other available services now, or to add services later. The Cluster Install wizard selects all available services for installation by default.

Choose or clear individual check boxes to define a set of services to install now.
After selecting the services to install now, choose **Next**.

![](https://github.com/acceldata-io/odpdocumentation/blob/main/assets/4.png)

# Assign Masters

The Cluster Install wizard assigns the master components for selected services to appropriate hosts in your cluster and displays the assignments in Assign Masters. The left column shows services and current hosts. The right column shows current master component assignments by host, indicating the number of CPU cores and amount of RAM installed on each host. To change the host assignment for a service, select a host name from the drop-down menu for that service.

![](https://github.com/acceldata-io/odpdocumentation/blob/main/assets/5.png)

# Assign Slaves and Clients

The Cluster Install wizard assigns the slave components, such as DataNodes, NodeManagers, and RegionServers, to appropriate hosts in your cluster. It also attempts to select hosts for installing the appropriate set of clients.

You must fine-tune your selections by using the check boxes next to specific hosts.


![](https://github.com/acceldata-io/odpdocumentation/blob/main/assets/6.png)


