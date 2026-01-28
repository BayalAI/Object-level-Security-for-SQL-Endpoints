#List of data sources and tables loaded into ODP Fabric

last update 12th December by Juergen Krauth

|original Data Source | loaded Data Source | table | Technologie | Description | Status | use case|
|:----------| :-------|:----|:-----------|:-------|:---------|:---------|
|SAP|Octopus|Aging Balance|Shortcut ADSL2|Basic table from O2C Octopus|Implemented in Dev| APPC|
|SAP|Octopus|ACCOUNT|Shortcut ADSL2|Basic table from O2C Octopus|Implemented in Dev| APPC|
|SAP|Octopus|COMPANY|Shortcut ADSL2|Basic table from O2C Octopus|Implemented in Dev| APPC|
|SAP|Octopus|PROFITCENTER|Shortcut ADSL2|Basic table from O2C Octopus|Implemented in Dev| APPC|
|SAP|Octopus|FISCALPERIOD|Shortcut ADSL2|Basic table from O2C Octopus|Implemented in Dev| APPC|
|SAP|Octopus|PROJECT|Shortcut ADSL2|Basic table from O2C Octopus|Implemented in Dev| APPC|
|SAP|Octopus|WBS_ELEMENT|Shortcut ADSL2|Basic table from O2C Octopus|Implemented in Dev| APPC|
|SAP|Octopus|CUSTOMER|Shortcut ADSL2|Basic table from O2C Octopus|Implemented in Dev| APPC|
|SAP|Octopus|Project Margin|Shortcut Fabric|Basic table from Fabric Finance Project Margin|Implemented in Dev|APPC|
|BUP|BUP|BUP_ER2OM|Lakehouse|manual Excel upload to lakehouse|Implemented in Dev|APPC|
|BUP|BUP|BUP_ER2PM|Lakehouse|manual Excel upload to lakehouse|Implemented in Dev|APPC|
|SalesRally|SalesRally|SAC_SalesRally|SQL Connector|Exported from SAC and loaded to SQL server|Implemented in Dev|APPC|
|Salesforce|Salesforce|Account|Fabric Connector|Object from Salesforce|Implemented in Dev|tdb|
|Salesforce|Salesforce|Opportunity|Fabric Connector|Object from Salesforce|Implemented in Dev|tdb|
|Salesforce|Salesforce|User|Fabric Connector|Object from Salesforce|Implemented in Dev|tdb|
|Salesforce|Salesforce|Product|Fabric Connector|Object from Salesforce|Implemented in Dev|tdb|
|Salesforce|Salesforce|Campaign|Fabric Connector|Object from Salesforce|Implemented in Dev|tdb|
|Salesforce|Salesforce|Lead|Fabric Connector|Object from Salesforce|Implemented in Dev|tdb|
|Salesforce|Salesforce|AccountContactRelation|Fabric Connector|Object from Salesforce|Implemented in Dev|tdb|
|Salesforce|Salesforce|AccountTeamMember|Fabric Connector|Object from Salesforce|Implemented in Dev|tdb|
|Salesforce|Salesforce|CampaignInfluenceModel|Fabric Connector|Object from Salesforce|Implemented in Dev|tdb|
|Salesforce|Salesforce|CampaignMember|Fabric Connector|Object from Salesforce|Implemented in Dev|tdb|
|Salesforce|Salesforce|CampaignMemberStatus|Fabric Connector|Object from Salesforce|Implemented in Dev|tdb|
|Salesforce|Salesforce|Contact|Fabric Connector|Object from Salesforce|Implemented in Dev|tdb|
|Salesforce|Salesforce|CurrencyType|Fabric Connector|Object from Salesforce|Implemented in Dev|tdb|
|Salesforce|Salesforce|OpportunityContactRole|Fabric Connector|Object from Salesforce|Implemented in Dev|tdb|
|Salesforce|Salesforce|OpportunityLineItem|Fabric Connector|Object from Salesforce|Implemented in Dev|tdb|
|Salesforce|Salesforce|OpportunityTeamMember|Fabric Connector|Object from Salesforce|Implemented in Dev|tdb|
|Ariba|Ariba Guided buying|Purchase requests|Rest API|Extracted via Rest Api and Json unfolded|Implemented in Dev|tbd|
|Ariba|Ariba Guided buying|Sourcing|Rest API|Extracted via Rest Api and Json unfolded|Implemented in Dev|tbd|
|Diarie|Diarie|LineItemMonthlySavingsEvolution|SQL Connector|Extracted SQL Server|Implemented in Dev|tbd|
|Diarie|Diarie|TargetMonthlySavingsEvolution|SQL Connector|Extracted SQL Server|Implemented in Dev|tbd|
|IRIS|IRIS|IRIS raw data|SQL Connector|Extracted by Automation Team and loaded to SQL server|Implemented in Dev|tbd|

