
# Estimate by product decomposition

###

| component name                                                | Estimated effort (person hours) |
| ------------------------------------------------------------  | ------------------------------- |
| _requirement document_                                        |              100                |
| _design document_                                             |              150                |
| _Desktop front-end_                                           |               85                |
| &nbsp;&nbsp;  _UI Login-page_                                 |               3                 |
| &nbsp;&nbsp;  _Dashboard page_                                |               12                |
| &nbsp;&nbsp;  _Catalogue page_                                |               8                 |
| &nbsp;&nbsp;&nbsp; catalogue filters and user-defined list    |               4                 |
| &nbsp;&nbsp;&nbsp; manual insertion of the product threshold  |               4                 |
| &nbsp;&nbsp;  _Inventory page_                                |               6                 |
| &nbsp;&nbsp;&nbsp; inventory filters and user-defined list    |               3                 |
| &nbsp;&nbsp;  _Sales page_                                    |               10                |
| &nbsp;&nbsp;&nbsp; Sales filters and user-defined list        |               5                 |
| &nbsp;&nbsp;&nbsp; refunds filters and user-defined list      |               5                 |
| &nbsp;&nbsp;  _Orders page_                                   |               14                |
| &nbsp;&nbsp;&nbsp; suppliers filters and user-defined list    |               5                 |
| &nbsp;&nbsp;&nbsp; orders filters and user-defined list       |               5                 |
| &nbsp;&nbsp;&nbsp; suggested orders tab                       |               2                 |
| &nbsp;&nbsp;&nbsp; orders status tab                          |               2                 |
| &nbsp;&nbsp;  _Accounting page_                               |              17                 |
| &nbsp;&nbsp;&nbsp; invoices filters and user-defined list     |               5                 |
| &nbsp;&nbsp;&nbsp; field to change the invoice status         |               3                 |
| &nbsp;&nbsp;&nbsp; income data with different granularities   |               3                 |
| &nbsp;&nbsp;&nbsp; expenses data with different granularities |               3                 |
| &nbsp;&nbsp;&nbsp; balance data                               |               3                 |
| &nbsp;&nbsp;  _Profile page_                                  |               5                 |
| &nbsp;&nbsp;  _Notification section_                          |               5                 |
| &nbsp;&nbsp;  _cash register page_                            |               5                 |
| &nbsp;&nbsp;&nbsp; filters and user-defined list              |               5                 |
|_Backend_                                                      |               334               |
| &nbsp;&nbsp; _Authentication_                                 |               15                |
| &nbsp;&nbsp;&nbsp;  set username-password                     |               3                 |
| &nbsp;&nbsp;&nbsp;  change username-password                  |               4                 |
| &nbsp;&nbsp;&nbsp;  verification                              |               4                 |
| &nbsp;&nbsp;&nbsp;  encryption                                |               4                 |
| &nbsp;&nbsp; _Csv management_                                 |               30                |
| &nbsp;&nbsp;&nbsp;  csv read                                  |               5                 |
| &nbsp;&nbsp;&nbsp;  csv write                                 |               3                 |
| &nbsp;&nbsp;&nbsp;  csv download                              |               3                 |
| &nbsp;&nbsp;&nbsp;  csv error detection                       |               12                |
| &nbsp;&nbsp;&nbsp;  csv data correction                       |               7                 |
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
| &nbsp;&nbsp;&nbsp;  change notifcation status                 |               3                 |                                  
| &nbsp;&nbsp; _Sales management_                               |               11                |
| &nbsp;&nbsp;&nbsp;  inherit from CSV management module        |               5                 |
| &nbsp;&nbsp;&nbsp;  implement merge between DB and CSV data   |               6                 |
| &nbsp;&nbsp; _refunds management_                             |               13                |
| &nbsp;&nbsp;&nbsp;  inherit from CSV management module        |               5                 |
| &nbsp;&nbsp;&nbsp;  implement merge between DB and CSV data   |               8                 |
| &nbsp;&nbsp; _Inventory management_                           |               22                |
| &nbsp;&nbsp;&nbsp;  CRUD operations over batches              |               5                 |
| &nbsp;&nbsp;&nbsp;  inherit from CSV management module        |               5                 |
| &nbsp;&nbsp;&nbsp;  implement merge between DB and CSV data   |               12                |
| &nbsp;&nbsp; _Catalogue management_                           |               24                |
| &nbsp;&nbsp;&nbsp;  CRUD operations over catalogue            |               5                 |
| &nbsp;&nbsp;&nbsp;  set threshold                             |               2                 |
| &nbsp;&nbsp;&nbsp;  inherit from CSV management module        |               5                 |
| &nbsp;&nbsp;&nbsp;  implement merge between DB and CSV data   |               12                |
| &nbsp;&nbsp; _invoice management_                             |               21                |
| &nbsp;&nbsp;&nbsp;  CRUD operations over invoices             |               5                 |
| &nbsp;&nbsp;&nbsp;  link invoice to a specific order          |               5                 |
| &nbsp;&nbsp;&nbsp;  inherit from CSV management module        |               5                 |
| &nbsp;&nbsp;&nbsp;  implement merge between DB and CSV data   |               6                 |
| &nbsp;&nbsp; _suppliers management_                           |              23                 |
| &nbsp;&nbsp;&nbsp;  CRUD operations over invoices             |               5                 |
| &nbsp;&nbsp;&nbsp;  link/unlink suppliers to orders/batches   |               5                 |
| &nbsp;&nbsp;&nbsp;  inherit from CSV management module        |               5                 |
| &nbsp;&nbsp;&nbsp;  implement merge between DB and CSV data   |               8                 |
| &nbsp;&nbsp; _orders management_                              |               66                |
| &nbsp;&nbsp;&nbsp;  _track orders section_                    |               20                |
| &nbsp;&nbsp;&nbsp;&nbsp; connection with Easy Post account    |               12                |
| &nbsp;&nbsp;&nbsp;&nbsp; token storage, management and update |               8                 |
| &nbsp;&nbsp;&nbsp;  CRUD operations over orders               |               5                 |
| &nbsp;&nbsp;&nbsp;  link/unlink orders to suppliers           |               5                 |
| &nbsp;&nbsp;&nbsp;  inherit from CSV management module        |               6                 |
| &nbsp;&nbsp;&nbsp;  implement merge between DB and CSV data   |               12                |
| &nbsp;&nbsp;&nbsp;  _track orders section_                    |               18                |
| &nbsp;&nbsp;&nbsp;&nbsp; threshold detection                  |               4                 |
| &nbsp;&nbsp;&nbsp;&nbsp; product-supplier match finding       |               4                 |
| &nbsp;&nbsp;&nbsp;&nbsp; order suggestion generation          |               6                 |
| &nbsp;&nbsp;&nbsp;&nbsp; order suggestion saving              |               4                 |
| &nbsp;&nbsp; _accounting management_                          |               66                |
| &nbsp;&nbsp;&nbsp; _income and expenses management_           |               32                |
| &nbsp;&nbsp;&nbsp;&nbsp  inherit from CSV management module   |               12                |
| &nbsp;&nbsp;&nbsp;&nbsp  implement merge between DB and CSV data|             20                |
| &nbsp;&nbsp; _cash regisger management_                       |               34                |
| &nbsp;&nbsp;&nbsp;  connection with POS                       |                14               |
| &nbsp;&nbsp;&nbsp;  registers list creation/update            |                6                |
| &nbsp;&nbsp;&nbsp;  catalogue synchronization logic           |                6                |
| &nbsp;&nbsp;&nbsp;  sales/refunds list update                 |                8                |
| Database                                                      |                30               |

_total amount of estimated person hours is: 334_ 
_total estimated calendar time is: 3 weeks_