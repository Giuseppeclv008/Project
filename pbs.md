
# Estimate by product decomposition

###

| component name                                                | Estimated effort (person hours) |
| ------------------------------------------------------------  | ------------------------------- |
| _requirement document_                                        |              100                |
| _design document_                                             |               20                |
| _Desktop front-end_                                           |               42                |
| &nbsp;&nbsp;  _UI Login-page_                                 |               3                 |
| &nbsp;&nbsp;  _Dashboard page_                                |               8                 |
| &nbsp;&nbsp;  _Catalogue page_                                |                                 |
| &nbsp;&nbsp;&nbsp; catalogue filters and user-defined list    |                                 |
| &nbsp;&nbsp;&nbsp; manual insertion of the product threshold  |                                 |
| &nbsp;&nbsp;  _Inventory page_                                |               6                 |
| &nbsp;&nbsp;&nbsp; inventory filters and user-defined list    |                                 |
| &nbsp;&nbsp;  _Sales page_                                    |               10                |
| &nbsp;&nbsp;&nbsp; Sales filters and user-defined list        |               5                 |
| &nbsp;&nbsp;&nbsp; refunds filters and user-defined list      |               5                 |
| &nbsp;&nbsp;  _Orders page_                                   |               4                 |
| &nbsp;&nbsp;&nbsp; suppliers filters and user-defined list    |                                 |
| &nbsp;&nbsp;&nbsp; orders filters and user-defined list       |                                 |
| &nbsp;&nbsp;&nbsp; suggested orders tab                       |                                 |
| &nbsp;&nbsp;&nbsp; orders status tab                          |                                 |
| &nbsp;&nbsp;  _Accounting page_                               |               4                 |
| &nbsp;&nbsp;&nbsp; invoices filters and user-defined list     |               5                 |
| &nbsp;&nbsp;&nbsp; field to change the invoice status         |                                 |
| &nbsp;&nbsp;&nbsp; income data with different granularities   |                                 |
| &nbsp;&nbsp;&nbsp; expenses data with different granularities |                                 |
| &nbsp;&nbsp;&nbsp; balance data                               |                                 |
| &nbsp;&nbsp;  _Profile page_                                  |               3                 |
| &nbsp;&nbsp;  _Notification section_                          |               3                 |
| &nbsp;&nbsp;  _cash register page_                            |               3                 |
| &nbsp;&nbsp;&nbsp; filters and user-defined list              |               3                 |
|_Backend_                                                      |                                 |
| &nbsp;&nbsp; _Authentication_                                 |               15                |
| &nbsp;&nbsp;&nbsp;  set username-password                     |               3                 |
| &nbsp;&nbsp;&nbsp;  change username-password                  |               4                 |
| &nbsp;&nbsp;&nbsp;  verification                              |               4                 |
| &nbsp;&nbsp;&nbsp;  encryption                                |               4                 |
| &nbsp;&nbsp; _Csv management_                                 |                                 |
| &nbsp;&nbsp;&nbsp;  csv read                                  |               2                 |
| &nbsp;&nbsp;&nbsp;  csv write                                 |               2                 |
| &nbsp;&nbsp;&nbsp;  csv download                              |               3                 |
| &nbsp;&nbsp;&nbsp;  csv error detection                       |                                 |
| &nbsp;&nbsp;&nbsp;  csv data correction                       |                                 |
| &nbsp;&nbsp; _Order management_                               |               20                |
| &nbsp;&nbsp;&nbsp;  CRUD operations over orders               |               10                |
| &nbsp;&nbsp;&nbsp;  send order request                        |               4                 |
| &nbsp;&nbsp;&nbsp;  update order status                       |               4                 |
| &nbsp;&nbsp;&nbsp;  csv import management                     |               6                 |
| &nbsp;&nbsp; _API integration_                                |               10                |
| &nbsp;&nbsp; _Orders suggestion_                              |               9                 |
| &nbsp;&nbsp;&nbsp;  retrieve low-stock products               |               2                 |
| &nbsp;&nbsp;&nbsp;  retrieve suppliers                        |               3                 |
| &nbsp;&nbsp;&nbsp;  suggest order                             |               2                 |
| &nbsp;&nbsp;&nbsp;  add order to suggested ones               |               2                 |
| &nbsp;&nbsp; _Accounting management_                          |               4                 |
| &nbsp;&nbsp;&nbsp;  manage invoices                           |               2                 |
| &nbsp;&nbsp;&nbsp;  perform analysis balance-expences         |               2                 |
| &nbsp;&nbsp; _Check internet connection_                      |               2                 |
| &nbsp;&nbsp; _Manage  Notifications_                          |               8                 |
| &nbsp;&nbsp;&nbsp;  generate notification                     |               5                 |
| &nbsp;&nbsp;&nbsp;  change notifcation status                 |                                 |                                  
| &nbsp;&nbsp; _Sales management_                               |                                 |
| &nbsp;&nbsp;&nbsp;  inherit from CSV management module        |                                 |
| &nbsp;&nbsp;&nbsp;  implement merge between DB and CSV data   |                                 |
| &nbsp;&nbsp; _refunds management_                             |                                 |
| &nbsp;&nbsp;&nbsp;  inherit from CSV management module        |                                 |
| &nbsp;&nbsp;&nbsp;  implement merge between DB and CSV data   |                                 |
| &nbsp;&nbsp; _Inventory management_                           |               11                |
| &nbsp;&nbsp;&nbsp;  CRUD operations over batches              |               5                 |
| &nbsp;&nbsp;&nbsp;  inherit from CSV management module        |                                 |
| &nbsp;&nbsp;&nbsp;  implement merge between DB and CSV data   |                                 |
| &nbsp;&nbsp; _Catalogue management_                           |               7                 |
| &nbsp;&nbsp;&nbsp;  CRUD operations over catalogue            |               5                 |
| &nbsp;&nbsp;&nbsp;  set threshold                             |               2                 |
| &nbsp;&nbsp;&nbsp;  inherit from CSV management module        |                                 |
| &nbsp;&nbsp;&nbsp;  implement merge between DB and CSV data   |                                 |
| &nbsp;&nbsp; _invoice management_                             |                                 |
| &nbsp;&nbsp;&nbsp;  CRUD operations over invoices             |               5                 |
| &nbsp;&nbsp;&nbsp;  link invoice to a specific order          |               5                 |
| &nbsp;&nbsp;&nbsp;  inherit from CSV management module        |                                 |
| &nbsp;&nbsp;&nbsp;  implement merge between DB and CSV data   |                                 |
| &nbsp;&nbsp; _suppliers management_                           |                                 |
| &nbsp;&nbsp;&nbsp;  CRUD operations over invoices             |               5                 |
| &nbsp;&nbsp;&nbsp;  link/unlink suppliers to orders/batches   |               5                 |
| &nbsp;&nbsp;&nbsp;  inherit from CSV management module        |                                 |
| &nbsp;&nbsp;&nbsp;  implement merge between DB and CSV data   |                                 |
| &nbsp;&nbsp; _orders management_                              |                                 |
| &nbsp;&nbsp;&nbsp;  _track orders section_                    |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp; connection with Easy Post account    |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp; token storage, management and update |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp; token storage, management and update |                                 |
| &nbsp;&nbsp;&nbsp;  CRUD operations over orders               |                                 |
| &nbsp;&nbsp;&nbsp;  link/unlink orders to suppliers           |                                 |
| &nbsp;&nbsp;&nbsp;  inherit from CSV management module        |                                 |
| &nbsp;&nbsp;&nbsp;  implement merge between DB and CSV data   |                                 |
| &nbsp;&nbsp;&nbsp;  _track orders section_                    |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp; threshold detection                  |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp; product-supplier match finding       |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp; order suggestion generation          |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp; order suggestion saving              |                                 |
| &nbsp;&nbsp; _accounting management_                          |                                 |
| &nbsp;&nbsp;&nbsp; _income and expenses management_           |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp  inherit from CSV management module   |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp  implement merge between DB and CSV data|                               |
| &nbsp;&nbsp; _cash regisger management_                       |                                 |
| &nbsp;&nbsp;&nbsp;  connection with POS                       |                                 |
| &nbsp;&nbsp;&nbsp;  registers list creation/update            |                                 |
| &nbsp;&nbsp;&nbsp;  connection with POS                       |                                 |
| &nbsp;&nbsp;&nbsp;  catalogue synchronization logic           |                                 |
| &nbsp;&nbsp;&nbsp;  sales/refunds list update                 |                                 |
| Database                                                      |                                 |
