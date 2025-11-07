

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

|  ID   | Description |
| :---: | :---------: |
|  FR1  | Manage sales |
|  FR2  | Manage inventory |
|  FR3  | Manage orders |
|  FR4  | Manage accounting |

- Manage sales
    * Read sale form cash register 
    * Save last sale  
    * Update inventory (with contents of the sale)
    * Export list as .csv
    * Display sale stats 
- Manage inventory
    * Manage items
        + Delete item from inventory
        + Add new item to inventory
        + Edit item characteristics
    + View items
        + Display list of available items
        + Search items by selected fields
        + Sort items by selected fields
        + Group items by selected fields
        + Filter items by selected fields
    + Display inventory stats
    + Change item status when expiration date is passed
    + Notify user when items are past the expiration date
    + Export list as .csv
- Manage orders
    * Add new order
    * Delete order
    * Edit order
    * Automatically *track order* status for supported suppliers
    * Suggest order when quantity of certain item is below threshold
        + Accept, delete, edit suggested order
    * View orders
        * Display list of orders
        + search orders by selected fields 
        + sort orders by selected fields
        + group orders by selected fields
        + filter orders by selected fields
    + Display order stats
    * Export list as .csv
- Manage accounting
    * Track Invoices
    * Track Incomes
    * Track balance
    * Track taxes
    * Display accounting stats
- Authenticate owner
    * Set password
    * Change password
    * Verify password

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
  - **Suitability**
    - All user needs identified in the use cases should map to at least one functional requirement
  - **Accuracy**
      * $99.999$ % of all sales should be correctly recorded
      * Exported `.csv` files should have less than $1$ mistaken row every $100'000$
      * Importing `.csv` files should generate less than $1$ mistaken row every $100'000$
      * CRUD operations should have less than $1$ error every $100'000$ operations
      * Notification should fail to trigger less than $1$ every $100'000$ expected notifications
      * Order status should fail to update properly less than $1$ time every $100'000$ updates
  - **Interoperability**
      * The application should use the Square API to extract sale information form cash registers
      * The application should use the ?supplier? API to interact with shipping companies
  - **Security**
      * Passwords must be encrypted using AES-256 
      * The application must pass Gitlab SATS without high severity issues (CSVV $\gt 7$) being highlighted
- **Reliability**
  - **Maturity**
      * The application should crash less than $1$ time every $200$ hours of operation
      * The application should suffer less than $1$ minor visual glitch (solved by changing/refreshing the current tab) every $50$ hours of operation
  - **Fault Tolerance**
      * The application should not crash when Importing `.csv` files without the right format 
      * The application should be able to display the data gathered and provide basic functionality even without an internet connection
      * The application should be able to work without crashing even when data read from the cash registers is corrupted
      * The application should be able to work without crashing even when data read from the shipping companies' APIs is corrupted 
  - **Recoverability**
      * ? 
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
          + to add a new product, batch, order, or cash register within $30$ minutes
  - **Operability**
      * All CRUD operations should be accessible within $2$ clicks
      * The GUI should be able to respond to user input within $500$ ms
  - **Usability compliance** 
      * The application should follow WCAG guidelines
- **Efficiency**
  - **Time Behavior**
      * All CRUD operations should be completed within $500$ ms 
      * The creation of user-defined lists should be completed within $5000$ ms
      * Importing and exporting `.csv` files should take within $10'000$ ms every $1000$ rows 
      * Order status for supported suppliers should be updated within $3$ h from the actual reported change
  - **Resource Utilization**
      * The application should use no more than $500$ MB of disk storage space
      * The application should use no more than $2$ GB of RAM memory
      * The application should use no more than $50$ % of the available CPU resources under normal load on average user hardware
- **Maintainability**
  - **Analyzability**
      * $95$ % of code functions should be documented
      * New functions should be documented within $1$ week
      * Mean time to diagnose a defect should be within $1$ day
  - **Changeability**
      * Mean time to implement a minor feature should be within $1$ working week
      * Mean time to implement major features should be within $1$ months
      * The cyclomatic complexity of the codebase should be less than $15$
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
      * The application should complete installation with a success rate greater than $95$ % on tested hardware
  - **Co-existence**
      * The application should be able to run alongside the common antivirus applications (such as: Windows Defender, Avast, McAfee, Norton, BitDefender, Kaspersky, AVG, ESET, Trend Micro, Sophos) without conficts
      * The application should be able to perform its functionalities without requiring exclusive system resources access
      * The application should be able to work alongside firewalls



# Table of rights

|  Actor   | FR1         | FRx |
| :---:    | :---------: | :---: |
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
    * The small business entity that uses the EzShop software to menage its operations, including sales, inventory, orders, and accounting. A shop tipically has one owner, two or more cash registers, and several suppliers. In the current scope, EZShop menages a single shop.
- **Sale** 
    * An Event, identified by a unique code, that occurs every time a customer completes the purchase of one or more items. A sale records the code, the quantity, the discount value, date, and the price of each item.
- **Order** 
    * The purchase of a collection of items from a supplier. Orders have a defined structure and status, typically one of: processing, shipped, in transit, out of delivery, delivered and cancelled.
- **Item** 
    * An ideal entity representing a type of product sold or stocked by the shop - not a single physical object. Each item describes the characteristics shared by all physical units of that product (e.g., 1L bottle of "GoodMilk!"). The item quantity indicates how many physical units of this item are available.
- **Inventory** 
    * The collection of all items (identified by code) and their quantities. It represents the shop's overall product availability and supports search, filtering, expiration tracking and quantity monitoring.
- **Stats** 
    * Aggregated or derived data generated from sales, orders, or accounting records, used to support decision-making. (e.g. Sales trends, revenue summarie or supplier performance indicators)
- **Fields** 
    * The recorded properties of an item, a sale, or an order. (e.g. name, code, price, quantity...)
- **Owner**
    * The shop holder or mananger who uses the EzShop software to control sales, invetory, orders, and accounting. The real end user of the software.
- **Cash Register**
    * A physical or digital terminal that records sales data and trasmits it to the EzShop application via API.
- **Supplier**
    * A business entity providing goods to the shop. Each supplier may have identifying details such as name and P.IVA.
- **Status** 
    * A descriptor indicating the current contion of an order or item. (e.g. pending, shipped, expired)
- **Shipping company** 
    * A third-party service that delivers items from suppliers to the shop. Some shipping company offer APIs to track delivery and shipment status.
- **Date**
    * A timestamp in the format: `YYYY-MM-DD-hh:mm:ss` 
- **Income**
    * The ammount of money earned from completed sales.
- **Invoice**
    * A formal document that records a financial transaction between the shop and a supplier or customer, serving as proof of purchase or sale.
- **Balance**
    * The overall financial position of the shop, calculated as the difference between total incomes and total expenses within a given period.

\<use UML class diagram to define important terms, or concepts in the domain of the application, and their relationships>

\<concepts must be used consistently all over the document, ex in use cases, requirements etc>

# System Design

\<describe here system design>

\<must be consistent with Context diagram>

# Hardware Software architecture

\<describe here the hardware software architecture using UML deployment diagram >


