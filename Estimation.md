# Project Estimation

Date:

Version:

# Estimation approach

Consider the EZShop project as described in your requirements document, assume that you are going to develop the project INDEPENDENT of the deadlines of the course, and from scratch

# Estimate by size

###

|                                                                                                         | Estimate    |
| ------------------------------------------------------------------------------------------------------- | --------    |
| NC = Estimated number of classes to be developed                                                        |  11         |
| A = Estimated average size per class, in LOC                                                            |  457        |
| S = Estimated size of project, in LOC (= NC \* A)                                                       |  5944       |
| E = Estimated effort, in person hours (here use productivity 10 LOC per person hour)                    |595 ph       |
| C = Estimated cost, in euro (here use 1 person hour cost = 30 euro)                                     |17850euro    |
| Estimated calendar time, in calendar weeks (Assume team of 5 people, 8 hours per day, 5 days per week ) |  3          |


###classes are: 
- User
- Sale
- Order
- Product
    - Batch
    - item (inside either batch or product, it has the same characteristics)
- Inventory
- Catalogue
- Accounting (all these below are attributes)
    - _balance_
    - _taxes (10% of income)_
    - _expenses_
    - _income_
- Invoice
- Product supplier (since its contact are saved and the system must use them)
- Payment (since we save if it is pending, done, its date etc)
- cash register
- 




# Estimate by product decomposition

###

| component name                                                | Estimated effort (person hours) |
| ------------------------------------------------------------  | ------------------------------- |
| requirement document                                          |               50                |
| design document                                               |               20                |
| _Desktop front-end_                                           |               42                |
| &nbsp;&nbsp;  UI Login-page                                   |               3                 |
| &nbsp;&nbsp;  Dashboard page                                  |               8                 |
| &nbsp;&nbsp;  Catalogue page                                  |               6                 |
| &nbsp;&nbsp;  Inventory page                                  |               6                 |
| &nbsp;&nbsp;  Sales page                                      |               5                 |
| &nbsp;&nbsp;  Orders page                                     |               4                 |
| &nbsp;&nbsp;  Accounting page                                 |               4                 |
| &nbsp;&nbsp;  Profile page                                    |               3                 |
| &nbsp;&nbsp;  Notification page                               |               3                 |
|_Backend_                                                      |              120                |
| &nbsp;&nbsp; _Authentication_                                 |               15                |
| &nbsp;&nbsp;&nbsp;  set username-password                     |               3                 |
| &nbsp;&nbsp;&nbsp;  change username-password                  |               4                 |
| &nbsp;&nbsp;&nbsp;  verification                              |               4                 |
| &nbsp;&nbsp;&nbsp;  encryption                                |               4                 |
| &nbsp;&nbsp; _Csv management_                                 |               7                 |
| &nbsp;&nbsp;&nbsp;  csv read                                  |               2                 |
| &nbsp;&nbsp;&nbsp;  csv write                                 |               2                 |
| &nbsp;&nbsp;&nbsp;  csv download                              |               3                 |
| &nbsp;&nbsp; _Order management_                               |               20                |
| &nbsp;&nbsp;&nbsp;  CRUD operations over orders               |               10                |
| &nbsp;&nbsp;&nbsp;  send order request                        |               4                 |
| &nbsp;&nbsp;&nbsp;  update order status                       |               4                 |
| &nbsp;&nbsp;&nbsp;  csv import management                     |               6                 |
| &nbsp;&nbsp; _API design_                                     |               10                |
| &nbsp;&nbsp; _Orders suggestion_                              |               9                 |
| &nbsp;&nbsp;&nbsp;  retrieve low-stock products               |               2                 |
| &nbsp;&nbsp;&nbsp;  retrieve suppliers                        |               3                 |
| &nbsp;&nbsp;&nbsp;  suggest order                             |               2                 |
| &nbsp;&nbsp;&nbsp;  add order to suggested ones               |               2                 |
| &nbsp;&nbsp; _Accounting management_                          |               4                 |
| &nbsp;&nbsp;&nbsp;  manage invoices                           |               2                 |
| &nbsp;&nbsp;&nbsp;  perform analysis balance-expences         |               2                 |
| &nbsp;&nbsp; _Check internet connection_                      |               2                 |
| &nbsp;&nbsp; _Manage  Notifications_                          |               8                 |
| &nbsp;&nbsp;&nbsp;  generate notification                     |               5                 |
| &nbsp;&nbsp;&nbsp;  change notifcation status                 |               3                 |                                   
| &nbsp;&nbsp; _Sales management_                               |               10                |
| &nbsp;&nbsp;&nbsp;  read barcode                              |               3                 |
| &nbsp;&nbsp;&nbsp;  find products                             |               3                 |
| &nbsp;&nbsp;&nbsp;  compute discount (from 0% to 90%)         |               2                 |
| &nbsp;&nbsp;&nbsp;  generate receipt                          |               2                 |
| &nbsp;&nbsp;&nbsp;  save sale                                 |               2                 |
| &nbsp;&nbsp; _Inventory management_                           |               11                |
| &nbsp;&nbsp;&nbsp;  CRUD operations over batches              |               5                 |
| &nbsp;&nbsp;&nbsp;  find batches near expiring date           |               3                 |
| &nbsp;&nbsp;&nbsp;  find expired batches                      |               3                 |
| &nbsp;&nbsp; _Catalogue management_                           |               7                 |
| &nbsp;&nbsp;&nbsp;  CRUD operations over catalogue            |               5                 |
| &nbsp;&nbsp;&nbsp;  set threshold                             |               2                 |
| Database                                                      |               17                |


