- **Manage CRUD operations**
    * *Inherited by: product, batch, suppliers, orders, invoices*
        + Create data entry (user action)
    * *Inherited by: product, batch, sales, refunds, suppliers, orders, invoices, cash registers*
        + Add data entry (system action)
        + Read data entry
        + Update data entry
        + Delete data entry
- **Manage data list**
    * *Inherited by: catalogue, inventory, sales, refunds, suppliers, orders, invoices, cash registers*
        * Combine filter and sorting/ranking operations on a list
    * *Inherited by: catalogue, inventory, sales, refunds, suppliers, orders, invoices, cash registers*
        + Search entry by its unique identifier
        + Filter list by one or more of the entry's attributes
        + Sort list by one or more of the entry's sortable attributes
        + Rank list by one or more of the entry's sortable attributes
    * *Inherited by: inventory, sales, refunds, orders, invoices*
        + Filter list by a specific time window
- **Manage inventory** 
    * Detect bach expiration
        + Detect batches within owner-defined days from the expiration date
        + Detect expired batches
- **Manage orders** 
    * *Automatically track order for supported couriers*
        + Check internet connection
        + Retrieve current order status
        + Update current order status
    * *Suggest order*
        + Retrieve products with item count below owner defined threshold
        + Retrieve possible supplier for products with item count below owner defined threshold
        + Generate order suggestion
        + Add suggested order to the list of orders
- **Manage `.csv`**
    * *Inherited by: catalogue, inventory, sales, refunds, suppliers, orders, invoices, cash registers*
        + Import data from `.csv` file
            + Detect import errors
            + Update data using selected (create, update, remove duplicates, ...) import strategy
        + Export data to `.csv` file 
            + Retrieve domain-specific data
            + Create `.csv` file and write the converted data in it
            + Detect exporting errors
- **Manage accounting**
    * *Inherited by: incomes, expenses, balance*
        + Compute at different time granularities
    * *Inherited by: incomes, expenses, balance*
        + Retrieve at different time granularities
- **Authenticate owner**
    * Set password
    * Change password
    * Verify password
    * Store password securely
- **Manage notifications**
    * Generate notification
    * Change notification status (read, unread, ...)
    * Delete notification
- **Manage cash registers**
    * *Link with POS provider’s account*
        + Redirect user to authorization URL
        + Retrieve access and refresh tokens
        + Store access and refresh tokens securely
        + Retrieve new token when expired
    * *Push data - inherited by: catalogue*
        + Convert data to POS provider's format
        + Push new data to cash registers
        + Detect unresponsive cash registers and update its status
    * *Retrieve data - inherited by: sales, refunds, cash registers*
        + Pull data list
        + Convert data list to application format
        + Update local data list
        + Detect unresponsive cash registers and update its status
