# Standalone Upgrade

### Download DQ Upgrade Package

**Note: Beginning December 2021, all Collibra DQ customers upgrading or patching will be receiving the Full package (vs. Base) and should follow the same Upgrade steps below**

Download tarball using the signed link to the full package tarball provided by Collibra. Replace `<signed-link-to-full-package>` with the link provided.

```
### Go to the OWL_BASE (home directory of the user is most common)
### This example we will use /home/owldq installing as the user owldq

cd /home/owldq 

### Download & untar
curl -o dq-full-package.tar.gz "<signed-link-to-full-package>"
tar -xvf dq-full-package.tar.gz

### Clean-up unnecessary tarball (optional)
rm dq-full-package.tar.gz
```

### Upgrade Steps

1. Copy the contents of the provided package e.g. owl-\<newversion>-\<SPARK301>-package-full.tar.gz to the system being upgraded (extract contents)
   * Best practice: Untar contents into a uniquely named folder e.g. 2021-12-dq-upgrade
2. Stop owlweb using `./owlmanage.sh stop=owlweb`
3. Stop owlagent using `./owlmanage.sh stop=owlagent`
4. Move old jars from `owl/bin`
   1. `mv owl-webapp-<oldversion>-<spark301>.jar /tmp`
   2. `mv owl-agent-<oldversion>-<spark301>.jar /tmp`
   3. `mv owl-core-<oldversion>-<spark301>.jar /tmp`
5. Copy new jars into the `owl/bin` folder from the extracted package
   1. `mv owl-webapp-<newversion>-<spark301>.jar /home/owldq/owl/bin`
   2. `mv owl-agent-<newversion>-<spark301>.jar /home/owldq/owl/bin`
   3. `mv owl-core-<newversion>-<spark301>.jar /home/owldq/owl/bin`
6. run `./owlmanage.sh start=owlweb` to start the owl-web application
7. run `./owlmanage.sh start=owlagent` to start owlagent

### Additional Notes / Steps Due To Log4J (December 2021)

#### Additional Step 1: Place Log4j-1.2-api-2.17.0.jar into /\<install-home>/owl/spark/jars

**Who: All Collibra DQ customers, particularly those leveraging CLI mode**

1. Navigate to the same folder where the Collibra provided upgrade package was extracted
2. Navigate to \<location of 2021-12-dq-upgrade>/packages/install-packages
3. Extract the needed log4j-1.2-api-2.17.0.jar via the command:`tar -xvf spark-extras.tar.gz spark-extras/log4j-1.2-api-2.17.0.jar`&#x20;
4. Move the log4j-1.2-api-2.17.0.jar file into /\<install-path>/spark/jars folder

**FAQ**

Q: (When) do I need to move Log4j-1.2-api-2.17.0.jar before or after swapping the main Collibra DQ jars?

* A: Sequence does not matter.

Q: (What) if I don't follow these additional upgrade steps?

* A: If your `SPARK_SUBMIT_MODE` within owl-env.sh is set to `SPARK_SUBMIT_MODE=native`, Collibra DQ will function properly without the above additional upgrade step, with the exception of CLI mode

#### Additional Step 2: Remove a legacy properties file

**Who: Only Collibra DQ customers upgrading Agents installed on Hadoop Edge Node**

1. Navigate to /\<agenthome>/owl/config/&#x20;
2. Remove `log4j-cluster.properties` file

**FAQ**

Q: (When) do I need to remove log4j-cluster.properties before or after swapping the main Collibra DQ jars?

* A: Remove the file before restarting owl-agent. Otherwise, stop owl-agent again, remove the file, then restart owl-agent.

Q: (What) if I don't follow these additional steps?

* A: For customers using agents on Hadoop edge nodes, they will receive errors when running DQ Jobs due to engaging a method that no longer exists.
