
# Estimate by product decomposition

###

| component name                                                | Estimated effort (person hours) |
| ------------------------------------------------------------  | ------------------------------- |
| requirement document                                          |              100                |
| design document                                               |               20                |
| _Desktop front-end_                                           |               42                |
| &nbsp;&nbsp;  UI Login-page                                   |               3                 |
| &nbsp;&nbsp;  Dashboard page                                  |               8                 |
| &nbsp;&nbsp;  Catalogue page                                  |               6                 |
| &nbsp;&nbsp;  Inventory page                                  |               6                 |
| &nbsp;&nbsp;  Sales page                                      |               5                 |
| &nbsp;&nbsp;  Orders page                                     |               4                 |
| &nbsp;&nbsp;  Accounting page                                 |               4                 |
| &nbsp;&nbsp;  Profile page                                    |               3                 |
| &nbsp;&nbsp;  Notification page                               |               3                 |
| &nbsp;&nbsp;  cash register page                              |               3                 |
|_Backend_                                                      |              120                |
| &nbsp;&nbsp; _Authentication_                                 |               15                |
| &nbsp;&nbsp;&nbsp;  set username-password                     |               3                 |
| &nbsp;&nbsp;&nbsp;  change username-password                  |               4                 |
| &nbsp;&nbsp;&nbsp;  verification                              |               4                 |
| &nbsp;&nbsp;&nbsp;  encryption                                |               4                 |
| &nbsp;&nbsp; _Csv management_                                 |               7                 |
| &nbsp;&nbsp;&nbsp;  csv read                                  |               2                 |
| &nbsp;&nbsp;&nbsp;  csv write                                 |               2                 |
| &nbsp;&nbsp;&nbsp;  csv download                              |               3                 |
| &nbsp;&nbsp;&nbsp;  merge data with existing information      |               3                 |
| &nbsp;&nbsp; _Order management_                               |                                 |
| &nbsp;&nbsp;&nbsp;  CRUD operations over orders               |               10                |
| &nbsp;&nbsp;&nbsp;  link/unlink order to specific supplier    |                                 |
| &nbsp;&nbsp;&nbsp;  send order request                        |               4                 |
| &nbsp;&nbsp;&nbsp;  update order status                       |               4                 |
| &nbsp;&nbsp;&nbsp;  csv import management                     |                                 |
| &nbsp;&nbsp; _API integration_                                |               10                |
| &nbsp;&nbsp; _Orders suggestion_                              |               9                 |
| &nbsp;&nbsp;&nbsp;  retrieve low-stock products               |               2                 |
| &nbsp;&nbsp;&nbsp;  retrieve suppliers                        |               3                 |
| &nbsp;&nbsp;&nbsp;  suggest order                             |               2                 |
| &nbsp;&nbsp;&nbsp;  add order to suggested ones               |               2                 |
| &nbsp;&nbsp;&nbsp;  csv file integration                      |                                 |
| &nbsp;&nbsp; _Accounting management_                          |               4                 |
| &nbsp;&nbsp;&nbsp;  manage invoices                           |               2                 |
| &nbsp;&nbsp;&nbsp;  perform analysis balance-expences         |               2                 |
| &nbsp;&nbsp;&nbsp;  CRUD operations over invoices             |                                 |
| &nbsp;&nbsp;&nbsp;  CRUD operations over invoices             |                                 |
| &nbsp;&nbsp;&nbsp;  track cash flow from cash registers       |                                 |
| &nbsp;&nbsp;&nbsp;  compute current balance                   |                                 |
| &nbsp;&nbsp; _Check internet connection_                      |               2                 |
| &nbsp;&nbsp; _Manage  Notifications_                          |               8                 |
| &nbsp;&nbsp;&nbsp;  generate notification                     |               5                 |
| &nbsp;&nbsp;&nbsp;  change notifcation status                 |               3                 |
| &nbsp;&nbsp; _sales management_                               |                                 |
| &nbsp;&nbsp;&nbsp;  CRUD operations over sales                |                                 |
| &nbsp;&nbsp;&nbsp;  csv file integration                      |                                 |
| &nbsp;&nbsp; _refunds management_                             |                                 |
| &nbsp;&nbsp;&nbsp;  CRUD operations over refunds              |                                 |
| &nbsp;&nbsp;&nbsp;  csv file integration                      |                                 |
| &nbsp;&nbsp; _cash register management_                       |                                 |
| &nbsp;&nbsp;&nbsp; _conenct to POS provider's account_        |                               |
| &nbsp;&nbsp;&nbsp;&nbsp; authorize user and receive token     |                               |
| &nbsp;&nbsp;&nbsp;&nbsp; encrypt token                        |                               |
| &nbsp;&nbsp;&nbsp;&nbsp; update token if needed               |                               |
| &nbsp;&nbsp;&nbsp; _get cash register list_                   |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp; decrypt token and access API         |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp; retrieve cash register list and update local one  |                                 |
| &nbsp;&nbsp;&nbsp; _update cash register catalogue_                        |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp; edit catalogue to API's compliant                 |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp; push catalogue to cash registers                  |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp; update status for unresponsive cash registers     |                                 |
| &nbsp;&nbsp;&nbsp; _retrieve sales from cash register_                     |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp; retrieve sale from cash registers in local list   |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp; convert to internal format                        |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp; update DB                                         |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp; update status for unresponsive cash registers     |                                 |
| &nbsp;&nbsp;&nbsp; _retrieve refunds from cash register_                   |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp; retrieve refund from cash registers in local list |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp; convert to internal format                        |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp; update DB                                         |                                 |
| &nbsp;&nbsp;&nbsp;&nbsp; update status for unresponsive cash registers     |                                 |
| &nbsp;&nbsp; _Inventory management_                                        |               11                |
| &nbsp;&nbsp;&nbsp;  CRUD operations over batches                           |               5                 |
| &nbsp;&nbsp;&nbsp;  find batches near expiring date                        |               3                 |
| &nbsp;&nbsp;&nbsp;  find expired batches                                   |               3                 |
| &nbsp;&nbsp;&nbsp;  csv file integration                                   |                                 |
| &nbsp;&nbsp; _suppliers management_                                        |                                 |
| &nbsp;&nbsp;&nbsp;  CRUD operations over suppliers                         |               5                 |
| &nbsp;&nbsp;&nbsp;  link/unlink supplier to a specific product             |                                 |
| &nbsp;&nbsp; _Catalogue management_                                        |               7                 |
| &nbsp;&nbsp;&nbsp;  CRUD operations over catalogue                         |               5                 |
| &nbsp;&nbsp;&nbsp;  set threshold                                          |               2                 |
| Database                                                                   |               17                |