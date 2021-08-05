# Enterprise

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Id` | string | required | Unique identifier of the enterprise. |
| `ChainId` | string | required | Unique identifier of the chain whose member the enterprise is. |
| `CreatedUtc` | string | required | Creation date and time of the enterprise in UTC timezone in ISO 8601 format. |
| `Name` | string | required | Name of the enterprise. |
| `TimeZoneIdentifier` | string | required | IANA timezone identifier of the enterprise. |
| `LegalEnvironmentCode` | string | required | Unique identifier of the legal environment where the enterprise resides. |
| `DefaultLanguageCode` | string | required | Language-culture codes of the enterprise default [Language](configuration.md#language). |
| `EditableHistoryInterval` | string | required | Editable history interval in ISO 8601 duration format. |
| `WebsiteUrl` | string | optional | URL of the enterprise website. |
| `Email` | string | optional | Email address of the enterprise. |
| `Phone` | string | optional | Phone number of the enterprise. |
| `LogoImageId` | string | required | Unique identifier of the enterprise logo image. |
| `CoverImageId` | string | required | Unique identifier of the enterprise cover image. |
| `Address` | [Address](configuration.md#address) | required | Address of the enterprise. |
| `Currencies` | array of [Accepted currency](configuration.md#accepted-currency) | required | Currencies accepted by the enterprise. |
| `Pricing` | string | required | [Pricing](configuration.md#pricing) of the enterprise. |
| `TaxPrecision` | string | optional | Tax precision used for financial calculations in the enterprise. If `null`, [Currency](configuration.md#currency) precision is used. |

#### Address

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Id` | string | required | Unique identifier of the address. |
| `Line1` | string | optional | First line of the address. |
| `Line2` | string | optional | Second line of the address. |
| `City` | string | optional | The city. |
| `PostalCode` | string | optional | Postal code. |
| `CountryCode` | string | optional | ISO 3166-1 code of the [Country](configuration.md#country). |
| `CountrySubdivisionCode` | string | optional | ISO 3166-2 code of the administrative division, e.g. `DE-BW`. |
| `Latitude` | number | optional | The latitude. |
| `Longitude` | number | optional | The longitude. |

#### Accepted currency

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Currency` | string | required | ISO-4217 code of the [Currency](configuration.md#currency). |
| `IsDefault` | bool | required | Whether the currency is a default accounting currency. |
| `IsEnabled` | bool | required | Whether the currency is enabled for usage. |

#### Pricing

* `Gross` - the enterprise shows amount with gross prices.
* `Net` - the enterprise shows amount with net prices.

#### Payment card storage

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `PublicKey` | string | required | Key for accessing PCI proxy storage. |

---



# Country

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Code` | string | required | ISO 3166-1 alpha-2 code, e.g. `US` or `GB`. |
| `EnglishName` | string | required | English name of the country. |

#### Country subdivision

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Code` | string | required | ISO 3166-2 code of the administrative division, e.g `AU-QLD`. |
| `CountryCode` | string | required | ISO 3166-1 code of the [Country](configuration.md#country). |
| `EnglishName` | string | required | English name of the country subdivision. |

#### Country alliance

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Code` | string | required | Code of the alliance, e.g `EU`, `SCHENGEN`, `SCHENGEN-VISA`. |
| `EnglishName` | string | required | English name of the alliance. |
| `CountryCodes` | array of string | required | ISO 3166-1 codes of the member countries. |

# Currency

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Code` | string | required | ISO-4217 three-letter code, e.g. `USD` or `GBP`. |
| `Precision` | number | required | Precision of the currency \(count of decimal places\). |

# Tax environment

Tax environment represents set of [Taxation](configuration.md#taxation)s together with optional validity interval.

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Code` | string | required | Code of the tax environment. |
| `CountryCode` | string | required | ISO 3166-1 alpha-3 code of associated country, e.g. `USA` or `GBR`. |
| `TaxationCodes` | array of string | required | Codes of the [taxation](configuration.md#taxation)s that are used by this environment. |
| `ValidityStartUtc` | string | optional | If specified, marks the start of the validity interval in UTC timezone in ISO 8601 format. |
| `ValidityEndUtc` | string | optional | If specified, marks the end of the validity interval in UTC timezone in ISO 8601 format. |

# Taxation

Taxation represents set of [Tax rate](configuration.md#tax-rate)s within [Tax environment](configuration.md#tax-environment).

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Code` | string | required | Code of the taxation. |
| `Name` | string | required | Name of the taxation. |
| `LocalName` | string | required | Local name of the taxation. |

#### Tax rate

Definition of single tax rate.

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Code` | string | required | Code of the tax rate. To be used when posting revenue items which should be accompanied by the tax rate\(s\) applicable to the nature of the item and the tax environment. |
| `TaxationCode` | string | required | Code of the [Taxation](configuration.md#taxation) the rate is part of. |
| `Strategy` | object [Tax rate strategy](configuration.md#tax-rate-strategy) | required | Tax strategy type, e.g. relative, flat or dependent. |

#### Tax rate strategy

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Discriminator` | string [Tax rate strategy discriminator](configuration.md#tax-rate-strategy-discriminator) | required | If tax rate is flat, relative or dependent. |
| `Value` | object | required | Structure of the object depends on [Tax rate strategy discriminator](configuration.md#tax-rate-strategy-discriminator). |

#### Tax rate strategy discriminator

* `Flat` - Used with [Flat tax rate strategy data](configuration.md#flat-tax-rate-strategy-data) \(e.g. 5.00 EUR\). 
* `Relative` - Used with [Relative tax rate strategy data](configuration.md#relative-tax-rate-strategy-data) \(e.g. 21%\). Relative tax is calculated only from net base value.
* `Dependent` - Used with [Dependent tax rate strategy data](configuration.md#dependent-tax-rate-strategy-data) \(e.g. 10%\). Dependent tax is calculated from net base value and all taxes it depends on.

#### Flat tax rate strategy data

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Value` | number | required | Absolute value of tax. |
| `CurrencyCode` | string | required | Code of [Currency](configuration.md#currency). |

#### Relative tax rate strategy data

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Value` | decimal | required | Tax rate, e.g. `0.21` in case of 21% tax rate. |

#### Dependent tax rate strategy data

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `BaseTaxationCodes` | array of string | required | Codes of the [taxation](configuration.md#taxation)s that are included in the base of calculation. |
| `Value` | decimal | required | Tax rate, e.g. `0.1` in case of 10% tax rate. |

# Language

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Code` | string | required | Language-culture code of the language. |
| `FallbackLanguageCode` | string | optional | Language-culture code of the fallback language. |
| `EnglishName` | string | required | English name of the language. |
| `LocalName` | string | required | Local name of the language. |

# Language texts

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `LanguageCode` | string | required | Language-culture code of the [Language](configuration.md#language). |
| `Texts` | number | required | Texts in the specified language by their keys. |

# Image URL

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `ImageId` | string | required | Unique identifier of the image. |
| `Url` | string | required | URL of the image. |

