Before starting the Ambari Server, you must set up the Ambari Server. Setup configures Ambari to talk to the Ambari database, installs the JDK and allows you to customize the user account the Ambari Server daemon will run as. 

Move _ambari-views-package-2.7.6.0.0.jar_ file to **tmp** before executing the `ambari-server setup` cmd. You can execute the following commands to accomplish this. 
```
Login into Ambari Server node:

$ mv /var/lib/ambari-server/resources/views/ambari-views-package-2.7.6.0.0.jar /tmp
$ ambari-server setup

```