

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
| Desktop OS| The device where the application resides |
| Product suppliers | Business who supply the shop with items |
| Shipping company | Company who delivers the items to the shop|
| DB service supplier | Stores data |
| Development team | Team responsible for the development of the application |
| Maintenance team | Team responsible for the long term support of the application |
| Competitors | Other companies that sell a similar product |

# Context Diagram and interfaces

## Context Diagram
```plantuml
!theme blueprint
skinparam backgroundColor transparent

skinparam actorStyle hollow
rectangle "EzShop" as system
actor "Shop Owner" as shopManager
actor "Cash register" as register
actor "Data base supplier " as db
actor "Shipping company" as shipping

shopManager <--> system
register --> system
system <--> db
system <-- shipping
```

## Interfaces

|   Actor   | Logical Interface | Physical Interface |
| :-------: | :---------------: | :----------------: |
| Shop manager | GUI | Desktop computer |
| Data base | API | Internet connection |
| Cash register | API | Internet connection |
| Shipping company | API | Internet connection |


# Functional and non functional requirements

## Functional Requirements

\<In the form DO SOMETHING, or VERB NOUN, describe high level capabilities of the system>

\<they match to high level use cases>

| ID | Description |
|:--:|:-------------|
| **FR1** | **Manage sales** |
| *FR1.1* | *Create owner-defined sale list* |
| FR1.1.1 | For each owner-defined list filter sales by a specified date (ISO 8601) or time window |
| FR1.1.2 | Retrieve sales filtered by products sold |
| FR1.1.3 | Retrieve sales ranked by number of items sold per specific product |
| FR1.1.4 | Retrieve sales ranked by the sum of its item's prices |
| *FR1.2* | *Manage `.csv`* |
| FR1.2.1 | Import sales list from `.csv` |
| FR1.2.2 | Export list of sales as `.csv` |
| **FR2** | **Manage refunds** |
| *FR2.1* | *Create owner-defined refund list* |
| FR2.1.1 | For each owner-defined list filter refunds by a specified date (ISO 8601) or time window |
| FR2.1.2 | Retrieve refunds filtered by products returned |
| FR2.1.3 | Retrieve refunds ranked by number of items given back per specific product |
| FR2.1.4 | Retrieve refunds ranked by the sum of its item's prices |
| *FR2.2* | *Manage `.csv`* |
| FR2.2.1 | Import refunds list from `.csv` |
| FR2.2.2 | Export list of refunds as `.csv` |
| **FR3** | **Manage catalogue** |
| *FR3.1* | *Manage CRUD operations* |
| FR3.1.1 | Create new product in the catalogue |
| FR3.1.2 | Update product from the catalogue |
| FR3.1.3 | Delete product from the catalogue |
| *FR3.2* | *Set product item quantity warning threshold* |
| *FR3.3* | *Create owner-defined product list* |
| FR3.3.1 | Retrieve list of products filtered by one or more of their attributes |
| FR3.3.2 | Retrieve number of items available for the selected product (sum of the quantity on each batch with the selected product) |
| *FR3.4* | *Manage `.csv`* |
| FR3.4.1 | Import product list from `.csv` |
| FR3.4.2 | Export list of products as `.csv` |
| *FR3.5* | *Update cash register's catalogue* |
| FR3.5.1 | Convert catalogue to API-specific format |
| FR3.5.2 | Check connection with cash register |
| FR3.5.3 | Send updated catalogue to connected cash register |
| **FR4** | **Manage inventory** |
| *FR4.1* | *Manage CRUD operations* |
| FR4.1.1 | Create new batch in the inventory |
| FR4.1.2 | Update batch from the inventory |
| FR4.1.3 | Delete batch from the inventory |
| *FR4.2* | *Create owner-defined batch list* |
| FR4.2.1 | Retrieve batches filtered by one or more product/batch attributes |
| *FR4.3* | *Manage `.csv`* |
| FR4.3.1 | Import batches list from `.csv` |
| FR4.3.2 | Export list of batches as `.csv` |
| **FR5** | **Manage suppliers** |
| *FR5.1* | *Manage CRUD operations* |
| FR5.1.1 | Create new supplier |
| FR5.1.2 | Update supplier from the list of suppliers|
| FR5.1.3 | Delete supplier from the list of suppliers |
| FR5.1.4 | Link supplier to one or more products|
| FR5.1.5 | Unlink supplier from one or more products|
| *FR5.2* | *Create owner-defined supplier list* |
| FR5.2.1 | Retrieve suppliers list filtered by one or more product they provide |
| FR5.2.2 | Retrieve suppliers list ranked by the number of associated purchase orders |
| *FR5.3* | *Manage `.csv`* |
| FR5.3.1 | Import supplier list from `.csv` |
| FR5.3.2 | Export list of suppliers as `.csv` |
| **FR7.1** | **Track invoices** |
| FR7.1.2 | *Manage CRUD operations* |
| FR7.1.2.1 | Create new invoice |
| FR7.1.2.2 | Update invoice |
| FR7.1.2.3 | Delete invoice |
| FR7.1.2.3 | Link invoice to a specific order|
| FR7.1.3 | *Create owner-defined invoice list* |
| FR7.1.3.1 | Retrieve list of invoices filtered by one or more of their attributes |
| *FR5.3* | *Manage `.csv`* |
| FR5.3.1 | Import invoices list from `.csv` |
| FR5.3.2 | Export invoices list as `.csv` |
| **FR6** | **Manage orders** |
| *FR6.1* | *Manage CRUD operations* |
| FR6.1.1 | Create new order in the list of orders |
| FR6.1.2 | Update order from the list of orders |
| FR6.1.3 | Delete order from the list of orders |
| FR6.1.4 | Link order to one supplier from the supplier list |
| FR6.1.5 | Unlink order from one supplier from the supplier list|
| *FR6.2* | *Automatically track order for supported couriers* |
| FR6.2.1 | Check internet connection |
| FR6.2.2 | Retrieve current order's status |
| FR6.2.3 | Update current order's status |
| *FR6.3* | *Create owner-defined orders list* |
| FR6.3.1 | Retrieve list of orders filtered by one or more of their attributes |
| *FR6.4* | *Manage `.csv`* |
| FR6.4.1 | Import orders list from `.csv` |
| FR6.4.2 | Export list of orders as `.csv` |
| *FR6.5* | *Suggest order* |
| FR6.5.1 | Retrieve products with item count below threshold |
| FR6.5.2 | Retrieve possible supplier for products with item count below threshold |
| FR6.5.3 | Generate order suggestion (without specifying the number of items) |
| FR6.5.4 | Add suggested order to list of orders |
| **FR7** | **Manage accounting** |
| *FR7.2* | *Track incomes* |
| FR7.2.1 | Compute incoming cash flow from sales list and refunds list at different time granularities (day, month, year, etc…)|
| FR7.2.2 | Retrieve incoming cash flow at different time granularities (day, month, year, etc…) |
| *FR7.3* | *Track expenses* |
| FR7.3.1 | Compute outgoing cash flow from orders list and refunds list at different time granularities (day, month, year, etc…)||
| FR7.3.2 | Retrieve outgoing cash flow at different time granularities (day, month, year, etc…) |
| *FR7.4* | *Track balance* |
| FR7.4.1 | Compute total balance based on incomes and expenses at different time granularities (day, week, month, quarter, semester, and year) |
| FR7.4.2 | Retrieve balance at different time granularities (day, week, month, quarter, semester, and year) |
| FR7.4.3 | Retrieve current balance |
| **FR8** | **Authenticate owner** |
| FR8.1 | Set password |
| FR8.2 | Change password |
| FR8.3 | Verify password |
| FR8.4 | Encrypt password |
| FR8.5 | Decrypt password |
| **FR9** | **Manage notifications** |
| FR9.1 | Create "order's status changed" notification |
| FR9.2 | Create "order's status unable to be automatically updated" notification (API not responding) |
| FR9.3 | Create "items below threshold" notification |
| FR9.4 | Create "batch is about to expire" notification when batch is within owner-defined days from expiration date in ISO 8601 format) |
| FR9.5 | Create "batch is expired" notification when batch is past the expiration date in ISO 8601 format |
| FR9.6 | Create "no internet connection" notification|
| FR9.7 | Create "cash register is not responding" notification |
| FR9.8 | Delete notification |
| **FR10** | **Manage cash registers** |
| *FR10.1* | *Link with POS provider's account* |
| FR10.1.1 | Redirect user to POS provider's authorization URL |
| FR10.1.2 | Retrieve access token and refresh token |
| FR10.1.3 | Encrypt access token |
| FR10.1.4 | Retrieve new token when old token is expired |
| *FR10.2* | *Get cash register list* |
| FR10.2.1 | Decrypt access token |
| FR10.2.2 | Retrieve list of cash registers using POS provider's API and access token |
| FR10.2.3 | Update local list of cash registers |
| *FR10.3* | *Sync catalogue* |
| FR10.3.1 | Convert catalogue to POS provider compliant format |
| FR10.3.2 | Push new catalogue to found cash registers |
| FR10.3.3 | Detect unresponsive (POS API returns error message or fails to respond within default timeout threshold) cash register and update its status |
| *FR10.4* | *Retrieve sales* |
| FR10.4.1 | Pull sales list from found cash registers |
| FR10.4.2 | Convert sales list to EzShop compliant format |
| FR10.4.3 | Update item quantities in the inventory |
| FR10.4.4 | Add sale to sales list |
| FR10.4.5 | Detect unresponsive (POS API returns error message or fails to respond within default timeout threshold) cash register and update its status |
| *FR10.5* | *Retrieve refunds* |
| FR10.5.1 | Pull refunds list from found cash registers |
| FR10.5.2 | Convert refunds list to EzShop compliant format |
| FR10.5.3 | Update item quantities in the inventory |
| FR10.5.4 | Add refunds to refunds list |
| FR10.5.5 | Detect unresponsive (POS API returns error message or fails to respond within default timeout threshold) cash register and update its status |
| *FR10.6* | *Create owner-defined list of cash registers* |
| FR10.6.1 | Retrieve list of cash registers filtered by one or more of its attributes |
| FR10.6.2 | Retrieve list of cash registers grouped by the POS provider's brand |


