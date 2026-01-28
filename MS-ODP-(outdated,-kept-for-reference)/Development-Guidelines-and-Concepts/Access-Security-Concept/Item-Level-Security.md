


In these cases, you want the users to be able to query data, here you want to go for a traditional approach assuming there is a database (in this case your Lakehouse) and you do not know physically where it resides. You just want users to have a connection string which they can use to connect on any tool like SSMS and be able to query and work with your data

You do not want the user to have any access to your workspace. Giving them this access does not allow them to see the workspace at all. They can only connect and query data traditionally via a tool. Do not go by the workspace level access route. It opens the entire workspace for them

Follow these steps to achieve item level security

##Approach 1

Go to your Lakehouse click on the Share option and here's what the options are going to be

  ![image.png](/.attachments/image-995e229a-9090-477e-8dd2-bf873d398314.png)  
Here you can see three parameters:
  - Read all SQL endpoint data gives permission to only access data through a tool that lets you connect to SQL enpoints.
  - Read all Apache Spark allows actual read access to delta files in the OneLake.
  - Build reports on the default semantic model allows building Power BI reports on top of the semantic model.

  So for example if I gave a user X 'Read all SQL endpoint data' they would be able to query data from tools connecting to sql endpoint, but user X would not have access to the actual workspace themselves.


## Approach 2
Note: This feature is in preview and is not yet available in all Lakehouses

Here is a link that clearly outlines the steps in which you can have OLS created for schema enabled Lakehouses.  

  <A  href="https://learn.microsoft.com/en-us/fabric/onelake/security/get-started-data-access-roles">Get started with OneLake data access roles (preview) - Microsoft Fabric | Microsoft Learn</A>  

  
   ![4.png](/.attachments/4-f42fd61f-aa8e-4867-8196-f00460d9311f.png)

   ![5.png](/.attachments/5-95638dc5-25af-41bf-8469-4a57cd71a257.png)

   ![6.png](/.attachments/6-2c2a16c1-0f6f-49d3-8085-67b11bb1fd3a.png)  

  Please Note that it is always best practice to give readers least privilege, therefore a READ access only unless required for specific other tasks


## You can follow the same steps for warehouses too