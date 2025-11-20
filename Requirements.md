

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
| **UC2 - Manage Supplier**          | Manage supplier                             | Owner creates, updates and deletes supplier |  
| **UC3 – Manage Orders**            | Manage supplier orders                      | Owner creates, updates, and deletes orders |
| **UC4 – Manage Invoices**          | Record and manage invoices                  | Owner creates, updates and deletes invoices |
| **UC5 – Authenticate Owner**       | Ensure secure access                        | Owner authenticates through a password |
| **UC6 - Change password**          | Change the password                         | Owner change system's password |
| **UC7 – Manage Product Catalogue** | Manage the product catalogue                | Owner creates, updates, and deletes products of the catalogue |
| **UC8 – Receive Notifications**    | Notify the user of relevant events          | The system sends notifications related to product expirations, ongoing orders, status changes, or orders' suggestions|
| **UC9 - Import Data**              | Import data as .csv                         | Owner imports products, sales, batches or order lists as .csv | 
| **UC10 - Export Data**              | Export data as .csv                         | Owner exports products, sales, batches or order lists as .csv |
| **UC11 - Retrieve Data**           | Retrieve data required  by the owner        | Owner retrieves list of products, sales, orders, batches, refunds, cash registers and invoices filtered by one or more fo their attributes |
| **UC12 - Manage accounting**        | Retrieve incomes, expenses and balance     | Owner retrieves incomes, outogings and balance tracked and computed by the system|     
| **UC13 - Manage cash registers**   | Add cash registers to the system            | Owner connect cash registers to the system through POS API |
| **UC14 – Manage Sales and Refunds**      | Send sales and refunds                      | The system sends api polling every 2 minutes asking to cash registers to send their stored sales and refunds |
| **UC15 - Get Catalogue**           | Get catalogue from system                   | The system sends api polling every day at 6.00 a.m. to update the cash register's internal catalogue |
| **UC16 - Track Orders** |   Get the current status of one or more orders        | The system ask to the shipping company tracking service via api the current status of the order and gets it |
## Use case diagram

\<define here UML Use case diagram UCD summarizing all use cases, and their relationships>

\<next describe here each use case in the UCD>

## Use case Manage Inventory, UC1 

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Precondition   | Owner is authenticated && DB services are available    |
|  Post condition  | CRUD-type batches of products's operation is performed |
| Nominal Scenario | - Owner creates a batches of products MI1 <br> - Owner updates a batches of products MI2 <br> - Owner deletes a batches of products MI3| 
|     Exception    | - Owner tries to create a batches of products that is alredy in the system MI1E1 <br> |


### Scenario MI1

|  Scenario MI1  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Owner is authenticated && DB services are available                        |
| Post condition | A new batch is inserted in the inventory                                   |

#### Steps

| Actor's Action                                  | System Action                                                      | FR needed |
|--------------------------------------------------|--------------------------------------------------------------------|-----------|
| Owner requests to create a new batch             | System opens a data-entry dialog requesting batch parameters       |4.1.1      |
| Owner enters batch parameters                    |                                                                    |4.1.1      |
|                                                  | System checks if a batch with the same identifying values exists   | 4.1.1     |
|                                                  | System creates and inserts a new batch in the DB using the parameters |4.1.1   |
                                        

### Scenario MI2 

|  Scenario MI2  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Owner is authenticated && DB services are available                                         |
| Post condition | The selected batch is updated in the inventory                              |

#### Steps

| Actor's Action                                  | System Action                                                      | FR needed |
|--------------------------------------------------|--------------------------------------------------------------------|-----------|
| Owner requests to update a batch                 | System opens a data-entry dialog requesting updated parameters     | 4.1.2          |
| Owner modifies batch parameters                  |                                                                    |   4.1.2        |
|                                                  | System updates the batch in the DB using the new parameters        |    4.1.2       |


### Scenario MI3 

|  Scenario MI3  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Owner is authenticated && DB services are available                                         |
| Post condition | The batch is deleted from the inventory                                     |

#### Steps

| Actor's Action                                  | System Action                                                      | FR needed |
|--------------------------------------------------|--------------------------------------------------------------------|-----------|
| Owner requests to delete a batch                 |                                                                    |     4.1.3      |
|                                                  | System deletes the batch from the DB                               |       4.1.3    |

### Scenario MI1E1

|  Scenario MI1E1 |                                                                            |
| :-------------: | :------------------------------------------------------------------------: |
| Precondition    | Owner is authenticated && DB services are available                        |
| Post condition  | No new batch is created          |

#### Steps

| Actor's Action                                  | System Action                                                      | FR needed |
|--------------------------------------------------|--------------------------------------------------------------------|-----------|
| Owner requests to create a new batch             | System opens a data-entry dialog requesting batch parameters       |   4.1.1        |
| Owner enters batch parameters                    |                                                                    |    4.1.1       |
|                                                  | System checks if a batch with the same identifying values exists   |     4.1.1      |
|                                                  | System detects the batch already exists                            |     4.1.1      |
|                                                  | System rejects the creation and displays an error message          |      4.1.1     |




