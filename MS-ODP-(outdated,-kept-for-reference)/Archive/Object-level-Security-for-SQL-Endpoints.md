

# 1. Introduction to Object-Level Security (OLS) 

Object-Level Security (OLS) allows for the control of access to specific objects (such as tables, columns, views) within a database. This security mechanism ensures that users can only interact with the data they are permitted to view, minimizing exposure of sensitive data. 

In the context of Microsoft Fabric, OLS can be enforced on SQL endpoints to restrict users’ access to certain database objects. The security is managed using Entra ID (formerly Azure Active Directory), allowing centralized and identity-based access control. 

[[_TOC_]]

# 2. Key Concepts 

SQL Endpoints: These are the entry points through which users can connect to the data stored in Microsoft Fabric. SQL endpoints expose the database to users or applications. 

Entra ID-based Security: With Microsoft Entra ID, you can enforce access control using the identities in your organization. Roles and permissions can be assigned to specific users or groups managed in Entra ID. 

Object-Level Security (OLS): Refers to restricting access to objects (e.g., tables, views, and columns) at the database level. This contrasts with Row-Level Security (RLS), which limits access at the row level within tables. 

# 3. Configuring Object-Level Security in Microsoft Fabric  
When managing data security, it’s crucial to apply the appropriate type of security based on the level of access required. **_Workspace Level Security_** is ideal for controlling access to the entire workspace, ensuring only authorized users can access all datasets and reports. **_Lakehouse Sharing Level Security_** is best for managing access to the entire Lakehouse, protecting large datasets. For more granular control, **_Object-Level Security (OLS)_** restricts access to specific tables or views, while **_Row-Level Security_** (RLS) ensures users can only see data relevant to their role or region. Finally, **_Column-Level Security (CLS)_** is essential for protecting sensitive information by restricting access to specific columns within a table. By strategically applying these security measures, you can ensure robust data protection and compliance.

 


**Walkthrough of different levels of controls that you actually have**

---
- Lets start with **_Workspace Roles_**  
  
  Once you come inside the workspace you see the Manage access option. Click on that. 
![image.png](/.attachments/image-ac9373cb-fc47-40b6-8c30-e7d273d1a468.png)

  Now there are four main roles when it comes to access on a workspace level, these include 
  - Admin
  - Contributor
  - Member
  - Viewer

  Here you are giving access to the entire workspace, but what if you want a traditional approach, not have users actually look into your workspace but only connect to the data and tables through SSMS, much like your traditional database approach. In such a case we do not want to give workspace access, so let us look at a more controlled access.

- Sharing feature on **_Lakehouses_**

  This feature gives us the control to grant other users access to the Lakehouse objects but also lets us decide how much access do they really get. Go to your lakehouse click on the Share option and here's what the options are going to be

  ![image.png](/.attachments/image-995e229a-9090-477e-8dd2-bf873d398314.png)  
Here you can see three parameters:
  - Read all SQL endpoint data gives permission to only access data through a tool that lets you connect to SQL enpoints.
  - Read all Apache Spark allows actual read access to delta files in the OneLake.
  - Build reports on the default semantic model allows building Power BI reports on top of the semantic model.

  So for example if I gave a user X 'Read all SQL endpoint data' they would be able to query data from tools connecting to sql endpoint, but user X would not have access to the actual workspace themselves.

- **_For schema enabled Lakehouses_**

   Here is a link that clearly outlines the steps in which you can have OLS created for schema enabled Lakehouses.  

  <A  href="https://learn.microsoft.com/en-us/fabric/onelake/security/get-started-data-access-roles">Get started with OneLake data access roles (preview) - Microsoft Fabric | Microsoft Learn</A>  

  
   ![4.png](/.attachments/4-f42fd61f-aa8e-4867-8196-f00460d9311f.png)

   ![5.png](/.attachments/5-95638dc5-25af-41bf-8469-4a57cd71a257.png)

   ![6.png](/.attachments/6-2c2a16c1-0f6f-49d3-8085-67b11bb1fd3a.png)  

  Please Note that it is always best practice to give readers least privilege, therefore a READ access only unless required for specific other tasks
---

---
 - You can do the same for warehouses
