# OLS Best Practice

## Principle of Least Privilege
The principle of least privilege states that users should only be granted the minimum permissions necessary for their tasks. This reduces the risk of data misuse and accidental changes.
 - Only grant permissions that are absolutely necessary.
 - Regularly review and update permissions to ensure they remain relevant.

## Use of EntraId Roles
Instead of granting permissions directly to EntraId users, you should use security groups. Groups allow you to manage permissions in groups, making management more efficient.

## Use of Database Roles
Instead of granting permissions directly to users, you should use roles. Roles allow you to manage permissions in groups, making management more efficient.
- Create roles that correspond to specific tasks or functions.
- Assign roles to users based on their tasks.
- Avoid granting permissions directly to users.

# How To

## Grant Read Access to Lakehouse
To Access SQL Endpoints, "_Read_" access on the Lakehouse is needed.

1. Read permissions can be granted either by clicking on "_Manage permissions_" or "_Share_" on the Lakehouse
![image.png](/.attachments/image-3580cb7a-8d92-4213-ab27-817379da297e.png)

1. If you select "_Manage permissions_", "_Add User_" must be selected in addition

1. Add the user or group
**Don't select any additional permissions**

![image.png](/.attachments/image-268dce61-79be-4f9a-bc52-527158aa921d.png)



## Grant Permissions on Objects
samples, tbd.

```
--create schema
create schema s2
GO
--create view
create view s2.v1 as select * from s1.t1
GO
-- create role
create role r1;
GO
--example to grant select on schema
grant select on schema :: s2 to r1
GO
--example to grant select on table
grant select on s1.t1 to r1;
GO
--add user/group to role
alter role r1 add member [EntraID_UserOrGroup];
GO
-- revoke select
revoke select on object :: s1.t1 to r1;
GO
```


## Validate Permissions
samples, tbd.


```
-- show permissions
SELECT DISTINCT pr.principal_id, pr.name, pr.type_desc, 
 pr.authentication_type_desc, pe.state_desc, pe.permission_name
FROM sys.database_principals AS pr
INNER JOIN sys.database_permissions AS pe
 ON pe.grantee_principal_id = pr.principal_id;
```



```
-- show object permissions
SELECT DISTINCT 
       pr.principal_id
     , pr.name AS [UserName]
     , pr.type_desc AS [User_or_Role]
     , pr.authentication_type_desc AS [Auth_Type]
     , pe.state_desc
     , pe.permission_name
     , pe.class_desc
     , coalesce(sch.name, o.[name]) AS [Object]
FROM sys.database_principals AS pr
    JOIN sys.database_permissions AS pe
        ON pe.grantee_principal_id = pr.principal_id
    LEFT JOIN sys.objects AS o
        ON o.object_id = pe.major_id
    LEFT JOIN sys.schemas AS sch
        ON sch.schema_id = pe.major_id
        AND class_desc = 'SCHEMA';
```



```
--show role members
SELECT DP1.name AS DatabaseRoleName,   
    isnull (DP2.name, 'No members') AS DatabaseUserName   
FROM sys.database_role_members AS DRM  
RIGHT OUTER JOIN sys.database_principals AS DP1  
    ON DRM.role_principal_id = DP1.principal_id  
LEFT OUTER JOIN sys.database_principals AS DP2  
    ON DRM.member_principal_id = DP2.principal_id  
WHERE DP1.type = 'R'
ORDER BY DP1.name;
```



