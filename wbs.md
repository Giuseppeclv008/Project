# Estimate by activity decomposition + Gantt chart

###
step 1: activities (WBS), step 2 Gantt chart
| Activity name                                              | Estimated effort (person hours) |
| ---------------------------------------------------------- | ------------------------------- |
| _requirement planning_                                     |                                 |
| &nbsp;&nbsp; define stakeholders                           |               10                |    
| &nbsp;&nbsp; define context diagram and interfaces         |                1                |
| &nbsp;&nbsp; research needed hardware                      |                2                |
| &nbsp;&nbsp; analyse existing similar products             |                1                |
| &nbsp;&nbsp; define functional requirements                |                30               |
| &nbsp;&nbsp; define non-functional requirements            |                2                |
| &nbsp;&nbsp; write glossary                                |                10               |
| &nbsp;&nbsp; review glossary and requirements              |                 3               |
| &nbsp;&nbsp; define use-cases and scenarios                |                25               |
| &nbsp;&nbsp; review use-cases and scenarios                |                 5               |
| &nbsp;&nbsp; define system design and hw-sw architecture   |                 2               |
| &nbsp;&nbsp; review requirements document                  |                 5               |
| _design planning_                                          |               148               |
| &nbsp;&nbsp; analyse requirement document                  |                10               |
| &nbsp;&nbsp; define architecture                           |                10               |
| &nbsp;&nbsp; define coding and convention                  |                25               |
| &nbsp;&nbsp;&nbsp; define repository structure             |                5                |
| &nbsp;&nbsp;&nbsp; choose programming language             |                10               |
| &nbsp;&nbsp;&nbsp; choose frameworks                       |                10               |
| &nbsp;&nbsp; define DBSM                                   |                30               |
| &nbsp;&nbsp;&nbsp; produce ER-model                        |                12               |
| &nbsp;&nbsp;&nbsp; define tables                           |                5                |
| &nbsp;&nbsp;&nbsp; define data integrity                   |                5                |
| &nbsp;&nbsp;&nbsp; define migration strategies             |                8                |
| &nbsp;&nbsp; define security                               |               27                |
| &nbsp;&nbsp;&nbsp; define authentication management        |               10                |
| &nbsp;&nbsp;&nbsp; define data encryption                  |                5                |
| &nbsp;&nbsp;&nbsp; define personal data storage            |                7                |
| &nbsp;&nbsp;&nbsp; define API and network security         |                5                |
| &nbsp;&nbsp; define error handling                         |                5                |
| &nbsp;&nbsp; define testing strategy                       |                5                |
| &nbsp;&nbsp; choose API                                    |                5o               |
| &nbsp;&nbsp; define classes                                |               10                |
| &nbsp;&nbsp; define methods                                |               12                |
| &nbsp;&nbsp; produce UML document                          |               4                 |
| _frontend implementation_                                  |               42                |
| &nbsp;&nbsp; Review visual design                          |               8                 |
| &nbsp;&nbsp; Install libraries                             |               2                 |
| &nbsp;&nbsp; Implement designed visual components          |              10                 |
| &nbsp;&nbsp; Implement filters                             |              10                 |
| &nbsp;&nbsp; Implement interactive components              |              10                 |
| _backend implementation_                                   |                                 |
| &nbsp;&nbsp; _Implement autenticathion section_              |                                 |
| &nbsp;&nbsp;&nbsp; write username-password set logic       |                                 |
| &nbsp;&nbsp;&nbsp; write username-password change logic    |                                 |
| &nbsp;&nbsp;&nbsp; implement secure verification and encryption algorithms    |                                 |
| &nbsp;&nbsp; _Implement CSV management_                      |                                 |
| &nbsp;&nbsp;&nbsp; manage CSV file creation                |                                 |
| &nbsp;&nbsp;&nbsp; manage CSV file read operation          |                                 |
| &nbsp;&nbsp;&nbsp; manage CSV file download operation      |                                 |
| &nbsp;&nbsp;&nbsp; merge CSV information with DB ones      |                                 |
| &nbsp;&nbsp; _write order management and suggestions section_|                                 |
| &nbsp;&nbsp;&nbsp; manage CRUD operations                  |                                 |
| &nbsp;&nbsp;&nbsp; manage requests to suppliers            |                                 |
| &nbsp;&nbsp;&nbsp; manage order status updates             |                                 |
| &nbsp;&nbsp;&nbsp; write algorithm to find items below threshold |                                 |
| &nbsp;&nbsp;&nbsp; write algorithm to suggest orders       |                                 |
| &nbsp;&nbsp;&nbsp; merge suggested orders with existing ones |                                 |
| &nbsp;&nbsp; _Implement accounting management section_       |                                 |
| &nbsp;&nbsp;&nbsp; Implement algorithms to perform financial analysis |                                 |
| &nbsp;&nbsp;&nbsp; implement invoice management            |                                 |
| &nbsp;&nbsp; _Integrate API for the interaction with the cash register_ |                                 |
| &nbsp;&nbsp; _Implement sales management section_            |                                 |
| &nbsp;&nbsp;&nbsp; integrate the barcode reader              |                                 |
| &nbsp;&nbsp;&nbsp; load portion of the DB in the cash register |                                 |
| &nbsp;&nbsp;&nbsp; apply discount if existing                |                                 |
| &nbsp;&nbsp;&nbsp; write code to generate receipt            |                                 |
| &nbsp;&nbsp;&nbsp; write code to save sale                   |                                 |
| &nbsp;&nbsp; _Implement inventory management section_        |                                 |
| &nbsp;&nbsp; _Implement catalogue management section_        |                                 |
| &nbsp;&nbsp; _Implement DBSM_                                |                                 |
| &nbsp;&nbsp; _Write internet connection check logic_         |                                 |