## Use case Manage Supplier, UC2 

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Precondition   | Owner is authenticated && DB services are available    |
|  Post condition  | CRUD-type suppliers's operation is performed |
| Nominal Scenario | - Owner creates a supplier MS1 <br> - Owner updates a supplier MS2 <br> - Owner deletes a supplier MS3|  
|     Exception    | - Owner tries to create a supplier that is alredy in the system MS1E1 <br> |

### Scenario MS1  

|  Scenario MS1  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Owner is authenticated && DB services are available                        |
| Post condition | A new supplier is inserted in the system                                    |

#### Steps

| Actor's Action                        | System Action                                                       | FR needed |
|----------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to create a new supplier| System opens a data-entry dialog requesting supplier parameters     |           |
| Owner inserts supplier parameters      |                                                                     |           |
|                                        | System creates and inserts a new supplier in the DB                 |           |

### Scenario MS2 

|  Scenario MS2  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Owner is authenticated && DB services are available                                      |
| Post condition | The selected supplier is updated in the system                             |

#### Steps

| Actor's Action                        | System Action                                                       | FR needed |
|----------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to update a supplier    | System opens a data-entry dialog requesting new parameters          |           |
| Owner modifies supplier parameters     |                                                                     |           |
|                                        | System checks if supplier already exists in the DB                  |           |
|                                        | System updates the supplier in the DB using the new parameters      |           |


### Scenario MS3 

|  Scenario MS3  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Owner is authenticated && DB services are available                                      |
| Post condition | The supplier is deleted from the system                                     |

#### Steps

| Actor's Action                        | System Action                                                       | FR needed |
|----------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to delete a supplier    |                                                                     |           |
|                                        | System deletes the supplier from the DB                             |           |

### Scenario MS1E1

|  Scenario MS1E1 |                                                                            |
| :-------------: | :------------------------------------------------------------------------: |
| Precondition    | Owner is authenticated && DB services are available                        |
| Post condition  | No new supplier is created |

#### Steps

| Actor's Action                        | System Action                                                       | FR needed |
|----------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to create a new supplier| System opens a data-entry dialog requesting supplier parameters     |           |
| Owner inserts supplier parameters      |                                                                     |           |
|                                        | System checks if supplier already exists in the DB                  |           |
|                                        | System detects duplication                                           |           |
|                                        | System rejects the creation and displays an error message            |           |




## Use case Manage Orders, UC3

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Precondition   | Owner is authenticated && DB services are available    |
|  Post condition  | CRUD-type order's operation is performed |
| Nominal Scenario | - Owner creates a order MO1 <br> - Owner updates a order MO2 <br> - Owner deletes a order MO3| 
|     Exception    | - Owner tries to create an order that is alredy in the system MO1E1 <br> |

### Scenario MO1  

|  Scenario MO1  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Owner is authenticated && DB services are available                        |
| Post condition | A new order is inserted in the inventory                                   |

#### Steps

| Actor's Action                        | System Action                                                       | FR needed |
|----------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to create a new order   | System opens a data-entry dialog requesting order parameters        |           |
| Owner inserts order parameters         |                                                                     |           |
|                                        | System creates and inserts a new order in the DB                   |           |


### Scenario MO2 

|  Scenario MO2  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Owner is authenticated && DB services are available                                        |
| Post condition | The selected order is updated in the inventory                             |

#### Steps

| Actor's Action                        | System Action                                                       | FR needed |
|----------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to update an order      | System opens a data-entry dialog requesting updated parameters      |           |
| Owner modifies the order parameters    |                                                                     |           |
|                                        | System updates the order in the DB using the new parameters         |           |


### Scenario MO3 

|  Scenario MO3  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Owner is authenticated && DB services are available                                      |
| Post condition | The order is deleted from the inventory                                     |

#### Steps

| Actor's Action                        | System Action                                                       | FR needed |
|----------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to delete the order     |                                                                     |           |
|                                        | System deletes the order from the DB                                |           |

### Scenario MO1E1

|  Scenario MO1E1 |                                                                            |
| :-------------: | :------------------------------------------------------------------------: |
| Precondition    | Owner is authenticated && DB services are available                        |
| Post condition  | No new order is created    |

#### Steps

| Actor's Action                        | System Action                                                       | FR needed |
|----------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to create a new order   | System opens a data-entry dialog requesting order parameters        |           |
| Owner inserts order parameters         |                                                                     |           |
|                                        | System checks if the order already exists in the DB                |           |
|                                        | System detects duplication                                           |           |
|                                        | System rejects the creation and displays an error message           |           |


