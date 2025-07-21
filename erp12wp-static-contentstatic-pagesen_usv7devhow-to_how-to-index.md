[Index](index.html)  [Home](getting-started_home.html)

How to documents

The following are some examples showing best practices to be adopted by development partners using the Sage X3 workbench.

# Normalization

**In this chapter, you will find the codification rules as well as the recommendations given to the developers producing standard, vertical and specific code in order to enhance the readability and to ease the future evolution of the code.**

* [Naming conventions](how-to_how-to-naming.html)
* [Writing and running Sage X3 unit tests](how-to_how-to-use-axunit.html)
* [How to create read-only pages that replace V6 objects](how-to_how-to-handle-read-only-pages.html)

# Code examples

* [CRUD example on 3 levels](how-to_how-to-crud-3-levels.html)
* [CRUD example on a version 6 "combined object"](how-to_how-to-crud-combined-object.html)
* [AXUNIT use: How to design a test case on a persistent class](how-to_how-to-test-a-class.html)

# V12 development examples

**You will find here examples based on a real development made by a team experiencing the development techniques for V12**.

* Property (Field) control:  
  + [How to set an initial value for a property](how-to_how-to-set-an-initial-value-for-a-property-field.html)
  + [How to process child collection rows](how-to_how-to-process-child-collection-rows.html)
  + [How to change the value of one property from an update to a different property](how-to_how-to-change-the-value-of-one-property-from-an-update-to-a-different-property.html)
  + [How to make a property mandatory or optional from an update to a different property](how-to_how-to-make-a-property-mandatory-or-optional-from-an-update-to-a-different-property.html)
  + [How to disable or make a property editable from an update to a different property](how-to_how-to-disable-or-make-a-property-editable-from-an-update-to-a-different-property.html)
  + [How to hide or make a property visible from an update to a different property](how-to_how-to-hide-or-make-a-property-visible-from-an-update-to-a-different-property.html)
  + [How to handle errors on interdependent fields](how-to_how-to-handle-errors-on-interdependent-fields.html)
* Methods / Operations:  
  + [How to change the properties of one data class from another data class using a standard Method](how-to_how-to-change-the-properties-of-one-data-class-from-another-data-class-using-a-standard-method.html)
  + [How to change the properties of one data class from another data class using an Operation](how-to_how-to-change-the-properties-of-one-data-class-from-another-data-class-using-an-operation.html)
  + [How to create data for a child class from another data class using an Operation](how-to_how-to-create-data-for-a-child-class-from-another-data-class-using-an-operation.html)
  + [How to use methods defined in other classes](how-to_how-to-use-methods-defined-in-other-classes.html)
  + [How to get information relating to the current context](how-to_how-to-get-information-relating-to-the-current-context.html)
* Representation (User interface) classes:  
  + [How to add a filter to the Query facet](how-to_how-to-add-a-filter-to-the-query-facet.html)
  + [How to modify the selections (Query facet) for a standard data table](how-to_how-to-modify-the-selections-query-facet-for-a-standard-data-table.html)
  + [How to add columns to a standard Query facet](how-to_how-to-add-columns-to-a-standard-query-facet.html)
  + [How to filter rows in a standard Query facet](how-to_how-to-filter-rows-in-a-standard-query-facet.html)
  + [How to add a URL to launch a web page](how-to_how-to-add-a-url-to-launch-a-web-page.html)
  + [How to add an image to a Representation class](how-to_how-to-add-an-image-to-a-representation-class.html)
  + [How to add a clob (text) to a Representation class](how-to_how-to-add-a-clob-text-to-a-representation-class.html)
  + [How to use multiple ASETERROR methods in a single Representation class](how-to_how-to-use-multiple-aseterror-methods-in-a-single-representation-class.html)
* V12 client configuration:  
  + [How to make a class representation visible in the client](how-to_how-to-make-a-class-representation-visible-in-the-client.html)
  + [How to make a class representation visible on a mobile device](how-to_how-to-make-a-class-representation-visible-on-a-mobile-device.html)
