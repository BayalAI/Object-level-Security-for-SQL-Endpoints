#Steps and pre-requirements to create a new Fabric Capacity

1. get Business Service
2. get Execution Platform
3. get Resource Group
4. add and Grant Contributor Access to the AD Group
5. create new Capacity
6.Including in the Fabric Metrics Report 

**Please be aware that the WBS is assigned on the level of the execution platform**

A. If the resource group exists you could directly create a Capacity in the Azure portal -> step 4. 
</p>
B. If a the resource group must be created, a ticket must be raised. To do this you must know the execution platform.
If the execution platform exists, you could create the Pisa ticket -> step 3. 
</p>
C. If the execution platform must be created, a ticket must be raised. If the Business Service exists, you could create the Pisa ticket -> step 2. 
</p>
D. If Business Service must be created, a ticket must be raised. -> step 1.
</p>
</p>
What exists today (August 2025)

#Business Services
related to ODP:
`Octopus Data Platform (ODP)`

#Execution Platform
related to ODP:
`Akela`
WBS: GL.IR1344.290
Business Service: SAC (SAP Analytics Cloud)
Department: A CIO IT Core Services Data

`Datalake Fabric`
WBS: GL.IP1363.500 
Business Service: SAC (SAP Analytics Cloud)
Department: A CIO IT Core Services Data

`Digital Octopus`
WBS: GL.IR1344.290 
Business Service: empty
Department: A CIO IT Core Services Data

`GenAI Services`
WBS: GL.IR1370.500
Business Service: Octopus Data Platform (ODP)
Department: A CIO IT Core Services Data


##Steps to create pre-requirements

**1. Business Service**
Raise Pisa Ticket to get a new Business Service
A business service will create a hierarchy in the Pisa portal too. e.g. 
[Pisa ODP](https://pisa.myatos.net/home?id=sc_category&sys_id=865f2b5dc37eca10a5d5f4177d013117&catalog_id=-1&spa=1)

**2. Execution Platform**
Raise Pisa Ticket to get a new Execution Platform
The Name and WBS must be defined.
As Business Service "Octopus Data Platform (ODP)" must be selected
[PISA KOT](https://pisa.myatos.net/home?id=sc_cat_item&sys_id=3f512c90db908610454964ebd39619d6&sysparm_category=3daf1848db27909454d3366af496190d)

**3. Resource Group**
Raise Pisa Ticket to get a new Resource Group
The Resource Group must be created in the production subscription to get the discount for reserved capacities
[Pisa KOT](https://pisa.myatos.net/pisa_old?id=sc_cat_item&sys_id=13218af21ba81d10668eddb59b4bcbdb)
You must select the platform

**4. Add and Grant Contributor Access to the AD Group**
Once the Resource Group has been created, contributor access must be assigned in order to create and manage resources within it. This access can be provisioned through a PISA ticket, with the required role explicitly requested as _Contributor_ to enable resource creation and management.
([Pisa KOT](https://pisa.myatos.net/home?id=pisa_sc_cat_item&table=sc_cat_item&sys_id=c405a03fdba49d1087140149f496199a&recordUrl=com.glideapp.servicecatalog_cat_item_view.do%3Fv%3D1&sysparm_id=c405a03fdba49d1087140149f496199a))

**5. Fabric Capacity**
a. create a Fabric Capacity in the Azure portal
[direct link](https://portal.azure.com/#view/Microsoft_Azure_Analytics/CreateCapacityBlade/_provisioningContext~/%7B%22initialValues%22%3A%7B%22subscriptionIds%22%3A%5B%2254d53b4f-0bef-4378-a318-d49b98f69c76%22%2C%22ccdb2f3a-dc8b-4dee-9965-75804f8130ab%22%5D%2C%22resourceGroupNames%22%3A%5B%5D%2C%22locationNames%22%3A%5B%22germanywestcentral%22%2C%22westeurope%22%5D%7D%2C%22telemetryId%22%3A%222a76aeab-a67a-473e-b08a-3ecb767eb259%22%2C%22marketplaceItem%22%3A%7B%22categoryIds%22%3A%5B%5D%2C%22id%22%3A%22Microsoft.Portal%22%2C%22itemDisplayName%22%3A%22NoMarketplace%22%2C%22products%22%3A%5B%5D%2C%22version%22%3A%22%22%2C%22productsWithNoPricing%22%3A%5B%5D%2C%22publisherDisplayName%22%3A%22Microsoft.Portal%22%2C%22deploymentName%22%3A%22NoMarketplace%22%2C%22launchingContext%22%3A%7B%22telemetryId%22%3A%222a76aeab-a67a-473e-b08a-3ecb767eb259%22%2C%22source%22%3A%5B%22BrowseResource.ReactView%22%2C%22%7B%20Name%3A%20Part%2C%20Type%3A%20%5B0%5DHubsExtension-%5B1%5DBrowseResource.ReactView-%5B2%5DAzBladeVirtualLens-%5B5%5DBrowseResource.ReactView%2C%20Id%3A%20Part-BrowseResource.ReactView-2%20%7D%22%2C%22Part-BrowseResource.ReactView-2%22%5D%2C%22galleryItemId%22%3A%22%22%7D%2C%22deploymentTemplateFileUris%22%3A%7B%7D%2C%22uiMetadata%22%3Anull%7D%7D)

b. all Capacities must be created in the production subscription to get the discount for reserved capacities

**6. Including in the Fabric Metrics Report**     