## Use case Manage Invoices, UC4

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Precondition   | Owner is authenticated && DB services are available && internet connection is available |
|  Post condition  | CRUD-type invoice's operation is performed |
| Nominal Scenario | - Owner creates a invoice MI1 <br> - Owner updates a invoice MI2 <br> - Owner deletes a invoice MI3| 
|     Exception    | - Owner tries to create an invoice that is alredy in the system MI1E1 <br> |

### Scenario MI1  

|  Scenario MI1  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Owner is authenticated && DB services are available                        |
| Post condition | A new invoice is inserted in the inventory                                 |

#### Steps

| Actor's Action                          | System Action                                                       | FR needed |
|------------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to create a new invoice   | System opens a data-entry dialog requesting invoice parameters      |           |
| Owner inserts invoice parameters         |                                                                     |           |
|                                          | System creates and inserts a new invoice in the DB                  |           |

### Scenario MI2 

|  Scenario MI2  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Owner is authenticated && DB services are available                                       |
| Post condition | The selected invoice is updated in the system                               |

#### Steps

| Actor's Action                          | System Action                                                       | FR needed |
|------------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to update an invoice      | System opens a data-entry dialog requesting updated parameters      |           |
| Owner modifies the invoice parameters    |                                                                     |           |
|                                          | System updates the invoice in the DB using the new parameters       |           |


### Scenario MI3 

|  Scenario MI3  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   |  Owner is authenticated && DB services are available                                        |
| Post condition | The invoice is deleted from the system                                      |

#### Steps

| Actor's Action                          | System Action                                                       | FR needed |
|------------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to delete an invoice      |                                                                     |           |
|                                          | System deletes the invoice from the DB                               |           |

### Scenario MI1E1

|  Scenario MI1E1 |                                                                            |
| :-------------: | :------------------------------------------------------------------------: |
| Precondition    | Owner is authenticated && DB services are available                        |
| Post condition  | No new invoice is created; system notifies that the invoice already exists |

#### Steps

| Actor's Action                          | System Action                                                       | FR needed |
|------------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to create a new invoice   | System opens a data-entry dialog requesting invoice parameters      |           |
| Owner inserts invoice parameters         |                                                                     |           |
|                                          | System checks if the invoice already exists in the DB               |           |
|                                          | System detects duplication                                           |           |
|                                          | System rejects creation and displays an error message               |           |

## Use case Authenticate Owner, UC5

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Precondition   |  Owner knows a password          |
|  Post condition  |  Owner is correctly authenticated |
| Nominal Scenario | - Authenticate owner AO1 <br> | 
|     Exception    | - Owner tries to authenticate with a wrong password <br> AOE1    | 

### Scenario AO1  

|  Scenario AO1  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Owner knows the correct password                                           |
| Post condition | Owner is correctly authenticated                                            |

#### Steps

| Actor's Action                       | System Action                                                       | FR needed |
|---------------------------------------|---------------------------------------------------------------------|-----------|
|                                       | System asks the Owner to insert the password (data-entry dialog)    |           |
| Owner inserts the password            |                                                                     |           |
|                                       | System checks the password                                          |           |
|                                       | System authenticates the Owner                                      |           |


### Scenario AO1E 

|  Scenario AOE1 |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Owner knows an incorrect password                                           |
| Post condition | Owner is not authenticated                                                  |

#### Steps

| Actor's Action                       | System Action                                                       | FR needed |
|---------------------------------------|---------------------------------------------------------------------|-----------|
| —                                     | System asks the Owner to insert the password (data-entry dialog)    |           |
| Owner inserts the password            |                                                                     |           |
|                                       | System checks the password                                          |           |
|                                       | System informs the Owner that the password is incorrect             |           |
|                                       | System does **not** authenticate the Owner                          |           |



## Use case Change Password, UC6

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------  |
|  Pre condition   |  Owner  is authenticated                                             |  
|  Post condition  |  Owner set a new password                                            |
| Nominal Scenario | - Authenticate owner CP1 <br>                                        |  
|     Exception    | - Owner tries to set an invalid type of password CP1E1 <br>          | 

### Scenario CP1

|  Scenario CP1  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Owner is authenticated                                                     |
| Post condition | Owner sets a new valid password                                            |

#### Steps

| Actor's Action                       | System Action                                                       | FR needed |
|---------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to change password     | System opens a data-entry dialog                                    |           |
| Owner inserts the new password        |                                                                     |           |
|                                       | System validates the password                                       |           |
|                                       | System changes the password                                         |           |

### Scenario CP1E1

|  Scenario CP1E1 |                                                                            |
| :-------------: | :------------------------------------------------------------------------: |
| Precondition    | Owner is authenticated && Owner inserts an invalid password                |
| Post condition  | Password is not changed                                                    |

#### Steps

| Actor's Action                       | System Action                                                       | FR needed |
|---------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to change password     | System opens a data-entry dialog                                    |           |
| Owner inserts the new (invalid) password |                                                                   |           |
|                                       | System validates the password                                       |           |
|                                       | System informs the Owner that the password is invalid               |           |
|                                       | System does **not** change the password                             |           |



