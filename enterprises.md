# Company

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the company. |
| `Name` | string | required | Name of the company. |
| `IsActive` | boolean | required | Whether the company is still active. |
| `Number`| number | required | Unique number of the company. |
| `Identifier` | string | optional | Identifier of the company \(e.g. legal identifier\). |
| `TaxIdentifier` | string | optional | Tax identification number of the company. |
| `AdditionalTaxIdentifier` | string | optional | Additional tax identifier of the company. |
| `ElectronicInvoiceIdentifier` | string | optional | Electronic invoice identifier of the company. |
| `AccountingCode` | string | optional | Accounting code of the company. |
| `BillingCode` | string | optional | Billing code of the company. |
| `Address` | [Address](configuration.md#address) | optional | Address of the company \(if it is non-empty, otherwise `null`\). |

# Travel agency contract

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the contract. |
| `ServiceId` | string | required | Unique identifier of the [Service](services.md#service) the contract is related to. |
| `CompanyId` | string | required | Unique identifier of the contracted [Company](enterprises.md#company). |
| `IsActive` | boolean | required | Whether the contract is still active. |
| `CommissionIncluded` | boolean | optional | Whether commission of the travel agency is included in the rate. |
| `Commission` | number | optional | Commission of the travel agency. |

# Department

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the department. |
| `IsActive` | boolean | required | Whether the department is still active. |
| `Name` | string | required | Name of the department. |

# Counter

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the counter. |
| `Name` | string | required | Name of the counter. |
| `IsDefault` | boolean | required | Whether the counter is used by default. |
| `Value` | number | required | Current value the counter. |
| `Format` | string | required | Format the counter is displayed in. |

# Outlet

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the outlet. |
| `IsActive` | boolean | required | Whether the outlet is still active. |
| `Name` | string | required | Name of the outlet. |

# Resource

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the resource. |
| `IsActive` | bool | required | Whether the resource is still active. |
| `Name` | string | required | Name of the resource \(e.g. room number\). |
| `ParentResourceId` | string | optional | Identifier of the parent [Resource](#resource) \(e.g. room of a bed\). |
| `State` | string [Resource state](#resource-state) | required | State of the resource. |
| `Data` | [Resource data](#resource-data) | required | Additional data of the resource. |
| `CreatedUtc` | string | required | Creation date and time of the resource in UTC timezone in ISO 8601 format. |
| `UpdatedUtc` | string | required | Last update date and time of the resource in UTC timezone in ISO 8601 format. |

#### Resource state

* `Dirty`
* `Clean`
* `Inspected`
* `OutOfService`
* `OutOfOrder`

#### Resource data

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Discriminator` | string [Resource data discriminator](#resource-data-discriminator) | required | If resource is space, object or person. |
| `Value` | object | required | Based on Resource data discriminator, e.g. [Space resource data](#space-resource-data)  |

#### Resource data discriminator

* `Space`
* `Object`
* `Person`

#### Space resource data

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `FloorNumber` | string | required | Number of the floor the space is on. |
| `LocationNotes` | string | optional | Location notes for the space. It can be eg. Building number the space is located in or the Parking area the particular parking space is at. |

#### Object resource data

| Property | Type | Contract | Description |
| --- | --- | --- | --- |

#### Person resource data

| Property | Type | Contract | Description |
| --- | --- | --- | --- |

#### Resource category

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the category. |
| `IsActive` | bool | required | Whether the category is still active. |
| `Type` | string [Resource category type](#resource-category-type) | required | Type of the category. |
| `Names` | [Localized text](enterprises.md#localized-text) | required | All translations of the name. |
| `ShortNames` | [Localized text](enterprises.md#localized-text) | required | All translations of the short name. |
| `Descriptions` | [Localized text](enterprises.md#localized-text) | required | All translations of the description. |
| `Ordering` | number | required | Ordering of the category, lower number corresponds to lower category \(note that uniqueness nor continuous sequence is guaranteed\). |
| `Capacity` | number | required | Capacity that can be served \(e.g. bed count\). |
| `ExtraCapacity` | number | required | Extra capacity that can be served \(e.g. extra bed count\). |

#### Resource category type

* `Room`
* `Dorm`
* `Bed`
* ...

#### Resource category assignment

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the assignment. |
| `IsActive` | bool | required | Whether the assignment is still active. |
| `CategoryId` | string | required | Unique identifier of the [Resource category](#resource-category). |
| `ResourceId` | string | required | Unique identifier of the [Resource](#resource) assigned to the Resource category. |
| `CreatedUtc` | string | required | Creation date and time of the assignment in UTC timezone in ISO 8601 format. |
| `UpdatedUtc` | string | required | Last update date and time of the assignment in UTC timezone in ISO 8601 format. |

#### Resource category image assignment

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the assignment. |
| `IsActive` | bool | required | Whether the assignment is still active. |
| `CategoryId` | string | required | Unique identifier of the [Resource category](#resource-category). |
| `ImageId` | string | required | Unique identifier of the image assigned to the Resource category. |
| `CreatedUtc` | string | required | Creation date and time of the assignment in UTC timezone in ISO 8601 format. |
| `UpdatedUtc` | string | required | Last update date and time of the assignment in UTC timezone in ISO 8601 format. |

#### Localized text

An object where keys are the [Language](configuration.md#language) codes and values texts in respective languages.

#### Resource feature

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the feature. |
| `ServiceId` | string | required | Unique identifier of the [Service](services.md#service). |
| `IsActive` | bool | required | Whether the resource feature is still active. |
| `Classification` | string [Resource feature classification](#resource-feature-classification) | required | Classification of the feature. |
| `Names` | [Localized text](enterprises.md#localized-text) | required | All translations of the name. |
| `ShortNames` | [Localized text](enterprises.md#localized-text) | required | All translations of the short name. |
| `Descriptions` | [Localized text](enterprises.md#localized-text) | required | All translations of the description. |

#### Resource feature classification

* `AccessibleBathroom`
* `AccessibleRoom`
* `AirConditioning`
* `Balcony`
* `DoubleBed`
* `ElevatorAccess`
* `EnsuiteRoom`
* `HighFloor`
* `Kitchenette`
* `LowerBed`
* `OceanView`
* `PrivateBathroom`
* `PrivateJacuzzi`
* `PrivateSauna`
* `RiverView`
* `RollawayBed`
* `SharedBathroom`
* `TwinBeds`
* `UpperBed`
* `SeaView`
* `...`

#### Resource feature assignment

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the assignment. |
| `IsActive` | bool | required | Whether the assignment is still active. |
| `ResourceId` | string | required | Unique identifier of the [Resource](#resource). |
| `FeatureId` | string | required | Unique identifier of the [Resource feature](#resource-feature) assigned to the Resource. |
| `CreatedUtc` | string | required | Creation date and time of the assignment in UTC timezone in ISO 8601 format. |
| `UpdatedUtc` | string | required | Last update date and time of the assignment in UTC timezone in ISO 8601 format. |

# Resource block

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the block. |
| `AssignedResourceId` | string | required | Unique identifier of the assigned [Resource](#resource). |
| `IsActive` | bool | required | Whether the block is still active. |
| `Type` | string [Resource block type](#resource-block-type) | required | Type of the resource block. |
| `StartUtc` | string | required | Start of the block in UTC timezone in ISO 8601 format. |
| `EndUtc` | string | required | End of the block in UTC timezone in ISO 8601 format. |
| `CreatedUtc` | string | required | Creation date and time of the block in UTC timezone in ISO 8601 format. |
| `UpdatedUtc` | string | required | Last update date and time of the block in UTC timezone in ISO 8601 format. |

#### Resource block type

* `OutOfOrder`
* `InternalUse`

# Task

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the task. |
| `Name` | string | required | Name \(or title\) of the task. |
| `State` | string [Task state](#task-state) | required | State of the task. |
| `Description` | string | optional | Further decription of the task. |
| `DepartmentId` | string | optional | Unique identifier of the [Department](#department) the task is addressed to. |
| `ServiceOrderId` | string | optional | Unique identifier of the order (for example a [Reservation](reservations.md#reservation) or [Product order](services#add-order)) the task is linked with. |
| `CreatedUtc` | string | required | Creation date and time of the task in UTC timezone in ISO 8601 format. |
| `DeadlineUtc` | string | required | Deadline date and time of the task in UTC timezone in ISO 8601 format. |
| `UpdatedUtc` | string | required | Last update date and time of the task in UTC timezone in ISO 8601 format. |

### Task state

* `Open` 
* `Closed` 
