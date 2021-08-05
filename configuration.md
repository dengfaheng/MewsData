# Configuration

## Get configuration

Returns configuration of the enterprise and the client.

### Request

`[PlatformAddress]/api/connector/v1/configuration/get`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0"
}
```

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `ClientToken` | string | required | Token identifying the client application. |
| `AccessToken` | string | required | Access token of the client application. |
| `Client` | string | required | Name and version of the client application. |

### Response

```javascript
{
    "NowUtc": "2018-01-01T14:58:02Z",
    "Enterprise": {
        "Id": "851df8c8-90f2-4c4a-8e01-a4fc46b25178",
        "ChainId": "8ddea57b-6a5c-4eec-8c4c-24467dce118e",
        "CreatedUtc": "2015-07-07T13:33:17Z",
        "Name": "Connector API Hotel",
        "TimeZoneIdentifier": "Europe/Budapest",
        "LegalEnvironmentCode": "UK",
        "DefaultLanguageCode": "en-US",
        "EditableHistoryInterval": "P0M3DT0H0M0S",
        "WebsiteUrl": "https://en.wikipedia.org/wiki/St._Vitus_Cathedral",
        "Email": "charging-api@mews.li",
        "Phone": "00000 123 456 789",
        "LogoImageId": null,
        "CoverImageId": null,
        "Address": {
            "Id": "8c2c4371-5d42-40a9-b551-ab0b00d75076",
            "Line1": "Anenské nám. 1",
            "Line2": "Ahoj",
            "City": "Prague",
            "PostalCode": "110 00",
            "CountryCode": "CZ",
            "CountrySubdivisionCode": null,
            "Latitude": 50.085180,
            "Longitude": 14.414926
        },
        "Currencies": [
            {
                "Currency": "GBP",
                "IsDefault": true,
                "IsEnabled": true
            },
            {
                "Currency": "USD",
                "IsDefault": false,
                "IsEnabled": true
            }
        ],
        "Pricing": "Gross",
        "TaxPrecision": null
    },
    "Service":
    {
        "Id": "bd26d8db-86da-4f96-9efc-e5a4654a4a94",
        "IsActive": true,
        "Name": "Accommodation",
        "StartTime": "PT14H",
        "EndTime": "PT12H",
        "Promotions": {
            "BeforeCheckIn": false,
            "AfterCheckIn": false,
            "DuringStay": false,
            "BeforeCheckOut": false,
            "AfterCheckOut": false
        },
        "Type": "Reservable"
    },
    "PaymentCardStorage": null
}
```

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `NowUtc` | string | required | Current server date and time in UTC timezone in ISO 8601 format. |
| `Enterprise` | [Enterprise](configuration.md#enterprise) | required | The enterprise \(e.g. hotel, hostel\) associated with the access token. |
| `Service` | [Service](services.md#service) | optional | The reservable service \(e.g. accommodation, parking\) associated with the access token of the service scoped integration. |
| `PaymentCardStorage` | [PaymentCardStorage](configuration.md#payment-card-storage) | optional | Contains information about payment card storage. |

#### Enterprise

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

## Get all currencies

Returns all currencies supported by the API.

### Request

`[PlatformAddress]/api/connector/v1/currencies/getAll`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0"
}
```

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `ClientToken` | string | required | Token identifying the client application. |
| `AccessToken` | string | required | Access token of the client application. |
| `Client` | string | required | Name and version of the client application. |

### Response

```javascript
{
    "Currencies": [
        {
            "Code": "USD",
            "Precision": 2
        },
        {
            "Code": "GBP",
            "Precision": 2
        }
    ]
}
```

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Currencies` | array of [Currency](configuration.md#currency) | required | The supported currencies. |

#### Currency

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Code` | string | required | ISO-4217 three-letter code, e.g. `USD` or `GBP`. |
| `Precision` | number | required | Precision of the currency \(count of decimal places\). |

## Get all tax environments

Returns all tax environments supported by the API.

### Request

