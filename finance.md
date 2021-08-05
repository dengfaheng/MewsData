# Exchange rate

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `SourceCurrency` | string | required | ISO-4217 code of the source [Currency](configuration.md#currency). |
| `TargetCurrency` | string | required | ISO-4217 code of the target [Currency](configuration.md#currency). |
| `Value` | number | required | The exchange rate from the source currency to the target currency. |

# Cashier

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the cashier. |
| `IsActive` | boolean | required | Whether the cashier is still active. |
| `Name` | string | required | Name of the cashier. |

# Cashier transaction

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the transaction. |
| `CashierId` | string | required | Unique identifier of the [Cashier](finance.md#cashier). |
| `PaymentId` | string | optional | Unique identifier of the corresponding payment [Accounting item](finance.md#accounting-item). |
| `CreatedUtc` | string | required | Creation date and time of the transaction. |
| `Number` | string | required | Number of the transaction. |
| `Notes` | string | optional | Additional notes of the transaction. |
| `Amount` | [Currency value](finance.md#currency-value) | required | Value of the transaction. |

# Accounting category

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the category. |
| `IsActive` | boolean | required | Whether the accounting category is still active. |
| `Name` | string | required | Name of the category. |
| `Code` | string | optional | Code of the category within Mews. |
| `Classification` | string [Accounting category classification](finance.md#accounting-category-classification) | optional | Classification of the accounting category allowing cross-enterprise reporting. |
| `ExternalCode` | string | optional | Code of the category in external systems. |
| `LedgerAccountCode` | string | optional | Code of the ledger account \(double entry accounting\). |
| `PostingAccountCode` | string | optional | Code of the posting account \(double entry accounting\). |
| `CostCenterCode` | string | optional | Code of cost center. |

#### Accounting category classification

* `Accommodation`
* `FoodAndBeverage`
* `Taxes`
* `Payments`
* `ExternalRevenue`
* `SundryIncome`
* `Wellness`
* `Sport`
* `Technology`
* `Facilities`
* `Events`
* `Tourism`
* ...



# Accounting item

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the item. |
| `CustomerId` | string | required | Unique identifier of the [Customer](customers.md#customer) whose account the item belongs to. |
| `OrderId` | string | optional | Unique identifier of the order \(or [Reservation](reservations.md#reservation) which is a special type of order\) the item belongs to. |
| `ServiceId` | string | optional | Unique identifier of the [Service](services.md#service) the item belongs to. |
| `ProductId` | string | optional | Unique identifier of the [Product](services.md#product). |
| `BillId` | string | optional | Unique identifier of the bill the item is assigned to. |
| `InvoiceId` | string | optional | Unique identifier of the invoiced [Bill](finance.md#bill) the item is receivable for. |
| `AccountingCategoryId` | string | optional | Unique identifier of the [Accounting category](finance.md#accounting-category) the item belongs to. |
| `CreditCardId` | string | optional | Unique identifier of the [Credit card](finance.md#credit-card) the item is associated to. |
| `Type` | string [Accounting item type](#accounting-item-type) | required | Type of the item. |
| `SubType` | string [Accounting item subtype](finance.md#accounting-item-subtype) | required | subtype of the item. Note that the subtype depends on the `Type` of the item.  |
| `Name` | string | required | Name of the item. |
| `Notes` | string | optional | Additional notes. |
| `ConsumptionUtc` | string | required | Date and time of the item consumption in UTC timezone in ISO 8601 format. |
| `ClosedUtc` | string | optional | Date and time of the item bill closure in UTC timezone in ISO 8601 format. |
| `State` | string [Accounting state](reservations.md#Accounting-item-state) | required | State of the accounting item. |
| `SubState` | string [Accounting item substate](#Accounting-item-substate) | optional | Substate of the item. Note that the substate depends on the `Type` of the item. |
| `Amount` | [Amount value](finance.md#amount-value) | required | Item's amout, negative amount represents either rebate or a payment. |

#### Accounting item type

* `ServiceRevenue`
* `ProductRevenue`
* `AdditionalRevenue`
* `Payment`

#### Accounting item subtype

* Revenue subtypes
  * `CancellationFee`
  * `Rebate`
  * `Deposit`
  * `ExchangeRateDifference`
  * `CustomItem`
  * `Surcharge`
  * `SurchargeDiscount`
  * `SpaceOrder`
  * `ProductOrder`
  * `Other`
* Payment subtypes
  * `CreditCard`
  * `Invoice`
  * `Cash`
  * `Unspecified`
  * `BadDebts`
  * `WireTransfer`
  * `ExchangeRateDifference`
  * `ExchangeRoundingDifference`
  * `BankCharges`
  * `Cheque`
  * `Other`

#### Accounting item substate

* Payment substates
  * `Pending`
  * `Verifying`
  * `Charged`
  * `Canceled`
  * `Failed`

#### Currency value

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Currency` | string | required | ISO-4217 code of the [Currency](configuration.md#currency). |
| `Value` | number | optional | Amount in the currency. |

#### Amount Value

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Currency` | string | required | ISO-4217 code of the [Currency](configuration.md#currency). |
| `NetValue` | number | optional | Net value in case the item is taxed. |
| `GrossValue` | number | optional | Gross value including all taxes. |
| `TaxValues` | array of [Tax Value](finance.md#tax-value) | optional | The tax values applied. |

For most amounts, precision of values depends on `TaxPrecision` of [Enterprise](configuration.md#entreprise) or [Currency](configuration.md#currency) precision. But in some cases, precision can be higher.

#### Tax value

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Code` | number | required | Code corresponding to tax type. |
| `Value` | number | required | Amount of tax applied. |

#### Credit card transaction

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the credit card transaction. |
| `PaymentId` | string | required | Unique identifier of the [Accounting item](#accounting-item). |
| `ChargedAmount` | [Amount](finance.md#amount-value) | required | Charged amount of the transaction. |
| `SettledAmount` | [Amount](finance.md#amount-value) | optional | Settled amount of the transaction. |
| `Fee` | [Amount](finance.md#amount-value) | optional | Fee of the transaction. |
| `SettlementId` | string | optional | Identifier of the settlement. |
| `SettledUtc` | string | optional | Settlement date and time in UTC timezone in ISO 8601 format. |

# Bill

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the bill. |
| `AccountId` | string | required | Unique identifier of the account (for example [Customer](customers.md#customer)) the bill is issued to. |
| `CustomerId` | string | optional | Unique identifier of the [Customer](customers.md#customer) the bill is issued to. |
| `CompanyId` | string | optional | Unique identifier of the [Company](enterprises.md#company) the bill is issued to. |
| `CounterId` | string | optional | Unique identifier of the bill Counter. |
| `State` | string [Bill state](finance.md#bill-state) | required | State of the bill. |
| `Type` | string [Bill type](finance.md#bill-type) | required | Type of the bill. |
| `Number` | string | required | Number of the bill. |
| `VariableSymbol` | string | optional | Variable symbol of the bill. |
| `CreatedUtc` | string | required | Date and time of the bill creation in UTC timezone in ISO 8601 format. |
| `IssuedUtc` | string | required | Date and time of the bill issuance in UTC timezone in ISO 8601 format. |
| `TaxedUtc` | string | optional | Taxation date of the bill in UTC timezone in ISO 8601 format. |
| `PaidUtc` | string | optional | Date when the bill was paid in UTC timezone in ISO 8601 format. |
| `DueUtc` | string | optional | Bill due date and time in UTC timezone in ISO 8601 format. |
| `Notes` | string | optional | Additional notes. |
| `Options` | [Bill options](#bill-options) | required | Options of the bill. |
| `Revenue` | array of [Accounting item](finance.md#accounting-item) | required | The revenue items on the bill. |
| `Payments` | array of [Accounting item](finance.md#accounting-item) | required | The payments on the bill. |
| `AssigneeData` | [Bill assignee data](#bill-assignee-data) | optional | Additional information about assignee of the bill. Persisted at the time of closing of the bill. |

#### Bill type

A bill is either a `Receipt` which means that it has been fully paid, or `Invoice` that is supposed to be paid in the future.

* `Receipt` - the bill has already been fully paid.
* `Invoice` - the bill is supposed to be paid in the future. Before closing it is balanced with an invoice payment.

#### Bill options

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `DisplayCustomer` | boolean | required | Display customer information on a bill. |
| `DisplayTaxation` | boolean | required | Display taxation detail on a bill. |
| `TrackReceivable` | boolean | required | Tracking of payments is enabled for bill, only applicable for `Invoice`. |
| `DisplayCid` | boolean | required | Display CID number on bill, only applicable for `Invoice`. |
| `Rebated` | boolean | required | Bill has been rebated. |

#### Bill assignee data

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Discriminator` | string [Bill assignee data discriminator](#bill-assignee-data-discriminator) | required | Determines type of value. |
| `Value` | object | required | Structure of object depends on [Bill assignee data discriminator](#bill-assignee-data-discriminator). |

#### Bill assignee data discriminator

* `BillCustomerData` - Assignee data specific to a customer.
* `BillCompanyData` - Assignee data specific to a company.

#### Bill customer data

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `ItalianFiscalCode` | string  | optional | Italian fiscal code. |

#### Bill company data

| Property | Type | Contract | Description |
| --- | --- | --- | --- |

# bill PDF

Creates a PDF version of the specified bill. In case it's not possible to return PDF immediately, you must retry the call later while providing the unique event identifier that is returned from the first invocation.

#### Bill PDF result

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Discriminator` | string [Bill PDF result discriminator](#bill-pdf-result-discriminator) | required | Determines type of result. |
| `Value` | object | required | Structure of object depends on [Bill PDF result discriminator](#bill-pdf-result-discriminator). |

#### Bill PDF result discriminator

* `BillPdfFile` - PDF version of a [Bill](finance.md#bill) was successfully created, `Value` is [Bill PDF file](#bill-pdf-file).
* `BillPrintEvent` - PDF version of a [Bill](finance.md#bill) couldn't be created at this moment (for example bill haven't been reported to authorities yet), `Value` is [Bill print event](#bill-print-event).

#### Bill PDF file

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Base64Data` | string  | required | BASE64 encoded PDF file. |

#### Bill print event

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `BillPrintEventId` | string  | required | Unique identifier of print event. Must be used in retry calls to retrieve the PDF. |

# Outlet item

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the item. |
| `BillId` | string | required | Unique identifier of the [Outlet bill](finance.md#outlet-bill) the item belongs to. |
| `AccountingCategoryId` | string | optional | Unique identifier of the [Accounting category](finance.md#accounting-category) the item belongs to. |
| `Type` | string [Outlet item type](finance.md#outlet-item-type) | required | Type of the item. |
| `Name` | string | required | Name of the item. |
| `UnitCount` | number | required | Unit count of the item. |
| `UnitAmount` | [Amount](finance.md#amount-value) | required | Unit amount of the item. |
| `CreatedUtc` | string | optional | Date and time of the item creation in UTC timezone in ISO 8601 format. |
| `ConsumedUtc` | string | required | Date and time of the item consumption in UTC timezone in ISO 8601 format. |
| `Notes` | string | optional | Additional notes. |

#### Outlet item type

* `Revenue`
* `NonRevenue`
* `Payment`

#### Outlet bill

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the bill. |
| `OutletId` | string | required | Unique identifier of the [Outlet](enterprises.md#outlet) where the bill was issued. |
| `Number` | string | required | Number of the bill. |
| `ClosedUtc` | string | required | Date and time of the bill closure in UTC timezone in ISO 8601 format. |
| `Notes` | string | optional | Additional notes on the bill. |

# Credit card

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the credit card. |
| `CustomerId` | string | required | Unique identifier of the credit card [owner](customers.md#customer). |
| `CreatedUtc` | string | required | Creation date and time of the credit card in UTC timezone in ISO 8601 format. |
| `Expiration` | string | optional | Expiration of the credit card in format `MM/YYYY`. |
| `IsActive` | boolean | required | Whether the credit card is still active. |
| `ObfuscatedNumber` | string | optinal | Obfuscated credit card number. At most first six digits and last four digits can be specified, otherwise the digits are replaced with `*`. |
| `Format` | string [Credit card format](finance.md#credit-card-format) | required | Format of the credit card. |
| `Kind` | string [Credit card kind](finance.md#credit-card-kind) | required | Kind of the credit card. |
| `State` | string [Credit card state](finance.md#credit-card-state) | required | State of the credit card. |
| `Type` | string [Credit card type](finance.md#credit-card-type) | required | Type of the credit card. |

#### Credit card format

* `Physical`
* `Virtual`

#### Credit card kind

* `Terminal`
* `Gateway`

#### Credit card state

* `Enabled`
* `Disabled`

#### Credit card type

* `MasterCard`, `Visa`, `Amex`, `Maestro`, `Discover`, `VPay`, ...

# Preauthorization

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the preauthorization. |
| `CreditCardId` | string | required | Unique identifier of the credit card. |
| `Amount` | [Amount value](finance.md#amount-value) | required | Value of the preauthorization. |
| `State` | string [Preauthorization State](finance.md#preauthorization-state) | required | State of the preauthorization. |
| `Code` | string | optional | Code of the preauthorization. |

#### Preauthorization state

* `Chargeable` - Created and prepared for the charging.
* `Expired` - A preauthorization that is not charged and expired.
* `Cancelled` - A preauthorization that was canceled before charging.
* `Charged` - Charged preauthorization.