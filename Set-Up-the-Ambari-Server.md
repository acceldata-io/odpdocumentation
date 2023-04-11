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
Alternatively, you can enter 2 to download a Custom JDK. If you choose Custom JDK, you must manually install the JDK on all hosts and specify the Java Home path.