## Use case Manage Product Catalogue, UC7

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Precondition   | Owner is authenticated && DB services are available && internet connection is available |
|  Post condition  | CRUD-type operation is performed in the catalogue  |
| Nominal Scenario | - Owner creates a product MP1 <br> - Owner updates a product MP2 <br> - Owner deletes a product MP3| 
|     Exception    | - Owner tries to create a product that is alredy in the system MP1E1 <br> |

### Scenario MP1  

|  Scenario MP1  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Owner is authenticated && DB services are available                        |
| Post condition | A new product is inserted in the catalogue                                 |

#### Steps

| Actor's Action                          | System Action                                                       | FR needed |
|------------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to create a new product   | System opens a data-entry dialog requesting product parameters      |           |
| Owner inserts product parameters         |                                                                     |           |
|                                          | System creates and inserts a new product in the DB                  |           |
                                                   

### Scenario MP2 

|  Scenario MP2  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Owner is authenticated && DB services are available                                      |
| Post condition | The selected product is updated in the catalogue                           |

#### Steps

| Actor's Action                          | System Action                                                       | FR needed |
|------------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to update a product       | System opens a data-entry dialog requesting updated parameters      |           |
| Owner modifies the product parameters    |                                                                     |           |
|                                          | System updates the product in the DB using the new parameters       |           |


### Scenario MP3 

|  Scenario MP3  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Owner is authenticated && DB services are available                                      |
| Post condition | The product is deleted from the catalogue                                  |

#### Steps

| Actor's Action                          | System Action                                                       | FR needed |
|------------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to delete a product       |                                                                     |           |
|                                          | System deletes the product from the DB                              |           |

### Scenario MP1E1

|  Scenario MP1E1 |                                                                            |
| :-------------: | :------------------------------------------------------------------------: |
| Precondition    | Owner is authenticated && product with same identifiers already exists     |
| Post condition  | No new product is created                     |

#### Steps

| Actor's Action                          | System Action                                                       | FR needed |
|------------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to create a new product   | System opens a data-entry dialog requesting product parameters      |           |
| Owner inserts product parameters         |                                                                     |           |
|                                          | System checks if the product already exists in the DB               |           |
|                                          | System detects duplication                                           |           |
|                                          | System rejects the creation and displays an error message           |           |

 
## Use case Receive Notifications, UC8

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Precondition   | Owner is authenticated && DB services are available &&  internet connection is available |
|  Post condition  | Owner receive the notification  |
| Nominal Scenario | - Owner is notified when an order status changes RN1 <br> - Owner is notified when a batch is expired RN2 <br> - Owner is notified when a cash is not responding RN3 <br> - Owner is notified when a product is going to run out RN4 <br> - Owner is notified when there is no internet connection RN5 <br> - Owner reads the list of notifications RN6 <br> | 
|     Variants     | - Owner is notified when an order status cannot be updated since API is not responding RN1V1 <br> - Owner reads the list of notification and clean it RN6V1 <br> |

### Scenario RN1

|  Scenario RN1  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Order status changes in the system                                         |
| Post condition | Owner receives a notification regarding the new status                     |

#### Steps

| Actor's Action                         | System Action                                                     | FR needed |
|-----------------------------------------|-------------------------------------------------------------------|-----------|
|                                       | System detects order status change                                |           |
|                                        | System generates a notification entity                            |           |
|                                        | System stores the notification in the DB                          |           |
|                                       | System displays the notification in a pop-up                      |           |
| Owner sees the pop-up notification      | System shows the same notification in the notification menu       |           |


### Scenario RN2

|  Scenario RN2  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | A batch expiration date is reached                                         |
| Post condition | Owner receives an expiration notification                                  |

#### Steps

| Actor's Action                         | System Action                                                     | FR needed |
|-----------------------------------------|-------------------------------------------------------------------|-----------|
|                                        | System detects an expired batch        |           |
|                                        | System generates an expiration notification                       |           |
|                                        | System stores the notification in the DB                          |           |
|                                       | System displays the notification in a pop-up                      |           |
| Owner sees the pop-up notification      | System shows the notification in the notification menu            |           |

### Scenario RN3

|  Scenario RN3  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | A cash register does not respond to system polling                         |
| Post condition | Owner receives a notification about the missing response                   |

#### Steps

| Actor's Action                         | System Action                                                     | FR needed |
|-----------------------------------------|-------------------------------------------------------------------|-----------|
|                                       | System polls cash registers                                       |           |
|                                        | System detects no response from a cash register                   |           |
|                                        | System generates a “cash not responding” notification             |           |
|                                        | System stores the notification in the DB                          |           |
|                                        | System displays the notification in a pop-up                      |           |
| Owner sees the pop-up notification      | System shows the notification in the notification menu            |           |

### Scenario RN4

|  Scenario RN4  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Product quantity falls below a stock threshold                             |
| Post condition | Owner receives a low-stock notification                                   |

