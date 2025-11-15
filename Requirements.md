

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

| **UC Name**                        | **Goal**                                   | **Description**|
| ---------------------------------- | ----------------------------------------- | ------------------------------------------------------------------------------------------------- |
| **UC1 – Manage Inventory**         | Track products                              | Owner creates, updates and deletes batches of products| 
| **UC2 – Manage Orders**            | Manage supplier orders                      | Owner creates, updates and deletes orders |
| **UC3 – Manage Invoices**          | Record and manage invoices                  | Owner creates, updates and deletes invoices |
| **UC4 – Authenticate Owner**       | Ensure secure access                        | Owner authenticates through a password |
| **UC5 - Change password**          | Change the password                         | Owner change system's password |
| **UC6 – Manage Product Catalogue** | Manage the product catalogue                | Owner creates, updates, and deletes products of the catalogue |
| **UC7 – Receive Notifications**    | Notify the user of relevant events          | The system sends notifications related to product expirations, ongoing orders, status changes, or orders' suggestions|
| **UC8 - Import Data**              | Import data as .csv                         | Owner imports products, sales, batches or order lists as .csv | 
| **UC9 - Export Data**              | Export data as .csv                         | Owner exports products, sales, batches or order lists as .csv |
| **UC10 - Retrieve Data**           | Retrieve data required  by the owner        | Owner retrieves list of products, sales, orders, batches, refunds, cash registers and invoices filtered by one or more fo their attributes |
| **UC11 - Manage cash flow**        | Retrieve incomes, outgoings and balance     | Owner retrieves incomes, outogings and balance tracked and computed by the system|     
| **UC12 - Manage cash registers**   | add cash registers to the system            | Owner connect cash registers to the system through POS API |
| **UC13 – Get cash operation**      | Send sales and refunds                      | Cash register sends information about sales and refunds to the system |
| **UC14 - Get Catalogue**           | Get catalogue from system                   | Cash register gets catalogue from the system |
## Use case diagram

\<define here UML Use case diagram UCD summarizing all use cases, and their relationships>

\<next describe here each use case in the UCD>

### Use case 1, UC1 

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Pre condition   | Owner is authenticated && DB services are available    |
|  Post condition  | CRUD-type batches of products's operation is performed |
| Nominal Scenario | - Owner creates a batches of products MI1 <br> - Owner updates a batches of products MI2 <br> - Owner deletes a batches of products MI3| 
|     Variants     | -  Owner deletes many batches of productss, filtering by products' attributes MI4 |
|     Exception    | - Owner tries to create a batches of products with inconsistent values MI5 <br> - Owner tries to create a batches of products that is alredy in the system MI6 <br> - Owner tries to update a batches of products not present in the system MI7 <br> - Owner tries to update a batches of products with inconsisten values MI8 <br> - Owner tries to delete a batches of products not present in the system MI9|

### Use case 2, UC2

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Pre condition   | Owner is authenticated && DB services are available    |
|  Post condition  | CRUD-type order's operation is performed |
| Nominal Scenario | - Owner creates a order MO1 <br> - Owner updates a order MO2 <br> - Owner deletes a order MO3| 
|     Variants     | -  Owner deletes many orders, filtering by products' attributes MO4 |
|     Exception    | - Owner tries to create a order with inconsistent values MO5 <br> - Owner tries to create a order that is alredy in the system MO6 <br> - Owner tries to update a order not present in the system MO7 <br> - Owner tries to update a order with inconsisten values MO8 <br> - Owner tries to delete a order not present in the system MO9|

### Use case 3, UC3

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Pre condition   | Owner is authenticated && DB services are available && internet connection is available |
|  Post condition  | CRUD-type invoice's operation is performed |
| Nominal Scenario | - Owner creates a invoice MI1 <br> - Owner updates a invoice MI2 <br> - Owner deletes a invoice MI3| 
|     Variants     | -  Owner deletes many invoices, filtering by products' attributes MI4 |
|     Exception    | - Owner tries to create a invoice with inconsistent values MI5 <br> - Owner tries to create a invoice that is alredy in the system MI6 <br> - Owner tries to update a invoice not present in the system MI7 <br> - Owner tries to update a invoice with inconsisten values MI8 <br> - Owner tries to delete a invoice not present in the system MI9|

### Use case 4, UC4

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Pre condition   |  Owner has a password          |
|  Post condition  |  Owner is correctly authenticated |
| Nominal Scenario | - Authenticate owner SP1 <br> | 
|     Exception    | - Owner tries to authenticate with a wrong password <br> SP2    | 