_since CRUD operations may be modulated, only the first time higher person hours count is considered_
_since design can be implemented in many different ways, 20 person hours average is considered as acceptable_

Estimated duration: (calendar time): 31 working days, a month and a week. 

# Estimate by activity decomposition + Gantt chart

###
step 1: activities (WBS), step 2 Gantt chart
| Activity name                                              | Estimated effort (person hours) |
| ---------------------------------------------------------- | ------------------------------- |
| _requirement planning_                                     |                                 |
| &nbsp;&nbsp; define stakeholders                           |                                 |    
| &nbsp;&nbsp; define context diagram and interfaces         |                                 |
| &nbsp;&nbsp; research needed hardware                      |                                 |
| &nbsp;&nbsp; analyse existing similar products             |                                 |
| &nbsp;&nbsp; analyse existing useful APIs                  |                                 |
| &nbsp;&nbsp; define functional requirements                |                                 |
| &nbsp;&nbsp; define non-functional requirements            |                                 |
| &nbsp;&nbsp; write glossary                                |                                 |
| &nbsp;&nbsp; review glossary and requirements              |                                 |
| &nbsp;&nbsp; define use-cases and scenarios                |                                 |
| &nbsp;&nbsp; review use-cases and scenarios                |                                 |
| &nbsp;&nbsp; define system design and hw-sw architecture   |                                 |
| &nbsp;&nbsp; review requirements document                  |                                 |
| _design planning_                                          |                                 |
| &nbsp;&nbsp; analyse requirement document                  |                                 |
| &nbsp;&nbsp; define architecture                           |                                 |
| &nbsp;&nbsp; define coding and convention                  |                                 |
| &nbsp;&nbsp;&nbsp; define repository structure             |                                 |
| &nbsp;&nbsp;&nbsp; choose programming language             |                                 |
| &nbsp;&nbsp;&nbsp; choose frameworks                       |                                 |
| &nbsp;&nbsp; define DBSM                                   |                                 |
| &nbsp;&nbsp;&nbsp; produce ER-model                        |                                 |
| &nbsp;&nbsp;&nbsp; define tables                           |                                 |
| &nbsp;&nbsp;&nbsp; define data integrity                   |                                 |
| &nbsp;&nbsp;&nbsp; define migration strategies             |                                 |
| &nbsp;&nbsp; define security                               |                                 |
| &nbsp;&nbsp;&nbsp; define authentication management        |                                 |
| &nbsp;&nbsp;&nbsp; define data encryption                  |                                 |
| &nbsp;&nbsp;&nbsp; define personal data storage            |                                 |
| &nbsp;&nbsp;&nbsp; define API and network security         |                                 |
| &nbsp;&nbsp; define error handling                         |                                 |
| &nbsp;&nbsp; define testing strategy                       |                                 |











| &nbsp;&nbsp; choose API                                    |                                 |
| &nbsp;&nbsp; define classes                                |                                 |
| &nbsp;&nbsp; define methods                                |                                 |
| &nbsp;&nbsp; produce UML document                          |                                 |








###

## Gantt chart
Insert here Gantt chart

Estimated duration: (calendar time)

# Summary

Report here the results of the three estimation approaches. The estimates may differ. Discuss here the possible reasons for the difference

|                                    | Estimated effort (ph) | Estimated duration (calendar time, relative)|
| ---------------------------------- | ---------------- | ------------------ |
| estimate by size                   |                  |                    |
| estimate by product decomposition  |                  |                    |
| estimate by activity decomposition (Gantt) |          |                    |