#### Steps

| Actor's Action                         | System Action                                                     | FR needed |
|-----------------------------------------|-------------------------------------------------------------------|-----------|
|                                        | System monitors product stock levels                              |           |
|                                        | System detects a product is running out                           |           |
|                                       | System generates a low-stock notification                         |           |
|                                        | System stores the notification in the DB                          |           |
|                                        | System displays the notification in a pop-up                      |           |
| Owner sees the pop-up notification      | System shows the notification in the notification menu            |           |

### Scenario RN5

|  Scenario RN5  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | System detects loss of internet connection                                 |
| Post condition | Owner receives a notification about connection loss                        |

#### Steps

| Actor's Action                         | System Action                                                     | FR needed |
|-----------------------------------------|-------------------------------------------------------------------|-----------|
|                                        | System detects internet connectivity failure                      |           |
|                                        | System generates a “no internet connection” notification          |           |
|                                        | System stores the notification in the DB (lan connected)             |           |
|                                        | System displays the notification in a pop-up                      |           |
| Owner sees the pop-up notification      | System shows the notification in the notification menu  |       |

### Scenario RN6

|  Scenario RN6  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | At least one notification exists in the system                             |
| Post condition | Notifications are displayed or marked as read                               |

#### Steps

| Actor's Action                         | System Action                                                     | FR needed |
|-----------------------------------------|-------------------------------------------------------------------|-----------|
| Owner opens the notification menu       | System retrieves notifications from the DB                        |           |
| Owner reads notifications               | System marks notifications as read                                |           |



### Scenario RN1V1

|  Scenario RN1V1 |                                                                           |
| :-------------: | :------------------------------------------------------------------------ |
| Precondition    | System fails to update the order status due to API timeout/failure        |
| Post condition  | Owner receives a notification about the failed update                     |

#### Steps

| Actor's Action                         | System Action                                                     | FR needed |
|-----------------------------------------|-------------------------------------------------------------------|-----------|
|                                        | System attempts to update order status                            |           |
|                                        | System detects API timeout / unreachable provider                 |           |
|                                        | System generates a “status update failed” notification            |           |
|                                        | System stores the notification in the DB                          |           |
|                                       | System displays the notification in a pop-up                      |           |
| Owner sees the pop-up notification      | System shows the notification in the notification menu            |           |

### Scenario RN6V1

|  Scenario RN6V1 |                                                                           |
| :-------------: | :------------------------------------------------------------------------ |
| Precondition    | At least one notification exists in the system                                    |
| Post condition  | All notifications are cleared from the list                               |

#### Steps

| Actor's Action                         | System Action                                                     | FR needed |
|-----------------------------------------|-------------------------------------------------------------------|-----------|
| Owner opens the notification menu       | System retrieves notifications from the DB                        |           |
| Owner selects “Clear notifications”     |                                                                   |           |
|                                         | System deletes or marks all notifications as cleared in the DB    |           |
|                                         | System updates the notification menu to show an empty list        |           |



## Use case Import Data, UC9

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Precondition   | Owner is authenticated && DB services are available && internet connection is available && file .csv data are in the correct format|
|  Post condition  | .csv file's data are correctly imported |
| Nominal Scenario | - Owner imports a set of lists containg products, invoices, suppliers, sales, refunds, orders as .csv file ID1| 
|     Exception    | - Owner imports .csv files with format error ID1E1|

### Scenario ID1

|  Scenario ID1  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Data in .csv files are in the correct format                               |
| Post condition | .csv files are imported into the system                                     |

#### Steps

| Actor's Action                              | System Action                                                       | FR needed |
|----------------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to import .csv files          | System opens file-import dialog                                     |           |
| Owner adds all .csv files                    |                                                                     |           |
|                                              | System checks if .csv files are in the correct format               |           |
|                                              | System imports new data into the system                             |           |

### Scenario ID1E1

|  Scenario IDE1 |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Data in .csv files are not in the correct format                           |
| Post condition | .csv files are not imported into the system                                |

#### Steps

| Actor's Action                              | System Action                                                       | FR needed |
|----------------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to import .csv files          | System opens file-import dialog                                     |           |
| Owner adds all .csv files                     |                                                                     |           |
|                                              | System checks if .csv files are in the correct format               |           |
|                                              | System detects format errors                                        |           |
|                                              | System informs the Owner that some data is not in the correct form  |           |
|                                              | System does **not** import any new data                              |           |


## Use case Export Data, UC10

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Precondition   | Owner is authenticated && DB services are available && internet connection is available && needed data are in the system|
|  Post condition  | data are correctly exported as .csv |
| Nominal Scenario | - Owner exports a set of lists containg products, invoices, suppliers, sales, refunds, orders as .csv file ED1| 
|     Exception    | - Owner exports corrupted .csv files ED1E1|

### Scenario ED1

