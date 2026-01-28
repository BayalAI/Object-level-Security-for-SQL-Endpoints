# Agenda
- To-Be-Workflow
- Current-Status
- How to deploy
  - Workspace Items deployment
  - Workspace items configuration
  - Sql Endpoint Deployment 


# To-Be-Workflow

::: mermaid
 graph LR;
 A[User Triggers Ado deployment pipeline] --> BR[Deploy Fabric Items to workspace branch] --> T[Configuration of Fabric Items ] --> U[Execution of Pipeline for Unit and Integration Tests] --> B[Pipeline executes built-in deployment to next stage] --> C[Pipeline executes deployment fabric pipeline] --> D[Fabric pipeline executes notebook] --> E[Fabric notebook updates all workspace references] --> F[Pipeline deploys SQL permission solution];
:::

# Current Status
- Workspace Items Deployment
   - Technical done
- Workspace Items Configuration
   - Technical done
   - must be optimized to use complex configuration
- Sql Endpoint Deployment 
   - Technical done
   - must be optimized to use parameters
- General ADO
   - must be optimized to use stages
   - Must be optimized to use deployment approval

# How to deploy

- Workspace Item Deployment [Christian]
- Workspace Item Configuration [Michael] 
   - Shortcuts must be created manual per workspace and lakehouse
   - Pipeline References
![image.png](/.attachments/image-52ee2e80-4726-40c2-b5f8-2a443d896f1e.png)
   - Notebook references
     - onelake path ...
- SQL Solution Project  [Christian]
   - Define Role
   - Define Permissions
   - Deploy Solution
   - Work with profiles


- CICD Automation Code - https://dev.azure.com/Atos-Akela/Fabric%20OneLake/_git/octopus-data-integration/pullrequest/229