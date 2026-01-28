[[_TOC_]]


#Definition of Ready for Data Engineering Development
##Introduction
The "Definition of Ready" (DoR) is a critical component in agile project management, ensuring that stories are fully prepared to be taken up for development. For data engineering development, the DoR helps in maintaining clarity, reducing ambiguities, and ensuring that the development team has all the necessary inputs to start work efficiently.
##Criteria for Definition of Ready
1. Clear Requirements
All requirements should be explicitly stated and well-documented. This includes:
   - Detailed descriptions of the data sources.
   - Specific business logic that needs to be implemented.
   - Acceptance criteria that define when the task is considered complete.

2. Data Availability
The relevant data should be accessible and available for processing. This entails:
   - Ensuring data sources are connected and authenticated.
   - Data quality assessments to confirm data readiness.
   - Availability of sample datasets for testing.
3. Technical Specifications
Technical details must be clear, including:
   - Defined data models and schemas.
   - Data transformation rules and mappings.
   - Infrastructure and environment setup requirements.
4. Dependencies Identified
All dependencies should be identified and managed. This includes:
   - Dependencies on other teams or external systems.
   - Interdependencies within the project stories/tasks.
   - Any blocking issues must be resolved prior to starting the story.
5. Team Alignment
The development team should have a shared understanding of the story. This involves:
   - Conducting pre-development meetings or grooming sessions.
   - Ensuring that each team member is aware of their roles and responsibilities.
   - Clarifying any ambiguities before the story commences.
6. Documentation
Proper documentation should be in place, covering:
   - Requirement documents and technical specifications.
   - Data dictionaries and metadata information.
   - Test cases and validation criteria.
7. Stakeholder Approval
Relevant stakeholders should give their approval before the development begins. This involves:
   - Reviewing and signing off on requirements and specifications.
   - Ensuring stakeholder expectations are aligned with the deliverables.
##Conclusion
A well-defined "Definition of Ready" is essential for the success of data engineering projects. It ensures that all prerequisites are met, reducing the risk of delays and rework. By adhering to the above criteria, data engineering teams can start development tasks with confidence, leading to more efficient and effective project execution.

# Checklist for Epics/Features
 
For the Dev-Team to take on a Use-Case the following minimal requirements need to be met:
 
## Use Case specific
 
- [ ] Detailed Use Case description is documented on Wiki
- [ ] Use Case project team has been identified (Key Users, Testers, PO, local IT support...)
- [ ] Functional Use Case description has been done (which dashboard provides which information)
- [ ] Each Use Case Feature has been documented
- [ ] Use Case Mockup has been built 
- [ ] Personas has been defined
- [ ] User Journey is clear
- [ ] Use Case value is clear
- [ ] Use Case has been prioritized
- [ ] Effort for each PBI has been estimated
 
## Data Specific
 
- [ ] Main Data Sources, Systems or Data Products identified
- [ ] Interoperability between multiple data sources is clear (e.g. primary keys between tables)
- [ ] Status of data availability is clear
- [ ] Status of data quality is clear (bronze, silver, gold)
- [ ] Data view (gold) for the specific use case has been defined in a tabled structure
- [ ] Data which is not available yet has been identified
- [ ] Data history information is clear (last 1,2,3, ... month/years, days)
- [ ] Data update frequency is clear (updates every 10 mins, every 1 hour, every 24 hours, ...)

# Checklist for PBIs
 
The Dev-Team uses Product Backlog Items (PBIs) as the unit of work to be accomplished within one sprint
 
The PBIs should follow the INVEST criteria:
 
|  |  |  |
|--|--|--|
| I | Independent | The PBI should be self-contained, and it should be possible to bring it into progress without a dependency upon another PBI or an external resource. |
| N | Negotiable | A good PBI should leave room for discussion regarding its optimal implementation. |
| V | Valuable    | The value a PBI delivers to stakeholders should be clear. |
| E | Estimable   | A PBI must have a size relative to other PBI |
| S | Small       | PBIs should be small enough to estimate with reasonable accuracy and to plan into a time-box such as a Sprint. |
| T | Testable    | Each PBI should have clear acceptance criteria which allow its satisfaction to be tested. |

 
## PBI ready for refinement
 
PBIs are created in state ```New``` and filled in by the creator.
Everybody can add PBIs.
 
- [ ] Description provides a clear understanding of the content and scope of the PBI
- [ ] Acceptance Criteria provide a clear understanding of how the PBI should be demonstrated
- [ ] Business context and business value are defined
- [ ] If applicable: technical context is defined
- [ ] Creator @mentions reviewers for the PBI
 
-> PBI is tagged with ```Refinement```
 
## PBI ready to be accepted
 
PBIs tagged with ```Refinement``` are discussed during the refinement meeting.
 
- [ ] Description is understood by the Dev-Team
- [ ] Acceptance Criteria are understood by the Dev-Team
 
-> Effort is estimated by the Dev-Team as complexity
 
- [ ] PBI can be finished inside a sprint, otherwise it needs to be broken up
 

-> PBI is eligible to be pulled into a sprint and so can be tagged with a sprint
 
## PBI committed
 
PBIs tagged with a sprint are pulled into the sprint during the sprint planning meeting.
 
-> PBI is set to state ```Active```