# Software Requirements

Ensure that the following software packages are installed on each host:
* **yum** and **rpm** (RHEL/CentOS/Oracle/Amazon Linux)
* Intsall  **snappy** , **snappy-devel**,**Python**, **Python2**, **Python-devel***, **libtirpc-devel** to all the nodes of the cluster. (RHEL/CentOS/Oracle/Amazon Linux)
* **Zypper** and **php_curl **(SLES)
* **apt** (Debian/Ubuntu)
* **scp, curl, unzip, tar, wget**, and **gcc***
* OpenSSL (v1.01, build 16 or later)

# Collect Information

Before deploying a cluster, gather the following information:

* The fully qualified domain name (FQDN) of each host in your system. The Ambari Cluster Install wizard supports using IP addresses. You can use the
  `hostname -f` command to check or verify the FQDN of a host.
* A list of components you want to set up on each host.

* The base directories to be used as mount points to store the following data:
    - NameNode data
    - DataNodes data
    - Secondary NameNode data
    - Oozie data
    - YARN data
    - ZooKeeper data,
    - Various log, pid, and db files, depending on your install type


