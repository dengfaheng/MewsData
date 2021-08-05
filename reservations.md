# Reservations

| Property                    | Type                                             | Contract | Description                                                  |
| --------------------------- | ------------------------------------------------ | -------- | ------------------------------------------------------------ |
| `Id`                        | string                                           | required | Unique identifier of the reservation.                        |
| `ServiceId`                 | string                                           | required | Unique identifier of the [Service](services.md#service) that is reserved. |
| `GroupId`                   | string                                           | required | Unique identifier of the [Reservation group](#reservation-group). |
| `Number`                    | string                                           | required | Confirmation number of the reservation in Mews.              |
| `ChannelNumber`             | string                                           | optional | Number of the reservation within the Channel \(i.e. OTA, GDS, CRS, etc\) in case the reservation group originates there \(e.g. Booking.com confirmation number\). |
| `ChannelManagerNumber`      | string                                           | optional | Unique number of the reservation within the reservation group. |
| `ChannelManagerGroupNumber` | string                                           | optional | Number of the reservation group within a Channel manager that transferred the reservation from Channel to Mews. |
| `ChannelManager`            | string                                           | optional | Name of the Channel manager \(e.g. AvailPro, SiteMinder, TravelClick, etc\). |
| `State`                     | string [Reservation state](#reservation-state)   | required | State of the reservation.                                    |
| `Origin`                    | string [Reservation origin](#reservation-origin) | required | Origin of the reservation.                                   |
| `CreatedUtc`                | string                                           | required | Creation date and time of the reservation in UTC timezone in ISO 8601 format. |
| `UpdatedUtc`                | string                                           | required | Last update date and time of the reservation in UTC timezone in ISO 8601 format. |
| `CancelledUtc`              | string                                           | optional | Cancellation date and time in UTC timezone in ISO 8601 format. |
| `StartUtc`                  | string                                           | required | Start of the reservation \(arrival\) in UTC timezone in ISO 8601 format. |
| `EndUtc`                    | string                                           | required | End of the reservation \(departure\) in UTC timezone in ISO 8601 format. |
| `ReleasedUtc`               | string                                           | optional | Date when the optional reservation is released in UTC timezone in ISO 8601 format. |
| `RequestedCategoryId`       | string                                           | required | Identifier of the requested [Resource category](enterprises.md#resource-category). |
| `AssignedResourceId`        | string                                           | optional | Identifier of the assigned [Resource](enterprises.md#resource). |
| `AssignedResourceLocked`    | bool                                             | required | Whether the reservation is locked to the assigned [Resource](enterprises.md#resource) and cannot be moved. |
| `BusinessSegmentId`         | string                                           | optional | Identifier of the reservation [Business segment](services.md#business-segment). |
| `CompanyId`                 | string                                           | optional | Identifier of the [Company](enterprises.md#company) on behalf of which the reservation was made. |
| `TravelAgencyId`            | string                                           | optional | Identifier of the [Company](enterprises.md#company) that mediated the reservation. |
| `AvailabilityBlockId`       | string                                           | optional | Unique identifier of the [Availability block](services.md#availability-block) the reservation is assigned to. |
| `RateId`                    | string                                           | required | Identifier of the reservation [Rate](services.md#rate).      |
| `VoucherId`                 | string                                           | optional | Unique identifier of the [Voucher](services.md#voucher) that has been used to create reservation. |
| `AdultCount`                | number                                           | required | Count of adults the reservation was booked for.              |
| `ChildCount`                | number                                           | required | Count of children the reservation was booked for.            |
| `CustomerId`                | string                                           | required | Unique identifier of the [Customer](customers.md#customer) who owns the reservation. |

#### Reservation group

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Id` | string | required | Unique identifier of the reservation group. |
| `Name` | string | optional | Name of the reservation group, might be empty or same for multiple groups. |

#### Reservation state

* `Enquired` - Confirmed neither by the customer nor enterprise.
* `Requested` - Confirmed by the customer but not by the enterprise \(waitlist\).
* `Optional` - Confirmed by enterprise but not by the guest \(the enterprise is holding resource for the guest\).
* `Confirmed` - Confirmed by both parties, before check-in.
* `Started` - Checked in.
* `Processed` - Checked out.
* `Canceled` - Canceled.

#### Reservation origin

* `Distributor`
* `ChannelManager`
* `Commander`
* `Import`
* `Connector`
* `Navigator`