- **Manage sales**
    * *Create owner-defined sale list*
        + For each owner-defined list filter sales by a specified date (ISO 8601) or time window
        + Retrieve sales filtered by products sold
        + Retrieve sales ranked by number of items sold per specific product
        + Retrieve sales ranked by the sum of its item's prices
    * *Manage `.csv`*
        + Import batches list from `.csv`
            + Detect import errors
            + Detect schema mismatch
            + Update sales
        + Export list of batches as `.csv`
            + Retrieve sales
            + Create `.csv` file
            + Detect export errors
- **Manage refunds**
    * *Create owner-defined refund list*
        + For each owner-defined list filter refunds by a specified date (ISO 8601) or time window
        + Retrieve refunds filtered by products returned
        + Retrieve refunds ranked by number of items given back per specific product
        + Retrieve refunds ranked by the sum of its item's prices
    - *Manage `.csv`*
        + Import batches list from `.csv`
            + Detect import errors
            + Detect schema mismatch
            + Update refunds
        + Export list of batches as `.csv`
            + Retrieve refunds
            + Create `.csv` file
            + Detect export errors
- **Manage catalogue**
    * *Manage CRUD operations*
        + Create new product in the catalogue
        + Update product from the catalogue
        + Delete product from the catalogue
    * *Set product item quantity warning threshold*
    * *Create owner-defined product list*
        + Retrieve list of products filtered by one or more of their attributes
        + Retrieve number of items available for a selected product
    * *Manage `.csv`*
        + Import products list from `.csv`
            + Detect import errors
            + Detect schema mismatch
            + Update products list
        + Export products list as `.csv`
            + Retrieve products list
            + Create `.csv` file
            + Detect export errors
