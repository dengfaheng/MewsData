# Customers

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the customer. |
| `Number` | string | required | Number of the customer. |
| `FirstName` | string | optional | First name of the customer. |
| `LastName` | string | required | Last name of the customer. |
| `SecondLastName` | string | optional | Second last name of the customer. |
| `Title` | string [Title](customers.md#title) | optional | Title prefix of the customer. |
| `Sex` | string [Sex](customers.md#Sex) | optional | Sex of the customer. |
| `NationalityCode` | string | optional | ISO 3166-1 code of the [Country](configuration.md#country). |
| `LanguageCode` | string | optional | Language and culture code of the customers preferred language. E.g. `en-US` or `fr-FR`. |
| `BirthDate` | string | optional | Date of birth in ISO 8601 format. |
| `BirthPlace` | string | optional | Place of birth. |
| `Email` | string | optional | Email address of the customer. |
| `Phone` | string | optional | Phone number of the customer \(possibly mobile\). |
| `TaxIdentificationNumber` | string | optional | Tax identification number of the customer. |
| `LoyaltyCode` | string | optional | Loyalty code of the customer. |
| `AccountingCode` | string | optional | Accounting code of the customer. |
| `BillingCode` | string | optional | Billing code of the customer. |
| `Notes` | string | optional | Internal notes about the customer. |
| `Classifications` | array of [Customer classification](customers.md#customer-classification) | required | Classifications of the customer. |
| `Options` | array of [Customer option](customers.md#customer-option) | required | Options of the customer. |
| `Address` | [Address](configuration.md#address) | optional | Address of the customer. |
| `CreatedUtc` | string | required | Creation date and time of the customer in UTC timezone in ISO 8601 format. |
| `UpdatedUtc` | string | required | Last update date and time of the customer in UTC timezone in ISO 8601 format. |
| `ItalianDestinationCode` | string | optional | Value of Italian destination code. |
| `ItalianFiscalCode` | string | optional | Value of Italian fiscal code. |
| `CompanyId` | string | optional | Unique identifier of [Company](enterprises.md#company) the customer is associated with. |

#### Title

* `Mister`
* `Miss`
* `Misses`

#### Sex

* `Male`
* `Female`

#### Customer classification

* `PaymasterAccount`
* `Blacklist`
* `Media`
* `LoyaltyProgram`
* `PreviousComplaint`
* `Returning`
* `Staff`
* `FriendOrFamily`
* `TopManagement`
* `Important`
* `VeryImportant`
* `Problematic`
* `Cashlist`
* `DisabledPerson`
* `Military`
* ...

#### Customer option

* `SendMarketingEmails`
* ...

----

# Document

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the document. |
| `CustomerId` | string | required | Identifier of the [Customer](customers.md#customer). |
| `Type` | string [Document type](#document-type) | required | Type of the document. |
| `Number` | string | optional | Number of the document \(e.g. passport number\). |
| `Expiration` | string | optional | Expiration date in ISO 8601 format. |
| `Issuance` | string | optional | Date of issuance in ISO 8601 format. |
| `IssuingCountryCode` | string | optional | ISO 3166-1 code of the [Country](configuration.md#country). |

#### Document type

* `Passport`
* `IdentityCard`
* `Visa`
* `DriversLicense`