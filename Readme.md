For starters, we have to retrieve all necessary information via the API `Get all Reservations`，which will provide us the following data:

| Property                      | Type                                                         | Contract | Description                                                |
| ----------------------------- | ------------------------------------------------------------ | -------- | ---------------------------------------------------------- |
| `BusinessSegments`            | array of [Business segment](services.md#business-segment)    | optional | Business segments of the reservations.                     |
| `Customers`                   | array of [Customer](customers.md#customer)                   | optional | Customers that are members of the reservations.            |
| `Items`                       | array of [Accounting item](finance.md#accounting-item)       | optional | Revenue items of the reservations.                         |
| `Products`                    | array of [Product](services.md#product)                      | optional | Products orderable with reservations.                      |
| `RateGroups`                  | array of [Rate group](services.md#rate-group)                | optional | Rate groups of the reservation rates.                      |
| `Rates`                       | array of [Rate](services.md#rate)                            | optional | Rates of the reservations.                                 |
| `ReservationGroups`           | array of [Reservation group](reservations.md#reservation-group) | optional | Reservation groups that the reservations are members of.   |
| `Reservations`                | array of [Reservation](reservations.md#reservation)          | optional | The reservations that collide with the specified interval. |
| `Services`                    | array of [Service](services.md#service)                      | optional | Services that have been reserved.                          |
| `Resources`                   | array of [Resource](enterprises.md#resource)                 | optional | Assigned resources of the reservations.                    |
| `ResourceCategories`          | array of [Resource category](enterprises.md#resource-category) | optional | Resource categories of the resources.                      |
| `ResourceCategoryAssignments` | array of [Resource category assignment](enterprises.md#resource-category-assignment) | optional | Assignments of the resources to categories.                |
| `Notes`                       | array of [Order note](#order-note)                           | optional | Notes of the reservations.                                 |
| `QrCodeData`                  | array of [QrCode data](#qrcode-data)                         | optional | QR code data of the reservations.                          |



#### Order note

| Property     | Type                                       | Contract | Description                                                  |
| ------------ | ------------------------------------------ | -------- | ------------------------------------------------------------ |
| `Id`         | string                                     | required | Unique identifier of the note.                               |
| `OrderId`    | string                                     | required | Unique identifier of the order or [Reservation](#reservations). |
| `Text`       | string                                     | required | Value of the note.                                           |
| `Type`       | string [Order note type](#order-note-type) | required | Type of the note.                                            |
| `CreatedUtc` | string                                     | required | Creation date and time of the note in UTC timezone in ISO 8601 format. |

#### Order note type

* `General`
* `ChannelManager`
* ...

#### QrCode data

| Property        | Type   | Contract | Description                              |
| --------------- | ------ | -------- | ---------------------------------------- |
| `ReservationId` | string | required | Unique identifier of the reservation.    |
| `Data`          | string | required | Reservation data for QR code generation. |



The  data samples are as follow:

```json
{
    "BusinessSegments": null,
    "Customers": [
        {
            "Address": null,
            "BirthDate": null,
            "BirthPlace": null,
            "CategoryId": null,
            "Classifications": [],
            "CreatedUtc": "2016-01-01T00:00:00Z",
            "Email": null,
            "FirstName": "John",
            "Sex": null,
            "Id": "35d4b117-4e60-44a3-9580-c582117eff98",
            "IdentityCard": null,
            "LanguageCode": null,
            "LastName": "Smith",
            "LoyaltyCode": null,
            "NationalityCode": "US",
            "Notes": "",
            "Number": "1",
            "Passport": null,
            "Phone": "00420123456789",
            "SecondLastName": null,
            "TaxIdentificationNumber": null,
            "Title": null,
            "UpdatedUtc": "2016-01-01T00:00:00Z",
            "Visa": null
        }
    ],
    "Items": null,
    "Products": null,
    "RateGroups": null,
    "Rates": null,
    "ReservationGroups": [
        {
            "Id": "c704dff3-7811-4af7-a3a0-7b2b0635ac59",
            "Name": "13-12-Smith-F712"
        }
    ],
    "Reservations": [
        {
            "Id": "bfee2c44-1f84-4326-a862-5289598f6e2d",
            "ServiceId": "bd26d8db-86da-4f96-9efc-e5a4654a4a94",
            "GroupId": "94843f6f-3be3-481b-a1c7-06458774c3df",
            "Number": "52",
            "ChannelManager": "",
            "ChannelManagerGroupNumber": null,
            "ChannelManagerNumber": null,
            "ChannelNumber": null,
            "State": "Processed",
            "Origin": "Connector",
            "CreatedUtc": "2016-02-20T14:58:02Z",
            "UpdatedUtc": "2016-02-20T14:58:02Z",
            "CancelledUtc": null,
            "StartUtc": "2016-02-20T13:00:00Z",
            "EndUtc": "2016-02-22T11:00:00Z",
            "ReleasedUtc": null,
            "RequestedCategoryId": "773d5e42-de1e-43a0-9ce6-f940faf2303f",
            "AssignedResourceId": "20e00c32-d561-4008-8609-82d8aa525714",
            "AssignedResourceLocked": false,
            "BusinessSegmentId": null,
            "CompanyId": null,
            "TravelAgencyId": null,
            "AvailabilityBlockId": null,
            "RateId": "ed4b660b-19d0-434b-9360-a4de2ea42eda",
            "VoucherId": null,
            "AdultCount": 2,
            "ChildCount": 0,
            "CustomerId": "35d4b117-4e60-44a3-9580-c582117eff98"
        }
    ],
    "Services": null,
    "Resources": null,
    "ResourceCategories": null,
    "ResourceCategoryAssignments": null,
    "Notes": null
}
```

