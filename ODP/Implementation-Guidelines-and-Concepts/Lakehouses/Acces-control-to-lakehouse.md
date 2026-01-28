#Access control to lakehouse

Citizen developer need access to the Gold lakehouses. Typically, the access will be implemented via shortcuts to their own workspace and lakehouse.
The Citizen must be authorized to the source Gold lakehouse to be able to read the data.
Today we use three options
1.      Share the workspace access including the lakehouse access
2.      Share the read access to the lakehouse without providing access to the workspace
3.      Using OneLake data access roles

      

##Share the workspace access

This is the simplest way but grant a to high authorization and should be avoided.

##Share the read access to the lakehouse

This approach is documented by Sarah in this PPT (1)
SPO: Octopus -> 01 Overview [LINK](https://atos365.sharepoint.com/:p:/r/sites/100002399/Shared%20Documents/Octopus/01%20Overview/Citizen%20Developer.pptx?d=wa18971fd9dd74f2bb5a4de9f94f64a6a&csf=1&web=1&e=Su6JyB)
This option is the current best way to provide needed access.

##Using OneLake data access roles

This option was recently introduced by MS and is available in preview.
[https://learn.microsoft.com/en-us/fabric/onelake/security/get-started-data-access-roles](https://learn.microsoft.com/en-us/fabric/onelake/security/get-started-data-access-roles)
This access control share read access to the lakehouse with the options:
1.      to select specific tables
2.      to select specific columns
3.      to create a SQL statement with a filter on values to implement RLS with it.

      

##Select specific tables

1.      Use inside of the lakehouse the option “manage OneLake data access” (2)
2.      Add a new role (3)  
only letters allowed in the role name ☹
3.      Select the table to be accessed (5)
4.      Add person or AD group (6)
5.      Open advanced option and select read (7)
6.      Save and check result

##Screenshots
       
(1)
![==image_0==.png](/.attachments/==image_0==-808de4ae-a8cd-4aa4-bcfb-d6f531425275.png) 

(2)
![==image_1==.png](/.attachments/==image_1==-6f92ff4b-7810-4d61-adba-373941e02e0f.png) 

(3)
![==image_2==.png](/.attachments/==image_2==-ce66e834-8b85-4e52-ac77-09a5d25708df.png) 
(4)
![==image_3==.png](/.attachments/==image_3==-4b2705a6-944b-49fb-aa42-39a82cc0e4ce.png) 
(5)
![==image_4==.png](/.attachments/==image_4==-841c6b0d-1fa4-42eb-ad82-db629e38b434.png) 

(6)
![==image_5==.png](/.attachments/==image_5==-cf16df46-35e3-492a-8d23-5e96ab3f4b8c.png) 
(7)
![==image_6==.png](/.attachments/==image_6==-76ef6d71-9018-40e4-a4d0-9a96be1630ba.png) 

(7)
Member with access including the one inherited from workspace access
![==image_7==.png](/.attachments/==image_7==-0502454d-0d6a-4926-bf52-7323c8368eeb.png) 
![==image_8==.png](/.attachments/==image_8==-c680e0ad-b4ab-45e1-ae9d-f10099842273.png) 