# Architecture Diagram

### Owl Standalone <a href="howlstandalone" id="howlstandalone"></a>

![Owl stand alone](https://lh3.googleusercontent.com/v8y\_20neYCCo1FoOAkc3Zc_xItIPevxxVGiNbYy5L1F9oi-lJF5lyNkAr5ZMN00ERbEU4FS_j3kvZzgUf08ceeo0U0Sgc3tnFflOuVShrRfETUSkhtYOmPQxmaCaGpHO2hrWIW_V)

The image above depicts owl-web, owl-core, postgres and orient all deployed on the same server.  This can be an edge node of a Hadoop cluster or a server that has access to run spark-submit jobs to the hadoop cluster.  This server could also have JDBC access to other DB engines interested in being quality scanned by Owl. Looking at this depiction from left to right the client uses their browser to connect to Owl’s Web Application running on port 9000 (default port).  The Owl Web Application communicates with the two metastores (Postgres and Orient). The Web Application can run a local owlcheck job, or the owlcheck script can be launched from the CLI natively. The owlcheck will launch a job using Owl’s built in Spark Local DQ Engine.  Depending on the options supplied to the owlcheck command the DQ job can scan a file or database with JDBC connectivity.

### Owl Distributed <a href="howldistributed" id="howldistributed"></a>

![Owl Semi-Distributed](https://lh4.googleusercontent.com/j4licslWJZLkm1CKVrD9P98RY8Ycjzphs1tUtVqrQuSms29yu5z4inBW3yxBCUR6JxpP8TIR45fiCshSJXVIHKQshIW4bREApPduNbewWf6cUPuvp\_26gYFcl1wruEsJEecMQrF4)

The image above depicts owl-web and owl-core deployed on different servers.  Example Owl-web would NOT be deployed on the edge node. Owl-core would be installed on the edge node and write Owlcheck results back to the metastore that Owl-web points to (NOTE in this scenario the metastore and the web-app are running on the same host).  The other change is that the owlcheck job will distribute the work on top of a Hadoop cluster in order to leverage spark and use the parallel processing that comes with the Hadoop engine itself.

### Owl Fully Distributed <a href="howlfullydistributed" id="howlfullydistributed"></a>

![](<../.gitbook/assets/image (77).png>)

The image above depicts all components deployed on different servers.  OrientDB setup as a cluster which provides fault tolerance in case there is an issue with a single machine (NOTE: starting with version 1.1.0 of Owl, Orient is an optional service – or Owl-Web and Owlcheck do not rely on Orient being Available).  Postgres setup in a cluster in case one server fails. Multiple owl-web deployed behind a load balancer yet communicating with the same Metadata. Owl-core would be installed on the edge node and write Owlcheck results back to the metastores that Owl-web points to.  In this depiction the owlcheck driver runs on the Edge Node while the majority of the work gets pushed to the cluster (deploymode = client flag was sent), so all communication connects from the edge node to the metastores.

![](<../.gitbook/assets/image (78).png>)

In this depiction the owlcheck driver and job gets pushed to the cluster (deploymode = cluster flag was sent), so all communication connects from any node on the cluster back to the metastore.  
