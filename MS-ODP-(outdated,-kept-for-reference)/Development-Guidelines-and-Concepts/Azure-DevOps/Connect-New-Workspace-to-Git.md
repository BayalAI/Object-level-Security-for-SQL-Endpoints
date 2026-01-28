**Draft - Description will be added soon....**

This page lists down steps on how to connect your Azure Devops To Git.


Come to workspace settings and select the Git Integration option
![image.png](/.attachments/image-92489231-f15d-4da4-9d86-ff348d483bd2.png)

Ensure your azure active directory account is correct and click on connect
![image.png](/.attachments/image-91f31576-254c-4d26-9eb9-5d09e77f0f11.png)
Now You can see your Git integration is done. To test branching out to a new branch, select on branch create a new branch
![image.png](/.attachments/image-3200fce5-f95b-4212-9b98-42106774c7d9.png)
Ensure that the new branch is always created from "main" branch
![image.png](/.attachments/image-0acc6a71-7d58-44ea-9258-676f8b1b677e.png)
For GIT folder give your intended git folder name. If you want to create a new folder enter the name of the folder and on connecting you will be prompted to "create and sync" as the folder dosent exist. Go ahead and do that
![image.png](/.attachments/image-f4327dc0-1bba-4210-b4fa-327430670f34.png)

![image.png](/.attachments/image-1a3fa0c6-8455-4b1a-9235-a387373b2fc1.png)


-----
Now after making changes in your sample branch, (always branch out to a new branch and work, and then create a merge request to the main branch, this allows your work to be reviewed and less chances of committing errors to main branch) create a pull request

![image.png](/.attachments/image-6360f997-8c67-464d-b487-157c6f8c5fc8.png)

![image.png](/.attachments/image-ff83f5fe-bcbe-44b4-8a13-78741a438065.png)

![image.png](/.attachments/image-e8ac771c-4749-4b15-97bd-46ded1d2cc58.png)
Select type Squash commit
![image.png](/.attachments/image-c7fcf83a-0f7b-43b9-8f87-b927c36890c0.png)

-----


![image.png](/.attachments/image-dfd4c89d-e2cb-429b-98df-bdfd4c7a11b5.png)

![image.png](/.attachments/image-302dc0d2-a135-41e1-b53e-df3487c2d91d.png)

![image.png](/.attachments/image-8da2f4e0-12c5-47c3-9a33-23f279e32c38.png)

------

![image.png](/.attachments/image-7378f019-f80f-4ce9-9619-f09ef12f5c31.png)


