Acceldata supports the Open-Source Data Platform. To use the Acceldata supported Open-Source Data Platform (ODP), you must install it. This documentation explains ODP and the installation process of (ODP). 

# Features of ODP

* ODP is an Open Source Data Platform.
* It provides an alternative to proprietary platform and a monopoly.
* ODP is available to Pulse customers who do not want to get locked with a single vendor.
* ODP is 100% Open source - Built and Tested by Acceldata using the latest upstream code.
* ODP uses the same stack Deployed at T-Mobile, AT&T , True Corp, AIS group PhonePe, HCSC, and Freddie Mac.


# ODP Architecture

The following image displays the architecture of ODP. 

![](https://github.com/acceldata-io/odpdocumentation/blob/main/myarch.png)

# Open Source Data Platform Specifications

## Component Versions

This section provides a list of the official Apache component versions for Hortonworks Data Platform (HDP). To ensure that you are working with the most recent stable software available, you must be familiar with the latest Apache component versions in HDP. You should also be aware of the available Technical Preview components and use them only in a testing environment.

The Acceldata approach is to provide patches only when necessary, to ensure the interoperability of components. Unless you are explicitly directed by Acceldata Support to install a patch, each of the HDP components should remain at the following package version levels to ensure a certified and supported copy of HDP.

Official Apache component versions for HDP.

* Ambari 2.7.6.0
* Hadoop 3.2.3
* HBase 2.4.11
* Phoenix 5.0.0
* Hive 3.1.3 / 4.0.0-Alpha1
* Tez 0.10.1
* Spark 2 2.4.8
* Spark 3 3.2.2
* Kafka 2.8.2
* Ranger 2.3.0
* Infra Solr 2.7.6.0
* Sqoop 1.4.7 
* Impala 4.1.0
* Hue 4.10.0
* Zookeeper 3.5.10
* Zeppelin 0.10.1


## Java Certifications

| Name | Status |
| --------------- | --------------- |
|Java  | JDK 8 (Complete) <br> JDK 11 (TBD) |


## Upcoming Releases
| Component | Version | Release Date |
| --------------- | --------------- | --------------- |
|Nifi  | 1.19.1 |Q2-2023  |
|Druid  |25.0.0  |Q2-2023  |
|Kudu  |1.16.0  |TBD  |
|Ozone  |1.3.0  |Q3-2023  |

# ODP Repositories

This section describes the process to obtain the HDP repositories.

| OS | Version Number | Repository Name | Format | URL |
| --------------- | --------------- | --------------- | --------------- | --------------- |
|Redhat Linux  |  |ODP  |  |  |
|Cent OS  | |ODP  |  |  |
|Ubuntu  |  |ODP  |  |  |
|Debian  |  |ODP  |  |  |
|Amazon Linux 2  |  |ODP  |  |  |
|SLES 12  |  |ODP  |  |  |


# ODP Process Methodology
![](https://github.com/acceldata-io/odpdocumentation/blob/main/ODP%20process%20management.drawio%20(2).png)

# ODP Migration Options

Acceldata supports three types of migrations for ODP. The three migration methods are described as follows. 

## In-Place Upgrade

This is the fastest migration process and does not require you to uninstall the existing version. You can start this migration process without saving data beyond normal precautions. 


<div align="center">
    <img src="https://github.com/acceldata-io/odpdocumentation/blob/main/In-place.png">
</div>

## Side-car Upgrade

You can use the side-car migration technique when you have tight service-level agreements (SLAs) that preclude an extended. This process minimizes downtime on individual workloads while providing a straightforward roll-back mechanism on a per-workload basis.

<div align="center">
    <img src="https://github.com/acceldata-io/odpdocumentation/blob/main/sidecar.drawio.png">
</div>

## Forklift Upgrade

Forklift upgrade requires major changes to your existing IT infrastructure. Forklift upgrades are a result of relatively minor enhancements that cannot be implemented piece by piece due to legacy systems. In such cases, the hardware and software needs to be updated simultaneously, creating a job so large that it requires a metaphorical forklift to carry it out.

<div align="center">
    <img src="https://github.com/acceldata-io/odpdocumentation/blob/main/sidecar.drawio.png">
</div>

