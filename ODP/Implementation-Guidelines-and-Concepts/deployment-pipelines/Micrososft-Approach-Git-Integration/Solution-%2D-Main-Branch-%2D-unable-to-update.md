# Introduction
After finalization of an PR and clicking on "update all" to update the main branch following error will be showen:

![image.png](/.attachments/image-ed789360-ee53-4d9e-899c-735244dad6b0.png =1000x)

# Issue description
This happens, when an artefact reference like a pipeline cannot be found.

# Solution

## Create a new feature branch 
Use "checkout new branch" to create a new feature branch

![image.png](/.attachments/image-a8afdd53-fa87-441e-98af-1b9b1e0227a2.png)

## Identification of missing object
Open the content file (in your newly created feature branch) of the causing artefact, e.g. pipeline-content.json for a pipeline.
In this sample the Bronze_Main caused the issue.
1. Open the file and validate the referenced pipelineId and workspaceId in a tool like Visual Studio Code or in the DevOps Portal:

![image.png](/.attachments/image-79419899-4660-48e8-97ca-2830ffbe0cbf.png =1000x)

2. Search for the referenced Id (in this case the pipelineId) in the files of the subfolder of your workspace and validate the workspaceId (can be found in the URL of the workspace)
![image.png](/.attachments/image-b70a5de8-ec19-4a90-9a55-4c45c3966c85.png =1000x)

## Change reference
Change the workspaceId or replace the (pipeline)Id by an existing Id.
The (pipline)Id can be found in the .platform file of the referenced artefact
![image.png](/.attachments/image-b845c5a4-4358-4436-b5ec-5e898fb2e1a8.png)

## Commit, Create PR, Switch back to main
1. Commit your changes, create and finalize a PR based on your feature branch
2. Switch back to the main branch in your workspace

  
