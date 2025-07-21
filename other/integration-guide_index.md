[Index](index.html)  [Home](getting-started_home.html)

Integration guide

**This set of documentations describes the use of extensibility scenarios. Some of them are experimentally deployed in upgrade 9. The APIs described in the corresponding documents require a manual deployment that prevents for the moment an installation on the Clouds. Some of them have minimal APIs that will change in the future.**

**For this reason, these integration techniques are usable only in an Early adopter program context.**

**The SAFE X3 platform has various components to ease its extension. The different integration layers can be described by the different schemas. In these schemas:**

* **The green boxes represent the layer that requests / calls the integrated component.**
* **The red boxes represent the layer that executes the component.**
* **The blue boxes are the integration layers.**

## Web services integration

The first type of integration is the supply of services hosted by the platform to external programs through web services. Two flavors of web services exist, SOAP and REST.

The first schema is related to SOAP web services:

![](images_extensibility.jpg)

SOAP web services are connected to classic code (V6 style objects and sub-programs). More details are given in the [following document](integration-guide_ws-overview.html).

The second schema is related to REST web services

![](images_extensibility1.jpg)

REST web services are connected to classes and representations (V7 style programming). More details are given in the [same document](integration-guide_ws-overview.html).

## 4GL extensibility

Managing integration can be done with the [File-oriented integration](integration-guide_file-integration.html) and the [Database-oriented integration](integration-guide_database-integration.html).

## Future extensions not yet documented

* [Administration extensibility](integration-guide_administration-extensibility-overview.html) is reserved for SAGE internal use at this stage.
* [Container-based extensibility](integration-guide_container-extensibility-overview.html) is not yet available but will likely play in both deployment contexts in the future.

## Online vs. on-premise

The integration and extensibility mechanisms are available both in Online and on-premise deployments of Sage X3, but with different levels of control. More specifically:

Integration through [Web Services](integration-guide_ws-overview.html): these mechanisms are supported at the same level online and on-premise. The only difference is on the supported authentication mechanisms. The online deployment imposes [OAuth2 authentication](integration-guide_ws-oauth2-authentication.html), while the on-premise deployment also supports [*basic*](integration-guide_ws-basic-authentication.html) and [*client certificate*](integration-guide_ws-certificates-authentication.html) authentication.  
  
  
[File-oriented integration](integration-guide_file-integration.html) is supported on-premise with regular files as infrastructures. In a future release, we expect to propose an integration with S3 buckets online.  
  
  
Direct SQL [database-oriented integration](integration-guide_database-integration.html) is only supported on-premise. Managed Cloud storage services are an alternative that will be considered in a further release for online integration.

  

[Index](index.html)  [Home](getting-started_home.html)