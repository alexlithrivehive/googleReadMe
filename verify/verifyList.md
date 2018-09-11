# Accounts.Locations.Verifications.List.md
*Lists all of the Pending, Failed, and Completed verifications for a specific business/location*

##### Required Oauth scope:
*https://www.googleapis.com/auth/plus.business.manage*

##### *Request:*
*GET https://mybusiness.googleapis.com/v4/{parent=accounts/`*`/locations/`*`}/verifications*
    
> Where `*`'s should be replaced with the corresponding id for the preceding field. eg: accounts/{account_id}/locations/{location_id}

> The exact string, accounts/{account_id}/locations/{location_id}, can be found in the `name` object of the returned `googleLocation` object in the response listed in the __googleLocations.search.md__ document

###### Parameters
- parent:
    > The string of the format: accounts/{account_id}/locations/{location_id}/verifications/{verification_id}

    > This is returned in the response from the __googleLocations.Search.md__ doc under `name`
- Query Parameters :
    - `pageSize` : Number of verifications to include per page (If not included, all verifications will be returned in one sitting)
    - `pageToken` : Token to receive the next page of verifications

### *Request Body Content:*
*Request Body __Must be empty__*

### *Response Body Content:*
###### JSON Representation:
```
{
  "verifications": [
    {
      object(Verification)
    }
  ],
  "nextPageToken": string
}
```
    
###### Value Descriptions:
- `verifications`:
    > List of *Verification* Objects describing each verification event that has occurred for a particular business

    > Described in the *Accounts.locations.verify.md* doc under *Response Body Content*
- `nextPageToken`:
    > Token that can be returned in the next __GET__ request to receive the next page page of verifications
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDI4MTE2OTI2XX0=
-->
