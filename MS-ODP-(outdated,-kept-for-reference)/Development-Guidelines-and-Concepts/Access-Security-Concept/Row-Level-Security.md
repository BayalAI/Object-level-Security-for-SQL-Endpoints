In this case let's say you have data in tables of various different countries and regions. Now any user of region A can only see data of region A. All other region data should be hidden from them

They cannot see workspace, they cannot see all tables, they also cannot see all rows/data.

Imagine you have a table called "publicholidays" that has a list of holidays categorized by the regions. You want to ensure that User A that belongs to region A can only access data and see rows that are having region A holidays. 

- _**Create a Security Group:**_ This step is typically done in your Active Directory or Azure AD, where you create a security group and add users to it. For this example, let’s assume you have a security group called RegionAUsers.


- **_Create a Function to Filter Rows:_** This function will determine which rows a user can access based on their region.

  
```
CREATE FUNCTION dbo.fn_securitypredicate(@countryOrRegion AS NVARCHAR(50))
RETURNS TABLE
AS
RETURN SELECT 1 AS fn_securitypredicate_result
WHERE @countryOrRegion = 'RegionA' AND USER_NAME() IN (SELECT name FROM sys.database_principals WHERE name = 'RegionAUsers');
```



   The function dbo.fn_securitypredicate checks if the countryOrRegion column matches ‘RegionA’ and if the current user belongs to the RegionAUsers group.
USER_NAME() returns the name of the current user.



- **_Create a Security Policy:_** This policy will apply the function to the public_holidays table.

  
```
CREATE SECURITY POLICY dbo.PublicHolidaysSecurityPolicy
ADD FILTER PREDICATE dbo.fn_securitypredicate(countryOrRegion)
ON dbo.public_holidays
WITH (STATE = ON);
```

The security policy dbo.PublicHolidaysSecurityPolicy applies the filter function to the public_holidays table.
The FILTER PREDICATE ensures that only rows where the countryOrRegion matches ‘RegionA’ and the user is part of RegionAUsers are returned.