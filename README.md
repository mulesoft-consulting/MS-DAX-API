
# Anypoint Template: MS Dynamics CRM to Salesforce Contact Migration	

<!-- Header (start) -->

<!-- Header (end) -->

# License Agreement
This template is subject to the conditions of the <a href="https://s3.amazonaws.com/templates-examples/AnypointTemplateLicense.pdf">MuleSoft License Agreement</a>. Review the terms of the license before downloading and using this template. You can use this template for free with the Mule Enterprise Edition, CloudHub, or as a trial in Anypoint Studio. 
# Use Case
<!-- Use Case (start) -->
As a Salesforce admin I want to synchronize Contacts between MS Dynamics CRM and Salesforce in a one-time manner.

This Template should serve as a foundation for setting an online migration of Contacts from MS Dynamics CRM to a Salesforce instance. Everytime the HTTP endpoint is triggered, the integration will migrate all contacts from the MS Dynamics CRM instance in manner of one-time integration and it will be responsible for updating or inserting the Contacts on the target Salesforce instance.

Requirements have been set not only to be used as examples, but also to establish a starting point to adapt your integration to your requirements.

As implemented, this Template leverages the [Batch Module](http://www.mulesoft.org/documentation/display/current/Batch+Processing).
The batch job is divided in *Process* and *On Complete* stages.

The integration is triggered by a HTTP endpoint defined in the flow that is going to trigger the application, querying the MS Dynamics contacts matching a filter criteria and executing the batch job.
During the *Process* stage, each MS Dynamics Contact will be filtered depending on if it has an existing matching Contact in the Salesforce instance.
The last step of the *Process* stage will group the Contacts and insert/update them in Salesforce.
Finally during the *On Complete* stage, the Template will log output statistics data into the console and send an email with the results.
<!-- Use Case (end) -->

# Considerations
<!-- Default Considerations (start) -->

<!-- Default Considerations (end) -->

<!-- Considerations (start) -->
To make this Anypoint Template run, there are certain preconditions that must be considered. All of them deal with the preparations in both source (MS Dynamics) and destination (Salesforce) systems, that must be made in order for all to run smoothly. 
**Failing to do so could lead to unexpected behavior of the template.**

This particular Anypoint Template illustrate the migration use case between MS Dynamics and Salesforce, thus it requires both instances to work.
<!-- Considerations (end) -->



## Salesforce Considerations

Here's what you need to know about Salesforce to get this template to work:

- Where can I check that the field configuration for my Salesforce instance is the right one? See: <a href="https://help.salesforce.com/HTViewHelpDoc?id=checking_field_accessibility_for_a_particular_field.htm&language=en_US">Salesforce: Checking Field Accessibility for a Particular Field</a>.
- Can I modify the Field Access Settings? How? See: <a href="https://help.salesforce.com/HTViewHelpDoc?id=modifying_field_access_settings.htm&language=en_US">Salesforce: Modifying Field Access Settings</a>.


### As a Data Destination

There are no considerations with using Salesforce as a data destination.





## Microsoft Dynamics CRM Considerations

### As a Data Source

You need to install Java Cryptography Extensions to be able to connect to MS Dynamics. Please [choose](http://www.oracle.com/technetwork/java/javase/downloads/index.html) a relevant version according to your Java installation.




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

### Running on Mule Standalone
Update the properties in one of the property files, for example in mule.prod.properties, and run your app with a corresponding environment variable. In this example, use `mule.env=prod`. 


## Running on CloudHub
When creating your application in CloudHub, go to Runtime Manager > Manage Application > Properties to set the environment variables listed in "Properties to Configure" as well as the mule.env value.
<!-- Running on Cloudhub (start) -->

<!-- Running on Cloudhub (end) -->

### Deploying a Template in CloudHub
In Studio, right click your project name in Package Explorer and select Anypoint Platform > Deploy on CloudHub.
<!-- Deploying on Cloudhub (start) -->

<!-- Deploying on Cloudhub (end) -->

## Properties to Configure
To use this template, configure properties such as credentials, configurations, etc.) in the properties file or in CloudHub from Runtime Manager > Manage Application > Properties. The sections that follow list example values.
### Application Configuration
<!-- Application Configuration (start) -->
**Application Configuration**
+ page.size `200`
+ http.port `8081`

**Salesforce Connector configuration**

+ sfdc.username `joan.baez@orgb`
+ sfdc.password `JoanBaez456`
+ sfdc.securityToken `ces56arl7apQs56XTddf34X`

**MS Dynamics Connector configuration**

+ msdyn.retries `3`
+ msdyn.username `username@company_name.onmicrosoft.com`
+ msdyn.password `password`
+ msdyn.url `https://company_name.api.crm4.dynamics.com/XRMServices/2011/Organization.svc`

**SMTP Services configuration**

+ smtp.host `smtp.gmail.com`
+ smtp.port `587`
+ smtp.user `johndoe%40gmail.com`
+ smtp.password `password`

**E-mail Details**

+ mail.from `batch.migratecontacts.migration%40mulesoft.com`
+ mail.to `user@example.com`
+ mail.subject `Batch Job Finished Report`

**Syncing policy for accounts**

+ account.sync.policy=syncAccount

**Note:** the property **account.sync.policy** can take any of the two following values:

+ **doNotCreateAccount**: The application will migrate the contacts over without assigning any account to them.
+ **syncAccount**: The application will migrate the contacts over and try to assign them their respective account in Salesforce, matching accounts by name. If no account is found for a specific contact, the application will create an account in Salesforce with the same name and assign it to the contact.
<!-- Application Configuration (end) -->

# API Calls
<!-- API Calls (start) -->
Salesforce imposes limits on the number of API Calls that can be made. Therefore calculating this amount may be an important factor to consider. Contact Migration Template calls to the API can be calculated using the formula:

***1 + X + X / ${page.size}*** 

Being ***X*** the number of Contacts to be synchronized on each run. 

The division by ***${page.size}*** is because, by default, Contacts are gathered in groups of ${page.size} for each Upsert API Call in the commit step. 

For instance if 10 records are fetched from origin instance, then 12 api calls will be made (1 + 10 + 1).

**Note:** if the property **account.sync.policy** is set as "syncAccount", the number of API calls will be increased because of the needed query for the specific account, before upserting the contact in the destination system.
<!-- API Calls (end) -->

# Customize It!
This brief guide provides a high level understanding of how this template is built and how you can change it according to your needs. As Mule applications are based on XML files, this page describes the XML files used with this template. More files are available such as test classes and Mule application files, but to keep it simple, we focus on these XML files:

* config.xml
* businessLogic.xml
* endpoints.xml
* errorHandling.xml<!-- Customize it (start) -->

<!-- Customize it (end) -->

## config.xml
<!-- Default Config XML (start) -->
This file provides the configuration for connectors and configuration properties. Only change this file to make core changes to the connector processing logic. Otherwise, all parameters that can be modified should instead be in a properties file, which is the recommended place to make changes.<!-- Default Config XML (end) -->

<!-- Config XML (start) -->

<!-- Config XML (end) -->

## businessLogic.xml
<!-- Default Business Logic XML (start) -->
Functional aspect of the Template is implemented on this XML, directed by one flow that will check for Salesforce creations/updates. The several message processors constitute three high-level actions that fully implement the logic of this Template:

1. The Template goes to the MS Dynamics and query all existing Contacts that match the filter criteria.
2. During the *Process* stage, each MS Dynamics Contact will be matched by name against Salesforce, in order to decide whether to create or update the contact.
3. The following Batch step will match the Accounts for each contact in the destination system if the syncAccount policy is set. The final batch step will upsert the contacts in Salesforce by gathering them in batches.

Finally during the *On Complete stage* the Template will log output statistics data into the console.<!-- Default Business Logic XML (end) -->

<!-- Business Logic XML (start) -->

<!-- Business Logic XML (end) -->

## endpoints.xml
<!-- Default Endpoints XML (start) -->
This file is conformed by a Flow containing the HTTP endpoint that triggers the migration by executing the batch job process, and a Mule component that returns the batch job response to the endpoint.<!-- Default Endpoints XML (end) -->

<!-- Endpoints XML (start) -->

<!-- Endpoints XML (end) -->

## errorHandling.xml
<!-- Default Error Handling XML (start) -->
This file handles how your integration reacts depending on the different exceptions. This file provides error handling that is referenced by the main flow in the business logic.<!-- Default Error Handling XML (end) -->

<!-- Error Handling XML (start) -->

<!-- Error Handling XML (end) -->

<!-- Extras (start) -->

<!-- Extras (end) -->
