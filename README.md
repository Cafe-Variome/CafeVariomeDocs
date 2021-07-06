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

## PHP binary path

Since Cafe Variome runs time-consuming tasks that go beyond the standard web request life-time, it is necessary to run such tasks in the background through the *shell_exec()* command. Therefore, the absolute path to the PHP binary needs to be configured in Constants.php that is located in app/Config/ directory. The appropriate path of php on linux systems can be found using *which php* command. Here is the sample of inserted php path within the Constant.php file.

```php
define('PHP_BIN_PATH', '/opt/php7/bin/php');

```
## Cafe Variome Net (CVNet)

CVNet is a network registry software that keeps a list of networks with corresponding installations. CVNet enables communication among Cafe Variome instances at query time. When a user creates and runs a query at one Cafe Variome instance, before processing the query, that Cafe Variome instance gets a list of participating installations in the network from CVNet, and finally sends the query to all installations in the network. Cafe Variome needs to communicate with CVNet to function properly.

## Dashboard

After logging in successfully, you will be redirected to the first page of Cafe Variome as illustrated below:

![Alt text](Archive/screenshots/1.successfull-login.png?raw=true "Successful Login")

By clicking on the Admin Dashboard, you will be redirected to main dashboard of Cafe Variome that contains the information about the system such as number of users, number of sources, current disk space status, which network you are in, related service statuses, so on and so forth. The concept of sources, networks, etc will be disccussed later in this document. After installing fresh Cafe Variome, sources, networks and other elements must be added and configured through the links on the left side under the dashboard. As shown in the below screenshot, dashboard is categorized into various sections with corresponding items in each section: Discovery (Discover), Data (Pipelines, Sources and Elastic Search), Network (Networks and Network Groups), Access Control (Users), Content (Pages) and System that contains Cafe Variome's instance settings.

![Alt text](Archive/screenshots/2.Admin-Dashboard.png?raw=true "Dashboard")

For further information regarding installing Cafe Variome, please refer to the main github page of Cafe Variome. Moreover, Elastic Search and Neo4J can be integrated with Cafe Variome to provide more capabilities to data discovery by including graph data bases by the aim of Neo4J and more speed for quering data when dealing with growing number of big documents by the aim of Elastic Search.

## Settings 

Various settings of Cafe Variome must be configured via the The System Settings under the Dashboard menu which is illustrated in the below screenshot consisting of numerous sections of Cafe Variome installation:

![Alt text](Archive/screenshots/3.Settings.png?raw=true "Settings")

- System Settings contain main system configurations such as Site Title, Authorization Server URL, Installation Key, etc.
- Authentication Settings consists of authentication elements of Cafe Variome including OpenID URL, Client ID, Client Secret, etc.
- Elastic Search Settings includes the URL for Elastic Search Service's Address.
- Neo4J Settings includes corresponding elements regarding the various settings of Neo4J Service like Address of Neo4J Server and its corresponding port, Username and Password.
- Discovery Settings is related to Access Control List (ACL) for sources. 
- Endpont Settings configure the URL addresses for HPO, ORPHA and SNOMED.

## Sources

 Sources are considered as placeholders for data files.  Thereby, a source can be created by clicking Create a Source under the Sources for data discovery. As a result, the below screenshot will be shown in which the Source Name, Owner Name, Owner Email and other related information regarding the source must be filled.

![Alt text](Archive/screenshots/4.Create-Source.png?raw=true "Source-Creation")

Following the successful creation of the source, the below screenshot will be shown on the screen in which various actions can be accomplished for the newly created sources as follows: Upload Data Files, Import Files, Edit Source, Source File Status, Data Attributes and Values and Delete Source.

![Alt text](Archive/screenshots/5.Source-Page.png?raw=true "Source-Page")

By clicking the Upload Data Files which is a green icon under the Actions, the following module will be shown to add the desired file. It must be mentioned that Cafe Variome accepts three kinds of files: Spreadsheet Files, PhenoPacket Files and VCF Files. It must be noted that the added data files only reside on the specified Cafe Variome instance and it would not be exposed to un authorized users. Thus, only count subject IDs will be shown to the others.

![Alt text](Archive/screenshots/6.Adding-Records.png?raw=true "Add-Record")

After clicking the Upload Spreadsheet Files, you will be redirected to the below page in which you are able to upload spreadsheets files such as XLS, XLSX and CSV files. There are two options available for adding the files to the source that are *append* and *overwrite*. It must be noted that the pipeline must be selected from drop down list as well which will be explained later in this document.

![Alt text](Archive/screenshots/7.Uploading-Files.png?raw=true "Upload-Files")