`[PlatformAddress]/api/connector/v1/taxenvironments/getAll`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0"
}
```

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `ClientToken` | string | required | Token identifying the client application. |
| `AccessToken` | string | required | Access token of the client application. |
| `Client` | string | required | Name and version of the client application. |

### Response

```javascript
{
    "TaxEnvironments": [
        {
            "Code": "AT-2020",
            "CountryCode": "AUT",
            "TaxationCodes": [
                "AT-2020",
                "AT-2020-Extra"
            ],
            "ValidityStartUtc": "2020-06-30T22:00:00Z",
            "ValidityEndUtc": null
        },
        {
            "Code": "AT-2016",
            "CountryCode": "AUT",
            "TaxationCodes": [
                "AT-2016"
            ]
            "ValidityStartUtc": "2016-05-01T00:00:00Z",
            "ValidityEndUtc": "2020-06-30T22:00:00Z"
        },
        {
            "Code": "AT",
            "CountryCode": "AUT",
            "TaxationCodes": [
                "AT"
            ],
            "ValidityStartUtc": null,
            "ValidityEndUtc": "2016-05-01T00:00:00Z"
        }
    ]
}
```

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `TaxEnvironments` | array of [Tax environment](configuration.md#tax-environment) | required | The supported tax environments. |

#### Tax environment

Tax environment represents set of [Taxation](configuration.md#taxation)s together with optional validity interval.

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Code` | string | required | Code of the tax environment. |
| `CountryCode` | string | required | ISO 3166-1 alpha-3 code of associated country, e.g. `USA` or `GBR`. |
| `TaxationCodes` | array of string | required | Codes of the [taxation](configuration.md#taxation)s that are used by this environment. |
| `ValidityStartUtc` | string | optional | If specified, marks the start of the validity interval in UTC timezone in ISO 8601 format. |
| `ValidityEndUtc` | string | optional | If specified, marks the end of the validity interval in UTC timezone in ISO 8601 format. |

## Get all taxations

Returns all taxations supported in tax environments.

### Request

`[PlatformAddress]/api/connector/v1/taxations/getAll`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0"
}
```

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `ClientToken` | string | required | Token identifying the client application. |
| `AccessToken` | string | required | Access token of the client application. |
| `Client` | string | required | Name and version of the client application. |

### Response

```javascript
{
    "Taxations": [
        {
            "Code": "AT-2020",
            "Name": "VAT",
            "LocalName": "MWST"
        },
        {
            "Code": "AT-2020-Extra",
            "Name": "Extra tax on top of VAT",
            "LocalName": "Extra tax on top of MWST"
        },
        {
            "Code": "AT-2016",
            "Name": "VAT",
            "LocalName": "MWST"
        },
        {
            "Code": "AT",
            "Name": "VAT",
            "LocalName": "MWST"
        }
    ],
    "TaxRates": [
        {
            "Code": "AT-2020-21%",
            "TaxationCode": "AT",
            "Strategy": {
                "Discriminator": "Relative",
                "Value": {
                    "Value": 0.21
                }
            }
        },       
        {
            "Code": "AT-2020-Extra-10%",
            "TaxationCode": "AT-2020-Extra-10%",
            "Strategy": {
                "Discriminator": "Dependent",
                "Value": {
                    "BaseTaxationCodes": [
                        "AT-2020"
                    ],
                    "Value": 0.1
                }
            }
        },
        {
            "Code": "AT-5-EUR",
            "TaxationCode": "AT",
            "Strategy": {
                "Discriminator": "Flat",
                "Value": {
                    "Value": 5.0,
                    "CurrencyCode": "EUR"
                }
            }
        }
    ]
}
```

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Taxations` | array of [Taxation](configuration.md#taxation) | required | The supported taxations. |
| `TaxRates` | array of [Tax rate](configuration.md#tax-rate) | required | The supported tax rates. |

#### Taxation

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

### Tax rate strategy data

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

## Get all languages

Returns all languages supported by the API.

### Request

`[PlatformAddress]/api/connector/v1/languages/getAll`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0"
}
```

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `ClientToken` | string | required | Token identifying the client application. |
| `AccessToken` | string | required | Access token of the client application. |
| `Client` | string | required | Name and version of the client application. |

### Response

```javascript
{
    "Languages": [
        {
            "Code": "zh-CN",
            "EnglishName": "Chinese (Simplified)",
            "FallbackLanguageCode": "en-US",
            "LocalName": "中文"
        },
        {
            "Code": "cs-CZ",
            "EnglishName": "Czech",
            "FallbackLanguageCode": "en-US",
            "LocalName": "Čeština"
        }
    ]
}
```

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Languages` | array of [Language](configuration.md#language) | required | The supported languages. |

#### Language

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Code` | string | required | Language-culture code of the language. |
| `FallbackLanguageCode` | string | optional | Language-culture code of the fallback language. |
| `EnglishName` | string | required | English name of the language. |
| `LocalName` | string | required | Local name of the language. |

## Get language texts

Returns translations of texts in the specified languages.

### Request

`[PlatformAddress]/api/connector/v1/languages/getTexts`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0",
    "LanguageCodes": [
        "en-US",
        "cs-CZ"
    ],
    "Scope": ""
}
```

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `ClientToken` | string | required | Token identifying the client application. |
| `AccessToken` | string | required | Access token of the client application. |
| `Client` | string | required | Name and version of the client application. |
| `LangaugeCodes` | array of string | required | Language-culture codes of the [Language](configuration.md#language)s whose texts to return. |
| `Scope` | string | required | Scope of texts to return. |

### Response

```javascript
{
    "LanguageTexts": [
        {
            "LanguageCode": "en-US",
            "Texts": {
                "Address": "Address",
                "AddressLine1": "Address line 1",
                "AddressLine2": "Address line 2",
                "AdultPlural": "Adults",
                "Apartment": "Apartment",
                "ApartmentPlural": "Apartments"
            }
        }
    ]
}
```

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `LanguageTexts` | array of [Language texts](configuration.md#language-texts) | required | Texts in the specified languages. |

#### Language texts

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `LanguageCode` | string | required | Language-culture code of the [Language](configuration.md#language). |
| `Texts` | number | required | Texts in the specified language by their keys. |

## Get image URLs

Returns URLs of the specified images.

### Request

`[PlatformAddress]/api/connector/v1/images/getUrls`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0",
    "Images":[
        {
            "ImageId": "57a971a5-a335-48f4-8cd1-595245d1a876",
            "Width": 200,
            "Height": 150,
            "ResizeMode": "Fit"
        }
    ]
}
```

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `ClientToken` | string | required | Token identifying the client application. |
| `AccessToken` | string | required | Access token of the client application. |
| `Client` | string | required | Name and version of the client application. |
| `Images` | array of [Image parameters](configuration.md#image-parameters) | required | Parameters of images whose URLs should be returned. |

#### Image parameters

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `ImageId` | string | required | Unique identifier of the image. |
| `Width` | number | required | Desired width of the image. |
| `Height` | number | required | Desired height of the image. |
| `ResizeMode` | string [Image resize mode](configuration.md#image-resize-mode) | required | Mode how the image should be resized to the desired width and height. |

#### Image resize mode

* `Fit` - resize to fit within the specified size, so the result might be smaller than requested.
* `FitExact` - resize and pad to exactly fit within the specified size.
* `Cover` - resize to cover the specified dimensions, so the result might be larger than requested.
* `CoverExact` - resize and clip to cover the specified size.

### Response

```javascript
{
    "ImageUrls": [
        {
            "ImageId": "57a971a5-a335-48f4-8cd1-595245d1a876",
            "Url": "https://cdn.demo.mews.li/Media/Image/57a971a5-a335-48f4-8cd1-595245d1a876?Mode=Fit&Width=200&Height=150"
        }
    ]
}
```

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `ImageUrls` | array of [Image URL](configuration.md#image-url) | required | URLs of the images. |

#### Image URL

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `ImageId` | string | required | Unique identifier of the image. |
| `Url` | string | required | URL of the image. |

