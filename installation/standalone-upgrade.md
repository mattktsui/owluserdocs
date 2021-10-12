# Standalone Upgrade

#### Steps

1. Copy the contents of the provided package e.g. owl-\<newversion>-\<SPARK301>-package-base.tar.gz to the system being upgraded (extract contents)
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
