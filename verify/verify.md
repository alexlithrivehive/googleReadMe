# accounts.locations.fetchVerificationOptions

##### Required Oauth scope:
*https://www.googleapis.com/auth/plus.business.manage*

##### *Request:*
_POST https://mybusiness.googleapis.com/v4/{name=accounts/`*`/locations/`*`}:verify_
    
> Where `*`'s should be replaced with the corresponding id for the preceding field. eg: accounts/{account_id}/locations/{location_id}

> The exact string, accounts/{account_id}/locations/{location_id}, can be found in the name of the returned `googleLocation` object in the response listed in the __googleLocations.search.md__ document (2 steps ago)

###### Parameters
- name:
    > The string of the format: accounts/{account_id}/locations/{location_id}

    > This is returned in the response from the __googleLocations.search.md__ doc under `name`

### *Request Body Content:*

###### JSON Representation:
*The request has 3 possibilities, based on the verification method that is being used (See Accounts.locations.fetchVerificationOptions.md doc, Response section for a detailed description of the return types*
 - VerificationMethod == `EMAIL`
    ```
    {
        "method": enum(VerificationMethod), //In this case, EMAIL
        "languageCode": string,
        "emailInput": {
            object(EmailInput)          //Defined below
        }
    }
    ```

 - VerificationMethod == `ADDRESS`
    ```
    {
        "method": enum(VerificationMethod), //In this case, ADDRESS
        "languageCode": string,
        "addressInput": {
            object(AddressInput)       //Defined below
        }
    }
    ```

 - VerificationMethod == `SMS` or `PHONE_CALL`
    ```
    {
        "method": enum(VerificationMethod), //In this case, SMS or PHONE_CALL
        "languageCode": string,
        "phoneInput": {
            object(PhoneInput)         //Defined below
        }
    }
    ```
    
###### Object Definitions and Value Descriptions:
- `method`:
    > The enum type describing the type of verification that is being used to verify the business location
- `languageCode`:
    > The BCP 47 language code that is also sent in in a PostalAddress object (*Listed in the Accounts.Locations.Outline.md doc*). Use `en` for U.S. based businesses
- `emailInput`:
    > The email information that will be used to verify via email
    
    > *`EmailInput` Object Definition*

    ```
    {
        "emailAddress":string
    }
    ``` 
    - `emailAddress`:
        > The email address where the verification email will be sent to

        > This address is only valid if it is one of the addresses used in the `locations.fetchVerificationOptions` step, or in the event that `isUserNameEditable` is true in the same step, an address with the same domain name
- `addressInput`:
    > The address information that will be used to verify via a post card

    > *`AddressInput` Object Definition*
    ```
    {
        "mailerContactName": string
    }
    ```
    - `mailerContactName`:
        > The name of the individual that the post card should be sent to (Just a person's name)
- `phoneInput`:
    > The phone information that will be used to verify via a phone call or sms text 

    > *`PhoneInput` Object Definition*
    ```
    {
        "phoneNumber": string
    }
    ```
    - `phoneNumber`:
        > The phone number that will be contacted to complete the verification process

        > This number must be the one(s) that was verified in the response from `locations.fetchVerificationOptions`


### *Response Body Content:*
```
{
  "verification": {
    object(Verification)
  }
}
```
*Verification Object*
```
{
  "name": string,
  "method": enum(VerificationMethod), //Defined Below
  "state": enum(VerificationState),   //Defined Below
  "createTime": string
}
```

###### Definitions and Explainations
 - `name`:
    > The `Accounts/{account_id}/locations/{location_id}/verifications/{verification_id}` Identifier for the location in question

 - `method`:
    > The enumerated descriptor for the verification process that the location is/has been undergoing

    - __*VerificationMethod Enum*__
        > `ADDRESS`, `EMAIL`, `PHONE_CALL`, `SMS`, `AUTO`, `VERIFICATION_METHOD_UNSPECIFIED`

        > Further defined in Accounts.locations.fetchVerificationOptions, under *Response Body Content*

 - `state`:
    > The enumerated descriptor of the state of the verification process

    - __*VerificationState Enum*__
        > `FAILED` - The verification has failed

        > `COMPLETED` - The verification has completed (Successful?)

        > `PENDING` - The verification is still in process

        > `VERIFICATION_STATE_UNSPECIFIED` - A default value that __WILL__ result in errors

 - `createTime`:
    > Timestamp indicating when the verification has been __Requested__
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY2NTkyMDg2MV19
-->
