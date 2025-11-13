# API reference

## Square POS
- Cash register: [Cash Register](https://squareup.com/us/en/hardware)
- General API reference: [API ref](https://developer.squareup.com/reference/square)
- Connect to cash register: [Hook](https://developer.squareup.com/reference/square/webhook-subscriptions-api)
- Push inventory to cash register: [Push catalogue](https://developer.squareup.com/reference/square/catalog-api/batch-upsert-catalog-objects)
- Retrieve receipts: [Pull receipts](https://developer.squareup.com/reference/square/payments-api/get-payment) -> and use `receipt_url ` field
- Retrieve invoices: [Pull invoices](https://developer.squareup.com/reference/square/invoices-api/list-invoices)

---

## Clover POS
- Cash register: [Cash Register](https://www.clover.com/pos-systems)
- General API reference: [API ref](https://docs.clover.com/dev/reference/api-reference-overview#)
- Connect to cash register: [Hook](https://docs.clover.com/dev/docs/merchant-interaction)
- Push inventory to cash register: [Push catalogue](https://docs.clover.com/dev/docs/managing-items-item-groups)
- Retrieve receipts: [Pull receipts](https://docs.clover.com/dev/docs/orders)
- Retrieve invoices: [Pull invoices]()

---

## SumUp POS
- Cash register: [Cash Register](https://www.sumup.com/it-it/panoramica-registratore-di-cassa/?prc=ITBF2025-s-ITBF2025-s-ITBF2025-s-ITBF2025-s-ITBF2025-s-ITBF2025-s-ITBF2025-s-ITBF2025-s-ITBF2025-s-ITBF2025)
- General API reference: [API ref](https://developer.sumup.com/api)
- Connect to cash register: [Hook]()
- Push inventory to cash register: [Push catalogue]()
- Retrieve receipts: [Pull receipts](https://developer.sumup.com/api/transactions/get)
- Retrieve invoices: [Pull invoices]()

---

## Nexi POS
- Cash register: [Cash Register]()
- General API reference: [API ref](https://developer.nexi.it/it/api/introduzione)
- Connect to cash register: [Hook]()
- Push inventory to cash register: [Push catalogue]()
- Retrieve receipts: [Pull receipts]()
- Retrieve invoices: [Pull invoices]()

---

## LightSpeed POS
- Cash register: [Cash Register]()
- General API reference: [API ref](https://developers.lightspeedhq.com/retail/introduction/introduction/)
- Connect to cash register: [Hook](https://developers.lightspeedhq.com/retail/authentication/authentication-overview/)
- Push inventory to cash register: [Push catalogue](https://developers.lightspeedhq.com/retail/endpoints/Item/)
- Retrieve receipts: [Pull receipts](https://developers.lightspeedhq.com/retail/endpoints/Sale/)
- Retrieve invoices: [Pull invoices]()

---
Excellent questions — this is exactly the kind of detail your Requirements and Design sections need. Let’s walk through how the Square POS API actually works when you want to:

- Connect your EZShop management software to a physical Square POS device  
- Push your catalogue (products)  
- Receive completed sales (receipts)  
- Handle authentication and authorization (OAuth)  

---

## 🧩 1. How “connecting to a POS” actually works in Square

There’s **no direct “pair this device” API call**.

Instead, Square ties everything to a **Square merchant account** (the shop owner’s account) and its **locations**.

Each physical POS device (like Square Register, Square Terminal, etc.) logs in to a **merchant’s account** and operates under a **location ID**.  
Your app integrates at the **account level**, not directly to a specific hardware device.

So in practice:

1. You register your app in the **Square Developer Dashboard**.  
2. The shop owner uses OAuth (“Sign in with Square”) to authorize EZShop.  
3. Your app receives an **access token** tied to that merchant account.  
4. You use the `/v2/locations` endpoint to list all locations (stores/registers) associated with the account.  
5. Any POS device logged into that merchant’s account will automatically sync catalog and orders for its assigned location.  

---

## 🧱 2. Pushing your catalogue to the POS

Once you have the merchant’s access token and the location ID, you can send catalog data via the **Catalog API**.

Typical workflow:

1. Your EZShop app builds a product list using Square’s `CatalogObject` model (items, categories, modifiers, etc.).  
2. Use the [`/v2/catalog/batch-upsert`](https://developer.squareup.com/reference/square/catalog-api/batch-upsert-catalog-objects) endpoint to push products.  
3. The changes automatically propagate to all POS devices logged in under that merchant’s account and location.

✅ No direct device connection is needed — synchronization happens via the merchant’s Square account.

---

## 💸 3. Receiving completed sales (receipts)

When a transaction occurs on a Square POS terminal:

1. The POS device records a **Payment** (via the Payments API).  
2. That Payment is linked to an **Order** (via the Orders API).  
3. Your app can:
   - **Subscribe to webhooks** like `payment.created`, `order.updated`, etc.  
   - Or **poll the API** periodically to fetch new transactions.

The preferred method is **webhooks**, since Square will automatically send your app a POST request when events occur.

For example:
- Webhook topic: `payment.created` → a new sale is completed  
- Your app receives the event payload, extracts the `payment_id`, and calls `/v2/payments/{payment_id}` or `/v2/orders/{order_id}` for details  
- You store the sale in EZShop’s database and update inventory accordingly  

Webhook setup documentation:  
👉 [Square Webhooks Overview](https://developer.squareup.com/docs/webhooks/overview)

---

## 🔐 4. OAuth (Authentication and Authorization)

Square requires **OAuth 2.0** for third-party integrations.  
This allows shop owners to securely link their Square account to EZShop without sharing credentials.

The sequence looks like this:

1. EZShop redirects the user to Square’s OAuth authorization URL.  
2. The user logs in and grants your app permission.  
3. Square redirects back with an authorization code.  
4. EZShop exchanges the code for an **access token** via the OAuth API.  
5. That token is stored securely and used for all future API calls on behalf of the merchant.

Documentation:  
👉 [Square OAuth API](https://developer.squareup.com/docs/oauth-api/overview)

---

## 🧾 Example Flow Summary

| Step | Action | API |
|------|---------|-----|
| 1 | Shop owner authorizes EZShop via OAuth | `/oauth2/authorize` |
| 2 | EZShop receives access token | `/oauth2/token` |
| 3 | EZShop lists merchant locations | `/v2/locations` |
| 4 | EZShop pushes product catalog | `/v2/catalog/batch-upsert` |
| 5 | POS device performs a sale | (handled by Square POS) |
| 6 | Square notifies EZShop via webhook | `/v2/webhooks` |
| 7 | EZShop retrieves sale/order details | `/v2/payments` & `/v2/orders` |


## 🧩 Common Conceptual Model Across POS APIs

| Concept | Common Meaning | Square | Clover | Lightspeed | SumUp | Nexi |
|:--------|:----------------|:--------|:---------|:-------------|:--------|:--------|
| **Merchant / Account** | The business entity that owns the POS system | `merchant` | `merchant` | `account` | `merchant` | `merchant` |
| **Location / Store** | A physical place or branch where sales occur | `location` | `merchant` → `merchant_id` (single store, or `multi-merchant` mode) | `shop` | `profile` (limited) | `store` |
| **Device / Terminal** | The physical POS hardware (register, reader, etc.) | `device` (implicit via location) | `device` (registered) | `register` | `terminal` | `terminal` |
| **Catalog / Inventory** | The list of products, variants, prices, and stock | `catalog` | `items` | `Item` | `products` | `catalog` |
| **Order / Transaction** | A record of a sale with its items and totals | `order` | `order` | `Sale` | `checkout` | `transaction` |
| **Payment** | Details of how the order was paid | `payment` | `payment` | `Payment` | `transaction` | `payment` |
| **Invoice** | A bill sent to a customer (B2B or deferred) | `invoice` | `invoice` | `Invoice` | `invoice` | `fattura elettronica` |
| **Customer** | Customer info linked to transactions | `customer` | `customer` | `Customer` | `customer` | `customer` |
| **Webhook / Event** | Real-time notification of actions | `webhook` | `webhook` | `Webhook` | `webhook` | (limited) |
| **OAuth / Token** | Authorization flow for your app | `OAuth` | `OAuth2` | `OAuth2` | `OAuth2` | `OAuth2` |

---

## 🔁 Common Integration Methodology

Despite vendor differences, all open POS systems share this **standard three-phase pattern**:

### 1️⃣ Authorization Phase
- Your app (EZShop) must be registered in the POS provider’s **developer dashboard**.  
- You integrate an **OAuth 2.0** flow so the shop owner (merchant) can grant your app permission to access their account.  
- The provider returns an **access token**, which you store securely and use for all subsequent API calls.

🧠 Analogy:  
> “The shop owner logs in with Square/Clover/… and authorizes EZShop to sync their sales and catalog.”

---

### 2️⃣ Synchronization Phase
- Your app **pushes the catalog** (products, prices, categories) to the POS provider’s system.
- Optionally, you may **pull the catalog** if the POS is the master source.
- You typically identify the **location** or **store** where these apply.

🧠 Analogy:  
> “EZShop sends its product list to the POS at the downtown shop.”

---

### 3️⃣ Transaction Tracking Phase
- The POS system generates sales, payments, and possibly invoices locally.
- Your app **subscribes to webhooks** (or polls endpoints) for:
  - `order.created`
  - `payment.updated`
  - `refund.created`
- On receiving these events, you **pull detailed data** (order, payment, receipt) and update EZShop’s internal records.

🧠 Analogy:  
> “When a sale is completed on the POS, EZShop automatically updates its sales and inventory data.”

---

## 🧱 Differences Between APIs (in Practice)

| Area | Square | Clover | Lightspeed | SumUp | Nexi |
|------|--------|--------|-------------|--------|--------|
| **Webhooks** | Full event system | Limited but available | Good support | Basic | Minimal |
| **Inventory detail** | Rich & structured | Medium | Very rich | Basic | Limited |
| **Invoices** | Complete API | Basic | Good | Partial | Excellent (e-invoicing) |
| **Hardware integration** | Excellent | Excellent | Good | Good | Very tied to bank |
| **API openness** | Public, self-service | Requires developer registration | Public | Semi-open | Partially closed (requires approval) |
| **Typical market** | Global, SMB | US/EU retail | EU retail | Microbusiness | Italian retail / fiscal POS |

---

## ⚙️ So, for your requirement document…

The **Square-based model** you’re defining is **a good reference baseline** for all these vendors.  
You can later adapt interface requirements like so:

- **FR1.1.1 – Read sale from POS:**  
  Implement via webhook subscription (`order.created`) or polling API.

- **FR2.x – Manage catalog:**  
  Implement via batch push to `/catalog` (Square) or `/items` (Clover).

- **FRx.x – Connect to POS:**  
  Use OAuth authorization to connect merchant → EZShop → POS.

Your **interface table** with:
is **fully valid and generalizable**.

---

## 🧭 Key Square API Terminology (reference for your model)

| Square Term | Meaning | Analogy in EZShop | Notes / Tips |
|--------------|----------|------------------|---------------|
| **Merchant** | The **business account** that owns the Square POS, locations, catalog, and transactions. Every Square account corresponds to one merchant entity. | **Shop Owner / Business** | Root entity you connect to using OAuth. |
| **Location** | A **specific shop or POS location** under a merchant’s account. A merchant can have multiple locations. | **Physical store or cash register location** | Identified by `location_id`. Needed when pushing catalogues or reading sales. |
| **Device** | A **hardware POS terminal** (Square Register, Reader, Terminal) that operates under a specific `location_id`. | **Cash Register** | You don’t “connect” directly — they sync via their location. |
| **Catalog** | Collection of `CatalogObject` items — products, modifiers, discounts, taxes, etc. | **Product list / Inventory** | Managed via Catalog API. |
| **Order** | A record of a customer transaction, including line items, taxes, and discounts. | **Sale transaction / Receipt** | Created automatically when a sale occurs. |
| **Payment** | A record of how an order was paid. | **Payment details for a sale** | Linked to an Order. |
| **Customer** | A stored customer profile. | **Customer entity** | Optional in your scope. |
| **Invoice** | A bill sent to a customer for later payment. | **Invoice object / Sale on account** | Different from a receipt — invoices are not created automatically. |
| **Webhook** | HTTP callback Square sends when an event occurs. | **Event listener in EZShop** | Use this to stay updated. |
| **Application** | Your registered Square integration. | **EZShop connector** | Managed in Square Developer Dashboard. |
| **Access Token** | OAuth token granting your app permission to act on behalf of a merchant. | **Stored API credential in EZShop** | Required for all API calls. |
| **Sandbox** | A test environment with fake merchants, locations, and transactions. | **Test mode** | Used for development. |

---

## 🧾 Example Flow

1. **Merchant** (your shop owner) logs into EZShop.  
2. They click “Connect with Square” — triggers OAuth.  
3. EZShop gets an **access token** for that merchant.  
4. EZShop calls `/v2/locations` — retrieves merchant’s **locations**.  
5. EZShop calls `/v2/catalog/batch-upsert` — updates **catalog**.  
6. A customer completes a sale at one of the **devices**.  
7. Square creates an **order** and **payment**.  
8. Square sends your webhook an event like `order.created`.  
9. EZShop retrieves full order details via **Orders API**.  

---

| ID | Description |
|:--:|:-------------|
| **FR1.0**| **Manage sales** |
| *FR1.2* | *Create owner-defined sale list* |
| FR1.2.1 | For each owner-defined list filter sales by a specified date (ISO 8601) or time window |
| FR1.2.2 | Retrieve sales filtered by products sold |
| FR1.2.3 | Retrieve sales ranked by number of items sold per specific product |
| FR1.2.4 | Retrieve sales ranked by the sum of its item's prices |
| *FR1.3* | *Manage `.csv`* |
| FR1.3.1 | Import sales list from `.csv` |
| FR1.3.2 | Export list of sales as `.csv` |
| **FR1.0**| **Manage refunds** |
| *FR1.2* | *Create owner-defined refund list* |
| FR1.2.1 | For each owner-defined list filter refunds by a specified date (ISO 8601) or time window |
| FR1.2.2 | Retrieve refunds filtered by products sold |
| FR1.2.3 | Retrieve refunds ranked by number of items given back per specific product |
| FR1.2.4 | Retrieve refunds ranked by the sum of its item's prices |
| *FR1.3* | *Manage `.csv`* |
| FR1.3.1 | Import refunds list from `.csv` |
| FR1.3.2 | Export list of refunds as `.csv` |
| **FR2** | **Manage catalogue** |
| *FR2.1* | *Manage CRUD operations* |
| FR2.1.1 | Create new product in the catalogue |
| FR2.1.2 | Update product from the catalogue |
| FR2.1.3 | Delete product from the catalogue |
| *FR2.2* | *Set product item quantity warning threshold* |
| *FR2.3* | *Create owner-defined product list* |
| FR2.3.4 | Retrieve list of products filtered by one or more of their attributes |
| FR2.3.5 | Retrieve number of items available for the selected product (sum of the quantity on each batch with the selected product) |
| *FR2.4* | *Manage `.csv`* |
| FR2.4.1 | Import product list from `.csv` |
| FR2.4.2 | Export list of products as `.csv` |
| **FR2.5** | *Update cash register's catalogue* |
| FR2.5.1 | Convert catalogue to API-specific format |
| FR2.5.2 | Check connection with cash register |
| FR2.5.3 | Send updated catalogue to connected cash register|
| **FR3** | **Manage inventory** |
| *FR3.1* | *Manage CRUD operations* |
| FR3.1.1 | Create new batch in the inventory |
| FR3.1.2 | Update batch from the inventory |
| FR3.1.3 | Delete batch from the inventory |
| *FR3.2* | *Create owner-defined batch list* |
| FR3.2.1 | Retrieve batches filtered by one or more product/batch attributes |
| *FR3.3* | *Manage `.csv`* |
| FR3.3.1 | Import batches list from `.csv` |
| FR3.3.2 | Export list of batches as `.csv` |
| **FR4** | **Manage orders** |
| *FR4.1* | *Manage CRUD operations* |
| FR4.1.1 | Create new order in the list of orders |
| FR4.1.2 | Update order from the list of orders |
| FR4.1.3 | Delete order from the list of orders |
| *FR4.2* | *Automatically track order for supported curriers* |
| FR4.2.1 | Check internet connection |
| FR4.2.2 | Retrieve current order's status |
| FR4.2.3 | Update current order's status |
| *FR4.3* | *Create owner-defined orders list* |
| FR4.3.1 | Retrieve list of orders filtered by one or more of their attributes |
| *FR4.4* | *Manage `.csv`* |
| FR4.4.1 | Import orders list from `.csv` |
| FR4.4.2 | Export list of orders as `.csv` |
| FR4.5   | *Suggest order* |
| FR4.5.1 | Retrieve products with item count below threshold |
| FR4.5.2 | Retrieve possible supplier for products with item count below threshold|
| FR4.5.3 | Generate order suggestion (without specifying the number of item) |
| FR4.5.4 | Add suggested order to list of orders|
| **FR5** | **Manage accounting** |
| *FR5.1* | *Track invoices* |
| FR5.1.1 | Track Invoices for orders made |
| FR5.1.2 | Create owner-defined invoice list |
| FR5.1.2.1 | Retrieve list of invoices filtered by one or more of their attributes |
| *FR5.2* | *Track incomes* |
| FR5.2.1 | Track incoming cash flow |
| FR5.2.3 | Retrieve income history at different time granularities (day, month, year etc…) |
| *FR5.3* | *Track expense* |
| FR5.3.1 | Track outgoing cash flow |
| FR5.3.2 | Retrieve outgoing history at different time granularities (day, month, year etc…) |
| *FR5.4* | *Track balance* |
| FR5.4.1 | Compute total balance based on incomes and expense with respect to day, week, month, quarter, semester, and year|
| FR5.4.2 | Retrieve current balance with respect to the current day, week, month, quarter, semester, and year|
| FR5.4.3 | Retrieve balance history  |
| **FR6** | **Authenticate owner** |
| FR6.1 | Set password |
| FR6.2 | Change password |
| FR6.3 | Verify password |
| FR6.4 | Encrypt password |
| FR6.5 | Decrypt password |
|**FR7** | **Manage notifications** |
| FR7.1 | Notify owner of order's status change |
| FR7.2 | Notify owner of when order status cannot be changed automatically (API not responding)|
| FR7.3 | Notify owner when quantity of a certain product is below a owner set threshold |
| FR7.4 | Notify owner when batch is within x days from expiration date (ISO 8601)|
| FR7.5 | Notify owner when batch is past the expiration date (ISO 8601)|
| FR7.6 | Notify owner when there is no internet connection |
| FR7.7 | Notify owner when cash register is not responding |
| FR7.8 | Delete notification |
|**FR8**| **Manage Cash registers**|
- Link with POS provider's account 
    * Redirect user to POS provider's authorization URL
    * Retrieve access Token and refresh token
        + Encrypt access token
    * Retrieve new token when old token is expired
- Get cash register list
    * Decrypt access token
    * Retrieve list of cash registers using POS provider's API and access token
    * Update local list of cash registers
- Sync catalogue
    * Convert catalogue to POS provider compliant format
    * Push new catalogue to found cash registers
    * Detect unresponsive (POS API returns error message or fails to respond within default timeout threshold) cash register and update its status
- Retrieve sales
    * Pull sales list from found cash registers
    * Convert sales list to EzShop compliant format
    * Update item quantities in the inventory
    * Add sale to sales list
    * Detect unresponsive (POS API returns error message or fails to respond within default timeout threshold) cash register and update its status
- Retrieve refunds
    * Pull refunds list from found cash registers
    * Convert refunds list to EzShop compliant format
    * Update item quantities in the inventory
    * Add refunds to sales list
    * Detect unresponsive (POS API returns error message or fails to respond within default timeout threshold) cash register and update its status
- Create owner-defined list of cash registers
    * Retrieve list of cash registers filtered by one or more of its attributes
    * Retrieve list of cash registers grouped by the POS provider's brand
 
---

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
| **FR5** | **Manage orders** |
| *FR5.1* | *Manage CRUD operations* |
| FR5.1.1 | Create new order in the list of orders |
| FR5.1.2 | Update order from the list of orders |
| FR5.1.3 | Delete order from the list of orders |
| *FR5.2* | *Automatically track order for supported couriers* |
| FR5.2.1 | Check internet connection |
| FR5.2.2 | Retrieve current order's status |
| FR5.2.3 | Update current order's status |
| *FR5.3* | *Create owner-defined orders list* |
| FR5.3.1 | Retrieve list of orders filtered by one or more of their attributes |
| *FR5.4* | *Manage `.csv`* |
| FR5.4.1 | Import orders list from `.csv` |
| FR5.4.2 | Export list of orders as `.csv` |
| *FR5.5* | *Suggest order* |
| FR5.5.1 | Retrieve products with item count below threshold |
| FR5.5.2 | Retrieve possible supplier for products with item count below threshold |
| FR5.5.3 | Generate order suggestion (without specifying the number of items) |
| FR5.5.4 | Add suggested order to list of orders |
| **FR6** | **Manage accounting** |
| *FR6.1* | *Track invoices* |
| FR6.1.1 | Track invoices for orders made |
| FR6.1.2 | Create owner-defined invoice list |
| FR6.1.2.1 | Retrieve list of invoices filtered by one or more of their attributes |
| *FR6.2* | *Track incomes* |
| FR6.2.1 | Track incoming cash flow |
| FR6.2.2 | Retrieve income history at different time granularities (day, month, year etc…) |
| *FR6.3* | *Track expenses* |
| FR6.3.1 | Track outgoing cash flow |
| FR6.3.2 | Retrieve outgoing history at different time granularities (day, month, year etc…) |
| *FR6.4* | *Track balance* |
| FR6.4.1 | Compute total balance based on incomes and expenses with respect to day, week, month, quarter, semester, and year |
| FR6.4.2 | Retrieve current balance with respect to the current day, week, month, quarter, semester, and year |
| FR6.4.3 | Retrieve balance history |
| **FR7** | **Authenticate owner** |
| FR7.1 | Set password |
| FR7.2 | Change password |
| FR7.3 | Verify password |
| FR7.4 | Encrypt password |
| FR7.5 | Decrypt password |
| **FR8** | **Manage notifications** |
| FR8.1 | Notify owner of order's status change |
| FR8.2 | Notify owner of when order status cannot be changed automatically (API not responding) |
| FR8.3 | Notify owner when quantity of a certain product is below a owner set threshold |
| FR8.4 | Notify owner when batch is within x days from expiration date (ISO 8601) |
| FR8.5 | Notify owner when batch is past the expiration date (ISO 8601) |
| FR8.6 | Notify owner when there is no internet connection |
| FR8.7 | Notify owner when cash register is not responding |
| FR8.8 | Delete notification |
| **FR9** | **Manage cash registers** |
| *FR9.1* | *Link with POS provider's account* |
| FR9.1.1 | Redirect user to POS provider's authorization URL |
| FR9.1.2 | Retrieve access token and refresh token |
| FR9.1.3 | Encrypt access token |
| FR9.1.4 | Retrieve new token when old token is expired |
| *FR9.2* | *Get cash register list* |
| FR9.2.1 | Decrypt access token |
| FR9.2.2 | Retrieve list of cash registers using POS provider's API and access token |
| FR9.2.3 | Update local list of cash registers |
| *FR9.3* | *Sync catalogue* |
| FR9.3.1 | Convert catalogue to POS provider compliant format |
| FR9.3.2 | Push new catalogue to found cash registers |
| FR9.3.3 | Detect unresponsive (POS API returns error message or fails to respond within default timeout threshold) cash register and update its status |
| *FR9.4* | *Retrieve sales* |
| FR9.4.1 | Pull sales list from found cash registers |
| FR9.4.2 | Convert sales list to EzShop compliant format |
| FR9.4.3 | Update item quantities in the inventory |
| FR9.4.4 | Add sale to sales list |
| FR9.4.5 | Detect unresponsive (POS API returns error message or fails to respond within default timeout threshold) cash register and update its status |
| *FR9.5* | *Retrieve refunds* |
| FR9.5.1 | Pull refunds list from found cash registers |
| FR9.5.2 | Convert refunds list to EzShop compliant format |
| FR9.5.3 | Update item quantities in the inventory |
| FR9.5.4 | Add refunds to sales list |
| FR9.5.5 | Detect unresponsive (POS API returns error message or fails to respond within default timeout threshold) cash register and update its status |
| *FR9.6* | *Create owner-defined list of cash registers* |
| FR9.6.1 | Retrieve list of cash registers filtered by one or more of its attributes |
| FR9.6.2 | Retrieve list of cash registers grouped by the POS provider's brand |

