# Project Estimation

Date:

Version:

# Estimation approach

Consider the EZShop project as described in your requirements document, assume that you are going to develop the project INDEPENDENT of the deadlines of the course, and from scratch

# Estimation by size

###

|                                                                                                         | Estimate    |
| ------------------------------------------------------------------------------------------------------- | --------    |
| NC = Estimated number of classes to be developed                                                        |  11         |
| A = Estimated average size per class, in LOC                                                            |  457        |
| S = Estimated size of project, in LOC (= NC \* A)                                                       |  5944       |
| E = Estimated effort, in person hours (here use productivity 10 LOC per person hour)                    |595 ph       |
| C = Estimated cost, in euro (here use 1 person hour cost = 30 euro)                                     |17850euro    |
| Estimated calendar time, in calendar weeks (Assume team of 5 people, 8 hours per day, 5 days per week ) |  3          |


### classes are: 
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

# Estimation by Function Points
In order to give a more precise forecast of the size of our project we can do an estimation using FP.\
Here are presented the evaluation of the various components with the associated weights.
### External Inputs (EI)
| ID  | Description                                         | Complexity | Weight |
|:---:|:----------------------------------------------------|:-----------|:-------:|
| EI1 | Read sale from cash register                        | Avg        | 4      |
| EI2 | Import sales/product/batch/order CSV                | High       | 6      |
| EI3 | CRUD Catalogue                                      | Avg        | 4      |
| EI4 | CRUD Inventory (Batches)                            | Avg        | 4      |
| EI5 | CRUD Orders                                         | Avg        | 4      |
| EI6 | CRUD Notifications                                  | Low        | 3      |
| EI7 | CRUD Cash Registers                                 | Low        | 3      |
| EI8 | Set / Change Password                               | Low        | 3      |
| EI9 | Authenticate / Verify Password                      | Avg        | 4      |
| EI10| Import products list from .csv                      | High       | 6      |
| EI11| Import batches list from .csv                       | High       | 6      |
| EI12| Import orders list from .csv                        | High       | 6      |
| EI13| Import refunds list from .csv                       | High       | 6      |
| EI14| Import suppliers list from .csv                     | Avg        | 4      |
| EI15| Import invoices list from .csv                      | Avg        | 4      |
| EI16| Link POS provider (redirect to auth URL)            | Avg        | 4      |
| EI17| Retrieve access & refresh token (POS)               | Avg        | 4      |
| EI18| Encrypt access token / store securely               | Avg        | 4      |
| EI19| Retrieve new token when expired (POS)               | Avg        | 4      |
| EI20| Push catalogue to cash register (convert + send)    | Avg        | 4      |
| EI21| Pull sales list from cash registers (manual/API)    | Avg        | 4      |
| EI22| Detect import errors / schema mismatch (CSV import) | Low        | 3      |
| EI23| Add suggested order to orders list                  | High       | 6      |

**Total EI = 103**

---

### External Outputs (EO)
| ID  | Description                                               | Complexity | Weight |
|:---:|:----------------------------------------------------------|:-----------|:------:|
| EO1 | Update Catalogue to Cash Register                         | Avg        | 5      |
| EO2 | Export lists to CSV                                       | Avg        | 5      |
| EO3 | Send updated catalogue                                    | Avg        | 5      |
| EO4 | Generate order suggestion                                 | High       | 7      |
| EO5 | Compute and display balance reports                       | High       | 7      |
| EO6 | Retrieve invoices and incomes/outgoings reports           | Avg        | 5      |
| EO7 | Export products list as .csv                              | Avg        | 5      |
| EO8 | Export batches list as .csv                               | Avg        | 5      |
| EO9 | Export refunds list as .csv                               | Avg        | 5      |
| EO10| Export orders list as .csv                                | Avg        | 5      |
| EO11| Export suppliers list as .csv                             | Avg        | 5      |
| EO12| Export invoices list as .csv                              | Avg        | 5      |
| EO13| Send confirmation / notification after catalogue push     | Avg        | 5      |

**Total EO = 69**

---

### External Inquiries (EQ)
| ID  | Description                                                       | Complexity | Weight |
|:---:|:------------------------------------------------------------------|:-----------|:------:|
| EQ1 | Retrieve filtered sales/products/batches/orders/invoices          | Avg        | 4      |
| EQ2 | Retrieve ranked sales                                             | Avg        | 4      |
| EQ3 | Retrieve number of items available per product                    | Low        | 3      |
| EQ4 | Retrieve order status                                             | Low        | 3      |
| EQ5 | Retrieve income/expense/balance history                           | Avg        | 4      |
| EQ6 | Retrieve filtered refunds / refunds by product                    | Avg        | 4      |
| EQ7 | Retrieve ranked refunds (by items / amount)                       | Avg        | 4      |
| EQ8 | Retrieve suppliers list filtered by product                       | Avg        | 4      |
| EQ9 | Retrieve suppliers ranked by associated purchase orders           | Avg        | 4      |
| EQ10| Retrieve shipping companies filtered by attributes                | Avg        | 4      |
| EQ11| Retrieve shipment/tracking status from courier API                | Avg        | 4      |
| EQ12| Retrieve products below threshold (for suggestions)               | Avg        | 4      |

