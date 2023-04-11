Before starting the Ambari Server, you must set up the Ambari Server. Setup configures Ambari to talk to the Ambari database, installs the JDK and allows you to customize the user account the Ambari Server daemon will run as. 

Move _ambari-views-package-2.7.6.0.0.jar_ file to **tmp** before executing the `ambari-server setup` cmd. You can execute the following commands to accomplish this. 
```
Login to Ambari Server node:

$ mv /var/lib/ambari-server/resources/views/ambari-views-package-2.7.6.0.0.jar /tmp
$ ambari-server setup

```

Respond to the setup prompt with the following steps. 

1. If you have not temporarily disabled SELinux, you may get a warning. Accept the default **(y)**, and continue.
2. By default, Ambari Server runs under **root**. Accept the default `(n)` at the **Customize user account for ambari-server daemon** prompt, to proceed as **root**. To create a different user to run the Ambari Server, or to assign a previously created user, select **y** at the **Customize user account for ambari-server daemon** prompt and provide a user name.