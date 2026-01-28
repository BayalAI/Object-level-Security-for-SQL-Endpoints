We use **Azure AD security groups** in ODP Fabric for mulitple use cases 
- to provide access to Azure resources
- to provide access Fabric workspaces
- to manage RLS/OLS in semantic models

  
#Types of Azure AD groups
**Microsoft 365** groups will be created by using channels in teams, SPO access, .. There is no need to request a creation of this type of groups. They will be created "implicitement".
![{181932EC-7B6E-4984-9F0F-4D9E84C8F0D9}.png](/.attachments/{181932EC-7B6E-4984-9F0F-4D9E84C8F0D9}-9965eb08-65a4-496a-9a15-16ff5ce41216.png =500x)

**Security** groups could technically created within Azure portal respectively in the Entra ID. Due to security reasons this is forbidden for us. Security groups must be requested by Pisa. Pisa will create the groups immediately.
![image.png](/.attachments/image-cd71b464-dad3-4f4d-a12f-e5fcb8b5eee9.png =500x)



#How to create Azure AD groups via Pisa
You should only add yourself as owner. 
Other owner and member could be added later. Please select always organisation Atos, never use Eviden.
Typically name should start with 
- GIT-ODP for providing access to workspaces
- GIT-Octopus to manage RLS/OLS

[Pisa Link](https://pisa.myatos.net/home?id=sc_cat_item&sys_id=bb592aa0db61d55087140149f49619b1&sysparm_category=5ecc2e63dba788903faba6b605961985&catalog_id=-1)

#How to add owner and member to Azure AD groups

    -    by [My Account](https://myaccount.microsoft.com/groups)

    -    by Pisa [Pisa Link](https://pisa.myatos.net/home?id=sc_cat_item&sys_id=3209ae09db35151087140149f49619d6)

    -    by [Azure Portal](https://portal.azure.com/#home)

As mentioned above the use of Entra ID UI is blocked **but** on every azure page you have the search box on top of your page. 
Type in the name of the Azure AD group!! 
Either the complete name or the first part of the group. Don't forget to extend the hit list.
![image.png](/.attachments/image-4a06a688-c34e-42be-9872-fdc974f767bd.png =300x)

![image.png](/.attachments/image-8a51109e-a8d0-478b-af06-5ee4aaf64fea.png =300x)
Now you could easily read and maintain owner and member. Including bulk upload and export.
![image.png](/.attachments/image-761eee89-9fe6-4449-9873-a87862abbb86.png =400x)