* Development environment / Development techniques / Best practice:  
  + [Best practice: Naming rules](how-to_best-practice-naming-rules.html)
  + [Best practice: Data classes](how-to_best-practice-data-classes.html)
  + [Best practice: Representation classes](how-to_best-practice-representation-classes.html)
  + [Best practice: Developing processes](how-to_best-practice-developing-processes.html)
  + [Best practice: Methods and operations](how-to_best-practice-methods-and-operations.html)
  + [Best practice: Grouping your development work](how-to_best-practice-grouping-your-development-work.html)
  + [Best practice: Avoid unnecessary Order By on SQL requests](how-to_best-practice-avoid-order-by.html)
  + [How to create and run an automatic unit test on a data class](how-to_how-to-create-and-run-an-automatic-unit-test-on-a-data-class.html)
  + [How to work with collections using AXUNIT](how-to_how-to-work-with-collections-using-axunit.html)
  + [How to install Eclipse and use it to debug Version 7 code](how-to_how-to-install-eclipse-and-use-it-to-debug-version-7-code.html)

# V12 development techniques

**When switching to development in V12 native developers, experienced in V6 development techniques, must adjust their coding methodology. It is therefore CRITICAL to read and understand ALL of the following details and advice on correct practice:**

[INTRODUCTION: READ THIS CAREFULLY](how-to_tip-version-7-development-techniques-and-examples.html)