Follow this document for clear steps on how to create and remove access from users  

   <A  href="https://learn.microsoft.com/en-us/fabric/data-warehouse/share-warehouse-manage-permissions">Share your warehouse and manage permissions - Microsoft Fabric | Microsoft Learn</A>

---



# 4. Defining Object-Level Permissions 

Permissions in OLS are set for specific database objects such as tables or views. It’s a good practice to use database roles for managing permissions. Here are some examples that follow this best practice:

Example 1: Create a Database Role

`CREATE ROLE FinanceRole;`

 Add Entra ID Users/Groups to the Role:


```
ALTER ROLE FinanceRole ADD MEMBER [tejas.radekar.external@atos.net]
ALTER ROLE FinanceRole ADD MEMBER [<other entra id of users in Finance role>];
```

Grant Permissions to the Role:

`Grant SELECT ON salaries TO FinanceRole;`

---


**Example 2:** Deny Access to a Specific Table 

If you want to prevent certain users from accessing a particular table (e.g., "Salaries"), you can use the DENY statement: 

`CREATE ROLE RestrictedRole;`


```
DENY SELECT ON employees TO RestrictedRole;

ALTER ROLE RestrictedRole ADD MEMBER [<entra id of user required>];
```


This block of code denies the SELECT permission on the "Salaries" table to the specified Entra ID user. 

 
 ---



## **5. Example Use Case:** 

A hospital maintains a comprehensive medical database that includes patient records, treatment histories, billing information, and research data. The database needs to ensure that only authorized personnel can access specific data, protecting patient privacy and complying with regulations like HIPAA.

 Create the Role:


```
CREATE ROLE DoctorGroup;
CREATE ROLE NurseGroup;
```


Grant Permissions to the Role:
SQL


```
GRANT SELECT ON patientrecords (PatientName, TreatmentDate) TO NurseGroup;
GRANT SELECT ON patientrecords (PatientName, SSN, Diagnosis, TreatmentDate) TO DoctorGroup;
```

Now you can assign doctors and nurses to the roles and now the appropriate personal will have access to right things only

 
---


## 6. Testing and Validating Object-Level Security 

1. Once OLS policies are implemented, it's essential to test them to ensure they are working as expected. 

1. Connect to SQL Endpoint: Use a SQL client like Azure Data Studio or SSMS to connect to the SQL endpoint using a test user’s credentials. 

1. Run Queries: Execute queries on the restricted objects to confirm that the correct permissions are in place. Users should see an error or lack access when attempting to query objects they don't have permission for. 

 

## 7. Best Practices for Managing OLS in Fabric 

 

1. Use Entra ID Groups: Instead of assigning roles to individual users, assign Entra ID groups. This simplifies management, especially as your user base grows. 

1. Minimal Permissions Principle: Follow the least-privilege principle—grant only the necessary permissions for users to perform their job functions. 

1. Regularly Review Permissions: As roles within the organization change, ensure that your OLS rules are regularly reviewed and updated to align with the current organizational structure. 

1. Document OLS Policies: Maintain clear documentation of the OLS policies, including which users or groups have access to specific objects. 

 

For further details, refer to the official Microsoft documentation:  

<A  href="https://learn.microsoft.com/en-us/fabric/onelake/security/best-practices-secure-data-in-onelake">Best practices for OneLake security - Microsoft Fabric | Microsoft Learn</A>  

<A  href="https://learn.microsoft.com/en-us/fabric/security/security-overview">Security in Microsoft Fabric - Microsoft Fabric | Microsoft Learn</A>  

<A  href="https://learn.microsoft.com/en-us/fabric/security/workspace-identity-authenticate">Authenticate with Microsoft Fabric workspace identity - Microsoft Fabric | Microsoft Learn</A>  

<A  href="https://learn.microsoft.com/en-us/fabric/onelake/security/fabric-onelake-security">Fabric and OneLake security - Microsoft Fabric | Microsoft Learn</A>  

<A  href="https://learn.microsoft.com/en-us/fabric/security/service-admin-object-level-security?tabs=table">Object-level security (OLS) with Power BI - Microsoft Fabric | Microsoft Learn</A>  

<A  href="https://learn.microsoft.com/en-us/fabric/data-engineering/lakehouse-sharing">Lakehouse sharing and permission management - Microsoft Fabric | Microsoft Learn</A>

 

 

 