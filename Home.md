Acceldata supports the Open-Source Data Platform. To use the Acceldata supported Open-Source Data Platform (ODP), you must install it. This documentation explains the installation process of Acceldata Open-Source Data Platform (ODP). 

# What is ODP

* An Open Source Data Platform 
* Alternative to proprietary platform and a monopoly
* Available to Pulse customers who don’t want to get locked in with a single Vendor
* 100% Open source - Built and Tested by Acceldata using latest upstream code
* Same stack Deployed at T-Mobile, AT&T , True Corp, AIS group & PhonePe, HCSC, Freddie Mac


# ODP Architecture

The following image displays the architecture of ODP. 

https://github.com/acceldata-io/odpdocumentation/blob/main/assets/arch2.png

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

# ODP Process Methodology
![](https://github.com/acceldata-io/odpdocumentation/blob/main/assets/ODP%20process%20management.drawio%20(2).png)

# ODP Migration Options

Acceldata supports three types of migrations for ODP. The three migration methods are described as follows. 

## In-Place Upgrade

This is the fastest migration process and does not require you to uninstall the existing version. You can start this migration process without saving data beyond normal precautions. 

![](https://github.com/acceldata-io/odpdocumentation/blob/main/assets/In%20place%20migrate.drawio.png)

## In-Place Upgrade




