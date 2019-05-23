# Anypoint Template: MS Dynamics AX API	

<!-- Header (start) -->

<!-- Header (end) -->


# Use Case
<!-- Use Case (start) -->
As a Mule developer I want to expose the underlying Microsoft Dynamics AX system to external systems.

This Template should serve as a foundation for exposing  MS Dynamics AX to the external systems. Everytime the HTTP endpoint is triggered, the integration will run different kind of operations on the DAX database and return the response.

Requirements have been set not only to be used as examples, but also to establish a starting point to adapt your integration to your requirements.


<!-- Use Case (end) -->





# Microsoft Dynamics AX Considerations

To deploy this app on the cloudhub or on-prem and accessing the Microsoft Dynamics AX instance, you will need to install Anypoint Gateway services on DAX host machine.

To install this gateway service, please refer the following link:
https://docs.mulesoft.com/connectors/windows/windows-gw-services-guide

The Windows Gateway Services agent performs protocol translation when calling the Dynamics AX System Services. The Dynamics AX System Services (Metadata Service, Query Service) use the net.tcp protocol which is not implemented in Java. To execute requests, the connector routes the requests through the Windows Gateway Services as described below.

 - The connector sends an HTTP request to the Windows Gateway Services.

 - The Windows Gateway Services receives the HTTP request.

 - The Windows Gateway Services executes the request against the Dynamics AX System Services using the netTcp protocol.

 - The Windows Gateway Services receives the response from the Dynamics AX System Services.

 - The Windows Gateway Services sends the response to the connector over HTTP.

 - The connector receives the response.

All communication between the Anypoint Platform and Windows Gateway Services is authenticated and secured by SSL.


# Run it!
Simple steps to get this template running.
<!-- Run it (start) -->

<!-- Run it (end) -->

## Running On Premises
In this section we help you run this template on your computer.
<!-- Running on premise (start) -->

<!-- Running on premise (end) -->

### Where to Download Anypoint Studio and the Mule Runtime
If you are new to Mule, download this software:

+ [Download Anypoint Studio](https://www.mulesoft.com/platform/studio)
+ [Download Mule runtime](https://www.mulesoft.com/lp/dl/mule-esb-enterprise)

**Note:** Anypoint Studio requires JDK 8.
<!-- Where to download (start) -->

<!-- Where to download (end) -->

### Importing a Template into Studio
In Studio, click the Exchange X icon in the upper left of the taskbar, log in with your Anypoint Platform credentials, search for the template, and click Open.
<!-- Importing into Studio (start) -->

<!-- Importing into Studio (end) -->

### Running on Studio
After you import your template into Anypoint Studio, follow these steps to run it:

+ Locate the properties file `mule.dev.properties`, in src/main/resources.
+ Complete all the properties required as per the examples in the "Properties to Configure" section.
+ Right click the template project folder.
+ Hover your mouse over `Run as`.
+ Click `Mule Application (configure)`.
+ Inside the dialog, select Environment and set the variable `mule.env` to the value `dev`.
+ Click `Run`.
<!-- Running on Studio (start) -->

<!-- Running on Studio (end) -->



## Running on CloudHub
When creating your application in CloudHub, go to Runtime Manager > Manage Application > Properties to set the environment variables listed in "Properties to Configure" as well as the mule.env value.
<!-- Running on Cloudhub (start) -->

<!-- Running on Cloudhub (end) -->




# Customize It!
This brief guide provides a high level understanding of how this template is built and how you can change it according to your needs. As Mule applications are based on XML files, this page describes the XML files used with this template. More files are available such as test classes and Mule application files, but to keep it simple, we focus on these XML files:

* config.xml
* documentService.xml
* queryTable.xml
* staticQuery.xml
* endpoints.xml
* errors.xml<!-- Customize it (start) -->

<!-- Customize it (end) -->

## config.xml
<!-- Default Config XML (start) -->
This file provides the configuration for connectors and configuration properties. Only change this file to make core changes to the connector processing logic. Otherwise, all parameters that can be modified should instead be in a properties file, which is the recommended place to make changes.<!-- Default Config XML (end) -->

<!-- Config XML (start) -->

<!-- Config XML (end) -->

## documentService.xml
<!-- Default Business Logic XML (start) -->
This file provides the api implentation for accessing a document service on the DAX instance
<!-- Default Business Logic XML (end) -->

## querytable.xml
<!-- Default Business Logic XML (start) -->
This file provides the api implentation for running a query on AOT table on the DAX instance
<!-- Default Business Logic XML (end) -->

## staticQuery.xml
<!-- Default Business Logic XML (start) -->
This file provides the api implentation for running a query on DAX instance
<!-- Default Business Logic XML (end) -->

<!-- Business Logic XML (start) -->

<!-- Business Logic XML (end) -->

## endpoints.xml
<!-- Default Endpoints XML (start) -->
This file is conformed by a Flow containing the HTTP endpoint that triggers different kind of DAX operations.<!-- Default Endpoints XML (end) -->

<!-- Endpoints XML (start) -->

<!-- Endpoints XML (end) -->

## errors.xml
<!-- Default Error Handling XML (start) -->
This file handles how your integration reacts depending on the different exceptions. This file provides error handling that is referenced by the main flow in the business logic.<!-- Default Error Handling XML (end) -->

<!-- Error Handling XML (start) -->

<!-- Error Handling XML (end) -->

<!-- Extras (start) -->

<!-- Extras (end) -->
