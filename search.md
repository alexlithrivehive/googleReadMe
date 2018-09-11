# googleLocations.search

##### Required Oauth scope:
*https://www.googleapis.com/auth/plus.business.manage*

##### *Request:*
POST https://mybusiness.googleapis.com/v4/googleLocations:search

### *Request Body Content:*

###### JSON Representation:
```
{
  "resultCount": number,

  // Union field search_query can be only one of the following:
  "location": {
    object(Location)
  },
  "query": string
  // End of list of possible types for union field search_query.
}
```
###### Value Descriptions:
- `resultCount`:
    >*Number of results requested (Range of 1-10, default of 3)*

- `location`: 
    > Data regarding the location of the business. See Accounts.Locations.Outline.md for a breakdown and description
    ```
    {
        object(Location)   
    },
    ```


- `query`:
    > A rough string of data to use for the search (not exact, but could provide some matches)

### *Response Body Content:*
*Locations will be listed in order from best to worst match*
```
{
    "googleLocations": [
        {
            object(googleLocation)
        }
    ]
}
```
*The google location will take the form:*
```
{
  "name": string,
  "location": {
    object(Location)        
  },
  "requestAdminRightsUrl": string
}
```
###### Definitions
 - `location` 
    > Returned location that possibly matches the location that was requested. Contains the location-specific searchable `name` for the business
    
    > `location.name` takes the form *accounts/{account_id}/locations/{location_id}*
 - `name`
    > Resource name of the googleLocation *googleLocation/{googleLocation_id}* 
        > I don't know what this would be used for currently...
 - `requestAdminRightsUrl`
    > URL that takes the user to a page where they can request admin rights for the location


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk2NDI1NzY3M119
-->
