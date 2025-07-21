[Index](index.html)  [Home](getting-started_home.html)

About files naming

When producing and managing a large number of setup and patch files, it is important to have a good naming convention for these files so that an installer can quickly and precisely identify what a file contains, regardless of where it is stored.

The naming convention for the files is the following:

```
Product-ComponentName-M.m.P.b-os-architecture.ext
```

  
With the following rules:

* **`Product`:** Product name such as, **x3** for Sage X3, **x3hr** for Sage X3 HR & Payroll, **x3wh** for Sage X3 Warehousing. The **Product** part is optional.
* **`ComponentName`:** Name of the component such as runtime, application, webserver, javabridge, syracuse. It can also indicate what the file is such as installer, patch, doc, readme, and so forth.
* **`M.m.P.b`:** Version formatted as **Major.minor.Patch.build**. The **build** part is optional.
* **`os`:** Windows or Linux OS â win or Linux
* **`architecture`:** Only fill in if required. Avoid adding this for a jar file.
  + -x86: 32 bits
  + -64: 64 bits
  + -x64: 32 and 64 bits
* **`ext`:** Is the extension.

# Note

The `ComponentName`and `M.m.P.b` elements do not contain any ' **-** ' or space characters. The names can be parsed and there is no issue with spaces. Additionally, they are all lowercase to avoid potential mismatches on Unix.

# Examples:

* `x3-application-12.0.19.jar`: build 19 of X3 version 12.0 application server installer.
* `runtime-91.3.5.12.jar`: build 12 of 91.3.5 runtime installer
* `syracuse-server-12.0.19.jar`: build 19 of Sage X3 Syracuse Server version 12.0.

For further information, please consult our [Naming Files-Components](https://confluence.sage.com/x/rtWRD) Confluence page.

  

[Index](index.html)  [Home](getting-started_home.html)