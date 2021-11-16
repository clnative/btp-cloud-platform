<!-- loioe956ba209f30447cb55140e38c15e345 -->

# Register an SAP SuccessFactors System in a Global Account in SAP BTP

To connect an SAP SuccessFactors system with a global account in SAP BTP, you need to register the system in the corresponding global account.



<a name="loioe956ba209f30447cb55140e38c15e345__prereq_jpy_ttz_w3b"/>

## Prerequisites

-   See [Registering an SAP System](Registering_an_SAP_System_2ffdaff.md).

-   You are an administrator of the global account where you want to register your SAP SuccessFactors system.

-   You have a dedicated SAP SuccessFactors company instance.

-   SAP SuccessFactors, First Half 2021 Release, you need a user with permissions to access SAP SuccessFactors Provisioning to configure the integration on the SAP SuccessFactors system side.

-   For SAP SuccessFactors, Second Half 2021 Release or later, you need a user with permissions to access *Extension Center* in SAP SuccessFactors Admin Center that include:

    -   *Configure Object Definitions* and *Admin Access to MDF OData API* permissions from the *Metadata Framework* category

    -   *Create Integration with SAP BTP* permission from the *Manage Extensions on SAP BTP* category


    See:

    -   [Permission to Access Admin Center](https://help.sap.com/viewer/6c9f794920b947648737d914a669f195/latest/en-US/83c5a81ecd51478db1dcc23835f80339.html)

    -   [Role-Based Permissions for Extension Center](https://help.sap.com/viewer/d4a86924740742048029a71b1d674130/latest/en-US/9c61e2ba02a145069fd1f7d8bcfc4455.html)





## Context

The registration process is based on an integration token that is used for the pairing of the SAP SuccessFactors company and the corresponding SAP BTP global account. You create the token in the global account, and then start the automated registration process on the SAP SuccessFactors company side using this token.

The registration process has the following states displayed in the SAP BTP cockpit:

-   *Pending* - the integration token for an SAP system has been created but the registration on the respective SAP system side has not been performed or completed.

-   *Registered* - the integration token has been used and the automated registration process has been successfully completed.
-   *Error* - the registration has failed.



<a name="loioe956ba209f30447cb55140e38c15e345__steps_xls_dvz_w3b"/>

## Procedure

1.  In the SAP BTP cockpit, navigate to your global account, and then choose *System Landscape* \> *Systems*.

2.  In the *Systems* panel, choose *Register System*.

3.  In the *Register System* dialog box:

    1.  Enter a name for the system you want to register.

        > ### Note:  
        > Use only printable ASCII characters.

    2.  In the *Type* dropdown list, select *SAP SuccessFactors*.

    3.  Choose *Register*.


    The cloud platform generates an integration token that is used for triggering the automated integration on the SAP SuccessFactors company side.

    > ### Note:  
    > To use the token:
    > 
    > -   For SAP SuccessFactors, Second Half 2021 Release or later, you need a user with access to Extension Center.
    > 
    > -   For SAP SuccessFactors, First Half 2021 Release, you need a user with access to SAP SuccessFactors Provisioning.

4.  Copy the integration token. The token is required for configuring the integration on the SAP SuccessFactors company side.

    You can also copy the integration token later, once the system appears in the list of registered systems.

    The integration token is valid for 7 days after it has been generated. When a token is not used within its validity period, it is no longer valid and cannot be used for registering an SAP SuccessFactors system. If the validity of the token expires before you use it to configure the integration on the SAP SuccessFactors system side and complete the registration, you need to create a new token. You can then copy it and use it to complete the registration.

    > ### Note:  
    > An integration token can be used only once, for registering a single SAP SuccessFactors system.

5.  Close the dialog box.

    The SAP SuccessFactors system appears in the list of registered systems. Its status is *Pending* because the registration process is not yet completed.

6.  \(Optional\) For systems in status *Pending*, you can view and copy the integration token. To do so, choose the ![](images/ViewIntegrationToken_b8ec588.png) \(Display token\) button.

7.  Start the automated integration process on the SAP SuccessFactors company side:

    -   SAP SuccessFactors, Second Half 2021 Release or later, proceed as follows:
        1.  In SAP SuccessFactors *Admin Center*, navigate to *Extension Center*.

            If you do not have permissions to access the Extension Center for the corresponding SAP SuccessFactors system, you need to send the integration token to a user with such permissions who will configure the integration on the SAP SuccessFactors system side.

        2.  On the *Extensions on SAP BTP* tab page, navigate to the *Add Integration with SAP BTP* screen area, and paste the integration token in the *Integration Token* input field.

        3.  Choose *Add*.

            The system appears in the integration list in the *Multi-Cloud Environment* screen area, and the status of the integration is displayed in the *Integration Status* column. To refresh the status of the process, choose the *Check Status* icon. Wait for the integration to finish.


    -   SAP SuccessFactors, First Half 2021 Release, proceed as follows:
        1.  Open SAP SuccessFactors Provisioning.

            If you do not have permissions to access SAP SuccessFactors Provisioning for the corresponding SAP SuccessFactors system, you need to send the integration token to a user with such permissions who will configure the integration on the SAP SuccessFactors system side.

        2.  In the *List of Companies*, choose your SAP SuccessFactors company.

        3.  In the *Edit Company Settings* section, choose *Extension Management Configuration*.

        4.  In the *Integration Token* input field, paste the integration token.

        5.  Choose *Add*.

            Wait for the integration to finish. You can check the status of the process with the *Check Status* button next to your system name.



8.  In the cockpit, check the status of the registration process. To do so, navigate to your global account, and on the *Systems* page, check if the status of the SAP System has changed to *Registered*.

    If you are already on the *Systems* page, refresh the page to check if the status has changed.

    > ### Note:  
    > You can register a system only once with the same name per global account.

    Once a system is registered, you can deregister it only after removing it from all entitlement configurations and formations it takes part in. If a problem occurs while deregistering the system, you get a status *Deregister Error*. In this case, you have to report an incident.

    > ### Note:  
    > You will not be able to deregister a system, if its status is one of the following:
    > 
    > -   *Error*
    > 
    > -   *Deregistering*
    > 
    > -   *Deregister Error*

