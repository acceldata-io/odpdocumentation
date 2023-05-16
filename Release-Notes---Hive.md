# Hive 3.1.4.3.2.2.0-1 Release Notes

 

Hive 3.1.4 for ODP is built on top of Apache Hive 4.0.0-Alpha-1 Release. Below mentioned is the list of patches applied on top of Apache Hive 4.0.0-Alpha-1 Release :

 

## Fixed Issues:

 
| JIRA      | Summary     |
| :---      | :---: |
| ODP-236   | Metastore Upgrade to 3.1.4 failing with Oracle 11g database   |
| ODP-121   | Update LLAP aux classes      |
| ODP-218   | Update LLAP Daemon log4j2 routing properties      |
| ODP-217   | LLAP Multinode failure with Netty mismatch version      |
| ODP-200   | HIVE-27240 NPE on Hive Hook Proto Log Writer      |
| ODP-119   | Revert HIVE-21033 patch to support Spark Hive integration      |


Relabelled 4.0.0-alpha-1 to 3.1.4.3.2.2.0-1.

Prepared for the HIVE-3.1.4.3.2.2.0-1 commit from apache hive 4.0.0-alpha-1 release

Base commit: Mapping ODP component versions & commons-lang fix 

## Known Issues:

| JIRA      | Summary     |
| :---      | :--- |
| ODP-240   | Beeline: ERROR imps.EnsembleTracker: Invalid config event received   |
| ODP-237              | Ambari UI shows "Sys DB and Information Schema not created yet" alarm on one of the Hive Metastore servers.     |
| ODP-226   | Hive v4 Hook class addition on ODP      |
| ODP-220   | Stop LLAP service fails with exceptions      |
| ODP-175   | abcs      |
| ODP-118   | Revert HIVE-21033 patch to support Spark Hive integration      |

 | JIRA       | Summary     |
 | :---       |    :---: |
 | ODP-240    | Beeline: ERROR imps.EnsembleTracker: Invalid config event received   |
 | ODP-237    | Ambari UI shows "Sys DB and Information Schema not created yet" alarm on one of the Hive Metastore servers.      |
 | ODP-226    | Hive v4 Hook class addition on ODP      |
 | ODP-220    | Stop LLAP service fails with exceptions      |
 | ODP-175    | [HIVE-18786] NPE in Hive windowing functions      |
 | ODP-118    | [HIVE-20221] Increase column width for partition_params      |


  
The detailed patch list for Apache Hive 4.0.0-Alpha-1 can be accessed [here](https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12351399&styleName=Html&projectId=12310843)