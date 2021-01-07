# # mulesoft-chargeback : This repository is created as Proof of Concept to prove out the chargeback model for MuleSoft Platform 
## # Table of Contents 
###   1. Use Case for the Prototype
###   2. Download and Run Source files after importing in Anypoint Studio
###   3. Closer look at Splunk Log4 Appender configuration for MuleSoft flows to ingest data in Splunk
###   4. Splunk set up on your system 
###   5. Splunk configuration and index creation
###   6. Import MuleSoft POC Flows app cores JSON files in Splunk
###   7. Configure Splunk Dashboards for application level counts and chargeback for clients
  
  Let's get Started !!!!

### Step 1: Use Case for Prototype 
  Let's take a fictitious use where we have two clients or groups in a company, Ecommerce and Mobile apps call respective experience api in mulesoft platform to submit/get an order to/from a common backend system (eg. SAP or OMS) . Mobile App calls Mobile Order EAPI ( Experience API ) and Ecommerce App calls Ecom Order EAPI (Experience API) to submit/get or perform crud operations. Each of experience API in turn calls common Order SAPI (system API) to perform respective crud operation 

![](https://github.com/nikhilgauba/mulesoft-chargeback/blob/main/UseCase.png)


### Step 2: Source files to import in Anypoint Studio 

In our prototype app we used the mule4 correlation ID configuration to pass the correlation ID down with a prefix of the calling group (e.g, mobile or ecom). This ID is logged with the standard JSON Logger to Splunk. An OOB platform API can pull the full set of application and core configurations to compute the bills

![](https://github.com/nikhilgauba/mulesoft-chargeback/blob/main/APILayers.png)

Download all application source jar files and import in Anypoint Studio (version 7) 
- Download and Import order-sapi.jar file in Anypoint Studio 
- Download and Import ecommerce-order-eapi.jar file in Anypoint Studio
- Download and Import mobile-order-eapi.jar file in Anypoint Studio

Make sure you are able to build and run applications in your studion or local server 
- order sapi is default running on url : localhost:8081/api/orders/123
- ecommerce eapi is default running on url : localhost:8082/ecomapi/orders/123
- mobile eapi is default running on url :  localhost:8083/mobileapi/orders/123

### Step 3: Closer look at Splunk appender configuration to ingest data in Splunk

![](https://github.com/nikhilgauba/mulesoft-chargeback/blob/main/log4jappender.png)
![](https://github.com/nikhilgauba/mulesoft-chargeback/blob/main/config.png)


### Step 4: Set up Splunk on your local machine 

https://dev.splunk.com/enterprise/dev_license


### Step 5: Splunk setup and configuration 

-  Set up Http and TCP Event Collectors 
   - Open Data Inputs under settings
![](https://github.com/nikhilgauba/mulesoft-chargeback/blob/main/DataInputs.png)
   - Set up HTTP Collector
![](https://github.com/nikhilgauba/mulesoft-chargeback/blob/main/HttpCollector.png)
   - Set up TCP Collector
![](https://github.com/nikhilgauba/mulesoft-chargeback/blob/main/TCPCollector.png)

###   6. Import MuleSoft POC Flows app cores JSON files in Splunk
- Dowload and Import app_vcore.json file ( this json file contains app level app cores utilized, remaining and total for group and environment). This data can be created using cloud hub api to get cores for each app in an environment 

  - Click Settings --> Add Data
![](https://github.com/nikhilgauba/mulesoft-chargeback/blob/SettingsAddData.png)
   - Upload app_core json file 
![](https://github.com/nikhilgauba/mulesoft-chargeback/blob/main/upload.png)
   - Choose index as main while uploading file 
![](https://github.com/nikhilgauba/mulesoft-chargeback/blob/main/mainindexforupload.png)

###   7. Configure Splunk Dashboards for application level counts and chargeback for clients

- Create and Save Table View 
  - Create Table View
![](https://github.com/nikhilgauba/mulesoft-chargeback/blob/CreateTableView.png)
   - Select all Fields
![](https://github.com/nikhilgauba/mulesoft-chargeback/blob/main/TableViewFields.png)
   - Save Table View 
![](https://github.com/nikhilgauba/mulesoft-chargeback/blob/main/SaveTableView.png)
  - Save Table View as ChargeBackTableView
![](https://github.com/nikhilgauba/mulesoft-chargeback/blob/main/SaveTableViewAsChargeBackTableView.png)

- Create Dashboard and Configure
  - Create Dashboard
![](https://github.com/nikhilgauba/mulesoft-chargeback/blob/main/CreateNewDashboard.png)
   - Configure Dashboard Panel
![](https://github.com/nikhilgauba/mulesoft-chargeback/blob/main/CopyChargeBackDemoDashboardxml.png)

![](https://github.com/nikhilgauba/mulesoft-chargeback/blob/main/Dashboard.png)
![](https://github.com/nikhilgauba/mulesoft-chargeback/blob/main/Cores.png)

