

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

- Manage Catalogue 
    * The system shall stores for each product :
        + the product name
        + the category
        + unit price
        + brand
    * Add new product to the catalogue
    * remove a prodcut from the catalogue
    * update a product in the catalogue 
    * Display product information
        + Display list of products filter by product attributes 
        +  Display list of products sorted by products attributes
    * Display product stats
        + Display quantity of items stored referred to a product in the catalogue ( sum of the quantity on each batch with the selected product)
        + Display quantity of items stored  grouped by one or more  product attributes  
- Manage inventory
    *  The system shall stores for each batch of products:
         + information the product contained  
         + description
         + expiration date 
         + quantity in stock 
    *  Add new batch to inventory
    *  Delete a batch from inventory 
    *  Update a batch 
    *  Display batch information 
        + Display batches information sorted by one or more product/batch attributes
        + Display batches information filtered by one or more product/batch attributes
    *  Display batches stats
         + Display number of batches per product 
         + Display number of batches grouped by one or more product attributes
    *  Display batches' supplier price
         + Display supplier price for batches  per one or more product attributes 
    *  If a batch has an expiration date, notify the user when it is expired 
    *  If a product is about to expire, notify the user
    *  Import batches list as `.csv` 
    *  Export batches list as `.csv`
- Manage orders
    * The system shall stores for each order :
        + the supplier 
        + the product that is ordered
        + number of batches ordered 
        + delivered or not
        + order and delivery date
        + supplier unit price 
        + number of items for each batch
    * Add new order
    * Delete order
    * Edit order
    * Automatically track order for supported suppliers
        + Display order status 
        + when a order is delivered update order information 
    * Notify the user when the quantity of a certain product is below a threshold 
        + Let user set warning threshold  
    * Display orders
        + Display list of orders sorted by order attributes
        + Display list of orders filtered by order attributes
    * Display order stats
        + Display quantities of product ordered grouped by order attributes   
    * Export list as `.csv`
- Manage sales
    * Read sale from cash register
    * The system shall stores for each sale :
        + list of products with associated quantities
        + the date  
        + the total amount spent 
    * Update inventory (with contents of the sale)
    * Export list as `.csv`
    * Display sale stats
        + Display sales volume per products
        + Display sales volume per one or more product attributes  
        + rank products by number of items sold 
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
| :-----: | :--------------------------------: | :---------: | :-------: |
|  NFR1   |                                    |             |           |
|  NFR2   |                                    |             |           |
|  NFR3   |                                    |             |           |
| NFRx .. |                                    |             |           |

# Table of rights

|  Actor   | FR1         | FRx |
| :---:    | :---------: | :---: |
|          |             |       |

# Use case diagram and use cases