* Data classes / Representations:  
  + [Class definition elements to include or exclude](how-to_tip-class-definition-elements-to-include-or-exclude.html)
  + [Data values used for a table's primary index must not change](how-to_tip-data-values-used-for-a-table-s-primary-index-must-not-change.html)
  + [Avoid data duplication in a class](how-to_tip-avoid-data-duplication-in-a-class.html)
  + [When code should be stored at the data class level and when at the representation level](how-to_tip-when-code-should-be-stored-at-the-data-class-level-and-when-at-the-representation-level.html)
  + [Use of child classes versus references](how-to_tip-use-of-child-classes-versus-references.html)
  + [Controlling the user interface on a mobile representation](how-to_tip-controlling-the-user-interface-on-a-mobile-representation.html)
* Methods and operations:  
  + [A method must have a return value](how-to_tip-a-method-must-have-a-return-value.html)
  + [The return value of a method must be checked](how-to_tip-the-return-value-of-a-method-must-be-checked.html)
  + [Control the parameters sent to a method or an operation](how-to_tip-control-the-parameters-sent-to-a-method-or-an-operation.html)
  + [Distinction between methods and operations and working in a stateless context](how-to_tip-distinction-between-methods-and-operations-and-working-in-a-stateless-context.html)
* Processes and best practice:  
  + [Avoid using global variables](how-to_tip-avoid-using-global-variables.html)
  + [Define your variables as local](how-to_tip-define-your-variables-as-local.html)
  + [Use constants to keep code readable](how-to_tip-use-constants-to-keep-code-readable.html)
  + [Handling void values in function parameters and return values](how-to_tip-handling-void-values-in-function-parameters-and-return-values.html)
  + [Always follow template script structures](how-to_tip-always-follow-template-script-structures.html)
  + [Error handling on properties via methods](how-to_tip-error-handling-on-properties-via-methods.html)
  + [Error management in version 7](how-to_tip-error-management-in-version-7.html)
  + [Checking class context in scripts](how-to_tip-checking-class-context-in-scripts.html)
  + [Closing tables](how-to_tip-closing-tables.html)
  + [New supervisor library functions to use](how-to_tip-new-supervisor-library-functions-to-use.html)
  + [When V6 code can be reused](how-to_tip-when-v6-code-can-be-reused.html)
  + [Constructing messages for improved localisation](how-to_tip-constructing-messages-for-improved-localisation.html)
  + [Handling or restricting the insertion of lines into an array](how-to_tip-handling-or-restricting-the-insertion-of-lines-into-an-array.html)
  + [Handling or restricting the deletion of lines from an array](how-to_tip-handling-or-restricting-the-deletion-of-lines-from-an-array.html)
  + [Use of constants when testing return values](how-to_tip-use-of-constants-when-testing-return-values.html)
  + [Storing and managing images (BLOBs)](how-to_tip-storing-and-managing-images.html)
  + [Storing and managing text (CLOBs)](how-to_tip-storing-and-managing-text.html)
  + [Best practice for opening and closing tables](how-to_best-practice-for-opening-and-closing-tables.html)
  + [Best practice for using the APARENT class property](how-to_best-practice-for-using-the-aparent-class-property.html)
  + [Best practice for controls on updated properties](how-to_best-practice-for-controls-on-updated-properties.html)
  + [Best practice for propagating updates](how-to_best-practice-for-propagating-updates.html)
  + [Best practice for handling collections](how-to_best-practice-for-handling-collections.html)
  + [Best practice when using snapshots](how-to_best-practice-when-using-snapshots.html)
  + [Best practices for data transaction handling](how-to_best-practice-for-data-transaction-handling.html)
  + [Best practices for updating a record if it exists otherwise creating a new one](how-to_best-practice-for-updating-a-record-if-it-exists-otherwise-creating-a-new-one.html)
  + [How to use filters with variables](how-to_how-to-use-filter-with-variables.html)
  + [Best practices for objects with header/lines structure](how-to_best-practices-for-header-line-objects-structure.html)

**Working in Classic mode with some external resources may need to use dedicated techniques. They are described here:**

* [Instructions and syntaxes no more usable in Classic code](how-to_tip-instructions-and-syntaxes-no-more-usable-in-classic-code.html)
* [How to manage files in the storage area](how-to_how-to-manage-files-in-the-storage-area.html)
* [How to handle documents in Classic pages](how-to_how-to-handle-documents-in-classic-pages.html)
* [Classic functions and new pages cohabitation](how-to_tip-classic-functions-and-new-pages-cohabitation.html)

# Platform administration and tools

**How to documents related to the platform administration are located here.**

* [How to set up Oauth2 authentication with a google account](how-to_how-to-set-up-gmail-account-sso.html)
* [How to set up Oauth2 authentication with a microsoft account](how-to_how-to-set-up-microsoft-account-sso.html)
* [How to configure Syracuse for MongoDB X509 authentication](how-to_how-to-configure-Syracuse-for-MongoDB-X509-authentication.html)
* [How to use QR-codes in mail merge templates](how-to_how-to-use-qr-codes-in-mail-merge-templates.html)
* [How to create an icon for a module](how-to_how-to-create-an-icon-for-a-module.html)
* [How to transfer administration data](how-to_how-to-transfer-administration-data.html)
* [How to duplicate a Syracuse server](how-to_how-to-duplicate-syracuse-server.html)
* [How to transfer mobile applications](how-to_how-to-copy-mobile-apps.html)
* [How to manage multiple http and https servers](how-to_how-to-manage-multiple-http-and-https-servers.html)
* [How to handle legacy passwords](how-to_how-to-handle-legacy-passwords.html)
* [Strategies for mongoDB data transfer and administration](how-to_how-to-transfer-mongoDB-data.html)
* [Ensure the security of mongoDB](how-to_how-to-secure-mongodb.html)
* [Force the connection of a user on a dedicated server for a solution](how-to_force-main-server-for-connection.html)
* [Comply with FDA regulations such as CFR 21-11](how-to_compliance-to-FDA.html)
* [Rename a server](how-to_how-to-rename-a-server.html)
* [Installing several node servers](how-to_how-to-install-several-node-servers.html)

# Crystal Reports

* [How to change the printer tray during the printing of a document](how-to_tray-change.html)

# Print server

* [Print server ODBC driver for Oracle](how-to_how-to-ODBC.html)

  

[Index](index.html)  [Home](getting-started_home.html)