- **Manage inventory**
    * *Manage CRUD operations*
        + Create new batch in the inventory
        + Update batch from the inventory
        + Delete batch from the inventory
    * *Create owner-defined batch list*
        + Retrieve batches filtered by one or more product/batch attributes
    * *Manage `.csv`*
        + Import batches list from `.csv`
            + Detect import errors
            + Detect schema mismatch
            + Update inventory
        + Export list of batches as `.csv`
            + Retrieve batches list
            + Create `.csv` file
            + Detect export errors
- **Manage invoices**
    * *Manage CRUD operations*
        + Create new invoice
        + Update invoice
        + Delete invoice
        + Link invoice to a specific order
    * *Create owner-defined invoice list*
        + Retrieve list of invoices filtered by one or more of their attributes
    * *Manage `.csv`*
        + Import invoices list from `.csv`
            + Detect import errors
            + Detect schema mismatch
            + Update invoices
        + Export list of invoices as `.csv`
            + Retrieve invoices
            + Create `.csv` file
            + Detect export errors
- **Manage suppliers**
    * *Manage CRUD operations*
        + Create new supplier
        + Update supplier
        + Delete supplier
        + Link supplier to one or more products
        + Unlink supplier from one or more products
        + Link supplier to one or more batches
        + Unlink supplier from one or more batches
    * *Create owner-defined supplier list*
        + Retrieve suppliers list filtered by one or more product they provide
        + Retrieve suppliers list ranked by number of associated purchase orders
    * *Manage `.csv`*
        + Import supplier list from `.csv`
            + Detect import errors
            + Detect schema mismatch
            + Update suppliers
        + Export list of suppliers as `.csv`
            + Retrieve suppliers
            + Create `.csv` file
            + Detect export errors
