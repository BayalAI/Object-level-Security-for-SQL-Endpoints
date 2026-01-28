# Reference (Juergen 2025-05-08)

This article descripe the way of working proposed by MS rpoject in autumn 2024.
It descripe the source code control with feature branches, pull request and approval steps.


[[_TOC_]]


# Introduction
Git integration in Microsoft Fabric enables developers to integrate their development processes, tools, and best practices straight into the Fabric platform. It allows developers who are developing in Fabric to:

- Backup and version their work
- Revert to previous stages as needed
- Collaborate with others or work alone using Git branches
- Apply the capabilities of familiar source control tools to manage Fabric items

The integration with source control is on a workspace level. Developers can version items they develop within a workspace in a single process, with full visibility to all their items. Only a few items are currently supported, but the [list of supported items](https://learn.microsoft.com/en-us/fabric/cicd/git-integration/intro-to-git-integration?tabs=azure-devops#supported-items) is growing.

See also [Fabric Git Integration Documentation](https://learn.microsoft.com/en-us/fabric/cicd/git-integration/intro-to-git-integration?tabs=azure-devops)

#Environment Setup
## Repository and Folder
The repository can be found at https://dev.azure.com/Atos-Akela/Fabric%20OneLake/_git/octopus-data-integration
A folder for each connected Workspace is created:

![image.png](/.attachments/image-4162c7e9-7153-4ac0-9383-d5f45f064fc6.png)

## Policies
**There are policies applied on the main branch to prevent from direct modification of the main branch, therefore it's always necessary to work in feature branches.**   

#Best Practice
## Use feature branches for your work
Develop your features and fix bugs in feature branches based off your main branch. These branches are also known as topic branches. Feature branches isolate work in progress from the completed work in the main branch. Git branches are inexpensive to create and maintain. Even small fixes and changes should have their own feature branch.
Creating feature branches for all your changes makes reviewing history simple. Look at the commits made in the branch and look at the pull request that merged the branch.

###Name your feature branches by convention
Use a consistent naming convention for your feature branches to identify the work done in the branch. You can also include other information in the branch name, such as who created the branch, e.g.
- feature/feature-name
- bugfix/description
- hotfix/description

## Review and merge code with pull requests
The review that takes place in a pull request is critical for improving code quality. Only merge branches through pull requests that pass your review process. Avoid merging branches to the main branch without a pull request.

Reviews in pull requests take time to complete. Your team should agree on what's expected from pull request creators and reviewers. Distribute reviewer responsibilities to share ideas across your team and spread out knowledge of your codebase.

Some suggestions for successful pull requests:

- At least one reviewer should be required.
- Take care assigning the same reviewers to a large number of pull requests. Pull requests work better when reviewer responsibilities are shared across the team.
- Provide enough detail in the description to quickly bring reviewers up to speed with your changes.

##Keep a high quality, up-to-date main branch
The code in your main branch should pass tests, build cleanly, and always be current. Your main branch needs these qualities so that feature branches created by your team start from a known good version of code.



# How to Work in Fabric

To change the branch, you have to klick on following buttons/icons:
![image.png](/.attachments/image-13900407-c7b6-4e03-b7df-552cea27b855.png)

## Checkout new branch
In Fabric it's not possible to work in one workspace with multiple branches.
Therefore, this option should only be used for environment setup tasks like creating the initial folder or Lakehouse structure.

## Branch out to new workspace
This option is the preferred option to work in independent branches for multiple users/stories.
A new workspace is created and should be deleted after the PR is finalized.
The branch name should contain the user story name and a description, e.g.
- feature/u123_description

**The workspace name should be similar to the branch name, but not contain any special characters except underscore _**, e.g.
- feature_u123_description
 
![image.png](/.attachments/image-2561b36a-5726-42fa-a733-a600f5f79e8f.png)

###Change Workspace Setting
After "Branch out to new workspace" open the workspace settings and change the "Spark settings" to enable high concurrency: 
 
![image.png](/.attachments/image-a4cceefd-13e2-44b0-81b1-277ac89f4409.png)

## Update/Commit Changes
To update or commit the changes, select following view:
![image.png](/.attachments/image-88460096-e530-4c99-8277-5fd3934f61e9.png)

##Merge via pull request
A pull request must be created and approved to merge the changes back into main branch.
Don't forget to switch to a different branch in Fabric before deleting the branch if you work in the original workspace.

#Know Issues

###Avoid special characters in workspace, lakehouse and table names
To avoid unexpected behavior, you should avoid special characters (expect underscore _ ) in workspace, lakehouse and table names.

###No Folder support
Currently folders are not supported. Therefore, you will not see any folders after branch out.
You can create folders and move items into folders directly in the main branch as workaround.
 

###Don't delete active feature branch 
- A feature branch mustn't be deleted before the main branch or a different existing branch is chosen again in Fabric 
###Branch out to new workspace error(s)
- Branch out to new workspace will stop with an error like:
![image.png](/.attachments/image-6f66cad6-693d-41fd-a2ff-4bcd2bb4443f.png)
Please check permissions on Data Sources of Copy Pipeline. **If the user doesn't have permissions on all used data sources and destinations, the Branch out to new workspace will fail.**
###Main Branch - Unable to complete update request
After clicking on update all on the main branch (after PR finalization) following error is shown:
![image.png](/.attachments/image-3990d846-4de2-4f3d-aa02-4e58ee5f40da.png)
This happens if a reference is missing to a different artefact, e.g. pipeline.
A possible solution is described here:

[Solution - Main Branch - unable to update](/ODP/Implementation-Guidelines-and-Concepts/Fabric-Git-Integration/Solution-%2D-Main-Branch-%2D-unable-to-update)