### Use case 5, UC5

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Pre condition   |  Owner  is authenticated
|  Post condition  |  Owner set a new password
| Nominal Scenario | - Authenticate owner AU1 <br> | 
|     Exception    | - Owner tries to set an empty password <br> AU2| 

### Use case 6, UC6

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Pre condition   | Owner is authenticated && DB services are available && internet connection is available |
|  Post condition  | CRUD-type operation is performed in the catalogue  |
| Nominal Scenario | - Owner creates a product MP1 <br> - Owner updates a product MP2 <br> - Owner deletes a product MP3| 
|     Variants     | -  Owner deletes many products, filtering by products' attributes MP4 |
|     Exception    | - Owner tries to create a product with inconsistent values MP5 <br> - Owner tries to create a product that is alredy in the catalogue MP6 <br> - Owner tries to update a product not present in the catalogue MP7 <br> - Owner tries to update a product with inconsisten values MP8 <br> - Owner tries to delete a product not present in the catalogue MP9|

### Use case 7, UC7

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Pre condition   | Owner is authenticated && DB services are available &&  internet connection is available |
|  Post condition  | Owner receive the notification  |
| Nominal Scenario | - Owner is notified when an order status changes MN1 <br> - Owner is notified when a batch is expired MN2 <br> - Owner is notified when a cash is not responding MN3 <<br> - Owner is notified when a product is going to run out MN4 <br> - Owner is notified when there is no internet connection MN5| 
|     Variants     | -  Owner is notified when a batch is about to expire MN6 <br> Owner is notified when an order status cannot be updated since API is not responding |

### Use case 8, UC8

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Pre condition   | Owner is authenticated && DB services are available && internet connection is available && file .csv data are in the correct format|
|  Post condition  | .csv file's data are correctly imported |
| Nominal Scenario | - Owner import a list of product as .csv file <br> -  Owner import a list of invoices as .csv file< <br> -  Owner import a list of suppliers as .csv file <br>  Owner import a list of sales as .csv file <br>  Owner import a list of refunds as .csv file <br> Owner importr a list of orders as .csv file | 
|     Exception    | - Owner import .csv file with format error |

### Use case 9, UC9 

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Pre condition   | Owner is authenticated && DB services are available && internet connection is available && needed data are in the system|
|  Post condition  | data are correctly exported as .csv |
| Nominal Scenario | - Owner export a list of product as .csv file <br> -  Owner export a list of invoices as .csv file< <br> -  Owner export a list of suppliers as .csv file <br>  Owner export a list of sales as .csv file <br>  Owner export a list of refunds as .csv file <br> Owner exportr a list of orders as .csv file | 
|     Exception    | - Owner export .csv file with format error |

### Use case 10, UC10

| Actors Involved  |                 Owner                                                |
| :--------------: | :----------------------------------------------------------------- |
|  Pre condition   | Owner is authenticated && DB services are available    |
|   Precondition   | Owner is authenticated && Data are in the system && BD services are available |
|  Post condition  |  Owner retrieves the desidered list of data |
| Nominal Scenario | Owner retrieves a list of products from the system RD1 <br> - Owner retrieves a list of sales from the system RD2 <br> - Owner retrieves a list of batches from the system RD3 <br> - Owner retrieves a list of orders from the system RD4 <br> - Owner retrieves a list of invoices from the system RD5 | 
|     Variants     | - Owner retrieves a list of products filtered by their attributes RD6 <br> - Owner retrieves a list of sales filtered by their attributes RD7 <br> - Owner retrieves a list of batches filtered by their attributes RD8 <br> - Owner retrieves a list of invoices filtered by their attributes RD9 <br> - Owner retrieves a list of cash registers filtered by their attributes RD10 <br>  - Owner retrieves a list of suppliers filtered by their attributes RD11 <br>  - Owner retrieves a list of refunds filtered by their attributes RD12 |
|    Exceptions    | - Owner selects filtering datat attribute's values that are absent |

### Use case 11, UC11

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Pre condition   | Owner is authenticated && DB services are available && internet connection is available|
|  Post condition  | cash flow is correctly tracked |
| Nominal Scenario | - Owner retrieves incomes at different time granularities <br> - Owner retrieves outgoing at different time granularities <br> - Owner retrieves balance at different time granularities <br> | 

### Use case 13, UC13
| Actors Involved  |                 Owner                                                |
| :--------------: | :----------------------------------------------------------------- |
|  Pre condition   | Owner is authenticated && DB services are available && internet connection is available && cash register is tracked by the system |
|  Post condition  | information about cash operations are gets and saved by the sytem |


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


