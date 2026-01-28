[[_TOC_]]

# Introduction

This documentation will explain the sample sql project deployment pipeline.
Detailed documentation for yaml pipelines in general can be found in the documentation at:
[Azure Pipelines documentation - Azure DevOps | Microsoft Learn](https://learn.microsoft.com/en-us/azure/devops/pipelines/?view=azure-devops)
SQL Projects are described here:
[What are SQL database projects? - SQL Server | Microsoft Learn](https://learn.microsoft.com/en-us/sql/tools/sql-database-projects/sql-database-projects?view=sql-server-ver16)

The sample pipeline can be found on:
[Pipelines - Runs for sample-sql-endpoint-deployment](https://dev.azure.com/Atos-Akela/Fabric%20OneLake/_build?definitionId=12)

The yaml pipeline files can be found in the repository:
[samplepipeline - Repos](https://dev.azure.com/Atos-Akela/Fabric%20OneLake/_git/octopus-data-integration?version=GBmain&path=/.azuredevops/samplepipeline)

And the sample database project is located here:
[SAMPLE_DATABASE - Repos](https://dev.azure.com/Atos-Akela/Fabric%20OneLake/_git/octopus-data-integration?version=GBmain&path=/SQL_ENDPOINT_DATABASES/SAMPLE_DATABASE) 

## YAML Files
All files are located in the folder .azuredevops
![image.png](/.attachments/image-7209c9d1-c557-413e-8c0b-000d7a51f0e7.png)

### pipeline.yml
This pipeline file is executed first and will do following steps:
- read variables
![image.png](/.attachments/image-68e328f8-042b-437b-89b4-e6e134f0a100.png)
- build database project and publish artifacts (stage: Build)
![image.png](/.attachments/image-34151a58-01f5-4603-aa1f-4de42139c0c8.png)
- deploy database project to multiple stages (stage: INT_Deployments, UAT Deployments)
For the deployment a sub yaml file will be executed (.templates/pipeline.db-deploy.jobs.yml)
and the environment will be used as a parameter:
![image.png](/.attachments/image-44c121f5-9501-4f7f-8e3f-5a505cfeba26.png)
You can find this section for each stage. If an additional stage is needed, only this section needs to be added again for the new stage and needed variables must be added in the variables.yml file.

### .templates/pipeline.db-deploy.jobs.yml
This pipeline deploys the database. All parameters are retrieved from the previous loaded variables file.
![image.png](/.attachments/image-71a1ccec-9d96-426c-91f1-2a315e6ea8dc.png)
All AdditionalArguments for SQL deployment can be found on: [SqlPackage Publish - SQL Server | Microsoft Learn](https://learn.microsoft.com/en-us/sql/tools/sqlpackage/sqlpackage-publish?view=sql-server-ver16)

### variables.yml
All needed variables are stored in this configuration file.
If an additional stage/environment is needed, also the variables for this environment must be added in this file.
  
![image.png](/.attachments/image-1fe39b11-d5bc-4e14-ab36-47db361469ae.png)

This is only one option, you can also store configurations in DevOps Libraries or KeyVault.
 

 