- **Manage Shipping companies**
    * *Manage CRUD operations*
        + Create new shipping company
        + Update shipping company
        + Delete shipping company
        + Link shipping company to one or more orders
        + Unlink shipping company from one or more orders
    * *Create owner-defined shipping companies list*
        + Retrieve shipping companies list filtered by one or more of their attributes 
        + Retrieve shipping companies list ranked by number of associated shipments with a selected status
    * *Manage `.csv`*
        + Import shipping companies list from `.csv`
            + Detect import errors
            + Detect schema mismatch
            + Update shipping companies list
        + Export list of shipping companies as `.csv`
            + Retrieve shipping companies list
            + Create `.csv` file
            + Detect export errors
- **Track order**
    * *Link with easy post account*
        + Redirect user to authorization URL
        + Retrieve access and refresh tokens
        + Store access and refresh tokens securely
        + Retrieve new token when expired
    * *Retrieve shipment status*
        + Retrieve tracking updates from provider API
        + Update order's status accordingly
- **Manage orders**
    * *Manage CRUD operations*
        + Create new order
        + Update order
        + Delete order
        + Link order to a supplier
        + Unlink order from a supplier
    * *Create owner-defined orders list*
        + Retrieve list of orders filtered by one or more attributes
    * *Manage `.csv`*
        + Import orders list from `.csv`
            + Detect import errors
            + Detect schema mismatch
            + Update orders
        + Export list of orders as `.csv`
            + Retrieve invoices
            + Create `.csv` file
            + Detect export errors
    * *Suggest order*
        + Retrieve products with item count below threshold
        + Retrieve possible supplier for products with item count below threshold
        + Generate order suggestion
        + Add suggested order to the list of orders
- **Manage accounting**
    * *Track incomes*
        + Compute incoming cash flow at different time granularities
        + Retrieve incoming cash flow at different time granularities
    * *Manage incomes `.csv`*
        + Import incomes list from `.csv`
            + Detect import errors
            + Detect schema mismatch
            + Update incomes
        + Export list of incomes as `.csv`
            + Retrieve incomes
            + Create `.csv` file
            + Detect export errors
    * *Track expenses*
        + Compute outgoing cash flow at different time granularities
        + Retrieve outgoing cash flow at different time granularities
    * *Manage expenses `.csv`*
        + Import expenses list from `.csv`
            + Detect import errors
            + Detect schema mismatch
            + Update expenses
        + Export list of expenses as `.csv`
            + Retrieve expenses
            + Create `.csv` file
            + Detect export errors
    * *Track balance*
        + Compute total balance at different time granularities
        + Retrieve balance at different time granularities
        + Retrieve current balance
- **Authenticate owner**
    * Set password
    * Change password
    * Verify password
    * Encrypt password
