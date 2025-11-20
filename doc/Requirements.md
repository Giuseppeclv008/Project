

# Requirements Document - EZShop

Date: 24/10/2025
Version: 1.0.0

| Version number | Change |
| :------------: | :----: |
|                |        |

# Contents

- [Requirements Document - EzShop](#requirements-document)
- [Contents](#contents)
- [Informal description](#informal-description)
- [Business model](#business-model)
- [Stakeholders](#stakeholders)
- [Context Diagram and interfaces](#context-diagram-and-interfaces)
  - [Context Diagram](#context-diagram)
  - [Interfaces](#interfaces)
- [Functional and non functional requirements](#functional-and-non-functional-requirements)
  - [Functional Requirements](#functional-requirements)
  - [Non Functional Requirements](#non-functional-requirements)
- [Table of Rights](#table-of-rights)
- [Use case diagram and use cases](#use-case-diagram-and-use-cases)
  - [Use case diagram](#use-case-diagram)
    - [Use case 1, UC1](#use-case-1-uc1)
      - [Scenario 1.1](#scenario-11)
      - [Scenario 1.2](#scenario-12)
      - [Scenario 1.x](#scenario-1x)
    - [Use case 2, UC2](#use-case-2-uc2)
    - [Use case x, UCx](#use-case-x-ucx)
- [Glossary](#glossary)
- [System Design](#system-design)
- [Hardware Software architecture](#Hardware-software-architecture)

# Informal description

Small shops require a simple application to support the owner or manager. A small shop (ex a food shop) occupies 50-200 square meters, sells 500-2000 different item types, has two or a few more cash registers. 
EZShop is a software application to:
* manage sales
* manage inventory
* manage orders to suppliers
* support accounting

In the following describe the requirements of the EZShop application. 
You are free to define the application as you deem more useful and effective for the stakeholders. 
You are also free to modify the structure of the document when needed.
The document will be evaluated considering the typical defects in requirements (omissions, ambiguities, contradictions, etc), and syntactic errors in the formalism used (UML diagrams). 
Consider that the document should be delivered to another team (unknown to you)
 which will be in charge of designing and implementing the system. The design team should be able to proceed only with the information in the document.

# Business Model
- Customer segment
    * Shop manager / owner
- Value proposition
    * Statistics reports
    * Accounting (revenue, costs, debts, ...)
    * Decision support
    * Assistance with logistics
    * Order management to suppliers
- Revenue Stream
    * Yearly fee
    * Privately founded



# Stakeholders

| Stakeholder name | Description |
| :--------------: | :---------: |
| Shop owner | Reviews accounting information and initiates orders to suppliers |
| Cashier | Handles transactions and enters sales info through the cash register |
| Cash register | Feeds data to the application |
| POS provider | Grants access token to identify and comunicate securely with the cash registers |
| Shipment tracking provider | Grants the ability to retrieve the current order's status|
| Desktop OS| The device where the application resides |
| Product suppliers | Business who supply the shop with items |
| Shipping company | Company who delivers the items to the shop|
| DB service supplier | Stores data |
| Development team | Team responsible for the development of the application |
| Maintenance team | Team responsible for the long term support of the application |
| Competitors | Other companies that sell a similar product |

# Context Diagram and interfaces

## Context Diagram
![missing-context-diagram](../res/plantuml/contextDiagram.svg)

## Interfaces

|   Actor   | Logical Interface | Physical Interface |
| :-------: | :---------------: | :----------------: |
| Shop manager | GUI | Desktop computer |
| Cash register | Square, lightspeed, nexi or clover API | Lan connection |
| POS provider | Square, lightspeed, nexi or clover API | Internet connection |
| Shipment tracking provider | easy post API | Internet connection |


# Functional and non functional requirements

## Functional Requirements

\<In the form DO SOMETHING, or VERB NOUN, describe high level capabilities of the system>

\<they match to high level use cases>

| ID | Description |
|:--:|:-------------|
|| |

| ID | Description |
|:--:|:------------|
| FR1 | Manage sales |
| FR1.1 | Create owner-defined sale list |
| FR1.1.1 | For each owner-defined list filter sales by a specified date (ISO 8601) or time window |
| FR1.1.2 | Retrieve sales filtered by products sold |
| FR1.1.3 | Retrieve sales ranked by number of items sold per specific product |
| FR1.1.4 | Retrieve sales ranked by the sum of its item's prices |
| FR1.2 | Manage `.csv` |
| FR1.2.1 | Import sales list from `.csv` |
| FR1.2.1.1 | Detect import errors |
| FR1.2.1.2 | Detect schema mismatch |
| FR1.2.1.3 | Update sales |
| FR1.2.2 | Export list of sales as `.csv` |
| FR1.2.2.1 | Retrieve sales |
| FR1.2.2.2 | Create `.csv` file |
| FR1.2.2.3 | Detect export errors |
| FR2 | Manage refunds |
| FR2.1 | Create owner-defined refund list |
| FR2.1.1 | For each owner-defined list filter refunds by a specified date (ISO 8601) or time window |
| FR2.1.2 | Retrieve refunds filtered by products returned |
| FR2.1.3 | Retrieve refunds ranked by number of items given back per specific product |
| FR2.1.4 | Retrieve refunds ranked by the sum of its item's prices |
| FR2.2 | Manage `.csv` |
| FR2.2.1 | Import refunds list from `.csv`|
| FR2.2.1.1 | Detect import errors |
| FR2.2.1.2 | Detect schema mismatch |
| FR2.2.1.3 | Update refunds |
| FR2.2.2 | Export list of refunds as `.csv`|
| FR2.2.2.1 | Retrieve refunds |
| FR2.2.2.2 | Create `.csv` file |
| FR2.2.2.3 | Detect export errors |
| FR3 | Manage catalogue |
| FR3.1 | Manage CRUD operations |
| FR3.1.1 | Create new product in the catalogue |
| FR3.1.2 | Update product from the catalogue |
| FR3.1.3 | Delete product from the catalogue |
| FR3.2 | Set product item quantity warning threshold |
| FR3.3 | Create owner-defined product list |
| FR3.3.1 | Retrieve list of products filtered by one or more of their attributes |
| FR3.3.2 | Retrieve number of items available for a selected product |
| FR3.4 | Manage `.csv` |
| FR3.4.1 | Import products list from `.csv` |
| FR3.4.1.1 | Detect import errors |
| FR3.4.1.2 | Detect schema mismatch |
| FR3.4.1.3 | Update products list |
| FR3.4.2 | Export list of products as `.csv` |
| FR3.4.2.1 | Retrieve products list |
| FR3.4.2.2 | Create `.csv` file |
| FR3.4.2.3 | Detect export errors |
| FR4 | Manage inventory |
| FR4.1 | Manage CRUD operations |
| FR4.1.1 | Create new batch in the inventory |
| FR4.1.2 | Update batch from the inventory |
| FR4.1.3 | Delete batch from the inventory |
| FR4.2 | Create owner-defined batch list |
| FR4.2.1 | Retrieve batches filtered by one or more product/batch attributes |
| FR4.3 | Manage `.csv` |
| FR4.3.1 | Import batches list from `.csv` |
| FR4.3.1.1 | Detect import errors |
| FR4.3.1.2 | Detect schema mismatch |
| FR4.3.1.3 | Update inventory |
| FR4.3.2 | Export list of batches as `.csv` |
| FR4.3.2.1 | Retrieve batches list |
| FR4.3.2.2 | Create `.csv` file |
| FR4.3.2.3 | Detect export errors |
| FR5 | Manage invoices |
| FR5.1 | Manage CRUD operations |
| FR5.1.1 | Create new invoice |
| FR5.1.2 | Update invoice |
| FR5.1.3 | Delete invoice |
| FR5.1.4 | Link invoice to a specific order |
| FR5.2 | Create owner-defined invoice list |
| FR5.2.1 | Retrieve list of invoices filtered by one or more of their attributes |
| FR5.3 | Manage `.csv` |
| FR5.3.1 | Import invoices list from `.csv` |
| FR5.3.1.1 | Detect import errors |
| FR5.3.1.2 | Detect schema mismatch |
| FR5.3.1.3 | Update invoices |
| FR5.3.2 | Export list of invoices as `.csv` |
| FR5.3.2.1 | Retrieve invoices |
| FR5.3.2.2 | Create `.csv` file |
| FR5.3.2.3 | Detect export errors |
| FR6 | Manage suppliers |
| FR6.1 | Manage CRUD operations |
| FR6.1.1 | Create new supplier |
| FR6.1.2 | Update supplier |
| FR6.1.3 | Delete supplier |
| FR6.1.4 | Link supplier to one or more products |
| FR6.1.5 | Unlink supplier from one or more products |
| FR6.1.6 | Link supplier to one or more batches |
| FR6.1.7 | Unlink supplier from one or more batches |
| FR6.2 | Create owner-defined supplier list |
| FR6.2.1 | Retrieve suppliers list filtered by one or more product they provide |
| FR6.2.2 | Retrieve suppliers list ranked by number of associated purchase orders |
| FR6.3 | Manage `.csv` |
| FR6.3.1 | Import supplier list from `.csv` |
| FR6.3.1.1 | Detect import errors |
| FR6.3.1.2 | Detect schema mismatch |
| FR6.3.1.3 | Update suppliers |
| FR6.3.2 | Export list of suppliers as `.csv` |
| FR6.3.2.1 | Retrieve suppliers |
| FR6.3.2.2 | Create `.csv` file |
| FR6.3.2.3 | Detect export errors |
| FR7 | Manage Shipping companies |
| FR7.1 | Manage CRUD operations |
| FR7.1.1 | Create new shipping company |
| FR7.1.2 | Update shipping company |
| FR7.1.3 | Delete shipping company |
| FR7.1.4 | Link shipping company to one or more orders |
| FR7.1.5 | Unlink shipping company from one or more orders |
| FR7.2 | Create owner-defined shipping companies list |
| FR7.2.1 | Retrieve shipping companies list filtered by one or more of their attributes |
| FR7.2.2 | Retrieve shipping companies list ranked by number of associated shipments with a selected status |
| FR7.3 | Manage `.csv` |
| FR7.3.1 | Import shipping companies list from `.csv` |
| FR7.3.1.1 | Detect import errors |
| FR7.3.1.2 | Detect schema mismatch |
| FR7.3.1.3 | Update shipping companies list |
| FR7.3.2 | Export list of shipping companies as `.csv` |
| FR7.3.2.1 | Retrieve shipping companies list |
| FR7.3.2.2 | Create `.csv` file |
| FR7.3.2.3 | Detect export errors |
| FR8 | Track order |
| FR8.1 | Link with easy post account |
| FR8.1.1 | Redirect user to authorization URL |
| FR8.1.2 | Retrieve access and refresh tokens |
| FR8.1.3 | Store access and refresh tokens securely |
| FR8.1.4 | Retrieve new token when expired |
| FR8.2 | Retrieve shipment status |
| FR8.2.1 | Retrieve tracking updates from provider API |
| FR8.2.2 | Update order's status accordingly |
| FR9 | Manage orders |
| FR9.1 | Manage CRUD operations |
| FR9.1.1 | Create new order |
| FR9.1.2 | Update order |
| FR9.1.3 | Delete order |
| FR9.1.4 | Link order to a supplier |
| FR9.1.5 | Unlink order from a supplier |
| FR9.2 | Create owner-defined orders list |
| FR9.2.1 | Retrieve list of orders filtered by one or more attributes |
| FR9.3 | Manage `.csv` |
| FR9.3.1 | Import orders list from `.csv` |
| FR9.3.1.1 | Detect import errors |
| FR9.3.1.2 | Detect schema mismatch |
| FR9.3.1.3 | Update orders |
| FR9.3.2 | Export list of orders as `.csv` |
| FR9.3.2.1 | Retrieve invoices |
| FR9.3.2.2 | Create `.csv` file |
| FR9.3.2.3 | Detect export errors |
| FR9.4 | Suggest order |
| FR9.4.1 | Retrieve products with item count below threshold |
| FR9.4.2 | Retrieve possible supplier for products with item count below threshold |
| FR9.4.3 | Generate order suggestion |
| FR9.4.4 | Add suggested order to the list of orders |
| FR10 | Manage accounting |
| FR10.1 | Track incomes |
| FR10.1.1 | Compute incoming cash flow at different time granularities |
| FR10.1.2 | Retrieve incoming cash flow at different time granularities |
| FR10.2 | Manage incomes `.csv` |
| FR10.2.1 | Import incomes list from `.csv` |
| FR10.2.1.1 | Detect import errors |
| FR10.2.1.2 | Detect schema mismatch |
| FR10.2.1.3 | Update incomes |
| FR10.2.2 | Export list of incomes as `.csv` |
| FR10.2.2.1 | Retrieve incomes |
| FR10.2.2.2 | Create `.csv` file |
| FR10.2.2.3 | Detect export errors |
| FR10.3 | Track expenses |
| FR10.3.1 | Compute outgoing cash flow at different time granularities |
| FR10.3.2 | Retrieve outgoing cash flow at different time granularities |
| FR10.4 | Manage expenses `.csv` |
| FR10.4.1 | Import expenses list from `.csv` |
| FR10.4.1.1 | Detect import errors |
| FR10.4.1.2 | Detect schema mismatch |
| FR10.4.1.3 | Update expenses |
| FR10.4.2 | Export list of expenses as `.csv` |
| FR10.4.2.1 | Retrieve expenses |
| FR10.4.2.2 | Create `.csv` file |
| FR10.4.2.3 | Detect export errors |
| FR10.5 | Track balance |
| FR10.5.1 | Compute total balance at different time granularities |
| FR10.5.2 | Retrieve balance at different time granularities |
| FR10.5.3 | Retrieve current balance |
| FR11 | Authenticate owner |
| FR11.1 | Set password |
| FR11.2 | Change password |
| FR11.3 | Verify password |
| FR11.4 | Encrypt password |
| FR12 | Manage notifications |
| FR12.1 | Create notification |
| FR12.2 | Change notification's status |
| FR12.3 | Delete notification |
| FR13 | Manage cash registers |
| FR13.1 | Link with POS provider’s account |
| FR13.1.1 | Redirect user to authorization URL |
| FR13.1.2 | Retrieve access and refresh tokens |
| FR13.1.3 | Store access and refresh tokens securely |
| FR13.1.4 | Retrieve new token when expired |
| FR13.2 | Get cash register list |
| FR13.2.1 | Retrieve list of cash registers from provider API |
| FR13.2.2 | Update local list of cash registers |
| FR13.3 | Sync catalogue |
| FR13.3.1 | Convert catalogue to provider format |
| FR13.3.2 | Push new catalogue to cash registers |
| FR13.3.3 | Detect unresponsive cash registers and update status |
| FR13.4 | Retrieve sales |
| FR13.4.1 | Retrieve sales list from cash register |
| FR13.4.2 | Update inventory quantities |
| FR13.4.3 | Add sale to sales list |
| FR13.4.4 | Detect unresponsive cash registers |
| FR13.5 | Retrieve refunds |
| FR13.5.1 | Retrieve refunds list from cash register |
| FR13.5.2 | Update item quantities |
| FR13.5.3 | Add refund to refunds list |
| FR13.5.4 | Detect unresponsive cash registers |
| FR13.6 | Create owner-defined cash register list |
| FR13.6.1 | Retrieve cash registers filtered by attributes |
| FR13.6.2 | Retrieve cash registers grouped by provider brand |

## Non Functional Requirements

\<Describe constraints on functional requirements>

|   ID    | Type (efficiency, reliability, ..) | Description | Refers to |
| :-----: | :--------------------------------: | :--------- | :-------: |
| || |

| ID   | Type          | Description | Refers to |
|------|---------------|-------------|-----------|
| NFR1 | Functionality | **Suitability**<br>• All owner needs identified in the use cases should map to at least one functional requirement<br><br>**Accuracy**<br>• Catalogue updates, order-status updates, sales, refunds and similar synchronization operations must achieve a guaranteed delivery rate greater than 99.999 %<br>• Exported `.csv` files should have less than 1 mistaken row every 100'000<br>• Importing `.csv` files should generate less than 1 mistaken row every 100'000<br>• CRUD operations should have less than 1 error every 100'000 operations<br>• Notification should fail to trigger less than 1 every 100'000 expected notifications<br>• Order status should fail to update properly less than 1 time every 100'000 updates<br><br>**Interoperability**<br>• The application should use the square API to pull/push data to square POS<br>• The application should use the lightspeed API to pull/push data to lightspeed POS<br>• The application should use the clover API to pull/push data to clover POS<br>• The application should use the nexi API to pull/push data to nexi POS<br>• The application should use the easy post API to interact with shipping companies and automatically track order status<br>• All functions that may access data concurrently, must be thread-safe<br><br>**Security**<br>• Passwords must be encrypted using AES-256<br>• The application must pass Gitlab SATS without high severity issues (CSVV > 7) being highlighted | |
| NFR2 | Reliability | **Maturity**<br>• The application should crash less than 1 time every 200 hours of operation<br>• The application should suffer less than 1 minor visual glitch (solved by changing/refreshing the current tab) every 50 hours of operation<br><br>**Fault Tolerance**<br>• The application should not crash when Importing `.csv` files without the right format<br>• The application should be able to perform all its operations, beside syncing with cash registers and shipping companies, even without an internet connection<br>• The application should be able to work without crashing even when data read from the cash registers is corrupted, malformed or absent<br>• The application should be able to work without crashing even when data read from the shipping companies' APIs is corrupted, malformed or absent<br>• The application should queue failed API calls and retry every 5 minutes<br>• All multi-steps functions must be atomic; partial updates should be rolled back or notified to the owner | |
| NFR3 | Usability | **Understandability**<br>• The application should display tooltips when hovering over buttons which can be pressed<br>• The application should use consistent design elements and language<br>• The application should follow industry standard practices and conventions<br>• All GUI elements should have a contrast rating greater than 4.5<br><br>**Learnability**<br>• A user with low to moderate digital literacy should be able to learn how to:<br>– navigate the main interface within 5 minutes<br>– correctly import a `.csv` file within 10 minutes<br>– modify how the data is displayed within 10 minutes<br>– add a new product, batch, order, invoice, supplier, shipping company or cash register within 30 minutes<br><br>**Operability**<br>• All CRUD operations should be accessible within 2 clicks<br>• The GUI should be able to respond to user input within 500 ms<br><br>**Usability compliance**<br>• The application should follow WCAG guidelines | |
| NFR4 | Efficiency | **Time Behavior**<br>• All CRUD operations operating on single entities should be completed within 1000 ms<br>• Retrieving ≈ 100 MB of data filtered, sorted or ranked by a specific set of rules should be completed within 10'000 ms<br>• Importing and exporting `.csv` files should take within 10'000 ms every 1000 rows<br>• Order status for supported suppliers should be updated within 3 h from the actual reported change<br>• Sales and refunds should be updated at least every 2 minutes<br>• Catalogue updates should be propagated to all cash registers every day at 6.00 a.m.<br>• Startup time should be within 5'000 ms<br><br>**Resource Utilization**<br>• The application should use no more than 500 MB of disk storage space (excluding data such as orders, sales, refunds, ...)<br>• The application should use no more than 2 GB of RAM memory under expected load<br>• The application should use no more than 50 % of the available CPU resources under normal load on tested hardware (Intel Core i5-8000 or i5-9000 series, 8 G of RAM) | |
| NFR5 | Maintainability | **Analyzability**<br>• 95 % of code functions should be documented<br>• New functions should be documented within 1 week<br>• Mean time to diagnose a defect should be within 1 day<br>• All API errors, sync errors, and critical errors must be logged and persisted<br><br>**Changeability**<br>• Mean time to implement a minor feature should be within 1 working week<br>• Mean time to implement major features should be within 1 months<br>• The cyclomatic complexity of functions should be on average less than 15; no single function should exceed a cyclomatic complexity of 20<br><br>**Stability**<br>• A new release should introduce less than 1 regression defect<br><br>**Testability**<br>• Unit tests should cover 90 % of the codebase<br>• Integration tests should cover 80 % of the codebase | |
| NFR6 | Portability | **Adaptability**<br>• The application should run on Windows 10 and 11 without code modification<br><br>**Installability**<br>• The application should complete installation within 10 minutes on tested hardware<br>• The application should complete installation with a success rate greater than 95 % on tested hardware (Intel Core i5-8000 or i5-9000 series, 8 G of RAM)<br><br>**Co-existence**<br>• The application should be able to run alongside the common antivirus applications (Windows Defender, Avast, McAfee, Norton, BitDefender, Kaspersky, AVG, ESET, Trend Micro, Sophos) without conflicts<br>• The application should be able to perform its functionalities without requiring exclusive system resources access<br>• The application should be able to work alongside firewalls<br><br>**Interoperability**<br>• Future version of the EzShop application should be able to import data in `.csv` format exported from previous version of the application | |




# Table of rights

|  Actor   | FR1         | FRx |
| user     |             | :---: |
|          |             |       |

# Use case diagram and use cases

## Use case brief
|  UC name   | Goal         | Description |
| :---:    | :---------: | :---: |
|          |             |       |



## Use case diagram

\<define here UML Use case diagram UCD summarizing all use cases, and their relationships>

\<next describe here each use case in the UCD>

### Use case 1, UC1

| Actors Involved  |                                                                      |
| :--------------: | :------------------------------------------------------------------: |
|   Precondition   | \<Boolean expression, must evaluate to true before the UC can start> |
|  Post condition  |  \<Boolean expression, must evaluate to true after UC is finished>   |
| Nominal Scenario |         \<Textual description of actions executed by the UC>         |
|     Variants     |                      \<other normal executions>                      |
|    Exceptions    |                        \<exceptions, errors >                        |

##### Scenario 1.1

\<describe here scenarios instances of UC1>

\<a scenario is a sequence of steps that corresponds to a particular execution of one use case>

\<a scenario is a more formal description of a story>

\<only relevant scenarios should be described>

|  Scenario 1.1  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
|  Precondition  | \<Boolean expression, must evaluate to true before the scenario can start> |
| Post condition |  \<Boolean expression, must evaluate to true after scenario is finished>   |


Steps

|     Actor's action      |  System action                                                                    | FR needed |
| :------------: | :------------------------------------------------------------------------: |:---:|
|               |                                                                 |  |
|   |  |  |
##### Scenario 1.2

##### Scenario 1.x

### Use case 2, UC2

### Use case x, UCx


# Glossary
- **Shop**
    * The small business entity that uses the EzShop software to manage its operations, including sales, inventory, orders, and accounting. A shop typically has one owner, two or more cash registers, and several suppliers. In the current scope, EzShop manages a single shop.
- **Product** 
    * An entity representing a type of product sold or stocked by the shop; not a single physical object. Each product describes the characteristics shared by all physical units of that product (e.g., 1L bottle of "GoodMilk!").
- **Batch**
    * A batch represents a specific group of items associated with a product in the inventory. Multiple batches can exist for the same product, each identified by its own quantity and expiration date.
- **Item**
    * An item represents a single physical unit of a product that exists in the shop’s inventory. Each item belongs to a specific batch.
- **Sale** 
    * An event, identified by a unique code, that occurs every time a customer completes the purchase of one or more items. A sale records a list of items with associated quantities, the date and the total amount spent.
- **Refund** 
    * An event, identified by a unique code, that occurs every time a customer successfully returns one or more items. A refund records a list of items with associated quantities, the date and the total amount owed.
- **Catalogue**
    * The catalog is the complete collection of all product available in the shop’s system. The catalog serves as a reference for managing inventory, creating orders, and displaying available products to the user.
- **Inventory** 
    * The collection of all batches (identified by code) and the name of the product they belong to. It represents the shop's overall product availability and supports search, filtering, expiration tracking and quantity monitoring.
- **Supplier**
    * A business entity providing batches to the shop. Each supplier may have identifying details such as name and P.IVA.
- **Invoice**
    * A formal document that records a financial transaction between the shop and a supplier or customer, serving as proof of purchase or sale.
- **Order** 
    * The purchase of a collection of batches from a supplier. Orders have a defined structure and status, typically one of: processing, shipped, in transit, delivered and cancelled.
- **Income**
    * The amount of money earned from completed sales.
- **Expenses** 
    * The amount of money spent by the shop to maintain it operation such as electrical bills, renting fees, wages, and products purchases.
- **Balance**
    * The overall financial position of the shop, calculated as the difference between total incomes and total expenses within a given period.
- **Owner**
    * The shop holder or manager who uses the EzShop software to control sales, inventory, orders, and accounting. The real end user of the software.
- **Cash Register**
    * A physical or digital terminal that records sales data and transmits it to the EzShop application via API.
- **Shipping company** 
    * A third-party service that delivers batches from suppliers to the shop. Some shipping company offer APIs to track delivery and shipment status.
- **Notification**
    * A system-generated message or alert that informs the shop owner about important events or conditions, such as changes in order status, low product quantity, batch expiration, or connectivity issues.


![missing-glossary](../res/plantuml/glossaryDiagram.svg) 

\<use UML class diagram to define important terms, or concepts in the domain of the application, and their relationships>

\<concepts must be used consistently all over the document, ex in use cases, requirements etc>

# System Design

\<describe here system design>
- EzShop Back end (cash registers comunication)
- Windows EzShop app (business logic + front end)

\<must be consistent with Context diagram>

# Hardware Software architecture

\<describe here the hardware software architecture using UML deployment diagram >


![missing-deployment](../res/plantuml/deploymentDiagram.svg) 