|  Scenario ED1  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Data to be exported exist in the system                                   |
| Post condition | Data are exported into one or more .csv files                             |

#### Steps

| Actor's Action                             | System Action                                                       | FR needed |
|---------------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to export data as .csv       | System retrieves the requested data from the DB                     |           |
|                                            | System formats the retrieved data in .csv format                    |           |
|                                            | System generates and provides one or more .csv files for download   |           |
| Owner downloads the .csv files              | System confirms successful export                                   |           |

### Scenario ED1E1

|  Scenario ED1E1 |                                                                           |
| :-------------: | :------------------------------------------------------------------------ |
| Precondition    | Data to be exported exist in the system                    |
| Post condition  | Data are NOT correctly exported                 |

#### Steps

| Actor's Action                             | System Action                                                       | FR needed |
|---------------------------------------------|---------------------------------------------------------------------|-----------|
| Owner requests to export data as .csv       | System retrieves data from the DB                                    |           |
|                                            | System attempts to format data into .csv files                      |           |
|                                            | System detects an error during file generation (corrupted output)   |           |
|                                           | System does **not** complete the export process                      |           |
|                                            | System informs the Owner that export has failed due to corrupted output |        |



## Use case Retrieve Data, UC11

| Actors Involved  |                 Owner                                                |
| :--------------: | :----------------------------------------------------------------- |
|   Precondition   | Owner is authenticated && Data are in the system && BD services are available |
|  Post condition  |  Owner retrieves the desidered list of data |
| Nominal Scenario | - Owner generates a list of one selected type: products, invoices, suppliers, sales, refunds, or orders RD1 | 
|     Variants     | - Owner generates a filtered list of one selected type based on specific attributes RDV1|

### Scenario RD1

|  Scenario RD1  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Requested data type exists in the system && Owner is authenticated         |
| Post condition | Owner receives the full list of the selected data type                     |

#### Steps

| Actor's Action                                        | System Action                                                       | FR needed |
|--------------------------------------------------------|---------------------------------------------------------------------|-----------|
| Owner selects a data type to retrieve (e.g. products, invoices, etc.) | System retrieves all records of the selected type from the DB       |           |
|                                                        | System returns the retrieved list to the Owner                      |           |
| Owner views the list                                   | System displays the data in the appropriate UI                      |           |

### Scenario RDV1

|  Scenario RDV1 |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Filterable data exist in the system && Owner is authenticated              |
| Post condition | Owner receives the filtered list                                           |

#### Steps

| Actor's Action                                        | System Action                                                       | FR needed |
|--------------------------------------------------------|---------------------------------------------------------------------|-----------|
| Owner selects a data type to retrieve                  | System opens a filter parameters dialog                             |           |
| Owner inserts filter attributes                        |                                                                     |           |
|                                                        | System retrieves only the records matching the filters from the DB  |           |
|                                                        | System returns the filtered list                                    |           |
| Owner views the filtered list                          | System displays the filtered data in the UI                          |           |



## Use case Manage Accounting, UC12

| Actors Involved  |                 Owner                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Precondition   | Owner is authenticated && DB services are available && internet connection is available|
|  Post condition  | Cash flow is correctly tracked |
| Nominal Scenario | - Owner retrieves incomes at different time granularities MA1<br> - Owner retrieves expenses at different time granularities MA2<br> - Owner retrieves balance at different time granularities MA3 <br> | 

### Scenario MA1

|  Scenario MA1  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Every income is correctly tracked                                          |
| Post condition | Owner retrieves incomes                                                     |

#### Steps

| Actor's Action                     | System Action                                                                  | FR needed |
|------------------------------------|--------------------------------------------------------------------------------|-----------|
| Owner requests the incomes         | System asks for the time window (year)                                         |           |
| Owner chooses the time window      | System asks for the time granularity (day, week, month, quarter, semester, year) |         |
| Owner chooses the granularity      | System retrieves and returns the incomes for the selected window & granularity |           |


### Scenario MA2  

|  Scenario MA2  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Every expenses is correctly tracked                                        |
| Post condition | Owner retrieves expenses                                                  |

#### Steps

| Actor's Action                     | System Action                                                                  | FR needed |
|------------------------------------|--------------------------------------------------------------------------------|-----------|
| Owner requests the expenses       | System asks for the time window (year)                                         |           |
| Owner chooses the time window      | System asks for the time granularity (day, week, month, quarter, semester, year) |         |
| Owner chooses the granularity      | System retrieves and returns the expenses for the selected window & granularity |         |


### Scenario MA3  

|  Scenario MA3  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Every outgoing and every income is correctly tracked                       |
| Post condition | Owner retrieves the balance                                                |

#### Steps

| Actor's Action                     | System Action                                                                  | FR needed |
|------------------------------------|--------------------------------------------------------------------------------|-----------|
| Owner requests the balance         | System asks for the time window (year)                                         |           |
| Owner chooses the time window      | System asks for the time granularity (day, week, month, quarter, semester, year) |         |
| Owner chooses the granularity      | System retrieves and returns the balance (incomes – expenses)                  |           |



