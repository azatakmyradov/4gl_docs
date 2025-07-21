[Index](index.html)  [Home](getting-started_home.html)

Installing Sage X3

# Prerequisites

This document describes how to install a Sage X3 solution on a Windows or Linux server.

**Note:** This procedure only applies to the first installation of a Sage X3 platform technology V12 product on new servers and workstations. It is important that a prior version of Sage X3 has never been installed on the server.

If you want to upgrade an existing Sage X3 solution from V11 to V12, refer to [Upgrading an Existing Sage X3 Solution](getting-started_quick-upgrade-guide.html).

Before the installation, you need to:

1. Define the architecture of the servers that make up the Sage X3 solution.
2. Check the [minimum requirements](prerequisites_last-version.html) of your system environment.
3. Make sure Java Runtime Environment or JDK version 8 is installed. It can be downloaded from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/index.html). Oracle Java Runtime Environment (JRE) or Java Development Kit (JDK) latest versions require commercial licensing to be used on production systems. You can download the open-source [Zulu JRE or JDK 8 provided by Azul Systems](https://www.azul.com/downloads/zulu-community/) instead. Make sure you download and install the Windows x86 Java version for your 64-bit Windows operating system.

You can then follow the installation procedure available on the official support (DVD-ROM or network location containing the installation files).

# Installation overview

The main installation steps are listed below. Additional information is available in the corresponding paragraphs.

## Installing and configuring the SAFE X3 solution (Linux or Windows)

1. [Install the AdxAdmin administration runtime.](#runtime)
2. [Install the components to configure a Sage X3 solution.](#solution)
3. [Install the console on a Windows workstation.](#console)
4. [Create a Sage X3 solution using the console.](#platform)

## Installing Sage X3 Syracuse server components (Linux or Windows)

1. [Install Elasticsearch.](#elastic)
2. [Install MongoDB.](#mongo)
3. [Install Sage X3 Syracuse server.](#node)

## Completing the installation for Sage X3 Syracuse server and the Sage X3 solution

1. [On the Syracuse server:](#compsyra)

1. Update MongoDB and the Syracuse server.
2. You need to update the Syracuse server and MongoDB with the latest patch.
3. Make sure that you have the [latest available version of MongoDB Community Edition](how-to_how-to-upgrade-to-MongoDB.html) installed with the corresponding prerequisites for the Syracuse server.

2. [On the Sage X3 solution:](#compsafe)

1. [Install the Seed folder.](#seed)
2. [Apply the list of patches.](#patches)
3. [Update the search index.](#indexsearch)

## Installing the Production Scheduler

**Caution:** This feature is only available on-premise. If you are using the Cloud solution, this step is not relevant. It is not available for new Sage X3 installations.

1. [Install the Production Scheduler.](#prodscheduler)

## Installing the Print server component (Windows)

1. [Install a Print server component.](#print)

## Installing additional and optional servers

1. [Install a Documentation server component (Linux or Windows).](#documentation)
2. [Install an additional Process server component (Linux or Windows).](#process)
3. [Install a Java Bridge component (Linux or Windows)](#java)
4. [Install web wervices and the legacy Automated Data Collection (ADC) server component (Linux or Windows).](#webservice)
5. [Install Sage X3 Services](#x3s).

## Installing and configuring the Sage X3 Automated Test Platform

1. [Install the Sage X3 Automated Test Platform](#atp).

# Installing and configuring the SAFE X3 solution (Linux or Windows)

## Installing the AdxAdmin administration runtime

For Linux Red Hat and Oracle servers, the **libunwind** library is mandatory since release 2022 R4/V12.0.32.

1. Open a command prompt and enter **yum install libunwind** to install the **libunwind** library before installing the runtime.
2. Go in the console to define the path (or paths if it is a multi-runtime configuration). Follow the instructions given in the [console documentation](configuration-console_console.html#sage-x3-runtime).
3. You can then install and configure the runtime.

You have to install an administration runtime on each Process, Application, Database, Print, Java, web service and ADC servers. However, it is not required on the client workstations or on the workstation that runs the management console.

Double-click **adxadmin-M.m.P.jar file** in the **AdxAdmin** folder.  
The default AdxAdmin service port is 1818. Make sure this port is not blocked by existing firewalls or antivirus software as it is used to communicate with the console.

**Caution:**

1. **For Windows servers**, run the installer as a user with administrator rights and rights to log on as a service.
2. **For Linux servers**, run the installer as root to create the AdxAdmin service. You can then run the AdxAdmin service as root and use the proprietary account of the SGBD Oracle installation to configure the database component in the SAFE X3 console. Refer to our [console documentation](configuration-console_console.html#component-loading) (**AdxAdmin process rights**) for more information.

## Installing the components to configure a Sage X3 solution

1. **On the database server only:**  
   Depending on the database used for SAFE X3, double-click **db-sql-M.m.P.jar file** or **db-ora-M.m.P.jar file** in the **DbSQL** or **DbORA** folder.  
   Make sure the appropriate database engine was installed with the required settings before attempting this installation.
2. **On the application server that hosts the Runtime component only:**  
   Double-click **x3-application-M.m.P.jar file** in the **Application** folder.  
   Select **New installation**.
3. **On the process server only:**  
   Double-click **runtime-M.m.P.jar file** in the **Runtime** folder.  
   Select **New installation**.

For further information, read the [application server installation procedure](getting-started_application-server-installation.html).

### Installing Microsoft PowerShell

PowerShell is a cross-platform task automation solution composed of a command-line shell, a scripting language, and a configuration management framework. PowerShell runs on Windows, Linux, and macOS.

For more details regarding Powershell, consult the [pre-requisites documentation](https://github.com/Sage-ERP-X3/dev-doc/blob/master/prerequisites/overview.md#microsoft-powershell).

#### PowerShell for Microsoft SQL Server architectures

1. Install the [MSI package](https://github.com/PowerShell/PowerShell/releases/download/v7.2.3/PowerShell-7.2.3-win-x64.msi).
2. Open an MS-DOS command prompt with administrator rights.
3. Enter **Pwsh.exe** to execute the PowerShell installation wizard.
4. Enter **$PSVersionTable** to check that you are in version 7.2 or higher.
5. Enter **Install-Module -Name SqlServer -Scope AllUsers -force** to install the Microsoft SQL Server PowerShell module.
6. Enter **Get-InstalledModule -Name SqlServer** to make sure that the installation went well.

**Note**: You can follow these procedures to install a PowerShell MSI package or module in offline mode:

* [Install a PowerShell MSI package in offline mode](getting-started_install-PowerShell-MSI-offline.html)
* [Install a PowerShell module in offline mode](getting-started_install-PowerShell-module-offline.html)

#### PowerShell for RedHat architectures

You can install via direct download [Microsoft PowerShell 7.2](https://learn.microsoft.com/en-us/powershell/scripting/install/install-rhel?source=recommendations&view=powershell-7.2) or later, or you can follow these steps:

1. Connect to the machine via PuTTy.
2. Enter **sudo -i** to execute the PowerShell installation wizard.
3. Enter **curl <https://packages.microsoft.com/config/rhel/7/prod.repo> | sudo tee /etc/yum.repos.d/microsoft.repo** to register the Microsoft RedHat repository.
4. Enter **sudo yum install --assumeyes powershell** to install PowerShell.
5. Enter **pswh** to launch PowerShell and make sure that the installation went well.
6. Enter **exit** to close PowerShell.

## Installing the console on a Windows workstation

Double-click the **console-M.m.P.jar** file in the **X3Installs\Console** folder to launch the installation.

## Creating a Sage X3 solution using the console

Since release 2022 R2/V12.0.30, Syracuse can consume the resource file of the Sage X3 application using either one of the following protocols:

* HTTP protocol (Apache Server)
* Sage X3 protocol (SADFSQ)

Sage recommends using SADFSQ from Syracuse server version 12.15 (delivered in release 2022 R2/V12.0.30). For older Syracuse versions, Apache is still required.

Before configuring a Sage X3 Solution, make sure that:

* Apache HTTP Server 2.2 or higher is installed on the application server. You can download it from the [Apache website](http://httpd.apache.org/download.cgi). For Windows distribution, select the **no\_ssl** MSI installer package under **binaries/win32**.
* The user account you use for the steps below has administrative rights and rights to log on as a service.

It is possible to configure Apache in the console but to use SADFSQ in Syracuse later. Select the **Sage X3 protocol (SADFSQ)** checkbox in the [X3 solutions](administration-reference_x3-solutions.html) function to do so.

To create a basic solution, consult our [console documentation](configuration-console_console.html#basic-solution).

# Installing MongoDB

MongoDB is an open-source document database. Follow the [detailed procedure](getting-started_MongoDB-installation-procedure.html) to install it.

**Note:** Make sure you install MongoDB before installing Sage X3 Syracuse Server.

# Installing Sage X3 Syracuse Server components (Linux or Windows)

## Installing Elasticsearch

Elasticsearch is an open-source, distributed real-time search and analytics engine.

Although Sage X3 is still compatible with previous releases, it is strongly recommended to install the latest version of Elasticsearch compatible with your release (to be checked in the [prerequisites overview page](prerequisites_overview.html)) as older versions will be no longer maintained by Elastic.

It is highly recommended to host Elasticsearch on a dedicated server.

Make sure you write down the Elasticsearch host name and its corresponding http service port number. These two parameters are defined in the elasticsearch.yml file. You will need to set these `hostname` and `port` parameters in the [nodelocal](getting-started_configuration-file-nodelocal.html) configuration file. These parameters are equivalent to `network.host` and `http.port` in the elasticsearch.yml file.

For further information on Elasticsearch set up, consult the [installation guide](https://www.elastic.co/guide/en/elasticsearch/reference/index.html).

## Installing the Sage X3 Syracuse server component

**Note:** Make sure you install MongoDB and Elasticsearch before installing the Sage X3 Syracuse server component.

Double-click **syracuse-server-M.m.P.jar** in the **SyracuseServer** folder to launch the installation:

* For Windows servers, run the installer as a user with administrator rights.
* For Linux servers, run the installer as root.

For more information on Sage X3 Syracuse server installation, refer to the [installation procedure](getting-started_web-syracuse-server-installation-procedure.html).

# Completing the installation for the Sage X3 Syracuse server and the Sage X3 solution

## On Sage X3 Syracuse server

1. Make sure the certificates were generated during the installation.  
   If not, generate the public key corresponding to the server (**server\_name.pwd**). Refer to the [certificate installation documentation](getting-started_certificate-installation.html) for more information.
2. Make sure the following services have been started:
   1. Agent Sage Syracuse
   2. Elasticsearch for Syracuse
   3. MongoDB for Syracuse
   4. Sage Syracuse

   ## On the Sage X3 solution

   1. Make sure the certificates were copied during the installation.  
      If not, copy the public key corresponding to the server (**server\_name.pem**) in the **keys** folder of the solution runtime.  
      If there are any periods (.) in the server name, replace them with underscores in the file name.
   2. Make sure the following services have been started:
      1. Sage X3 solution service
      2. Database services
   3. From a Sage X3 Syracuse server connection:
      1. Open an Internet browser and log on as **admin/admin** to **<http://ServerName:port>**.
      2. Go to **Administration > Endpoints > X3 solutions**.  
         When prompted to, click **+New X3 solution**. Enter a code, a description, an application, and the exact name of the Sage X3 solution, the main server host and the main server port. Click **Save**.
      3. Click **Create endpoints** in this new X3 solution and select the root folder.
      4. Click **Administration > Endpoints > Endpoints** and select the endpoint you created.  
         Add the **Super administrator** group in the **Administration** section and click **Save**.
      5. From the root folder endpoint, click **Personalizations and Menus initialization** in the right-hand panel.  
         Wait until the end of the import.
      6. Log out from the web server and log back in as admin.
      7. Click the endpoint name in the header and select the endpoint of the Sage X3 root folder.
      8. Click **Setup > Users > Users** (**GESAUS** function).  
         Wait until the Supervisor installation is complete.

   ## Installing the Seed folder

   The Seed folder is the demonstration folder supplied with Sage X3. Aside from root folder X3, the Seed folder is the first endpoint you can connect to. After completing the installation, you can use the Seed folder as a sandbox.

   To install it:

   1. Navigate to the **Seed** directory in the product DVD-ROM.
   2. Double-click the **x3-seed-M.m.P.zip** file to launch the self-extracting archive.
   3. Copy the extracted **Seed** folder to where the Sage X3 application folders are installed.
   4. Copy the extracted **X3\_PUB\Seed** subfolder to where the Sage X3 application **X3\_PUB** directory is located.
   5. Open the Console, select the Sage X3 solution from the **Solutions** tab and click the folders icon.
   6. Click **Import**, select the **Seed** folder from the drop-down list and make sure that **SVG** is set as the data directory.  
      Make sure **Import of the table structure only** is not selected and click **OK**.
   For more detail, consult our [console documentation](configuration-console_console.html#Import a folder).7. Define an endpoint for the **Seed** folder before using it.

   ## Applying the list of patches

   For a first installation, use the applicative setup installation support available from your local Sage download center.

   Mandatory if a zip file exists under the directory Patch:

   1. Go to **Administration > Utilities > Update > Updates** and click **Add an update**.
   2. Upload the zip file located in the **Patch** directory.
      For more details, refer to the [Administration reference updates](administration-reference_updates.html) documentation.

   ## Updating the search index

   You have to update the search index in order to use the data search feature for an endpoint.

   1. Log in to Sage X3 as admin.
   2. Go to **Administration > Usage > Search Index Management**.
   3. Select the data source endpoint to index.  
      Leave **Entities** blank.
   4. Select the locale for which the index must be updated.
   5. Select **Delete index before update**.
   6. Click **Update index**.  
      Refer to Search Indexes Administration for more information.

   # Installing the Production Scheduler

   The Production Scheduler is an option of the Manufacturing module.

   Double-click **production-scheduler-M.m.P.jar** in the **ProductionScheduler** folder to launch the installation.  
     
   Refer to [Installing the Production Scheduler](getting-started_production-scheduler-software-installation-procedure.html) for more information.

   # Installing a PrintServer component

   1. Double-click **print-server-M.m.P-win.jar** in the **PrintServer** folder.
   2. To implement a print server, consult our [console documentation](configuration-console_console.html#sage-x3-print-server).

   # Installing additional and optional servers

   ## Installing a Sage X3 Documentation server component

   By default, Sage X3 tries to access the online documentation server through the internet, but an optional local server can be installed. This allows customers to manage custom help pages or to access help when the internet is unavailable.

   1. Double-click **x3-documentation-M.m.P.jar** in the **Documentation** folder.
   2. Enter a name for the local documentation server, as well as an available port number.  
      This port will be used for the help base URL.
   3. When prompted to select the installation packages, select **Sage X3 V12 documentation files** if you want to copy the standard help pages locally.  
      If you only want to manage custom pages on the local documentation server, do not check this option.
   4. Finish the installation process.
   5. For each endpoint from where you want to access the local documentation server, enter the help base URL (<http://server_name:documentation_server_port/>).

   ## Installing an additional SAFE X3 Process server component

   Double-click  **runtime-M.m.P.jar** in the **Runtime** folder to launch the installation.

   **Caution:**

   * **For Windows servers**, run the installer as a user with administrator rights and rights to log on as a service.
   * **For Linux servers**, run the installer as root to create the AdxAdmin service. You can then run the adxadmin service as root and use the proprietary account of the SGBD Oracle installation to configure the database component in the Console. Refer to our [console documentation](configuration-console_console.html#component-loading) (**AdxAdmin process rights**) for more information.

   To implement an additional SAFE X3 Process server component, consult our [console documentation](configuration-console_console.html#additional-x3-process-server).

   ## Installing a Java Bridge component

   1. Double-click **java-bridge-M.m.P.jar** in the **JavaBridge** folder.
   2. To implement a Java Bridge server, consult our [console documentation](configuration-console_console.html#sage-x3-java-bridge-server).

   ## Installing web services and the legacy ADC server component

   ### Installing web services and legacy ADC server component

   This component provides a web service SOAP server (for the Sage X3 HR portal) and VT connection.

   1. Make sure all system requirements (on [Windows](prerequisites_webservice-and-adc-server-on-windows.html) or on [Linux](prerequisites_webservice-and-adc-server-on-linux.html)) are met.
   2. Double-click **vt-web-server-M.m.P.jar** in the **VTWebServer** folder.
   3. Select **New installation**.
   4. Enter the installation path.
   5. Enter the server name, the path for all temporary files and logs, and the passphrase to use to encrypt the private key that will be generated at the end of the installation.  
      Make sure you write down the passphrase and keep it at hand when launching the configuration of the component.
   6. For Linux installations, set the user and group who will own the folder where the component will be located.
   7. Configure the component with the management console.

   ### Configuring the web services and the legacy ADC server using the Console

   From the Console:

   1. Define the port to use and enter the passphrase you have set during the installation.  
      Enter specific parameters, if required.
   2. Link the folders that will be used for web service or VT connection to the component, and complete the required setup.  
      The web service component public key that was generated during the installation is automatically copied in the appropriate folder of the runtime server. This is done in order to establish an operational connection between the two components.
   3. Define web service pools to enable SOAP clients to call X3 Objects and sub-programs using the SOAP protocol.  
      Configure a pool per folder.  
      **Note:** The web server uses the passphrase you configured to encrypt the private key. This allows a secure connection between the runtime and the web service server. The passphrase is also encrypted.
   4. If you connect to the management console from another user account, re-enter the passphrase.
   5. If you update an ADC server 231 web service to a newer product update, and if you have already published the solution, make sure that the public key of the ADC server web service is in the **keys** sub-directory of each runtime directory of the linked solutions.

   **Caution:** If you have installed a Sage X3 Syracuse server before installing the ADC server web service component, make sure you copy the public key of the Sage X3 Syracuse server to **\data\KEYSTORE\WEBSERVER\** for a secure connection between Sage X3 Syracuse Server and the ADC server web service for the HRM portal.

   ## Installing Sage X3 Services

   You need to install Sage X3 Services to use [Mobile Automation (ADC) for distribution](https://online-help.sageerpx3.com/erp/12/wp-static-content/whitepapers/en_US/negoce/adc/default.htm).

   Refer to the [Sage X3 Services installation procedure](getting-started_Sage-X3-Services-installation.html) for more information.

   # Installing the Sage X3 Automated Test Platform

   Refer to the following Automated Test Platform documents for more information:

   * [Automated Test Platform - User guide](https://online-help.sageerpx3.com/erp/12/wp-static-content/public/ATP%20User%20Guide/Default.htm)
   * [Automated Test Platform - Client installer](https://online-help.sageerpx3.com/erp/12/wp-static-content/public/ATP%20Client%20Installer/Default.htm)
   * [Automated Test Platform - Jenkins installation and setup](https://online-help.sageerpx3.com/erp/12/wp-static-content/public/ATP%20Jenkins%20installation%20and%20setup/Default.htm)
   * [Automated Test Platform - Third-party components](https://online-help.sageerpx3.com/erp/12/wp-static-content/public/ATP%20Third%20Party%20Components/Default.htm)
   * [Automated Test Platform - Step definitions guide](https://online-help.sageerpx3.com/erp/12/wp-static-content/public/ATP%20Step%20definitions%20Guide/Default.htm)  

   [Index](index.html)  [Home](getting-started_home.html)