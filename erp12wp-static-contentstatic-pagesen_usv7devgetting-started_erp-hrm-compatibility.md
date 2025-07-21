[Index](index.html)  [Home](getting-started_home.html)

Constraints using Sage X3 and Sage X3 HR & Payroll on the same site

Sage X3 and Sage X3 HR & Payroll can be installed on the same site, even if they are not in the same version. The constraints are as follows:

* They must be installed as separate solutions.
* They must share the same Syracuse server as endpoints of the same website (on different applications).
* The sitemap (navigation page), menu entries and authoring associated with each application must all be delivered and installed with the Syracuse server.  
  To avoid dysfunctions related to links definition or authoring, Sage X3 and Sage X3 HR & Payroll must be updated to the version that match the menus and authoring delivered with the Syracuse server.  
  For example, update 11 of the Syracuse server is delivered with the same sitemap and authoring as Sage X3 version 11, while Sage X3 People uses version 9 elements. As a result, you can use both Sage X3 version 11 and Sage X3 People version 9 with version 11 of the Syracuse server.
* A single Syracuse server can have different endpoints representing different solutions. However, all solutions of a given application (Sage X3 and Sage X3 HR & Payroll) must be updated to the same version as they share the same authoring and links definitions.

As of version 9, the Sage X3 and Sage X3 People compatibility matrix is as follows:

| Syracuse | Sage X3 | Sage X3 People |
| --- | --- | --- |
| Version 9 | Version 9 | Version 9 |
| Version 11 | Version 11 | Version 9**\*** |

If the Syracuse server is common to Sage X3 and Sage X3 HR & Payroll but both applications are not in the same version, you should install the additional patch delivered with the main patch. It contains the menus, navigation pages, and the authoring. This allows you to upgrade the version and work with the correct level of resources.

The resources pack is delivered starting from version 9 patch 09 for Sage X3 People, or version 11 patch 08 for Sage X3.

  

[Index](index.html)  [Home](getting-started_home.html)