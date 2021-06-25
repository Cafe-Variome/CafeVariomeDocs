# CafeVariomeDocs

This repository contains software documentation for [Cafe Variome](https://github.com/CafeVariomeUoL/CafeVariomeCI4). 

These documents mainly include technical documentation and UML diagrams and explain the various sections of cafevariome based on existence functionalities. Current installation of Cafe Variome can be done both manually via command line or automatically via ansible which is idempotent and less error prone. For more information regarding the installation please refer to the main github page of cafevariome as stated above. As mentioned earlier, this document explains the functionalities of Cafe Variome to help Cafe Variome users to be familiarized from the begining like authentication up to the end such as uploading thier data and creating queries based on the data for data discovery purpose. Thereby, the authentication is the 1st phase that needs to be explained as follows. The rest of functionalities will be explained accordingly.

## Authentication

After installing the Cafe Variome, the authentication must be accomplished in order to access to the dashboard. However, the authentication can be done locally or through keycloak which is an open source Red Hat software product to allow single sign-on with Identity and Access Management aimed at modern applications and services. Keycloak can be integrated with ELIXIR AAI to federate identities from ELIXIR to access resources that are provided by Cafe Variome for data discovery. For distinguishing between various authentication modes, the AuthAdapter.php is used as follows:

```php
class AuthAdapter extends \CodeIgniter\Config\BaseConfig
{

    /**
     * Valid values:
     *  1. KeyCloakFirst : If keycloak URI is configured properly and an endpoint exists,
     *  Keycloak is used as authentication engine. Otherwise, IonAuth is used.
     *  2. KeyCloakOnly
     *  3. IonAuthOnly
     *  4. OAuth
     */
    public $authRoutine = 'IonAuthOnly';
}

```
$authRoutine is the variable for determining the modes of authentication. KeycloakFirst that represents the authentication through keycloak first and IonAuthOnly that authenticates users locally are the most popular modes among the above authentication modes. As noted above, if the keycloak first is utilized as an authentication mode, the keycloak first is used for authentication and in the case of keycloak failure local authentication will be used. It must be noted that the users must be available in the local database of Cafe Variome. Keycloak is able to register a new user and even enforce adding the record for the new user in the local database. As a result, the registed user can be added to the local database of Cafe Variome which means authentication from federated identities. The next section will discuss the dashboard of Cafe Variome.

## Dashboard

After logging in successfully, you will be redirected to the first page of Cafe Variome as illustrated below:

![Alt text](Archive/screenshots/1.successfull-login.png?raw=true "Successful Login")

By clicking on the Admin Dashboard, you will be redirected to main dashboard of Cafe Variome that contains the information about the system such as number of users, number of sources, current disk space status, which network you are in, related service statuses, so on and so forth. The concept of sources, networks, etc will be disccussed later in this document. After installing fresh Cafe Variome, sources, networks and other elements must be added which must be configured through the links on the left side under the dashboard. As shown in the below screenshot, dashboard is categorized into various sections with corresponding items in each section: Discovery (Discover), Data (Pipelines, Sources and Elastic Search), Network (Networks and Network Groups), Access Control (Users), Content (Pages) and System that contains Cafe Variome's instance settings.

![Alt text](Archive/screenshots/2.Admin-Dashboard.png?raw=true "Dashboard")

Before delving into details of uploading data for Data Discovery purpose, it must be noted that the CVNet is a network registry that keeps list of networks with corresponding installations. CVNet is a significant application that enables communications between Cafe Variome instances throught the unique identifier for each Cafe Variome (Installation Key). Thereby, CVnet is a tool for data discovery purpose between Cafe Variomes which enable us to perform queries from different Cafe Variomes that would be shown as an aggregated result on the query page. For further information regarding installing Cafe Variome, please refer to the main github page of Cafe Variome. Moreover, Elastic Search and Neo4J can be integrated with Cafe Variome to provide more capabilities to data discovery by including graph data bases by the aim of Neo4J and more speed for quering data when dealing with growing number of big documents by the aim of Elastic Search.  The System Setting under the settings must be clicked as depicted in the below screenshot consists of various sections of Cafe Variome installation:

![Alt text](Archive/screenshots/3.Settings.png?raw=true "Settings")

- System Settings contain main system configurations such as Site Title, Authorization Server URL, Installation Key, etc.
- Authentication Settings consists of authentication elements of Cafe Variome including OpenID URL, Client ID, Client Secret, etc.
- Elastic Search Settings includes the URL for Elastic Search Service's Address.
- Neo4J Settings includes corresponding elements regarding the various settings of Neo4J Service like Address of Neo4J Server and its corresponding port, Username and Password.
- Discovery Settings is related to Access Control List (ACL) for sources. 
- Endpont Settings configure the URL addresses for HPO, ORPHA and SNOMED.

## Sources

After explaining the various settings of Cafe Variome, it is time to explain about adding sources to the Cafe Variome. Sources are the containers which must be added as containers for data files. Each source may contain numerous data files. Therefore, the inserted data files that are inserted in the sources will be queried for data discovery purpose. In this stage, Create a Source under the sources must be clicked in the left hand side of the dash board. As a result, the below screenshot will be shown on the dashboard in which the Source Name, Owner Name, Owner Email and other related information regarding the source must be filled.

![Alt text](Archive/screenshots/4.Create-Source.png?raw=true "Source-Creation")

Following the successful creation of the source, the below screenshot will be illustrated on the screen in which various actions can be accomplished to the newly created sourcs as follows: Upload Data Files, Import Files, Edit Source, Source File Status, Data Attributes and Values and Delete Source.

![Alt text](Archive/screenshots/5.Source-Page.png?raw=true "Source-Page")

By clicking the Upload Data Files which is a green icon under the Actions, the following page will be shown to add the desired file. It must be mentioned that Cafe Variome accepts three kinds of files: Spreadsheet Files, PhenoPacket Files and VCF Files.

![Alt text](Archive/screenshots/6.Adding-Records.png?raw=true "Add-Record")

After clicking the Upload Spreadsheet Files, you will be redirected to the below page in which you are able to upload spreadsheets files such as XLS, XLSX and CSV files. There are two options available for adding the files to the source that are append and overwrite. It must be noted that the pipeline must be selected from drop down list as well which will be explained later in this document.

![Alt text](Archive/screenshots/7.Uploading-Files.png?raw=true "Upload-Files")

It must be noted appropriate installation path of php must be inserted in Constant.php that is located in app/Config directory. The appropriate path of php on linux systems can be found with *which php* command. Here is the sample of inserted php path within the Constant.php file.

```php
define('PHP_BIN_PATH', '/opt/php7/bin/php');

```

After adding the data files, data attributes and values can be viewed by clicking on Data Attributes and Values under action which is illustrated on the below screenshot:

![Alt text](Archive/screenshots/8.Data-Attributes-and-Values.png?raw=true "Data-Attributes")


















