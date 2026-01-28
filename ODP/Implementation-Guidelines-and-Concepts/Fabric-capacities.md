## Workspace overview ##
![image.png](/.attachments/image-a2a81072-117c-430a-82db-fa45de094fa2.png =1200x)
#Production
In production we use these capacities (2025-12-05)
- **fbgitdaprdfabricgewc** Fabric data ingestion capacity with Bronze and Silver Lakehouse and data load procedures
- **fbgitdaprdgoldgewc** Fabric Gold capacity with Gold Lakehouse, semantic model and reports
- **fbgitdaprdppugewc** Fabric pay per use (PPU) capacity with lakehouses, data load procedures, semantic model and reports
- **fbgitdaprdcopilotgewc** Fabric capacity to run Copilot
- **fbgitdaprdcopilotsciagewc** Fabric capacity to run Copilot Agents (Oliver Kopitz)
- **fbgitdaprdfabautomationgewc** Fabric capacity for RPA / Automation team
- **fbgitdaprdfabaiplaygroundne** Fabric capacity for IT /        we have an IT internal capacity where GIT can play around and        Enrique’s team
- **fbgitdaprdcipgewc** Fabric capacity to run WebCIP reports.
- **fbgitdaprdfincopilotgewc** Fabric capacity to run Data Agents.

#Stage
In stage we use only one capacity (2025-10-13)
- **fbgitdastgfabricgewc** Fabric data ingestion capacity with Bronze, Silver, Gold lakehouses, data load procedures, semantic model and reports
- **fbgitdastgfabautomationgewc** Fabric capacity for RPA / Automation team
- **fbgitdastgsnpgewc** Fabric capacity for SNP Project
- **fbgitdaitgewc** Fabric capacity for PISA Mulesoft


Details of the capacity structure documented in the Workspace area

All Fabric Capacities located in the IT-DA-Production subscription. I's needed due to reserved capacity approach.
Below costs are without reserved capacity discount

#Sizing and costs (2025-10-17)
- fbgitdaprdfabricgewc **F64** ~7.680 Euro
- fbgitdaprdgoldgewc **F128** ~ 15.000Euro 
- fbgitdaprdppugewc **F32** ~3.840 Euro
- fbgitdastgfabricgewc **F64** ~ 7.680 Euro
- fbgitdaprdcopilotgewc **F4** ~400 Euro
- fbgitdaprdcopilotsciagewc **F4** ~400 Euro
- fbgitdaprdfabautomationgewc **F16** ~1.600 Euro
- fbgitdastgfabautomationgewc **F16** ~1.600 Euro
- fbgitdaprdfabaiplaygroundne **F16** ~1.864 Euro
- fbgitdaprdcipgewc **F4** ~539 Euro
- fbgitdastgsnpgewc **F4** ~539.62 Euro
- fbgitdaitgewc **F4** ~539.62 Euro

-------------------------

#Compute usage and workload
The workload could be reported with the Fabric capacity report
[PBI report](https://app.powerbi.com/groups/me/reports/6bcd900b-ca5a-436a-b241-c318d3467ddd/ReportSection9acbdaaf706063e57b07?experience=power-bi)
Understand the Fabric capacity report and CU's
[MS Article](https://learn.microsoft.com/en-us/fabric/enterprise/metrics-app-compute-page)

A F64 Capacity provide:
- per second 64 CU
- per minute 3840 CU
- per hour 230400 CU
- per day 5529600 (5 milion CU)
- per month 165888000 (165 million CU)

The dataset below consumed in the last 14 day 1 million CU running in the PPU capacity. The F32 provide 77 million CU in 14 days. the data consume 1 million / 80 million = 1,3 % of the available capacity

![image.png](/.attachments/image-ff78fa91-1c68-41ce-a74e-e6c66813cd36.png =1000x)

##Material from Angel
[Fabric versus PBI capacities]([MS Fabric and PBI Capacities - Comparison_v1.pptx](https://atos365.sharepoint.com/:p:/r/sites/100002399/_layouts/15/Doc.aspx?CID=1f67aaeb-0ceb-f00c-f5d9-04d278d5d6bf&sourcedoc=%7BFA56CEE1-D0CD-4A08-872C-E656D33DA049%7D&file=MS%20Fabric%20and%20PBI%20Capacities%20-%20Comparison_v1.pptx&action=edit&mobileredirect=true&previoussessionid=25100b98-6191-789a-d45a-ac2a7caaaa44))




















