Security Documentations Aspects to be covered


Key Principals involved
- Architecture 
    - Detailed view of the resources and networking involved.
    - An overview of all authentication and authorizations in this Fabric set-up
- Networking
    - use private endpoints/link where possible
    - Use gateways where this is not possible
    - Use Identity protection everywhere
Identity - authentication
    - Always use 2FA authentication
    - Protect public access with Conditional Access
    - Protect power BI (and other ?) traffic with Defender for Cloud Apps
Identity – authorization
    - Have a clear RBAC model for each of the authorization layers: Azure, Azure AD, MS Fabric, …
- Data Security
    - Encryption at rest /transit
    - Sensitive Data Protection ... Dynamic Masking...
    - Data Back-up/Restore 
Compliances on Security that are inherent with Fabric 
In case of any data loss, what are escalation procedures to be aware .


______________________________________________




Defender for Cloud Apps (available in fabric?)
Report Access Management (refer to powerbi)
Conditional Access (prepare scenarios)

Authorization 
-> MFA + EntraID
-> 
 