- **Manage notifications**
    * Create notification
    * Change notification's status
    * Delete notification
- **Manage cash registers**
    * *Link with POS provider’s account*
        + Redirect user to authorization URL
        + Retrieve access and refresh tokens
        + Store access and refresh tokens securely
        + Retrieve new token when expired
    * *Get cash register list*
        + Retrieve list of cash registers from provider API
        + Update local list of cash registers
    * *Sync catalogue*
        + Convert catalogue to provider format
        + Push new catalogue to cash registers
        + Detect unresponsive cash registers and update status
    * *Retrieve sales*
        + Retrieve sales list from cash register
        + Update inventory quantities
        + Add sale to sales list
        + Detect unresponsive cash registers
    * *Retrieve refunds*
        + Retrieve refunds list from cash register
        + Update item quantities
        + Add refund to refunds list
        + Detect unresponsive cash registers
    * *Create owner-defined cash register list*
        + Retrieve cash registers filtered by attributes
        + Retrieve cash registers grouped by provider brand

**Design cues** 
- The system shall store for each sale:
    * the cash that sales products
    * list of items with associated quantities
    * the date  
    * the total amount spent 
- The system shall store for each order :
    * the supplier 
    * the product that is ordered
    * number of batches ordered 
    * delivered or not
    * order and delivery date
    * supplier unit price 
    * number of items for each batch
- The system shall store for each product:
    * product name
    * category
    * unit price
    * brand
- The system shall store for each batch of products:
    * information the product contained  
    * description
    * expiration date 
    * quantity in stock 

**Usecase**:
- item fields
    + code 
    + issued date 
    + delivery date 
    + name
    + category
    + brand
    + status (pending, ordered, shipped, delivered, unloaded, damaged, expired)
    + Supplier
    + Shipping company
    + price 
    + number of items ordered
- orders fields
    * code
    * supplier name
    * date
    * status
    * quantity
    * items

## Non Functional Requirements

\<Describe constraints on functional requirements>