After adding the data files, data attributes and values can be viewed by clicking on Data Attributes and Values under action which is illustrated on the below screenshot:

![Alt text](Archive/screenshots/8.Data-Attributes-and-Values.png?raw=true "Data-Attributes")

## Networks

 Communication among multiple instances of Cafe Variome can be done through Networks. This is useful for data discovery where several Cafe Variome instances are utilized for sharing data among each other. For data discovery, information can be gathered from various data files on each Cafe Variome instance due to network design. The following diagram depicts the communication among Cafe Variome instances in the network for data discovery purpose.

![Alt text](Archive/screenshots/9.Networks.png?raw=true "Network")

The following screenshot illustrates different sections of Network in Cafe Variome. 

![Alt text](Archive/screenshots/10.NetworkSection.png?raw=true "Network-Section")

As explained above, each source must be joined to a network for data discovery. First, the network must be created by clicking Create a Network as shown here:

![Alt text](Archive/screenshots/11.CreateNetwork.png?raw=true "Create-Network")

After creating the network successfully following screenshot will be shown on your screen:

![Alt text](Archive/screenshots/12.Successful-Netwrk-Creation.png?raw=true "Create-Network-Successful")


## Network Groups

Network Groups concept aims us for data discovery where data belongs to various stakeholders in a secure manner. Thereby, you are only allowed to access the specific attributes that are defined by the data owner. By clicking *Create a Network Group*, you will be redirected to the Create Group page. In this page, following information must be filled out: Network Name, Group Name, Description and Group Type as depicted in the below screenshot:

![Alt text](Archive/screenshots/13.CreateNetworkGroups.png?raw=true "Create-Network-Groups")

Following successful creation of Network Groups the below page is shown. This page consists of two groups a newly created network group and the master one which is not deletable. It must be mentioned that network groups can not be created prior to creating networks.

![Alt text](Archive/screenshots/14.NetworkGroupsPage.png?raw=true "Network-Groups")

After successful creation of Network Groups, the user can be assigned to access to the specific source through the Network Groups concept as depicted here:

![Alt text](Archive/screenshots/15.EditUserNetworkGroups.png?raw=true "Network-Groups-Users")

## Pipeline

A pipeline plays a pivotal role in processing data files. First of all, it determines the unique value for each record or row such as Subject_ID inside the file or even for the individual files. Secondly, the various columns can be grouped together for better query performance that can be grouped individually or customly. Thus, by ordering the records within the files or the individaual files, data discovery can be accomplished quickly and accurately. By clicking the pipeline in the dashboard under the data section two options will be shown as follws: *Create a Pipeline* and *View Pipelines* as depicted in the below screenshot:

![Alt text](Archive/screenshots/16.Pipelines.png?raw=true "Pipelines")


You will be redirected to Create Data Pipeline page by clicking *Create a Pipeline*. As shown below, the followowing entries can be defined for each pipeline:

- Name: Each pipeline can be recognized by its name.
- Subject ID Location: This is the unique identifier for each record within the file by specifying the attribute name for it or file itself.
- Subject ID Attribute Name: If Attribute in File is selected for the Subject ID Location, the attribute can be filled out here as a unique identifier.
- Grouping: as discussed earlier, grouping can be used to group numerous attributes together that can be done *Group Individually* or *Custom*.
- Internal Delimeter: By describing the value here like , or /, it can be determined by Cafe Variome how to seperate each record within the an individual cell in the file. 
- HPO Attribute Name, Negated HPO Attribute Name or ORPHA Attribute Name can also be defined for each pipeline.

![Alt text](Archive/screenshots/17.CreateDataPipeline.png?raw=true "CreatePipelines")

After creating the pipeline, the pipelines can be viewed by clicking *View Pipeline* as depicted here:

![Alt text](Archive/screenshots/18.DataPipelines.png?raw=true "ViewPipelines")

For uploading the data file names in the sources, the pipeline must be selected for ordering purpose.

## Discover

This section is utilized for data discovery purpose based on the data files which were inserted in each source. It must be mentioned that Elasticsearch is the search engine for Cafe Variome queries. Thus, it must be installed and enabled for data discovery. If elastic search is run properly, it will be shown on the dashboard as a Running Service. Please consider Service Status in the below screenshot regarding the running services:

![Alt text](Archive/screenshots/19.ServiceStatus.png?raw=true "ES")

For data discovery, first you need to select the network you would like to search as shown here:

![Alt text](Archive/screenshots/20.SelectNetwork.png?raw=true "SelectNetwork")

Finally, this is Query Builder interface. Various fields can be selected in the below page from patient charectristics up to HPO and ORPHA Terms.

![Alt text](Archive/screenshots/21.Query.png?raw=true "Query")













































