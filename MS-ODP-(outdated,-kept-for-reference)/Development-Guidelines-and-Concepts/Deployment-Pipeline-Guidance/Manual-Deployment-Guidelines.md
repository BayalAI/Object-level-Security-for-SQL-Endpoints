# Deployment from Workspace Staging to Production
@TODO: pipeline (pipeline => pipeline link, parameters, scheduling), notebook(azure key vault), lakehouse(shortcuts)

Notes: notebook(workspace lakehouse link => no need, managed by code, workspace intra-workspace link => no need, managed by code)



1. ## Create the deployment pipeline
Open the DEV Workspace
Select "Create deployment pipeline" (admin permissions needed)

![image.png](/.attachments/image-3fb0f749-7093-48da-bb17-8d3de7a9b9fb.png)

Add Pipeline name and select "Next":
![image.png](/.attachments/image-bdcba89d-03c6-4462-ac84-78fafd04f311.png)

Keep two stages and rename them (Staging and Production):
![image.png](/.attachments/image-e8616253-2458-4363-99f4-c1b5f6c3935e.png)

Select the target Workspace for production:
![image.png](/.attachments/image-f6ad0107-6f5d-4611-8674-4f45870417d1.png)