**Total EQ = 46**

---

### External Interface Files (EIF)
| ID   | Description                      | Complexity | Weight |
|:----:|:----------------------------------|:-----------|:------:|
| EIF1 | Cash register API data            | Avg        | 7      |
| EIF2 | Supplier API data                 | Avg        | 7      |
| EIF3 | External CSV files                | Low        | 5      |
| EIF4 | Shipping / Courier API data       | Avg        | 7      |

**Total EIF = 26**

---

### Internal Logical Files (ILF)
| ID   | Description                        | Complexity | Weight |
|:----:|:-----------------------------------|:-----------|:------:|
| ILF1 | Sales                              | Avg        | 10     |
| ILF2 | Catalogue                          | Avg        | 10     |
| ILF3 | Inventory (Batches)                | Avg        | 10     |
| ILF4 | Orders                             | Avg        | 10     |
| ILF5 | Invoices                           | Avg        | 10     |
| ILF6 | Accounting data                    | Avg        | 10     |
| ILF7 | Users / Owner credentials          | Low        | 7      |
| ILF8 | Notifications                      | Low        | 7      |
| ILF9 | Cash Registers list                | Low        | 7      |
| ILF10| Refunds                            | Avg        | 10     |
| ILF11| Suppliers                          | Avg        | 10     |
| ILF12| Shipping Companies                 | Avg        | 10     |

**Total ILF = 111**

---

## Total UFP - Unadjusted Function Points

- EI = 103  
- EO = 69  
- EQ = 46  
- EIF = 26  
- ILF = 111  

**Grand Total = 355 UFP**\
It is needed to calculate the Adjusted Function Points in order to provide a more accurate measure of the\
project's scope. For this reason, Technical Complexity Factors and Environmental Complexity Factors are\
needed to adjust the UFP.

## Technical Complexity Factors (TCF) — Values and Justifications
**TCF = 0.6 + (0.01 * TFW)**\
TFW stands for Technical Factor Weight
- It's calculated starting from 14 Technical Complexity Factors **T**

| ID  | Factor (T)                | Value (0–5) | Short justification                                                                 |
|:---:|:--------------------------|:-----------:|:-----------------------------------------------------------------------------------|
| T1  | Data communications       | 4           | Many POS / courier integrations → significant API data exchanges.                 |
| T2  | Distributed processing    | 2           | Logic mainly centralized; a few distributed components.                           |
| T3  | Performance               | 4           | Response time and catalogue/sales synchronization are time-sensitive.            |
| T4  | Heavily used configuration| 3           | Medium/high backend loads during peak periods.                                    |
| T5  | Transaction rate          | 4           | High number of transactions from cash registers / periodic imports.               |
| T6  | Online data entry         | 3           | Online entries for orders/stock/users but not massive.                            |
| T7  | End-user efficiency       | 3           | Usability requirements important for owners/operators.                           |
| T8  | Online update             | 4           | Catalogue and inventory updates in real time toward POS.                         |
| T9  | Complex processing        | 3           | Moderate logic: suggestions, reporting, reconciliations.                          |
| T10 | Reusability               | 2           | Some components reusable; not a driving requirement.                              |
| T11 | Installation ease         | 2           | Deployment involves tokens/encryption; not straightforward.                       |
| T12 | Operational ease          | 3           | Monitoring and notifications required; moderate operational needs.               |
| T13 | Multiple sites            | 3           | Multiple cash registers and potentially multiple sites → multi-site support.     |
| T14 | Facilitate change         | 4           | System must be easily modifiable / extensible.                                    |
|   ||**TOTAL TFW=44**

**TCF = 0.6+(0.01*44) = 1.04**

## Environmental Complexity Factors (ECF) — Values and Justifications
**ECF=1.4+(-0.03*EF)**
| ID  | Factor                           | Value (0–5) | Justification                                                                 |
|:---:|:---------------------------------|:-----------:|:-------------------------------------------------------------------------------|
| E1  | Familiarity with programming     | 4           | All team members have degrees in Computer Science/Engineering; good language knowledge. |
| E2  | Application experience           | 3           | Moderate experience with similar applications (management/POS) in university projects. |
| E3  | Analyst capability               | 4           | Good requirements analysis skills thanks to academic background.              |
| E4  | Software engineering capability  | 4           | Good theoretical knowledge and university practice; limited industrial support. |
| E5  | Virtual machine experience       | 2           | Use of VMs and virtualized environments for courses; limited industrial experience. |
| E6  | Programming language experience  | 4           | Solid knowledge of main languages (Java, Python, SQL).                         |
| E7  | Motivation                       | 4           | Team is motivated and engaged in the project.                                  |
| E8  | Stability of requirements        | 3           | Requirements defined in course documents, but some details may change.        |
|||**TOTAL EF=28**

**ECF=1.4+(-0.03*28)=0.56**

## AFP - Adjusted Function Points
Given the values calculated in the previous sections we can finally evalute the AFP as:\
**AFP =UFP * TCF * ECF = 355 * 1.04 * 0.56= 206,75**\
Assuming that the project will be devolped using Python as coding language, with an\
an estimation of about *25 LOC/FP* we can forecast a total of about\
**AFP * 25=206.75 * 25 = 5169 LOC**





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