|   ID    | Type (efficiency, reliability, ..) | Description | Refers to |
| :-----: | :--------------------------------: | :--------- | :-------: |
|  NFR1  |Efficiency| - All CRUD operations should be in the range $[100, 500] \, ms$ <br>- The creation of user-defined lists should be in the range $[1000, 5000] \, ms$<br>- The desktop application should occupy no more than $500 \, MB$ of space<br>- The import/export of `.csv` files with $500$ rows should take $[1000, 10'000] \, ms$<br>- Order status for supported suppliers should be updated at least $1$ time every $6 \, h$<br>
| NFR2   |Usability| - The application should be accessible to people with low to moderate skill with smartphone devices, web services and apps. All usability NFR are defined with this target demographic in mind.<br>-- Setting and updating the owner's password should take no more than $5 \, min$ <br>-- Defining a custom list should take less than $1 \, min$<br>-- All CRUD operations should take less than $1 \, min$ for element<br>-- Importing/exporting a correctly formatted `.csv` file should take less than $1 \, min$<br>-- Reviewing application notifications should take less than $1 \, min$ ||
| NFR3 |Reliability| - $99.999$ % of all sales should be correctly recorded<br>- Exported `.csv` files should have less than $1$ mistaken row every $100'000$ <br>- Importing `.csv` files should generate less than $1$ mistaken row every $100'000$<br> - CRUD operations should have less than $1$ error every $100'000$ operations<br>- Notification should fail to trigger less than $1$ every $100'000$ notifications<br>- Order status should fail to update properly less than $1$ every $100'000$ updates<br>
| NFR4 |Portability| The application should work on Windows operating system from the first version of Windows 10 up to the latest version of Windows 11||
| NFR5 |Security| - All passwords should be stored using some type of encryption<br>- The application must pass common static application security testing||
| NFR6 |Maintainability | - Static analysis of the code should yield the following results:<br>-- $95$ % of all the code base should be documented<br>-- New functionality should be documented within $1$ week from being deployed<br>-- Unit tests should cover $90$ % of the project's LOCs<br>-- The cyclomatic complexity of the codebase should be $\lt 15$|

- **Functionality**
    * **Suitability**
        + All owner needs identified in the use cases should map to at least one functional requirement
    * **Accuracy**
        + Catalogue updates, order-status updates, sales, refunds and similar synchronization operations must achieve a guaranteed delivery rate greater than $99.999$ %
        + Exported `.csv` files should have less than $1$ mistaken row every $100'000$
        + Importing `.csv` files should generate less than $1$ mistaken row every $100'000$
        + CRUD operations should have less than $1$ error every $100'000$ operations
        + Notification should fail to trigger less than $1$ every $100'000$ expected notifications
        + Order status should fail to update properly less than $1$ time every $100'000$ updates
    * **Interoperability**
        + The application should use the square API to pull/push data to square POS      
        + The application should use the lightspeed API to pull/push data to lightspeed POS      
        + The application should use the clover API to pull/push data to clover POS      
        + The application should use the nexi API to pull/push data to nexi POS      
        + The application should use the easy post API to interact with shipping companies and automatically track order status
        + All functions that may access data concurrently, must be thread-safe
    * **Security**
        + Passwords must be encrypted using AES-256 
        + The application must pass Gitlab SATS without high severity issues (CSVV $\gt 7$) being highlighted
- **Reliability**
  - **Maturity**
      * The application should crash less than $1$ time every $200$ hours of operation
      * The application should suffer less than $1$ minor visual glitch (solved by changing/refreshing the current tab) every $50$ hours of operation
  - **Fault Tolerance**
      * The application should not crash when Importing `.csv` files without the right format 
      * The application should be able to perform all its operations, beside syncing with cash registers and shipping companies, even without an internet connection 
      * The application should be able to work without crashing even when data read from the cash registers is corrupted, malformed or absent
      * The application should be able to work without crashing even when data read from the shipping companies' APIs is corrupted, malformed or absent
      * The application should queue failed API calls and retry every $5$ minutes
      * All multi-steps functions must be atomic; partial updates should be rolled back or notified to the owner
- **Usability**
  - **Understandability**
      * The application should display tooltips when hovering over buttons which can be pressed
      * The application should use consistent design elements and language
      * The application should follow industry standard practices and conventions
      * All GUI elements should have a contrast rating greater than $4.5$
  - **Learnability**
      * A user with low to moderate digital literacy should be able to learn how to:
          + navigate the main interface within $5$ minutes
          + to correctly import a `.csv` file within $10$ minutes
          + to modify how the data is displayed within $10$ minutes
          + to add a new product, batch, order, invoice, supplier, shipping company or cash register within $30$ minutes
  - **Operability**
      * All CRUD operations should be accessible within $2$ clicks
      * The GUI should be able to respond to user input within $500$ ms
  - **Usability compliance** 
      * The application should follow WCAG guidelines
- **Efficiency**
  - **Time Behavior**
      * All CRUD operations operating on single entities should be completed within $1000$ ms 
      * Retrieving $\approx 100$ MB of data filtered, sorted or ranked by a specific set of rules should be completed within $10'000$ ms
      * Importing and exporting `.csv` files should take within $10'000$ ms every $1000$ rows 
      * Order status for supported suppliers should be updated within $3$ h from the actual reported change
      * Sales and refunds should be updated at least every $15$ minutes
      * Catalogue updates should be propagated to all cash registers within $15$ minutes from the last change
      * Startup time should be within $5'000$ ms
  - **Resource Utilization**
      * The application should use no more than $500$ MB of disk storage space (excluding data such as orders, sales, refunds, ...)
      * The application should use no more than $2$ GB of RAM memory under expected load
      * The application should use no more than $50$ % of the available CPU resources under normal load on tested hardware (Intel Core i5-8000 or i5-9000 series, $8$ G of RAM)
- **Maintainability**
  - **Analyzability**
      * $95$ % of code functions should be documented
      * New functions should be documented within $1$ week
      * Mean time to diagnose a defect should be within $1$ day
      * All API errors, sync errors, and critical errors must be logged and persisted
  - **Changeability**
      * Mean time to implement a minor feature should be within $1$ working week
      * Mean time to implement major features should be within $1$ months
      * The cyclomatic complexity of functions should be on average less than $15$; no single function should exceed a cyclomatic complexity of $20$
  - **Stability**
      * A new release should introduce less than $1$ regression defect
  - **Testability**
      * Unit tests should cover $90$ % of the codebase
      * Integration tests should cover $80$ % of the codebase
- **Portability**
  - **Adaptability**
      * The application should run on Windows 10 and 11 without code modification
  - **Installability**
      * The application should complete installation within $10$ minutes on tested hardware
      * The application should complete installation with a success rate greater than $95$ % on tested hardware (Intel Core i5-8000 or i5-9000 series, $8$ G of RAM)
  - **Co-existence**
      * The application should be able to run alongside the common antivirus applications (such as: Windows Defender, Avast, McAfee, Norton, BitDefender, Kaspersky, AVG, ESET, Trend Micro, Sophos) without conflicts
      * The application should be able to perform its functionalities without requiring exclusive system resources access
      * The application should be able to work alongside firewalls
  - **Interoperability**
      * Future version of the EzShop application should be able to import data in `.csv` format exported from previous version of the application 



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
    * The small business entity that uses the EzShop software to manage its operations, including sales, inventory, orders, and accounting. A shop typically has one owner, two or more cash registers, and several suppliers. In the current scope, EZShop menages a single shop.
- **Sale** 
    * An Event, identified by a unique code, that occurs every time a customer completes the purchase of one or more items. A sale record the list of items with associated quantities, the date and the total amount spent.
- **Order** 
    * The purchase of a collection of batches from a supplier. Orders have a defined structure and status, typically one of: processing, shipped, in transit, out of delivery, delivered and cancelled.
- **Product** 
    * An ideal entity representing a type of product sold or stocked by the shop; not a single physical object. Each product describes the characteristics shared by all physical units of that product (e.g., 1L bottle of "GoodMilk!").
- **Batch**
    * A batch represents a specific group of items associated with a product in the inventory. Multiple batches can exist for the same product, each identified by its own quantity and expiration date.
- **Item**
    * An item represents a single physical unit of a product that exists in the shop’s inventory. Each item belongs to a specific batch.
- **Inventory** 
    * The collection of all batches (identified by code) and the name of the product they belong to. It represents the shop's overall product availability and supports search, filtering, expiration tracking and quantity monitoring.
- **Catalogue**
    * The catalog is the complete collection of all product available in the shop’s system. The catalog serves as a reference for managing inventory, creating orders, and displaying available products to the user.
- **Stats** 
    * Aggregated or derived data generated from sales, orders, or accounting records, used to support decision-making. (e.g., Sales trends, revenue summary or supplier performance indicators)
- **Owner**
    * The shop holder or manager who uses the EzShop software to control sales, inventory, orders, and accounting. The real end user of the software.
- **Cash Register**
    * A physical or digital terminal that records sales data and transmits it to the EzShop application via API.
- **Supplier**
    * A business entity providing batches to the shop. Each supplier may have identifying details such as name and P.IVA.
- **Shipping company** 
    * A third-party service that delivers batches from suppliers to the shop. Some shipping company offer APIs to track delivery and shipment status.
- **Income**
    * The amount of money earned from completed sales.
- **Expenses** 
    * The amount of money spent by the shop to maintain it operation such as electrical bills, renting fees, and products purchases.
- **Invoice**
    * A formal document that records a financial transaction between the shop and a supplier or customer, serving as proof of purchase or sale.
- **Balance**
    * The overall financial position of the shop, calculated as the difference between total incomes and total expenses within a given period.
- **Notification**
    * A system-generated message or alert that informs the shop owner about important events or conditions, such as changes in order status, low product quantity, batch expiration, or connectivity issues.


\<use UML class diagram to define important terms, or concepts in the domain of the application, and their relationships>

\<concepts must be used consistently all over the document, ex in use cases, requirements etc>

# System Design

\<describe here system design>
- EzShop Back end (cash registers comunication)
- Windows EzShop app (business logic + front end)

\<must be consistent with Context diagram>

# Hardware Software architecture

\<describe here the hardware software architecture using UML deployment diagram >