## Use case brief
| **UC Name**                        | **Goal**                                  | **Description**|
| ---------------------------------- | ----------------------------------------- | ------------------------------------------------------------------------------------------------- |
| **UC1 - create batch**             | Add new batch                             | Add a new batch to the inventory                                                    |
| **UC2 - delete batch**             | Delete batch                              | Delete a batch from the inventory                                                                 |
| **UC3 - update batch**             | Update batch                              | Update information of a batch stored in the inventory
| **UC4 - create product**          | Add new product                           | Add a new product to the list of products                                                            |
| **UC5 - delete product**          | Delete product                            | Delete an product from the list of products                                                          |
| **UC6 - update product**          | Update product                            | Update product's information from the list of products                                               |
| **UC7 - create order**            | Add new order                             | Add a new order to the list of orders                                                            |
| **UC8 - delete order**            | Delete order                              | Delete an order from the list of orders                                                          |
| **UC9 - update order**            | Update order                              | Update order's information from the list of orders                                               |
| **UC10 - add cash register**       | Add new cash register                     | Add a new cash register it to the list of cash registers                                                   |
| **UC11 - delete cash register**    | Delete cash register                      | Delete a cash register from the list of cash registers                                           |
| **variantUC18 - retrieve batch**           | Retrieve batch                            | Retrieve batch's information from the inventory                                                  |
| **variantUC17 - retrieve product**         | Retrieve product                          | Retrieve product's information from the inventory                                                  |
| **UC12 - retrieve incomes**        | Retrieve shop incomes                     | Retrieve shop's income at different time granularity                                              |
| **UC13 - retrieve expenses**       | Retrieve shop expenses                    | Retrieve shop's expenses at different time granularity                                             |
| **UC14 - retrieve balance**        | Retrieve balance                          | Retrieve current balance and balance history at different time granularity                       |
| **UC15 - create sales list**       | Create owner-defined orders list          | Retrieve batches list filtered by a set of orders' attributes |
| **UC16 - create invoice list**     | Create owner-defined invoice list         | Retrieve invoices filtered by one or more invoice's attributes                                   |
| **UC17 - create product list**     | Create owner-defined product list         | Retrieve products filtered by one or more product's attributes                                   |
| **UC18 - create batches list**      | Create owner-defined batches list         | Retrieve batches list filtered by a set of batches' attributes                                            |
| **UC19 - set password**            | Set owner password                        | Let owner set a new password                                                                     |
| **UC20 - authenticate**            | Authenticate owner                        | Authenticate the owner if the password provided is correct                                       |
|**UC21 - set threshold**            | set item quantity threshold               | set for a product a threshold value for item quantity                                               |
| **UC22 - suggest new order**       | Suggest new order                         | Suggest a new order when a product is about to run out                                           |
| **UC23 - import products list**    | Import orders list as `.csv`              | Read `.csv` file and add new orders                                                              |
| **UC24 - import batches list**      | Import batches list as `.csv`             | Read `.csv` file and create new batches in the inventory                                         |
| **UC25 - import sales list**        | Import sales list as `.csv`               | Read `.csv` file and update the sales list                                                        |
| **UC26 - import orders list**      | Import orders list as `.csv`              | Read `.csv` file and add new orders                                                              |
| **UC27 - export sales list**       | export a sales list as '.csv'             | return '.csv' file with a list of sales                                                         | 
| **UC28 - export orders list**       | export a orders list as '.csv'             | return '.csv' file with a list of orders                                                         | 
| **UC29 - export batches list**       | export a batches list as '.csv'             | return '.csv' file with a list of batches                                                         | 
| **UC30 - export products list**       | export a products list as '.csv'             | return '.csv' file with a list of products                                                         | 



| **UC Name**                        | **Goal**                                   | **Description**|
 **UC1 – Manage Inventory**         | Track products                              | Owner creates, updates and deletes batches of products|
| **UC2 – Manage Orders**            | Manage supplier orders                      | Owner creates, updates and deletes orders |
| **UC3 - Suggest Orders**           | Suggest orders to a user                    | When a product quantity is behind a defined threshold the system suggest an order to the owner |
| **UC4 – Manage Invoices**          | Record and manage invoices                  | Owner creates, updates and deletes invoices |
| **UC5 – Authenticate Owner**       | Ensure secure access                        | Owner authenticates through a password and manage it (creation, modification)|
| **UC6 – Manage Product Catalogue** | Manage the product catalogue                | Owner creates, updates, and deletes products of the catalogue |
| **UC7 – Receive Notifications**    | Notify the user of relevant events          | The system sends notifications related to product expirations, ongoing orders, status changes, or quantity reached thresholds|
| **UC8 - Import Data**              | Import data as .csv                         | Owner imports products, sales, batches or order lists as .csv | 
| **UC9 - Export Data**              | Export data as .csv                         | Owner exports products, sales, batches or order lists as .csv |
| **UC10 - Retrieve Data**           | Retrieve data required  by the owner        | Owner retrieves list of products, sales, orders, batches and invoices filtered by one or more fo their attributes |
| **UC11 - Manage cash flow**        | Retrieve incomes, outgoings and balance     | Owner retrieves incomes, outogings and balance tracked and computed by the system 3|     
| **UC12 – Manage Sales**            | Record and manage sales                     | To do... |

## Use case diagram

\<define here UML Use case diagram UCD summarizing all use cases, and their relationships>

\<next describe here each use case in the UCD>

### Use case 10, UC10

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------: |
|   Precondition   | Data are in the system && attributes' values are present in the system |
|  Post condition  |  Owner retrieves the desidered list of data   |
| Nominal Scenario | Owner retrieves a list of data from the system                       | 
|     Variants     | Owner retrieves a list of data filtered by their attributes          |
|    Exceptions    | Owner selects attribute's values (for filtering) that are incorrect or absent|

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


