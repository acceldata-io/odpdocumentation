Before starting the Ambari Server, you must set up the Ambari Server. Setup configures Ambari to talk to the Ambari database, installs the JDK and allows you to customize the user account the Ambari Server daemon will run as. 

Move _ambari-views-package-2.7.6.0.0.jar_ file to **tmp** before executing the `ambari-server setup` cmd. You can execute the following commands to accomplish this. 
```
Login to Ambari Server node:

$ mv /var/lib/ambari-server/resources/views/ambari-views-package-2.7.6.0.0.jar /tmp
$ ambari-server setup

```

Respond to the setup prompt with the following steps. 

1. If you have not temporarily disabled SELinux, you may get a warning. Accept the default **(y)**, and continue.
2. By default, Ambari Server runs under **root**. Accept the default **(n)** at the **Customize user account for ambari-server daemon** prompt, to proceed as **root**. To create a different user to run the Ambari Server, or to assign a previously created user, select **y** at the **Customize user account for ambari-server daemon** prompt and provide a user name.
3. If you have not temporarily disabled **iptables** you may get a warning. Enter **y** to continue.
4. Select a JDK version to download. Enter **1** to download Oracle JDK 1.8.\
By default, Ambari Server setup downloads and installs Oracle JDK 1.8 and the accompanying Java Cryptography Extension (JCE) Policy Files.
5. To proceed with the default installation, accept the Oracle JDK license when prompted. You must accept this license to download the necessary JDK from Oracle. The JDK is installed during the deploy phase.\
Alternatively, you can enter **2** to download a Custom JDK. If you choose Custom JDK, you must manually install the JDK on all hosts and specify the Java Home path.

**Note**: To install OpenJDK, use the Custom option. Be prepared to provide the valid JAVA_HOME value to Ambari. Acceldata strongly recommends that you install the JDK packages consistently on all the hosts.

6. Review the GPL license agreement when prompted. To explicitly enable Ambari to download and install LZO data compression libraries, you must answer **y**. If you enter **n**, Ambari does not automatically install LZO on any new host in the cluster. In this case, you must ensure LZO is installed and configured appropriately. Without LZO being installed and configured, data compressed with LZO is not readable. If you do not want Ambari to automatically download and install LZO, you must confirm your choice to proceed.

7. Select **n** at **Enter advanced database configuration** to use the default, embedded PostgreSQL database for Ambari. The default PostgreSQL database name is **ambari**. The default user name and password are **ambari/bigdata**. To use an existing PostgreSQL, MySQL/MariaDB or Oracle database with Ambari, select **y**.

    a If you are using an existing PostgreSQL, MySQL/MariaDB, or Oracle database instance, use one of the following prompts.
    b You must prepare an existing database instance, before running setup and entering advanced database configuration.
