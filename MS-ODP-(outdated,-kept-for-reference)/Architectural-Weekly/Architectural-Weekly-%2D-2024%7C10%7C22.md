# Participants
@<F2DE3148-CBA1-6AFF-B0D2-DE79E6EFE81C> 
@<A26E216D-1956-6CE2-8B9B-3DF2D403AD6B> 
@<8028F629-D116-6CA1-8EA1-C0E7ACC5A839> 


# Agenda
| Topic | Issued By | Description | Priority |
|:------|:----------|:------------|:---------| 
|Security Concept| @<F2DE3148-CBA1-6AFF-B0D2-DE79E6EFE81C> | Concept for scenarios | 4| 
|BUP Data Integration| @<F2DE3148-CBA1-6AFF-B0D2-DE79E6EFE81C> | Sharepoint connection via Fabric or Gateway? | 1|
|Treasure Data in Gold Synapse? | @<F2DE3148-CBA1-6AFF-B0D2-DE79E6EFE81C>  | | 2 |
|ML Requirements | @<F2DE3148-CBA1-6AFF-B0D2-DE79E6EFE81C> | Pushed the concrete topics towards GBB for better roadmap overview | 3| 
|HLD Review next week | @<F2DE3148-CBA1-6AFF-B0D2-DE79E6EFE81C>  | Would like to have a review together to understand gap | 5 |
|Operations Zone Integration| @<8028F629-D116-6CA1-8EA1-C0E7ACC5A839> | | 9 |
| Data Sources Sprint 3/4 | @<8028F629-D116-6CA1-8EA1-C0E7ACC5A839>  | | 3 |
 


# BUP Integration 
- data ingestion from sharepoint files - https://atos365.sharepoint.com/:f:/r/sites/AtosIT-Akela/Shared%20Documents/BUP
- Structured data - but dummy data 
- Data Access Pattern to be defined by MSFT this sprint 
- Functional Account: Get Username and Password in KeyVault by @<A26E216D-1956-6CE2-8B9B-3DF2D403AD6B> 

- while onelake extension or filedrop could be a cool final solution fo edgecases, we rather want to do it with notebooks for overall reference implementation standard due to business concerns. 
- MSFT to create BUP workspaces by 22/10/2024

# Topic Treasury Datain Gold
- yes. defined by Atos

# Topic Data Source Sprint 3/4
- SAP HR slip to sprint 3 -> silver can be done in sprint 3
- iris -> bronze to silver
- diariedb -> bronze to silver
- SAP Ariba to be defined by Atos as internal discussions on their reporting strategy are ongoing 
   - create concepts for fabric 
   - if fabric way is easier - then go fabric - else on hold 
- fieldglass -> stories for synapse in sprint 3 , silver in sprint 4
- Operational DLZ Concept 
   - multi tenant from fabric 
   - 