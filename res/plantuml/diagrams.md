## Context diagram
```plantuml
@startuml contextDiagram
skinparam backgroundColor #fcf7f2
skinparam actorStyle Hollow

usecase "EzShop" as shop
actor "Owner" as owner
actor "Cash register" as cs
actor "Shipment tracking provider" as stp
actor "POS provier" as pos

shop <--> owner 
shop <-- cs
shop <-- stp
shop <-- pos

@enduml

```

---
## Glossary diagram
```plantuml
@startuml glossaryDiagram
!pragma layout smetana
skinparam backgroundColor #fcf7f2

class Shop {
    + name
    + address
}

class Product {
    + id
    + name
    + description
    + price
    + category
    + brand
    + discount
    + IVA
}

class Batch {
    + code
    + expirationDate
    + productionDate
}

class Item {
    + id
    + status
}

class Sale {
}

class Refund {
}

class Catalogue {
}

class Inventory {
}

class Supplier {
    + id
    + name
    + pIva
    + contactInfo
    + address
}

class Invoice {
}

class Order {
    + id
    + status
    + orderDate
    + deliveryDate
}

class Income {
    + id
    + amount
    + date
    + source
}

class Expense {
    + id
    + amount
    + date
    + source
}

class Balance {
    + totalIncome
    + totalExpenses
}

class Owner {
    + id
    + password
}

class CashRegister {
    + id
    + location
    + provider
    + accessToken
    + refreshToken
}

class ShippingCompany {
    + id
    + name
    + apiAvailable
    + contactInfo
}

class Notification {
    + id
    + message
    + date
    + status
    + tag
}


Balance  -- "0..*" Expense: > based on 
Balance  -- "0..*" Income: > based on

Sale "0.*" -- "1.*" Product : has
Refund "0.*" -- "1.*" Product: has
Catalogue  -- "1.*" Product:has
Batch "0..*" --  Product: related to
Supplier "1..*" -- "1..*" Product: provides


(Sale, Product) .. SaleOf
class SaleOf{
    + quantity
}
(Refund, Product) .. RefundOf
class RefundOf{
    + quantity
}

Batch  -- "1..*" Item: > has

Order  -- "1..*" Batch: > has
Order "0..*" -- "1..*" Supplier: > made to 
Order "0..*" -- "1..*" ShippingCompany: > delivered by 

Invoice --  Order:> associated with

CashRegister  -- "0..*" Refund: > sends
CashRegister  -- "0..*" Sale: > sends
CashRegister "0..*" -- "0,1" Catalogue: > receives

Inventory  -- "0..*" Batch: > contains

Income <|-- Sale
Expense <|-- Refund
Expense <|-- Invoice


Owner  -- "1..*" Shop:> manages
Owner  -- "1..*" Notification:> interacts with

Shop -- Inventory : > has

Refund .r[hidden]. Catalogue
Catalogue .r[hidden]. Sale


@enduml

```

---
## UseCase diagram
```plantuml
@startuml usecaseDiagram
left to right direction 
!pragma layout smetana
skinparam backgroundColor #fcf7f2

usecase "manage accounting" as mnga
usecase "manage product catalogue" as mngc
usecase "manage orders" as mngo
usecase "manage suppliers" as mngs
usecase "manage cash register" as mngcs
usecase "manage inventory" as mngiv
usecase "manage invoices" as mngio
usecase "manage shipping companies" as mngsc
usecase "manage sales and refunds" as mngsr

usecase "get catalogue" as getc
usecase "track orders" as tracko

usecase "authenticate owner" as auth
usecase "change password" as password

usecase "import data" as import
usecase "export data" as export
usecase "retrieve data data" as retrieve

usecase "receive notification" as notification


actor owner
actor "POS provider" as pos
actor "cash register" as cs
actor "shipment tracking provider" as stp


owner --> mnga
owner --> mngc
owner --> mngo
owner --> mngs
owner --> mngcs
owner --> mngiv
owner --> mngio
owner --> mngsc
owner --> mngsr

owner --> password
owner --> import
owner --> export
owner --> getc
owner <-- notification
owner <-- retrieve

mnga --> auth : <<include>>
mngc --> auth : <<include>>
mngo --> auth : <<include>>
mngs --> auth : <<include>>
mngcs --> auth : <<include>>
mngiv --> auth : <<include>>
mngio --> auth : <<include>>
mngsc --> auth : <<include>>
mngsr --> auth : <<include>>
export --> auth : <<include>>
import --> auth : <<include>>
password --> auth : <<include>>
notification --> auth : <<include>>
retrieve --> auth : <<include>>


cs --> mngsr
cs <-- getc

stp <-- tracko

pos <-- mngcs

@enduml

```



---
## Deployment diagram
```plantuml
@startuml deploymentDiagram
!pragma layout smetana
skinparam backgroundColor #fcf7f2

' Define artifact symbol with file icon
artifact "POS service" as POS
artifact "EzShop Windows app" as EzShopWinApp
artifact "Order tracking service" as OrderTracking
artifact "DB service" as DBService
artifact "EzShop back end" as EzShopBackEnd

node "Cash register" as CashRegister
node "client Windows computer" as ClientPC
node "Shipping company service" as ShippingService
node "EzShop server" as EzShopServer
node "POS provider" as pos

' Deployment relationships (dashed with <<deploy>>)
POS --> CashRegister : <<deploy>>
EzShopWinApp --> ClientPC : <<deploy>>
OrderTracking --> ShippingService : <<deploy>>
DBService --> EzShopServer : <<deploy>>
EzShopBackEnd --> EzShopServer : <<deploy>>

' Network links (solid lines with labels)
CashRegister -r- EzShopServer : LAN link
ClientPC -l- EzShopServer : LAN link
ClientPC -r- ShippingService : internet link
EzShopServer -- pos: internet link
@enduml

```

