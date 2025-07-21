[Index](index.html)  [Home](getting-started_home.html)

Architecture schema

The Sage X3 version 7 platform includes several components. Some of them are new and linked to the Version 7 platform, and some are required to support the version 6 technology used by the Classic mode.

The following schema shows all the servers that might be installed in a complete Sage X3 implementation:

![](images_architecture.jpg)

On this schema:

* The node.js server is the main web server that connects the user interface to the different servers, manages administration data, and authentication. It can be a storage of servers, every server running one or several node.js processes (usually one per core). When several node.js processes are present, a load balancer is used to distribute the requests to the different node instances.
* The mongodb server is used to store the administration data in mongoDB noSQL database. This logical server can also be a storage of servers configured for [replication](http://docs.mongodb.org/manual/core/replication-introduction/) and/or [sharding](http://docs.mongodb.org/manual/core/sharding-introduction/).
* The Elasticsearch server is used to handle the search index update and search functions. This logical server can also scale in [clusters](http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/distributed-cluster.html).
* The X3 process servers and the X3 application server manage the X3 process execution including the connection to the database servers. They perform the same role as in version 6.
* The database server is the server in which the database service runs (Oracle or SQL server).
* The version 6 web server is an optional server that is still used for some applications such as the VT connection and the SOAP V6 web services. It will become obsolete in future versions.
* The Java bridge server is an optional server that works similarly in version 6 and that is used for SOAP web services. It will also become obsolete in the future.
* The print server runs the Crystal Reports used in Sage X3. As the version 6 client that was able to embed the Crystal Report runtime is no longer used, it becomes mandatory to install it.
* The SAP Business Object server is used to run Business Object reports. It is an optional component.
* The SMTP server is used to send email messages (with the V6 workflow tool).

All these servers are "logical servers" that can be deployed on a single server (especially for demo purposes). Usually, dedicated servers are used for database, search, and mongoDB. They can be virtualized based on the specifications of the corresponding vendors.

If we focus on the main components of the platform, the schema can be described as following:

![](images_architecture-schema2.jpg)

This schema shows the following elements:  
\* a client can have one or several browser instances, that connect on version 7 web server (1). The node.js web server can have several instances and a load balancer is provided to handle a reasonable number of node.js instances (usually one per core on 1 to 5 servers). An external load balancer can of course also be used to distribute the http/https requests on several node servers.  
\* The MongoDB is able to run on clusters as well (2).  
\* Lucene and Elasticsearch are also technologies built for the cloud, able index and search over millions of entries (3).  
\* The standard databases used (Sql server, oracle) are highly scalable and able to run in distributed environment when necessary (4).  
\* The server that runs Sage X3 application code can be distributed on several servers (5).

If a huge number of data need to be managed by MongoDB and/or Elasticsearch, they are even able to split the data on several shards (but this is unlikely to happen in the ERP field).

  

[Index](index.html)  [Home](getting-started_home.html)