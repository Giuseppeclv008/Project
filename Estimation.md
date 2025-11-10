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

| component name       | Estimated effort (person hours) |
| -------------------- | ------------------------------- |
| requirement document |                                 |
| Desktop front-end                 |                                 |
| &nbsp;&nbsp;UI Login-page |                        |
| &nbsp;&nbsp; Dashboard page     |                         |
| &nbsp;&nbsp; Catalogue page      |                      |
| &nbsp;&nbsp; Inventory page      |                      |
| &nbsp;&nbsp; Sales page      |                      |
| &nbsp;&nbsp; Orders page      |                      |
| &nbsp;&nbsp; Accounting page      |                      |
| &nbsp;&nbsp; Profile page      |                      |
| &nbsp;&nbsp; Notification page      |                      |
| Backend                       |                                 |
| &nbsp;&nbsp; Authentication      |                      |
| &nbsp;&nbsp;&nbsp; set username-password                   |                                 |
| &nbsp;&nbsp;&nbsp; change username-password                   |                                 |
| &nbsp;&nbsp;&nbsp; verification                  |                                 |
| &nbsp;&nbsp;&nbsp; encryption                   |                                 |
| &nbsp;&nbsp; Csv management                     |                                 |
| &nbsp;&nbsp; API for tracking orders                       |                                 |
| &nbsp;&nbsp; Orders suggestion |                      |
| &nbsp;&nbsp;&nbsp; retrieve low-stock products                   |                            
| &nbsp;&nbsp;&nbsp; retrieve suppliers                   |                                   |
| &nbsp;&nbsp;&nbsp; suggest order                   |                                   |
| &nbsp;&nbsp;&nbsp; add order to suggested ones                   |                                   |
| &nbsp;&nbsp; Accounting management                       |                                 |
| &nbsp;&nbsp; Software management                      |                                 |
| &nbsp;&nbsp;&nbsp; Check internet connection                    |                                 |
| &nbsp;&nbsp; Manage Notifications                    |                                 |
| &nbsp;&nbsp;&nbsp; generate notification                   |                                   |
| &nbsp;&nbsp;&nbsp; manage user interaction with notification                   |                                   |

| &nbsp;&nbsp; Cash register management                   |                                 |
| Database                      |                                 |

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
