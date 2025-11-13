

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
| FR2.1.2 | Retrieve refunds filtered by products sold |
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
| *FR7.1* | *Track invoices* |
| FR7.1.1 | Track invoices for orders made |
| FR7.1.2 | Create owner-defined invoice list |
| FR7.1.2.1 | Retrieve list of invoices filtered by one or more of their attributes |
| *FR7.2* | *Track incomes* |
| FR7.2.1 | Compute incoming cash flow from sales list and refunds list|
| FR7.2.2 | Retrieve incoming cash flow at different time granularities (day, month, year etc…) |
| *FR7.3* | *Track expenses* |
| FR7.3.1 | Compute outgoing cash flow from orders list and refunds list|
| FR7.3.2 | Retrieve outgoing cash flow at different time granularities (day, month, year etc…) |
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
| FR9.1 | Notify owner of order's status change |
| FR9.2 | Notify owner of when order status cannot be changed automatically (API not responding) |
| FR9.3 | Notify owner when quantity of a certain product is below a owner set threshold |
| FR9.4 | Notify owner when batch is within x days from expiration date (ISO 8601) |
| FR9.5 | Notify owner when batch is past the expiration date (ISO 8601) |
| FR9.6 | Notify owner when there is no internet connection |
| FR9.7 | Notify owner when cash register is not responding |
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
| :-----: | :--------------------------------: | :---------: | :-------: |
|  NFR1   |                                    |             |           |
|  NFR2   |                                    |             |           |
|  NFR3   |                                    |             |           |
| NFRx .. |                                    |             |           |

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
- **Sale** 
    * Event, identified by a code, that happens every time a customer completes the purchase of one or more items. This records the code, the quantity, the discount value, date, and the price of each item.
- **Order** 
    * The purchase of a collection of items from a supplier.
- **Item** 
    * The distinct products identified by a code. (e.g. 1l bottle of "goodMilk!", 1l bottle of "calciumJuice")
- **Inventory** 
    * The collection of all items (identified by code) and their quantities in the shop's stock.
- **Stats** 
    * A collection of inferred information from the available data on a specific subject.
- **Fields** 
    * The recorded properties of an item, a sale, or an order
- **Owner** 
- **Status** 
- **Shipping company** 
- **Date**
    * A timestamp in the format: `YYYY-MM-DD-hh:mm:ss` 
- **Income** 
- **Invoice** 
- **Balance** 

\<use UML class diagram to define important terms, or concepts in the domain of the application, and their relationships>

\<concepts must be used consistently all over the document, ex in use cases, requirements etc>

# System Design

\<describe here system design>

\<must be consistent with Context diagram>

# Hardware Software architecture

\<describe here the hardware software architecture using UML deployment diagram >


