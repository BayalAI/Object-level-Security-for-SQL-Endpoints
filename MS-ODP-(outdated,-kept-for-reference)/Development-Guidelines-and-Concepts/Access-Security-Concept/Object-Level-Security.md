Now in this scenario you want the user to be only accessing, let's say 5 out of 10 tables that are relevant to them. They cannot query any other tables that are not required for their role. 

The users cannot see the workspace and can also not query all tables in the Lakehouse. they can only query some tables. In this case Do not go through workspace or item level route. You give them unnecessary access to data here.

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


**Example 2:** Deny Access to a Specific Table 

If you want to prevent certain users from accessing a particular table (e.g., "Salaries"), you can use the DENY statement: 

`CREATE ROLE RestrictedRole;`


```
DENY SELECT ON employees TO RestrictedRole;

ALTER ROLE RestrictedRole ADD MEMBER [<entra id of user required>];
```


![image.png](/.attachments/image-e970d4ef-44e4-432b-babd-5ef9bfcdb34f.png)

