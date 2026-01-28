#Power BI Gateway in the Fabric architecture

The purpose of the **Power BI Gateway** in **Microsoft Fabric**, as outlined the presentation PBI gateway [LINK](https://atos365.sharepoint.com/:p:/r/sites/100001266/Shared%20Documents/01%20Organisation/KT%20Juergen/PBI%20gateway/PBI%20Gateway.pptx?web=1), is to enable secure and structured connectivity between Power BI and various data sources—both on-premises and cloud-based—within the Fabric ecosystem.

### Core Functions of the PBI Gateway in MS Fabric
1.  **secure Connectivity via VPN and Firewalls**
    The gateway facilitates connections through **VPNs** and **firewalls** to ensure secure access to internal servers and cloud services like Azure, Synapse, and SQL 
2.  **Integration with Diverse Data Sources**
    It supports connections to:
        *   **On-premise servers**
        *   **Clarity systems**
        *   **ADSL2 storage accounts**
        *   **SAP, Nessie, HEC**
        *   **Synapse and VM environments**
        *   **Web services** like **Glow**, **Salesforce**, **Ariba**, and **MS Graph** via REST APIs 
3.  **Specialized Query Support**
    For BP2 connections, only **MDX queries** are supported. These must be implemented in **dataflows** or **Power Query** within Power BI 
4.  **REST API Enablement**
    The gateway enables REST API connections for services like **Mulesoft**, which uses a gateway connection created by Ashwini. Other services like Glow and Ariba do not use the gateway directly
5.  **Operational Infrastructure**
    The gateway operates through specific virtual machines (`GITDTAPRDAS02`) and the gateway instance (`OPgateway-Akela`) with designated IP's or url's of SQL server (e.g. `10.79.199.7`, `akela.database.windows.net`)         .
6.  **Expert Contacts**
    For setup and troubleshooting, the go-to experts are Ravali, Ashwini, Sudheer and Vikas
    The credentials used for the connections managed by Sudheer and Vikas.
7.  **PBI Connections**
The list of used PBI connections created by Juergen in September 2025 is located here [PBI gateway connections](https://atos365.sharepoint.com/:x:/r/sites/100001266/Shared%20Documents/01%20Organisation/KT%20Juergen/PBI%20gateway/PBI%20gateway%20connections.xlsx?d=w3053474ca6974d17a63b90f594549b79&csf=1&web=1&e=G7cfUh)