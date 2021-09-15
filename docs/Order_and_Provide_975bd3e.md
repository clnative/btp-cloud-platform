<!-- loio975bd3e54cbe4e52af346740658d1a4a -->

# Order and Provide

After the initial add-on version has been built, you have to deploy and provide it as a SaaS solution so that the add-on can be consumed by customers via a subscription in the SAP BTP cockpit.

 <a name="loio975bd3e54cbe4e52af346740658d1a4a loio4e35eb027f284b7fa6219bc70561fb4e__loio4e35eb027f284b7fa6219bc70561fb4e"/>

<!-- loio4e35eb027f284b7fa6219bc70561fb4e -->

# Deploy



For the deployment and offering of the add-on as SaaS solution, you have to create a dedicated global account and implement a multitenant application. For multitenant applications based on the ABAP environment, the ABAP Solution service is used to provision ABAP systems, tenants, and users on demand. Once you’ve configured this implementation, you can deploy it to the *05 Provide* space of your provider subaccount *05 Provide*. See [Prepare a Production Account](Develop,_Test,_Build_3bf575a.md#loio4338854e3133407abb47d3a281dbd1e1__prepare_production_account).

 <a name="loio975bd3e54cbe4e52af346740658d1a4a loio4e35eb027f284b7fa6219bc70561fb4e loio1782f253e102484dac378887b3d6d769__loio1782f253e102484dac378887b3d6d769"/>

<!-- loio1782f253e102484dac378887b3d6d769 -->

# Sizing

The sizing of the SaaS application determines the scope and metric of your offering.

For multitenancy offerings, there’s no sizing/quota per customer. You must decide on an overall sizing depending on the expected load in a region. Sizing can be configured via parameters in the ABAP Solution service, that is managing systems and tenants for systems used to provide the SaaS application.

 <a name="loio975bd3e54cbe4e52af346740658d1a4a loio4e35eb027f284b7fa6219bc70561fb4e loio6cb128101a6f40f3a8f234a1d9bb8b01__loio6cb128101a6f40f3a8f234a1d9bb8b01"/>

<!-- loio6cb128101a6f40f3a8f234a1d9bb8b01 -->

# Multitenancy

As a DevOps engineer using parameter `tenant_mode` in the ABAP Solution service, you can define whether a customer gets a tenant in a dedicated system \(single\) or a shared system \(multi\).

> ### Note:  
> As of now, there is no consumer tenant threshold available to specify the number of tenants to be onboarded per system.

> ### Tip:  
> For in-depth information about multitenancy, check out [Multitenancy](Concepts_9482e7e.md#loioc8730736a52645b49ca76c08214bf181).

 <a name="loio975bd3e54cbe4e52af346740658d1a4a loio4e35eb027f284b7fa6219bc70561fb4e loiobb8bc1e3c99145c79106ecafc73f5a4f__loiobb8bc1e3c99145c79106ecafc73f5a4f"/>

<!-- loiobb8bc1e3c99145c79106ecafc73f5a4f -->

# Runtime and Persistence

Parameters `size_of_runtime` and `size_of_persistence` are used to determine the number of ABAP compute units and HANA compute units for the creation of an ABAP system.

For systems and tenants created automatically by the ABAP Solution service, the following parameters can be used to determine the sizing of runtime and persistence:


<table>
<tr>
<td>

`size_of_runtime`



</td>
<td>

Default sizing for solution



</td>
<td>

Parameter `size_of_runtime` is part of the quota plan `abap/abap_compute_unit`, with the ABAP compute unit representing the number of 16 GB blocks. The following sizes are available: 1, 2, 4, 6, 8 \(16, 32, 64, 96, 128 GB RAM\).



</td>
</tr>
<tr>
<td>

`size_of_persistence`



</td>
<td>

Default sizing for solution



</td>
<td>

Parameter `size_of_persistence` is part of the quota plan `abap/hana_compute_unit`, with the HANA compute unit representing the number of 16 GB blocks. The following sizes are available: 4, 8, 16 \(64, 128, 256 GB RAM\).



</td>
</tr>
</table>

See [Define Your ABAP Solution](Define_Your_ABAP_Solution_1697387.md).

> ### Note:  
> If the quota for a system is exceeded, you can request a resizing of the ABAP runtime or persistency depending on the needs of the SaaS application.

 <a name="loio975bd3e54cbe4e52af346740658d1a4a loio4e35eb027f284b7fa6219bc70561fb4e loiof3305f65648248318028e02c84375323__loiof3305f65648248318028e02c84375323"/>

<!-- loiof3305f65648248318028e02c84375323 -->

# SaaS Registry and ABAP Solution Provider

**Implement the ABAP Solution Provider**

As a DevOps engineer, you can implement the ASP functionality using SAP Business Application Studio in the development subaccount.

For more information on how to create multitenant-enabled applications in the ABAP environment, see [Developing Multitenant Applications in the ABAP Environment](Developing_Multitenant_Applications_in_the_ABAP_Environment_195031f.md).

1.  You start off by defining your ABAP solution, for example, the parameters explained in the previous chapter need to be configured. See [Define Your ABAP Solution](Define_Your_ABAP_Solution_1697387.md).

    > ### gCTS:  
    > When defining your ABAP solution, you can ignore the add-on product name in the service configuration. The value for `addon_product_name` has to be empty so that ABAP systems without an add-on \(abap/standard\) are provisioned for the solution.

2.  In the configuration for the XSUAA instance, you specify the functional authorization scopes for the application. See [Create an XSUAA Instance](Create_an_XSUAA_Instance_2ce1a96.md).

3.  A tenant-aware approuter application is developed that is used to authenticate business users of the application at runtime. See [Develop the Approuter Application](Develop_the_Approuter_Application_44dbd0a.md).

    Depending on the purpose of the approuter application, whether used for development or production, it needs to be configured differently. See [Configure the Approuter Application](Configure_the_Approuter_Application_3725815.md)

4.  To make a multitenant application available for subscription to SaaS consumer tenants, you have to register the application in the Cloud Foundry environment via the SaaS Provisioning service \(saas-registry\). See [Register the Multitenant Application to the SaaS Provisioning Service](Register_the_Multitenant_Application_to_the_SaaS_Provisioning_Service_2cd8913.md).

5.  Bind your approuter application to the xsuaa service instance, which acts as an OAuth 2.0 client to your application, and to the ABAP Solution service instance, which represents your ABAP solution. See [Bind the approuter Application to the xsuaa and the ABAP Solution Service Instance](Bind_the_approuter_Application_to_the_xsuaa_and_the_ABAP_Solution_Service_Instance_04b9258.md).


> ### Recommendation:  
> We recommend following the MTA-based implementation approach.

> ### Note:  
> If you need support or experience issues, please report an incident under component `BC-CP-ABA-INT`.

**Deploy ABAP Solution Provider**

After completing development, you, as a DevOps engineer, must build and deploy the resulting ABAP solution implementation.

By using MTA extension descriptors, you can configure the required values during deployment. See [Using MTA Extension Descriptors](Using_MTA_Extension_Descriptors_383f3a3.md).

> ### gCTS:  
> f you use gCTS instead of add-ons for delivering software components to production systems, the value for the add-on product name inside the MTA extension descriptor file has to be empty.

**Create ASP Cloud Controller Destination**

As an operator of the provider subaccount, you need to create a destination for the Cloud Foundry Cloud Controller access. See [Create a Destination for the Cloud Foundry Cloud Controller Access](Create_a_Destination_for_the_Cloud_Foundry_Cloud_Controller_Access_35b5acb.md). The Cloud Foundry Cloud Controller API maintains records of orgs, spaces, services, service instances, user roles, and more and is used by the ABAP Solution Provider service to create new ABAP instances in the *05 Provide* space when necessary.

> ### Recommendation:  
> We recommend using a dedicated technical Cloud Foundry platform user registered in SAP ID Service for Cloud Controller access. This can either be a non-personalized S-user created via SAP One Support Launchpad or a P-user registered directly for an SAP ID account. See [Create SAP User Accounts](Create_SAP_User_Accounts_ebe42f6.md).

 <a name="loio975bd3e54cbe4e52af346740658d1a4a loio4e35eb027f284b7fa6219bc70561fb4e loio195a685a71f84953813e7b3bd255e849__loio195a685a71f84953813e7b3bd255e849"/>

<!-- loio195a685a71f84953813e7b3bd255e849 -->

# Access to Landscape Portal

The *Landscape Portal* acts as a central tool that allows you to perform lifecycle management operations, such as provisioning new consumers tenants, users, and more. See [Landscape Portal](Landscape_Portal_5eb70fb.md).

As an operator of the provider subaccount, subscribe to the Landscape Portal application. The security administrator role is needed to assign the `LandscapePortalAdminRoleCollection` to the users in the configured default identity provider of the subaccount that you want to provide access to the *Landscape Portal* app. Note that this only applies to Feature Set A. See [Accessing the Landscape Portal](Accessing_the_Landscape_Portal_2e1e393.md).

> ### gCTS:  
> In the Landscape Portal, you can access the provider system and choose the provider tenant. Via the provider tenant, you get access to Fiori Apps, for example the *Manage Software Components* app, which is used for importing software components via gCTS. For the initial import, you have to clone the software component first and pull the maintenance branch.

 <a name="loio975bd3e54cbe4e52af346740658d1a4a loio57c19c7c4dfa4c3cbb846c1ac57e2095__loio57c19c7c4dfa4c3cbb846c1ac57e2095"/>

<!-- loio57c19c7c4dfa4c3cbb846c1ac57e2095 -->

# Commercialize



To offer your SaaS solution to customers, register the SaaS solution in the SAP App Center. See [SAP App Center](https://www.sapappcenter.com/en/partner-with-us/documentation).

Additionally, you can request an SAP Extension Suite certification for your product so that it gets listed in the SAP Certified Solutions Directory. See [SAP Extension Suite Certification](https://www.sap.com/documents/2016/10/7cf3eaec-907c-0010-82c7-eda71af511fa.html) and [SAP Certified Solutions Directory](https://www.sap.com/dmc/exp/2013_09_adpd/enEN/#/solutions).

After finishing this process, your customers can order the SaaS solution, which is the preliminary step to actual subscription.

 <a name="loio975bd3e54cbe4e52af346740658d1a4a loio57c19c7c4dfa4c3cbb846c1ac57e2095 loio607aa8614ea34ee7b366b01ad03bfc4c__loio607aa8614ea34ee7b366b01ad03bfc4c"/>

<!-- loio607aa8614ea34ee7b366b01ad03bfc4c -->

# \(Optional\) Register SaaS Solution in SAP App Center

SAP App Center is the enterprise marketplace where we bring together customers and partners on a single, easy-to-use, global online platform. See [SAP App Center](https://www.sapappcenter.com/).

To learn more about how you can offer your SaaS solution to SAP customers via the App Center, see [Getting Started with the New SAP App Center](https://www.sapappcenter.com/en/partner-with-us/documentation).

 <a name="loio975bd3e54cbe4e52af346740658d1a4a loio57c19c7c4dfa4c3cbb846c1ac57e2095 loioace3b22147eb40d3989c5525491eb729__loioace3b22147eb40d3989c5525491eb729"/>

<!-- loioace3b22147eb40d3989c5525491eb729 -->

# \(Optional\) Certification

With an SAP Extension Suite certification, your SaaS solution is featured in the SAP Certified Solution Directory, which allows for more growth and customer participation. See [SAP ICC Integration Scenario - SAP Extension Suite Certification](https://www.sap.com/documents/2016/10/7cf3eaec-907c-0010-82c7-eda71af511fa.html) and [SAP Certified Solution Directory](https://www.sap.com/dmc/exp/2013_09_adpd/enEN/#/solutions).

 <a name="loio975bd3e54cbe4e52af346740658d1a4a loioa24217a0d6fa434bbce97869dfb70dda__loioa24217a0d6fa434bbce97869dfb70dda"/>

<!-- loioa24217a0d6fa434bbce97869dfb70dda -->

# Order and Provide



Once the SaaS solution has been fully deployed and commercialized, customers can order the offered product. After the buying process has been completed, you, as a SaaS solution operator, have to create a consumer subaccount in the global production account and subscribe to the SaaS solution. This in turn triggers the provisioning of the required ABAP systems and tenants for the customer. You can follow this process using the *Landscape Portal* service, which gives you an overview of the available ABAP systems and tenants belonging to a SaaS solution.

When tenant or system provisioning has been completed, you, as a SaaS solution operator, receive a confirmation mail.



### Customer Buys SaaS Solution

Depending on the marketplace platform \(for example SAP App Center\) or other distribution channels, customers can buy the SaaS solution.

-   Customer name and email address for the creation of a consumer subaccount admin userFor the following process of creating a consumer subaccount for your customer, you should have the following information readily available:
-   Name and scope of the SaaS solution for the subscription to the SaaS solution
-   Quantity of users, t-shirt size of solution etc. to determine necessary configuration steps

 <a name="loio975bd3e54cbe4e52af346740658d1a4a loioa24217a0d6fa434bbce97869dfb70dda loio8b92024cc5d44268bf4737551e4fa981__loio8b92024cc5d44268bf4737551e4fa981"/>

<!-- loio8b92024cc5d44268bf4737551e4fa981 -->

# Create Consumer Subaccount

**Consumer account structure**

For the following process of creating a consumer subaccount for your customer, you have to create consumer subaccounts in the global production account so that customers can subscribe to the provided SaaS solution.

This means, on top of subaccount*04 Build/Test* and *05 Provide*, you have to create a subaccount in the production global account for each consumer. See [Set Up a Production Account](Develop,_Test,_Build_3bf575a.md#loio2e7b4b631e814de1b8fe3959af4105bc).

After a customer has ordered the SaaS solution, you, as an operator of the global production account, need to create a *06 Consume* subaccount. See [Subscribe New Consumers](Subscribe_New_Consumers_b90cde1.md).

While creating the subaccount, you must provide the following details:

-   **Name**: Give the subaccount a unique display name. This can be the name of the customer, a customer number or a specific naming pattern
-   **Provider**: Choose the IaaS provider according to the IaaS provider selected for the provider subaccount
-   **Region**: Choose the subaccount region according to the region where the provider subaccount was created. See [Regions and API Endpoints for the ABAP Environment](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/350356d1dc314d3199dca15bd2ab9b0e.html#loio879f37370d9b45e99a16538e0f37ff2c).
-   **Subdomain**: The subdomain of the subaccount becomes part of the application URL, according to the `TENANT_HOST_PATTERN` that you defined in the approuter configuration for the multitenant application. See [Configure the Approuter Application](Configure_the_Approuter_Application_3725815.md).

 <a name="loio975bd3e54cbe4e52af346740658d1a4a loioa24217a0d6fa434bbce97869dfb70dda loio477ea31394504182b2ea5ef9ce26802d__loio477ea31394504182b2ea5ef9ce26802d"/>

<!-- loio477ea31394504182b2ea5ef9ce26802d -->

# Subscribe to SaaS Solution

After you have finalized the consumer subaccount configuration as an operator user on the provider side, the subscription to the SaaS solution is enabled for the consumer.

**Subscribe to SaaS solution in consumer subaccount**

To provide a consumer tenant to the customer, you, as an operator user, need to trigger the subscription process in the subaccount. Go to *Subscriptions* \> *SaaS Application* and choose *Subscribe*.

**Check tenant provisioning in Landscape Portal**

The subscription process triggers provisioning of

-   A new ABAP system, if necessary according to ABAP solution configuration \(single/multi-tenancy\)

-   A new consumer tenant that is represented by an additional client in the ABAP system


In both cases, you, as a SaaS solution operator, receive a confirmation mail.

As an operator user assigned to the role collection `LandscapePortalAdminRoleCollection`, you can access the systems overview of the *Landscape Portal* and check both provisioned systems and new tenants.

See [Landscape Portal](Landscape_Portal_5eb70fb.md).

**Assign `SolutionAdmin` role**

Once the SaaS subscription process is completed, as an operator user in the trust settings of the *06 Consume* subaccount, assign the user onboarding role `SolutionAdmin` provided by the multitenant application to a customer user.

 <a name="loio975bd3e54cbe4e52af346740658d1a4a loioa24217a0d6fa434bbce97869dfb70dda loio3c44b19161d742a5a96576d64e70d505__loio3c44b19161d742a5a96576d64e70d505"/>

<!-- loio3c44b19161d742a5a96576d64e70d505 -->

# Configure Consumer Subaccount \(Feature Set A\)

Depending on the scope of the SaaS solution and consumer requirements, you, as an operator, have to configure the following:

-   Trust configuration for integration of corporate identity provider

    If you want to integrate an existing corporate identity provider for authentication/authorization in the consumer subaccount, please refer to [Trust and Federation with Identity Providers](Trust_and_Federation_with_Identity_Providers_cb1bc8f.md). To restrict access based on certain criteria, such as the IP address,. you need to use the Identity Authentication service. See [Identity Authentication Service](https://help.sap.com/viewer/6d6d63354d1242d185ab4830fc04feb1/Cloud/en-US/d17a116432d24470930ebea41977a888.html).

-   Destinations and connectivity whenever the SaaS solution requires to connect to a destination \(cloud or on-premise\) that is configured by the consumer. See [Connectivity in the Cloud Foundry Environment](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/34010ace6ac84574a4ad02f5055d3597.html).


**Option A: Provider configures consumer subaccount**

As an operator user of the provider, you configure the consumer subaccount *06 Consume* for the customer. The customer only needs to provide the following:

-   Configuration details regarding the identity provider that is supposed to be used by providing the relevant SAML metadata file. See [Exporting SAML Identity Provider Metadata](Exporting_SAML_Identity_Provider_Metadata_5c1479e.md).

-   Configuration details regarding Cloud Connector connectivity: to configure the Cloud Connector, you, as the provider, need to enable a technical user of the customer as a security administrator of the consumer subaccount. See [Security Administration: Managing Authentication and Authorization](Security_Administration_Managing_Authentication_and_Authorization_1ff47b2.md). This can either be a nonpersonalized S-user created by the customer in SAP One Support Launchpad or a P-user directly registered in SAP ID service.

    Subsequently, the customer configures the subaccount in the Cloud Connector by authenticating with the provided technical user.

-   Configuration details regarding destinations: The destination credentials might be exchanged in file format.

    > ### Note:  
    > Destination credentials need to be provided in clear text to the provider, which might be a security risk. In that case, option B might be more suitable.


On the provider side, you, as a SaaS solution operator, must take care of the following:

-   Set up the trust configuration according to customer configuration details. See [Establishing Trust to the SAML Identity Provider for the Cloud Foundry Account](Establishing_Trust_to_the_SAML_Identity_Provider_for_the_Cloud_Foundry_Account_55e7d92.md).

-   Add a technical user of the customer as a security administrator of the consumer subaccount

-   Configure destinations according to the credentials provided by the customer


**Option B: Consumer configures consumer subaccount**

The consumer configures the consumer subaccount after you, as an operator user on the provider side, grant access by doing the following:

-   In the consumer subaccount, enable the Cloud Foundry organization so that organization members can be added to that subaccount

-   As an operator, add the customer user as a member of the enabled Cloud Foundry organization such that the consumer subaccount *06 Consume* is visible to the customer user even without global account member privileges. No role needs to be assigned to the organization member.

-   To configure trust configuration and connectivity/destination settings in the subaccounts, add the customer user as a security administrator. See [Security Administration: Managing Authentication and Authorization](Security_Administration_Managing_Authentication_and_Authorization_1ff47b2.md).


Once you, as an operator, have provided the relevant subaccount information, the customer user can then log on to the SAP BTP cockpit as the consumer subaccount admin and configure trust settings and connectivity/destination settings in the subaccount.

 <a name="loio975bd3e54cbe4e52af346740658d1a4a loioa24217a0d6fa434bbce97869dfb70dda loio4a9c5011922847ac91db165c78656149__loio4a9c5011922847ac91db165c78656149"/>

<!-- loio4a9c5011922847ac91db165c78656149 -->

# Initial User Onboarding

After trust/connectivity configuration in the consumer subaccount, your customer needs an initial administrator user in the consumer tenant that was created for the subscription.

To create such an initial administrator user, you, as a consumer subaccount administrator assigned to the `SolutionAdmin` role collection need to onboard an initial user during the initial logon to the SaaS solution.

In a confirmation form, you have to confirm details such as email, subdomain, and subaccount ID. Afterwards, the customer user must wait until the tenant user provisioning is completed.

> ### Note:  
> Depending on the approuter configuration, you, as the operator, might need to add a new tenant-specific route pointing to the approuter application. See [Configure the Approuter Application](Configure_the_Approuter_Application_3725815.md) and [Create Routes](Create_Routes_9fddeea.md).

**Check tenant user provisioning in Landscape Portal**

On the provider side, as an operator user assigned to the `LandscapePortalAdminRoleCollection`, you can check ongoing tenant user provisioning in the *Landscape Portal*. After selecting the target system in the system overview app, ongoing tenant user provisioning is displayed in the *Requests* section. See [View the Request Log](View_the_Request_Log_0ea69c2.md).

After you have set up the consumer subaccount, tenant, and tenant user, a remaining customer implementation project can start.
