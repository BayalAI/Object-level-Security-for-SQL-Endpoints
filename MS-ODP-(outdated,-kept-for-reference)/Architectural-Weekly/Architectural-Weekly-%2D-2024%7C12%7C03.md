# Participants
@<8028F629-D116-6CA1-8EA1-C0E7ACC5A839> 
@<A26E216D-1956-6CE2-8B9B-3DF2D403AD6B> 
@<F2DE3148-CBA1-6AFF-B0D2-DE79E6EFE81C> 


# Agenda
| Topic | Issued By | Description |Priority|
|:------|:----------|:------------|:----------|
| APPC Workspace Setup & Data Sharing | @<A26E216D-1956-6CE2-8B9B-3DF2D403AD6B>  | | 1 | 
| Workspace Usecase Strategy | @<8028F629-D116-6CA1-8EA1-C0E7ACC5A839>  || 2 |
| Data Lab Architecture| @<8028F629-D116-6CA1-8EA1-C0E7ACC5A839> | | 3 |
| Backlog Fillup | @<F2DE3148-CBA1-6AFF-B0D2-DE79E6EFE81C>  | | 4 |
| Handover Requirements | @<F2DE3148-CBA1-6AFF-B0D2-DE79E6EFE81C>  | | 5 | 

# Topic APPC Workspace 
- Driver License needs to be completed
  - to be teach by Angel
- APPC Decidsion
  - Finance LAkehouse in Gold WS
  - APPC Lakehouse in Gold WS Too
  - APPC Lakeohouse in UC WS + onelake shortcut to appc gold lakehouse
  - Create app/report in UC WS and give item level access to viewers via Azure Entra Id Security Groups

- appc uc ws dev  -> finance_gold ws prod
- appc uc ws prod -> finance_gold ws prod

UC workspaces should always use shortcut to production WS 

- Connection/ITem ownership after deleting account?
  - what happen to shortcuts created by deleted account?
  - TODO @<F2DE3148-CBA1-6AFF-B0D2-DE79E6EFE81C> 

# Topic APPC ML Extract
- To be done in APPC gold in IT WS
- shortcut to appc uc ws 
- then create dataset in azure ml from onelake (appointment with niama) @<F2DE3148-CBA1-6AFF-B0D2-DE79E6EFE81C> 

# Topic Handover Requirements
- KT 
  - DevOps run & impelmentation 
  - KeyVault Setup review
  - Permissions done within user story
  - (Network discussion with Dagwin) more internal discussion 
  - APPC Spark Code handover (jürgen + andre) / ML Extract 
  - Internal operation landing zone (gateway) (more internally)
  - review comments by archi done on Wiki discussion pane for all pages
