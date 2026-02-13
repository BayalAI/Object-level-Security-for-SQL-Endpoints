The following are some basic demo scenarios that will help you to decide which level of access or what way should you go about to give access to the users for your data. All you need to do is identify which use case resonates with you and fit it in one of these below

## Scenario 1: Have access to fabric workspace and all data in it

### Data Access Requirements: 
- Person or Group should be allowed to see all data within a given workspace

### Reference Concept 
- Implementation [Workspace Level Security](/MS-ODP-\(outdated,-kept-for-reference\)/Development-Guidelines-and-Concepts/Access-Security-Concept/Workspace-Level-Security)


## Scenario 2: Cannot see the workspace but can query data of Lakehouses/Warehouses in Fabric

### Data Access Requirements: 
- Person or Group should be able to query all data in a given Fabric Lakehouse in a workspace.
- Person or Group should not see the workspace content

### Reference Concept:
- Implementation: [Item Level Security](/MS-ODP-\(outdated,-kept-for-reference\)/Development-Guidelines-and-Concepts/Access-Security-Concept/Item-Level-Security)





## Scenario 3: Cannot see workspace, but can query some tables in the Lakehouse, not all

### Data Access Requirements: 
- Person or Group should only be allowed to query a subset of tables or schematas in a given lakehouse in a given workspace
- Person or Group should not be allowed to see the workspace


### Reference Concept:
- Implementation: Here you take the OLS( Object level Security) route.
[Object Level Security](/MS-ODP-\(outdated,-kept-for-reference\)/Development-Guidelines-and-Concepts/Access-Security-Concept/Object-Level-Security)



## Scenario 4: Should have access to only query and see data in particular regions

### Data Access Requirements: 
- Person or Group should only see a subset of data in a given table in a given Lakehouse in a given workspace
- Person or Group should not see the workspace
- Person or Group should be able to see all columns of a table but not all rows. 

### Reference Concept:
- Implementation: Here you take the RLS (Row Level Security) route.
[Row Level Security](/MS-ODP-\(outdated,-kept-for-reference\)/Development-Guidelines-and-Concepts/Access-Security-Concept/Row-Level-Security)



## Scenario 5: Should have access to only query and see columns of data which is relevant to them.

### Data Access Requirements: 
- Person or Group should only see a subset of data in a given table in a given lakehouse in a given workspace
- Person or Group should not see the workspace
- Person or Group should be able to see all rows of a table but not all columns. 


### Reference Concept:
- Implementation: Here you take the CLS (Column Level Security) route.
[Column Level Security](/MS-ODP-\(outdated,-kept-for-reference\)/Development-Guidelines-and-Concepts/Access-Security-Concept/Column-Level-Security)
