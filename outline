### Accounts.Locations Outlines and Breakdowns

##### Locations Object
```
{
  "name": string,            // A searchable description of the business name, 
                             // that can be parsed for the account_id and location_id. 
                             // Takes the form 'Accounts/{account_id}/locations{location_id}'
  "languageCode": string,
  "storeCode": string,
  "locationName": string,
  "primaryPhone": string,
  "additionalPhones": [
    string
  ],
  "address": {
    object(PostalAddress)     //Defined below
  },
  "primaryCategory": {
    object(Category)          //Defined below
  },
  "additionalCategories": [
    {
      object(Category)        //Defined below
    }
  ],
  "websiteUrl": string,
  "regularHours": {
    object(BusinessHours)     //Defined below
  },
  "specialHours": {
    object(SpecialHours)      
  },
  "serviceArea": {
    object(ServiceAreaBusiness)
  },
  "locationKey": {
    object(LocationKey)
  },
  "labels": [
    string
  ],
  "adWordsLocationExtensions": {
    object(AdWordsLocationExtensions)
  },
  "latlng": {
    object(LatLng)      //Defined Below
  },
  "openInfo": {
    object(OpenInfo)
  },
  "locationState": {
    object(LocationState)
  },
  "attributes": [
    {
      object(Attribute)
    }
  ],
  "metadata": {
    object(Metadata)
  },
  "priceLists": [
    {
      object(PriceList)
    }
  ],
  "profile": {
    object(Profile)
  },
  "relationshipData": {
    object(RelationshipData)
  }
}
```

##### PostalAddress Object
```
{
    "revision": number,           //Must be set to 0
    "regionCode": string,         //Must be set to the code for the country/region that the business resides in. 'US' for united states companies
    "languageCode": string,       //Optional, but should be set to 'en' for U.S. companies if it is to be set
    "postalCode": string,         //Optional but recommended to be included
    "sortingCode": string,        //Optional
    "administrativeArea": string, //Optional, but this would be the state if we use it (Recommended)
    "locality": string,           //Optional, but this would be the city (Recommended)
    "sublocality": string,        //Optional, but this would be a district or a borough if we were to use it (Maybe for cities like LA or NY?)
    "addressLines": [
      string                      //This is the Street address. ex: Line 1: 1550 Wynkoop Street \n Line 2: Floor 2 (City, State, Zip... are already included, so they should not be listed)
    ],
    "recipients": [
      string                      //Optional, a specific individual/group at a location (Not Recommended)
    ],
    "organization": string        //Optional, the name of the company at this address
}
```

##### Category Object
```
{
    "displayName": string,  //Human readable version of the categoryId (What we would show to the user)
    "categoryId": string    //Google Id for the category. Must be provided when creating or updating a category for a location
}
```

##### BusinessHours Object
```
{
    "periods": [
      { 
        object(TimePeriod)  //Yep, another sub-object, Defined below
      }
    ]
}
```

##### TimePeriod Object
```
{
    "openDay": enum(DayOfWeek),     //MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY, DAY_OF_WEEK_UNSPECIFIED (Not sure what this one would be for)
    "openTime": string,             //24-hr hh:mm format, ranging 00:00-24:00 eg: 2:32pm would be input as 14:32 
    "closeDay": enum(DayOfWeek),    //MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY, DAY_OF_WEEK_UNSPECIFIED (Not sure what this one would be for)
    "closeTime": string             //24-hr hh:mm format, ranging 00:00-24:00 eg: 2:32pm would be input as 14:32 
}  
```
>NOTE: openDay and openTime would be the day and time of open. closeDay and closeTime would be the day and time of close. 
>      so if the business opens at 8am on Friday and Closes at 5pm on Friday, then this would look like this:
```
{
  "openDay": FRIDAY,
  "openTime": "08:00",
  "closeDay": FRIDAY,
  "closeTime": "17:00"
}
```
>     If the shop opened at the same time on Friday, and closed at 5pm on Saturday (33hr pop up store, I suppose), then the input would be:
```
{
  "openDay": FRIDAY,
  "openTime": "08:00",
  "closeDay": SATURDAY,
  "closeTime": "17:00"
}
```

##### LatLng Object
```
{
    "latitude":number 
    "longitude":number
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDYyOTY3NTc3XX0=
-->