## Use case Manage Cash Registers, UC13

| Actors Involved  |                - Main: Owner <br> - Passive: POS provider, Cash Register                                               |
| :--------------: | :------------------------------------------------------------------ |
|  Precondition   | Owner is authenticated && DB services are available && internet connection is available|
|  Post condition  | Cash register's list is up to date |
| Nominal Scenario |  - Owner add a new cash register to the list CR1 <br> - Owner updates a cash register in the list CR2 <br> - Owner deletes a cash register from the list CR3 | 
|     Exception    | - Owner tries to add a cash register that is alredy in the list CR1E1 <br> |

### Scenario CR1

|  Scenario CR1  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Owner is authenticated && DB services are available && internet connection is available |
| Post condition | A new cash register is added to the system                                |

#### Steps

| Actor's Action                                      | System Action                                                     | FR needed |
|------------------------------------------------------|-------------------------------------------------------------------|-----------|
| Owner opens the cash registers list                  |                                                                   |           |
| Owner authenticates on the POS provider website      |                                                                   |           |
| Owner adds a new cash register on the POS provider website |                                                             |           |
| Owner enters the cash register attributes and API token |                                                                |           |
|                                                      | System validates the token with the POS provider                  |           |
|                                                      | System inserts the new cash register into the database            |           |

### Scenario CR2

|  Scenario CR2 |                                                                            |
| :-----------: | :------------------------------------------------------------------------: |
| Precondition  | Owner is authenticated && DB services are available && internet connection is available |
| Post condition| The selected cash register is updated in the system                        |

#### Steps

| Actor's Action                                      | System Action                                                     | FR needed |
|------------------------------------------------------|-------------------------------------------------------------------|-----------|
| Owner opens the cash registers list                  |                                                                   |           |
| Owner selects an existing cash register to update    |                                                                   |           |
| Owner modifies the cash register attributes          |                                                                   |           |
|                                                      | System updates the cash register in the database                  |           |

### Scenario CR3

|  Scenario CR3 |                                                                            |
| :-----------: | :------------------------------------------------------------------------: |
| Precondition  | Owner is authenticated && DB services are available |
| Post condition| The selected cash register is removed from the system                     |

#### Steps

| Actor's Action                                      | System Action                                                     | FR needed |
|------------------------------------------------------|-------------------------------------------------------------------|-----------|
| Owner opens the cash registers list                  |                                                                   |           |
| Owner selects a cash register to delete              |                                                                   |           |
| Owner confirms deletion                              |                                                                   |           |
|                                                      | System removes the cash register from the database                |           |

### Scenario CR1E1

|  Scenario CR1E2 |                                                                            |
| :-------------: | :------------------------------------------------------------------------: |
| Precondition    | Owner is authenticated && DB services are available && internet connection is available |
| Post condition  | No cash register is added, user is notified                                |

#### Steps

| Actor's Action                                      | System Action                                                     | FR needed |
|------------------------------------------------------|-------------------------------------------------------------------|-----------|
| Owner attempts to add a new cash register            |                                                                   |           |
| Owner enters attributes already present in the system|                                                                   |           |
|                                                      | System checks for duplicates                                      |           |
|                                                      | System rejects creation and notifies "Cash register already exists" |         |



## Use case Manage Sales and Refunds, UC14

| Actors Involved  |                 Cash Register                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Precondition   | Cash Registers are turned on && DB services are available && lan connection is available|
|  Post condition  | The system received new sales and refunds from the cash register|
| Nominal Scenario |  - The system ask to the cash register sales MS1 <br> - The system ask to the cash register refunds MS2 <br> | 
|     Exception    | - The data transfer is corrupted MSE1 <br>|


### Scenario MS1

|  Scenario MS1  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
|  Precondition  | Cash registers are turned on && DB services are available && LAN connection is available |
| Post condition | The system stores the new sales provided by the cash register              |

#### Steps

| Actor's Action                                  | System Action                                                  | FR needed |
|--------------------------------------------------|----------------------------------------------------------------|-----------|
|                                                  | System polls the cash register requesting new sales            |           |
| Cash register receives the polling request        |                                                                |           |
| Cash register sends sales data to the system     |                                                                |           |
|                                                  | System receives the sales data                                 |           |
|                                                  | System validates the sales data                                 |           |
|                                                  | System inserts new sales into the database                     |           |

### Scenario MS2

|  Scenario MS2  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
|  Precondition  | Cash registers are turned on && DB services are available && LAN connection is available |
| Post condition | The system stores the new refunds provided by the cash register            |

#### Steps

