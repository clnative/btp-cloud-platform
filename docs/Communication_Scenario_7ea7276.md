<!-- loio7ea7276c89a644d9867bf0f8627aed67 -->

# Communication Scenario

A communication scenario is a design time description of how two communication partners communicate with each other.

It provides technical information, such as the used inbound and outbound services and their service type, for example OData or SOAP, and the number of allowed communication arrangement instances.

The following types of communication scenarios are available:

-   **Managed by SAP**, where SAP provides a communication scenario and you create and maintain a communication arrangement
-   **Managed by customer**, where you or your partner develop a communication scenario and you or your customer create and maintain a communication arrangement

A communication scenario is created in the development system by a developer using ABAP Development Tools. It is then transported to other systems via the [Manage Software Components](Manage_Software_Components_3dcf76a.md) app. To maintain a communication scenario, business catalog `SAP_A4C_BC_DEV_PC` needs to be assigned to the corresponding user.

**Related Information**  


[Display Communication Scenarios](Display_Communication_Scenarios_baa798b.md "You can use this app to get an overview of available communication scenarios.")

[Consuming Services in the Context of API with Technical Users](https://help.sap.com/viewer/5371047f1273405bb46725a417f95433/Cloud/en-US/54886e183a3a40cbae912cf3b09dc46a.html)

[Business Catalogs for Development Tasks](Business_Catalogs_for_Development_Tasks_a9f4278.md "Get an overview of available business role catalogs and their restrictions.")
