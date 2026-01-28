[[_TOC_]]

# Introduction
You will find different options/pattern to integrate SAP Hana on this page.
Please consider also the chapter "Architectural Considerations" for final decisions!

| Key | Value |
|:----|:------|
|Data Source | SAP SAC - Rest |
|Network | SAC is public internet |
| Authorization | Technical User |
| Power BI Gateway required | No |
| Fabric native support | Yes - Webactivity/Notebooks |
| Workaround Method | -- n/a -- |
| Fabric availability ETA | -- n/a -- |
| MSFT documneation | |
| Supported Fabric Items ||
| Permissions Required Connection Creation | | 
| Permissions Required Connection Usage | | 


#Architectural Considerations
- SAP currently only supports SAC Data Exports though the rest api of the report designer API. This is always a full load. 