| Actor's Action                                  | System Action                                                  | FR needed |
|--------------------------------------------------|----------------------------------------------------------------|-----------|
|                                                  | System polls the cash register requesting new refunds          |           |
| Cash register receives the polling request        |                                                                |           |
| Cash register sends refund data to the system    |                                                                |           |
|                                                  | System receives the refund data                                |           |
|                                                  | System validates the refund data                               |           |
|                                                  | System inserts new refunds into the database                   |           |

### Scenario MSE1

|  Scenario MSE1 |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
|  Precondition  | Cash registers are turned on && DB services are available && LAN connection is available |
| Post condition | No new sales/refunds are saved                                             |

#### Steps

| Actor's Action                                   | System Action                                                    | FR needed |
|--------------------------------------------------|------------------------------------------------------------------|-----------|
|                                                  | System polls the cash register requesting data                   |           |
| Cash register sends corrupted/invalid data       |                                                                  |           |
|                                                  | System detects corrupted or unreadable data                      |           |
|                                                  | System rejects the data                                          |           |


## Use case Get Catalogue, UC15

| Actors Involved  |                 Cash Register                                                |
| :--------------: | :------------------------------------------------------------------ |
|  Precondition   |  Cash Registers are turned on && DB services are available && lan connection is available|
|  Post condition  | The cash register internal catalogue is consistent with the db's|
| Nominal Scenario | - The system sends to the cash register the updated catalogue GC1<br>| 
|     Exception    | - The data transfer is corrupted GCE1 <br>|

### Scenario GC1

|  Scenario GC1 |                                                                            |
| :-----------: | :------------------------------------------------------------------------: |
| Precondition  | Cash registers are turned on && DB services are available && LAN connection is available |
| Post condition| Cash register catalogue is aligned with the system catalogue                |

#### Steps

| Actor's Action                                 | System Action                                                      | FR needed |
|------------------------------------------------|----------------------------------------------------------------------|-----------|
|                                                | System polls the cash register to check catalogue synchronization    |           |
| Cash register responds to the polling           |                                                                      |           |
|                                                | System retrieves the latest catalogue from the database              |           |
|                                                | System sends the updated catalogue to the cash register              |           |
| Cash register receives the catalogue            |                                                                      |           |
| Cash register updates its internal data         |                                                                      |           |

### Scenario GCE1

|  Scenario GCE1 |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | Cash registers are turned on && DB services are available && LAN connection is available |
| Post condition | The cash register catalogue is not updated                                 |

#### Steps

| Actor's Action                             | System Action                                                      | FR needed |
|---------------------------------------------|--------------------------------------------------------------------|-----------|
|                                             | System polls the cash register to check catalogue synchronization   |           |
| Cash register responds to the polling        |                                                                    |           |
|                                             | System sends the catalogue to the cash register                     |           |
| Cash register receives corrupted data        |                                                                    |           |
|                                             | System detects corruption (checksum/format error)                   |           |
|                                             | System aborts the catalogue update                                  |           |



## Use case Track Orders, UC16

| Actors Involved  |                 Shipment tracking provider                                               |
| :--------------: | :------------------------------------------------------------------ |
|  Precondition   | DB services are available && internet connection is available|
|  Post condition  | The order status is up to date |
| Nominal Scenario | - The system ask a status update to the shipping tracking service TO1 <br> | 
|     Exception    | - The traking service is unreachable TOE1 <br> |

### Scenario TO1

|  Scenario TO1  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
| Precondition   | DB services are available && internet connection is available              |
| Post condition | The order status is up to date                                             |

#### Steps

| Actor's Action                                              | System Action                                                         | FR needed |
|-------------------------------------------------------------|-----------------------------------------------------------------------|-----------|
|                                                            | System sends an API request to the shipment tracking provider         |           |
| Shipment tracking provider returns updated status           | System receives, validates, and processes the tracking response       |           |
|                                                          | System updates the order status in the database                       |           |
|                                                            | System sends an acknowledgment (ACK) if required by the protocol      |           |


### Scenario TOE1 

|  Scenario TOE1  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
|  Precondition  | DB services are available && internet connection is available | 
| Post condition | The order status is not up to date |

#### Steps

| Actor's Action                                   | System Action                                                    | FR needed |
|--------------------------------------------------|------------------------------------------------------------------|-----------|
|                                               | System sends a request to the shipment tracking provider         |           |
| Shipment tracking provider is unreachable         | System fails to receive a response (timeout / network error)     |           |
|                                              | System logs the communication error                              |           |
|                                              | System stops the status update process                           |           |
|                                                | System keeps the current order status unchanged                  |           |




##### Scenario 1.1

\<describe here scenarios instances of UC1>

\<a scenario is a sequence of steps that corresponds to a particular execution of one use case>

\<a scenario is a more formal description of a story>

\<only relevant scenarios should be described>

|  Scenario 1.1  |                                                                            |
| :------------: | :------------------------------------------------------------------------: |
|  Precondition  | \<Boolean expression, must evaluate to true before the scenario can start> |
| Post condition |  \<Boolean expression, must evaluate to true after scenario is finished>   |


### Steps

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


