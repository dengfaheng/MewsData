# Service

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the service. |
| `IsActive` | boolean | required | Whether the service is still active. |
| `Name` | string | required | Name of the service. |
| `Data` | [Service data](#service-data) | required | Additional information about the specific service. |

#### Service data

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Discriminator` | string [Service data discriminator](#service-data-discriminator) | required | Determines type of value. |
| `Value` | object | required | Structure of object depends on [Service data discriminator](#service-data-discriminator). |

#### Service data discriminator

* `Bookable` - Data specific to a bookable service.
* `Additional` - Data specific to an additional service.

#### Bookable service data

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `StartOffset` | string | required | Offset from the start of the time unit defining the default start of the service orders in ISO 8601 duration format. |
| `EndOffset` | string | required | Offset from the end of the time unit defining the default end of the service orders in ISO 8601 duration format. |
| `OccupancyStartOffset` | string | required | Offset from the start of the time unit defining the occupancy start of the service in ISO 8601 duration format that is considered regarding the availability and reporting. |
| `OccupancyEndOffset` | string | required | Offset from the end of the time unit defining the occupancy end of the service in ISO 8601 duration format that is considered regarding the availability and reporting. |
| `TimeUnit` | [Time unit](#time-unit) | required | Time unit of the service. |

Time units represent a fixed, finite time interval: a minute, a day, a month, etc. A Time unit defines the operable periods for a bookable service. We currently only support the Day unit.
We think of the daily time unit as the physical time unit that starts at midnight and ends at midnight the following day.

Start offsets are anchored to the start of the time unit and end offsets are anchored to the end of the time unit.
`StartOffset` and `EndOffset` define the default start and end of the service (so, the service orders).
`OccupancyStartOffset` and `OccupancyEndOffset` define the time where the space is considered occupied in Mews. 

Positive end offsets of the daily time unit define the nightly service as depicted in the diagram below.
![](../.gitbook/assets/timeunits-connector-night.png)

Negative or zero end offsets of the daily time unit define the daily service as depicted on the picture below.
![](../.gitbook/assets/timeunits-connector-day.png)

#### Time unit

* `Day`
* ...

#### Additional service data

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Promotions` | [Promotions](#promotions) | required | Promotions of the service. |

##### Promotions

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `BeforeCheckIn` | boolean | required | Whether it can be promoted before check-in. |
| `AfterCheckIn` | boolean | required | Whether it can be promoted after check-in. |
| `DuringStay` | boolean | required | Whether it can be promoted during stay. |
| `BeforeCheckOut` | boolean | required | Whether it can be promoted before check-out. |
| `AfterCheckOut` | boolean | required | Whether it can be promoted after check-out. |
| `DuringCheckOut` | boolean | required | Whether it can be promoted during check-out. | 



# Availability block

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the availability block. |
| `ServiceId` | string | required | Unique identifier of the [Service](#service) the block is assigned to. |
| `RateId` | string | required | Unique identifier of the [Rate](#rate) the block is assigned to. |
| `StartUtc` | string | required | Start of the interval in UTC timezone in ISO 8601 format. |
| `EndUtc` | string | required | End of the interval in UTC timezone in ISO 8601 format. |
| `ReleasedUtc` | string | required | The moment when the block and its availability is released in UTC timezone in ISO 8601 format. |
| `ExternalIdentifier` | string | optional, max 255 characters | Identifier of the block from external system. |



# Availability block adjustment

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `AvailabilityBlockId` | string | required | Unique identifier of the [Availability block](#availability-block) whose availability is updated. |
| `ResourceCategoryId` | string | required | Unique identifier of the [Resource category](enterprises.md#resource-category) whose availability is updated. |
| `StartUtc` | string | required | Start of the interval in UTC timezone in ISO 8601 format. |
| `EndUtc` | string | required | End of the interval in UTC timezone in ISO 8601 format. |
| `UnitCount` | string | required | Adjustment value applied on the interval. |



# Resource category availability

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `CategoryId` | string | required | Unique identifier of the [Resource category](enterprises.md#resource-category). |
| `Availabilities` | array of number | required | Absolute availabilities of the resource category in the covered dates. |
| `Adjustments` | array of number | required | Relative availability adjustments set for resource category in the covered dates. |



# Product

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the product. |
| `ServiceId` | string | required | Unique identifier of the [Service](services.md#service). |
| `CategoryId` | string | optional | Unique identifier of the Product category. |
| `IsActive` | boolean | required | Whether the product is still active. |
| `Name` | string | required | Name of the product.  |
| `ExternalName` | string | required | Name of the product meant to be displayed to customer. |
| `ShortName` | string | required | Short name of the product. |
| `Description` | string | optional | Description of the product. |
| `Charging` | string [Product charging](services.md#product-charging) | required | Charging of the product. |
| `Posting` | string [Product posting](services.md#product-posting) | required | Posting of the product. |
| `Promotions` | [Promotions](services.md#promotions) | required | Promotions of the service. |
| `Classifications` | [Product classifications](services.md#product-classifications) | required | Classifications of the service. |
| `Price` | [Currency value](finance.md#currency-value) | required | Price of the product. |

#### Product charging

* `Once`
* `PerTimeUnit`
* `PerPersonPerTimeUnit`
* `PerPerson`

#### Product posting

* `Once`
* `Daily`

#### Product classifications

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Food` | boolean | required | Product is classified as food. |
| `Beverage` | boolean | required | Product is classified as beverage. |
| `Wellness` | boolean | required | Product is classified as wellness. |
| `CityTax` | boolean | required | Product is classified as city tax. |

# Rule

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the rule. |
| `Conditions` | [Rule conditions](#rule-conditions) | required | Conditions of the rule. |

#### Rule conditions

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `RateId` | [Rule condition](#rule-condition) | required | Condition based on [Rate](#rate). |
| `RateGroupId` | [Rule condition](#rule-condition) | required | Condition based on [Rate group](#rate-group). |
| `BusinessSegmentId` | [Rule condition](#rule-condition) | required | Condition based on [Business segment](#business-segment). |
| `ResourceCategoryId` | [Rule condition](#rule-condition) | required | Condition based on [Resource category](enterprises.md#resource-category). |
| `ResourceCategoryType` | [Rule condition](#rule-condition) | required | Condition based on [Resource category type](enterprises.md#resource-category-type). |
| `Origin` | [Rule condition](#rule-condition) | required | Condition based on [Reservation origin](reservations.md#reservation-origin). |
| `MinimumTimeUnitCount` | string | required | Condition based on minimum amount of time units. |
| `MaximumTimeUnitCount` | string | required | Condition based on maximum amount of time units. |

#### Rule condition

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `ConditionType` | string [Condition type](#condition-type) | required | Type of condition. |
| `Value` | string | required | Value of the condition depending on the property. E.g. [Reservation origin](reservations.md#reservation-origin) in case of origin condition or unique identifier of a rate in case of rate condition. |

#### Condition type

* `Equals`
* `NotEquals`

#### Rule action

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the rule action. |
| `RuleId` | string | required | Unique identifier of the rule. |
| `Data` | [RuleActionData](#rule-aciton-data) | optional | Additional information about action. |

#### Rule action data

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Discriminator` | string [Rule action discriminator](#rule-action-discriminator) | required | Determines type of value. |
| `Value` | object | required | Structure of object depends on [Rule action discriminator](#rule-action-discriminator). |

#### Rule action discriminator

* `Product` - Data specific to a product.

#### Rule action product data

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `ProductId` | string | required | Unique identifier of product. |
| `ActionType` | string [Product action type](#product-action-type) | required | Action of rule. |

#### Product action type

* `Add` - Adds specified item.
* `Delete` - Deletes specified item.



----



# Business segment

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the segment. |
| `ServiceId` | string | required | Unique identifier of the [Service](#service). |
| `IsActive` | boolean | required | Whether the business segment is still active. |
| `Name` | string | required | Name of the segment. |

# Rate

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the rate. |
| `GroupId` | string | required | Unique identifier of [Rate group](#rate-group) where the rate belongs. |
| `BaseRateId` | string | required | Unique identifier of the base [Rate](services.md#rate). |
| `ServiceId` | string | required | Unique identifier of the [Service](#service). |
| `IsActive` | boolean | required | Whether the rate is still active. |
| `IsEnabled` | boolean | required | Whether the rate is currently available to customers. |
| `IsPublic` | boolean | required | Whether the rate is publicly available. |
| `Name` | string | required | Name of the rate. |
| `ShortName` | string | required | Short name of the rate. |
| `ExternalNames` | [Localized text](enterprises.md#localized-text) | required | All translations of the external name of the rate. |

# Rate group

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the group. |
| `ServiceId` | string | required | Unique identifier of the [Service](#service). |
| `IsActive` | boolean | required | Whether the rate group is still active. |
| `Name` | string | required | Name of the rate group. |

# Get rate pricing

Returns prices of a rate in the specified interval. Note that response contains prices for all dates that the specified interval intersects. So e.g. interval `1st Jan 13:00 - 1st Jan 14:00` will result in one price for `1st Jan`. Interval `1st Jan 23:00 - 2nd Jan 01:00` will result in two prices for `1st Jan` and `2nd Jan`.

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Currency` | string | required | ISO-4217 code of the [Currency](configuration.md#currency). |
| `DatesUtc` | array of string | required | Covered dates in UTC timezone in ISO 8601 format. |
| `BasePrices` | array of number | required | Base prices of the rate in the covered dates. |
| `CategoryPrices` | array of [Resource category pricing](#resource-category-pricing) | required | Resource category prices. |
| `CategoryAdjustments` | array of [Resource category adjustment](#resource-category-adjustment) | required | Resource category adjustments. |
| `RelativeAdjustment` | decimal | required | Specific amount which shows the difference between this rate and the base rate. |
| `AbsoluteAdjustment` | decimal | required | Relative amount which shows the difference between this rate and the base rate. |
| `EmptyUnitAdjustment` | decimal | required | Price adjustment for when the resource booked with this rate is not full to capacity. |
| `ExtraUnitAdjustment` | decimal | required | Price adjustment for when the resource booked with this rate exceeds capacity. |

#### Resource category pricing

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `CategoryId` | string | required | Unique identifier of the [Resource category](enterprises.md#resource-category). |
| `Prices` | array of number | required | Prices of the rate for the resource category in the covered dates. |

#### Resource category adjustment

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `CategoryId` | string | required | Unique identifier of the adjustment [Resource category](enterprises.md#resource-category). |
| `ParentCategoryId` | string | optional | Unique identifier of the parent [Resource category](enterprises.md#resource-category) that serves as a base price for the current category. |
| `RelativeValue` | number | required | Relative value of the adjustment \(e.g. `0.5` represents 50% increase\). |
| `AbsoluteValue` | number | required | Absolute value of the adjustment \(e.g. `50` represents 50 EUR in case the rate currency is `EUR`\). |

# Restriction

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the restriction. |
| `ServiceId` | string | required | Unique identifier of the [Service](#service). |
| `ExternalIdentifier` | string | optional | External identifier of the restriction. |
| `Conditions` | string | required | [Conditions](services.md#restriction-conditions) are rules that must be met by a reservation for the restriction to apply. |
| `Exceptions` | string | optional | [Exceptions](services.md#restriction-exceptions) are rules that prevent the restriction from applying to a reservation, even when all conditions have been met. |

#### Restriction Conditions

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Type` | string | required | [Restriction type](services.md#restriction-type). |
| `ExactRateId` | string | optional | Unique identifier of the restricted [Exact rate](services.md#rate). |
| `BaseRateId` | string | optional | Unique identifier of the restricted [Base rate](services.md#rate). |
| `RateGroupId` | string | optional | Unique identifier of the restricted [Rate group](services.md#rate-group). |
| `ResourceCategoryId` | string | optional | Unique identifier of the restricted [Resource category](enterprises.md#resource-category). |
| `ResourceCategoryType` | string | optional | Name of the restricted [Resource category type](enterprises.md#resource-category-type). |
| `StartUtc` | string | optional | Start of the restricted interval in UTC timezone in ISO 8601 format. |
| `EndUtc` | string | optional | End of the restricted interval in UTC timezone in ISO 8601 format. |
| `Days` | array of string [Day](services.md#day) | required | The restricted days of week. |

#### Restriction Exceptions

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `MinAdvance` | string | optional | The minimum time before the reservation starts, you can reserve in ISO 8601 duration format. |
| `MaxAdvance` | string | optional | The maximum time before the reservation starts, you can reserve in ISO 8601 duration format. |
| `MinLength` | string | optional | Minimal reservation length in ISO 8601 duration format. |
| `MaxLength` | string | optional | Maximal reservation length in ISO 8601 duration format. |
| `MinPrice` | [Currency value](finance.md#currency-value)| optional | Value of the minimum night price. |
| `MaxPrice` | [Currency value](finance.md#currency-value)| optional | Value of the maximum night price. |

#### Day

* `Monday`
* `Tuesday`
* `Wednesday`
* `Thursday`
* `Friday`
* `Saturday`
* `Sunday`

#### Restriction type

* `Stay` - guests can't stay overnight within specified dates.
* `Start`- guests can't check in within specified dates.
* `End` - guests can't check out within specified dates.

# Companionship

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of [Companionship](services.md#Companionship). |
| `CustomerId` | string | required | Unique identifier of [Customer](customers.md#customer). |
| `ReservationId` | string | optional | Unique identifier of [Reservation](reservations.md#reservation). |
| `ReservationGroupId` | string | required | Unique identifier of [Reservation group](reservations.md#reservation-group). |

# Resource access token

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of [Resource access token](#resource-access-token). |
| `ServiceOrderId` | string | required | Unique identifier of a service order (for example [Reservation](reservations.md#reservation)). |
| `CompanionshipId` | string | optional | Unique identifier of [Companionship](services.md#companionship). |
| `ResourceId` | string | optional | Unique identifier of [Resource](enterprises.md#resource). |
| `Type` | [Resource access token type](#resource-access-token-type) | required | Type of stored value. |
| `Value` | string | required | Value of resource access token |
| `SerialNumber` | string | optional | Serial number of [Resource access token type](#resource-access-token-type). |
| `ValidityStartUtc` | string | required | Marks the start of interval in which the resource access token can be used. |
| `ValidityEndUtc` | string | required | Marks the end of interval in which the resource access token can be used. |
| `Permissions` | [Resource access token permissions](#resource-access-token-permissions) | required | Specify permissions of [Resource access token](#resource-access-token). |

#### Resource access token type

* `PinCode`
* `RfidTag`

#### Resource access token permissions

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Bed` | bool | required | Specify whether [Resource access token](#resource-access-token) grants permission to access bed. |
| `Room` | bool | required | Specify whether [Resource access token](#resource-access-token) grants permission to access room. |
| `Floor` | bool | required | Specify whether [Resource access token](#resource-access-token) grants permission to access floor. |
| `Building` | bool | required | Specify whether [Resource access token](#resource-access-token) grants permission to access building. |

# Voucher

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of voucher. |
| `ServiceId` | string | required | Unique identifier of [Service](#service) the voucher belongs to. |
| `Name` | string | required | Internal name of the voucher. |
| `CreatedUtc` | string | required | Creation date and time of the voucher in UTC timezone in ISO 8601 format. |
| `UpdatedUtc` | string | required | Last update date and time of the voucher in UTC timezone in ISO 8601 format. |
| `ActivityState` | string [Activity state](#activity-state) | required | Whether voucher is active or deleted. |
| `CompanyId` | string | optional | Unique identifier of [Company](enterprises.md#company) the voucher is related to. |
| `TravelAgencyId` | string | optional | Unique identifier of [Company](enterprises.md#company) with [Travel agency contract](enterprises.md#travel-agency-contract) the voucher is related to. |

#### Voucher code

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `VoucherId` | string | required | Unique identifier of [Voucher](#voucher) the code belongs to. |
| `Value` | string | required | Value of voucher code used by customers. |
| `ValidityStartUtc` | string | optional | If specified, marks the beginning of interval in which the code can be used. |
| `ValidityEndUtc` | string | optional | If specified, marks the end of interval in which the code can be used. |
| `CreatedUtc` | string | required | Creation date and time of the voucher in UTC timezone in ISO 8601 format. |
| `UpdatedUtc` | string | required | Last update date and time of the voucher in UTC timezone in ISO 8601 format. |
| `ActivityState` | string [Activity state](#activity-state) | required | Whether voucher code is active or deleted. |

#### Voucher assignment

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `VoucherId` | string | required | Unique identifier of [Voucher](#voucher). |
| `RateId` | string | required | Unique identifier of [Rate](#rate) the voucher is assigned with. |
