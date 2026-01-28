**Deployment pipelines names**
The authorisation to run a deployment is limited to the group git-odp-deployment.

Deployment pipelines names must start with the name of the workspace. e.g.:
`ODP-SAP-INGEST-STG transport`
`ODP-FIN-MD-STG transport`

Access to all deployment pipeline should be granted to 
`GIT-ODP-ADMIN`

Depending to the domain the deployment must be granted to
`GIT-ODP-DEPLOYMENT-FIN (Ashwini, Eswar)`
`GIT-ODP-DEPLOYMENT-EMP (Thirumala)`
`GIT-ODP-DEPLOYMENT-CUST (Ashwini, Eswar)`


To run successful deployments to production (e.g. Lakehouse) the deployment Azure AD groups or the "deployment person" must have admin access in the production workspace!

**Fabric deployment procedure**
1.	Upcoming changes must be described in front of the deployment in below deployment Excel
2.	IT DA responsible must review all items and insure that naming and guidelines are considered.
3.	All items must be committed to git (Azure devops repository) before deployment
4.	Deployment will happen on Tuesday and Thursday
5.	Each domain has a dedicated Azure AD deployment group
The data engineer is not authorized to execute a transport to production. 
The deployment will be done in a meeting with the data engineer the owner of the deployment group
6.	It is mandatory to enter a description in the deployment with reference to deployment Excel (deployemt number)
7.	Changes with impact to other domains should be communicated in a Teams channel
a.	FIN-MD Master data changes
b.	EMP-PA Employee Master data changes
c.	Changes on ACDOCA
d.	…
8. The changes must be communicated to the domain and sub-domain responsible person.

**Deployment Excel**
[Link](https://atos365.sharepoint.com/:x:/r/sites/100002399/Shared%20Documents/Octopus/02%20Data%20Architecture/99%20organisational/Deployments.xlsx?d=wfdb5d5b88e8a44999842070a2262fb81&csf=1&web=1&e=WV9fEl)
