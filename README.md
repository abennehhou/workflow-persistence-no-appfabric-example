Workflow Service Persistence Example
====================================

This example is based on the tutorial [Creating a Long-running Workflow Service]( https://msdn.microsoft.com/en-us/library/ff432975%28v=vs.110%29.aspx).

It doesn't use AppFabric. AppFabric support will end soon: [link to MSDN blog post]( https://blogs.msdn.microsoft.com/appfabric/2015/06/19/microsoft-appfabric-1-1-for-windows-server-support-lifecycle-extension-4112017/).

# Setup

* Create a new database.
* Get sql queries located in `C:\Windows\Microsoft.NET\Framework\v4.0.30319\SQL\en`.
* Execute queries *SqlWorkflowInstanceStoreSchema.sql* and *SqlWorkflowInstanceStoreLogic.sql* in the created database.
* Check that some tables (should be 10) are created for *System.Activities.DurableInstancing*.
* Change *connectionString* in Web.config file to use your database.

# Run

To run the service and check that all works fine:
* Start (with or without debugging) the service.
* From the WCF test client:
  * Call StartOrder with a customer name.
  * Check that the workflow is persisted in the database in *System.Activities.DurableInstancing.InstancesTable* table.
  * Check that its  status is idle and that there is a blocking bookmark: *AddItem*.  
  * Copy the value returned by StartOrder and call *AddItem* using this value as *p_orderId* and with a *p_itemId*.
  * Check that the workflow is deleted, as specified in the config file:  instanceCompletionAction is "DeleteAll".
