# System Setup

### Prerequisites

#### System Specification recommendations (Running owl-web and owl-core):

Operating System

* RHEL6+ RHEL7+ 
* Centos6+ Centos 7+

Hardware Based on Role (standalone, distributed, or fully-distributed)

| Role                     | Ram | CPU | Storage | Concurrent Users |
| ------------------------ | --- | --- | ------- | ---------------- |
| owl-web                  | 32  | 8   | 100 GB  | \~50             |
| owl-metastore (postgres) | 16  | 4   | 250 GB  | --               |
| edge node / agent        | 16  | 4   | 50 GB   | --               |

Java Version

* Oracle JDK version "1.8.0\_152" +
* Open JDK version 1.8.0+

Encryption

* Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction

Client Browser

* Chrome 70.0.3538.102+
* Firefox - 52.8.0+
* Safari Version 12.0.1+
* Support of IE 11.0+

Postgres Version

* Owl come prepackaged with version 11.4 of postgres
* Version 9.6.5 and above is supported if wanting to use an external metastore

#### User Privileges:

* Installation is completed via tarball
* User needs to be able to create directories, launch scripts, and start processes (java processes)
* SUDO is not required
* ULIMIT settings of 4096 or higher (see below)
  * All owl services typically consume about 428 threads.
  * During each owlcheck about 400 additional threads are consumed.
  * Thus 4096 threads can allow for about 9 concurrent owlcheck jobs (on a standalone install).  If more are needed plan accordingly.

#### Default Ports used by Owl

* 5432 - Postgres
* 9000 - Owl-web

### Planning the installation

It is always best to consult the field team from Collibra DQ for more information about what options make the most sense for your environment.

1. Determine how we are planning to install Collibra DQ (standalone or distributed) as shown in Owl-Analytics Architecture section
2. Plan infrastructure, scale, and HA
3. Validate your system prereqs
4. Obtain the Packages from Collibra DQ

### Installation Packages/Files (BOM)

* demoscripts.tar.gz
* log4j\*
* owlcheck
* owl-core-2.1.0-jar-with-dependencies.jar
* owl-webapp-2.1.0.jar
* owl-agent-2.1.0.jar
* setup.sh
* owl-postgres.tar.gz
* owlmanage.sh
