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
| design document                                               |                                 |
| Desktop front-end                                             |               42                |
| &nbsp;&nbsp;  UI Login-page                                   |               3                 |
| &nbsp;&nbsp;  Dashboard page                                  |               8                 |
| &nbsp;&nbsp;  Catalogue page                                  |               6                 |
| &nbsp;&nbsp;  Inventory page                                  |               6                 |
| &nbsp;&nbsp;  Sales page                                      |               5                 |
| &nbsp;&nbsp;  Orders page                                     |               4                 |
| &nbsp;&nbsp;  Accounting page                                 |               4                 |
| &nbsp;&nbsp;  Profile page                                    |               3                 |
| &nbsp;&nbsp;  Notification page                               |               3                 |
| Backend                                                       |                                 |
| &nbsp;&nbsp;  Authentication                                  |               15                |
| &nbsp;&nbsp;&nbsp;  set username-password                     |               3                 |
| &nbsp;&nbsp;&nbsp;  change username-password                  |               4                 |
| &nbsp;&nbsp;&nbsp;  verification                              |               4                 |
| &nbsp;&nbsp;&nbsp;  encryption                                |               4                 |
| &nbsp;&nbsp;  Csv management                                  |               7                 |
| &nbsp;&nbsp;&nbsp;  csv read                                  |               2                 |
| &nbsp;&nbsp;&nbsp;  csv write                                 |               2                 |
| &nbsp;&nbsp;&nbsp;  csv download                              |               3                 |
| &nbsp;&nbsp;  Order management                                |               14                |
| &nbsp;&nbsp;&nbsp;  CRUD operations over orders               |               10                |
| &nbsp;&nbsp;&nbsp;  send order request                        |               4                 |
| &nbsp;&nbsp;&nbsp;  update order status                       |               4                 |
| &nbsp;&nbsp;  API design                                      |               10                |
| &nbsp;&nbsp;  Orders suggestion                               |               9                 |
| &nbsp;&nbsp;&nbsp;  retrieve low-stock products               |               2                 |
| &nbsp;&nbsp;&nbsp;  retrieve suppliers                        |               3                 |
| &nbsp;&nbsp;&nbsp;  suggest order                             |               2                 |
| &nbsp;&nbsp;&nbsp;  add order to suggested ones               |               2                 |
| &nbsp;&nbsp;  Accounting management                           |               4                 |
| &nbsp;&nbsp;&nbsp;  manage invoices                           |               2                 |
| &nbsp;&nbsp;&nbsp;  perform analysis balance-expences         |               2                 |
| &nbsp;&nbsp;  Check internet connection                       |               2                 |
| &nbsp;&nbsp; Manage  Notifications                            |                                 |
| &nbsp;&nbsp;&nbsp;  generate notification                     |                                 |
| &nbsp;&nbsp;&nbsp;  manage user interaction with notifications|                                 |                                   
| &nbsp;&nbsp;  Sales management                                |                                 |
| &nbsp;&nbsp;&nbsp;  read barcode                              |                                 |
| &nbsp;&nbsp;&nbsp;  find products                             |                                 |
| &nbsp;&nbsp;&nbsp;  compute discount (from 0% to 90%)         |                                 |
| &nbsp;&nbsp;&nbsp;  generate receipt                          |                                 |
| &nbsp;&nbsp;&nbsp;  save sale                                 |                                 |
| &nbsp;&nbsp;  Inventory management                            |                                 |
| &nbsp;&nbsp;&nbsp;  CRUD operations over batches              |               5                 |
| &nbsp;&nbsp;&nbsp;  find batches near expiring date           |                                 |
| &nbsp;&nbsp;&nbsp;  find expired batches                      |                                 |
| &nbsp;&nbsp;  Catalogue management                            |                                 |
| &nbsp;&nbsp;&nbsp;  CRUD operations over catalogue            |               5                 |
| &nbsp;&nbsp;&nbsp;  set threshold                             |                                 |
| Database                                                      |                                 |


_since CRUD operations may be modulated, only the first time higher person hours count is considered_

Estimated duration: (calendar time)

# Estimate by activity decomposition + Gantt chart

###
step 1: activities (WBS), step 2 Gantt chart
| Activity name | Estimated effort (person hours) |
| ------------- | ------------------------------- |
|               |                                 |



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
