#How to use MS Graph 
_Microsoft Graph is the gateway to data and intelligence in Microsoft cloud services like Microsoft Entra and Microsoft 365. 
Access the data of your organization through Microsoft Graph.
Microsoft Graph exposes REST APIs and UI to access data on the Microsoft cloud services_

This article describes how to use MS graph to help us to manage our Azure AD groups.

- With explorer UI [Graph Explorer | Try Microsoft Graph APIs - Microsoft Graph](https://developer.microsoft.com/en-us/graph/graph-explorer)
- Within Fabric Pyspark
- MS articles

#MS Graph explorer UI
After using above url and signin, screen should look like below screenshot
1) you are logged in
2) you are using the Atos tenant
3) first api call by default generated
4) hit the run query button
5) you get all data about your-self available in Azure AD (Entra ID). This data is coming from DAS forward to Entra ID

The result will be always a json structure. Via the UI but also via REST api call

![image.png](/.attachments/image-a481cd5e-d7b4-43f2-b1ca-97731881d2f4.png =1000x)

After first success you could explorer sample queries in the left navigation of the MS graph explorer UI

#MS Graph samples
By default you are getting all available information and attributes stored in Entra ID. 
There are multiple options to limit the attributes and to filter the result
You don't need to be a member or owner of the group the get access to the data.

You must copy and paste the http to the explorer. Don't click on it!

- list all groups where I'm a member
member list 
https://graph.microsoft.com/v1.0/me/transitiveMemberOf/microsoft.graph.group?$count=true
member list filtered by name and description
https://graph.microsoft.com/v1.0/me/transitiveMemberOf/microsoft.graph.group?&$select=displayName,description

- list all Azure AD groups starting with GIT-Octopus
https://graph.microsoft.com/v1.0/groups/?$filter=startswith(displayName,'GIT-Octopus')

- limited to ID, name, description
https://graph.microsoft.com/v1.0/groups/?$filter=startswith(displayName,'GIT-Octopus')&$select=id,displayName,description

- get all information of one group by using the id
https://graph.microsoft.com/v1.0/groups/75a80280-53c0-4822-b4fd-f57e6deadf9e

- get member (user) of a specific AD group. Must be filtered by Group id from above result 
https://graph.microsoft.com/v1.0/groups/75a80280-53c0-4822-b4fd-f57e6deadf9e/members?$select=id,displayName,userPrincipalName

- get from the group the owner name only
https://graph.microsoft.com/v1.0/groups/75a80280-53c0-4822-b4fd-f57e6deadf9e/owners?$select=displayName

With this basics we could use MS Grap via the API in pyspark

#MS graph in PySpark

As per today 2025-07-04 there is one big limitation / pre-requirement:
Today you must login to the MS Graph UI and copy the access token.
The authentication within PySpark must be investigated.

Select the access token menu and copy the token:

![image.png](/.attachments/image-cf12850a-8af3-4666-9e46-d52925b2263b.png =1000x)

- Go to the Fabric playground workspace to get acces to the sample notebook.
- Open Folder "MS Graph" [direct link to Fabric MS Graph api sample folder](https://app.powerbi.com/groups/8a383c1d-7d35-4eb8-85a3-793f32ac84ac/list?experience=power-bi&subfolderId=31140)

- Copy the sample notebook ;-)
- open your notebook and replace the access token
- review the code, modify the code, run the code and have fun

#use MS graph to manage groups
In case you are a owner of a group you could use the UI or python to add or delete member.
For example to add a new member (Swapnil) by id to Group GIT-ODP-Reader by id
`https://graph.microsoft.com/v1.0/groups/0fccffdd-50c1-4c5a-9be1-ce2f2ab5f8ac/members/$ref`
`Body:`
`{`
`    "@odata.id": "https://graph.microsoft.com/v1.0/directoryObjects/18796bfc-c3ef-46a4-ac2b-0e5c94feceb8"`
`}`

In case you want to code a PySpark notebooks for such use cases please get in contact with Swapnil!



#MS Graph articles
[Overview](https://learn.microsoft.com/en-us/graph/overview)
[Access via API](https://learn.microsoft.com/en-us/graph/graph-explorer/graph-explorer-overview)
[REST API Reference](https://learn.microsoft.com/en-us/graph/api/overview?view=graph-rest-1.0&preserve-view=true)
[REST API filter/selection/..](https://learn.microsoft.com/en-us/graph/aad-advanced-queries?tabs=http)


