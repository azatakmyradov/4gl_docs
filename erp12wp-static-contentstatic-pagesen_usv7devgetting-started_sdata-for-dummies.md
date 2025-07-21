[Index](index.html)  [Home](getting-started_home.html)

Sdata for dummies

`SData` is a web protocol created by Sage that:

* Is standard-based, building upon the HTTP, ATOM, and JSON specifications.
* Conforms to the REST principles.
* Is applicable to a variety of scenarios such as APIs, mobile apps, or third party integration.
* Is free to use.

Versions 7 and above use this protocol between the Sage X3 Web Server and the various clients such as web services, Microsoft Office software, mobile client, and web client with some extensions:  
\* There are two branches of protocol:   
 \* The first one is RESTful and stateless and used when data is browsed.   
 \* The second one is stateful, and is only used when an update is in progress. A working copy unique ID identifies the resource in which the modification is in progress and deltas are exchanged.  
\* When a resource is needed for a page, there are two data feeds:   
 \* The first one returns the prototype. It is the description of the data feed managed by the resource, and corresponds to the description of the contract.   
 \* The second one is the data by itself. A data feed may include additional prototypes updates.

For more information about `SData`, go to the following website: <http://sdata.sage.com/>

  

[Index](index.html)  [Home](getting-started_home.html)