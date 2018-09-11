# accounts.locations.verifications.complete
*Completes a __PENDING__ verification*

##### Required Oauth scope:
*https://www.googleapis.com/auth/plus.business.manage*

##### *Request:*
_POST https://mybusiness.googleapis.com/v4/{name=accounts/`*`/locations/`*`/verifications/`*`}:complete_
    
> Where `*`'s should be replaced with the corresponding id for the preceding field. eg: accounts/{account_id}/locations/{location_id}

> The exact string, accounts/{account_id}/locations/{location_id/verifications/`*`}, can be found in the name of the returned `verification` object in the response listed in the __Accounts.locations.verify.md__ document

###### Parameters
- name:
    > The string of the format: accounts/{account_id}/locations/{location_id}/verifications/{verification_id}

    > This is returned in the response from the __Accounts.location.verify.md__ doc under `name`

### *Request Body Content:*

###### JSON Representation:
```
{
    "pin": string
}
```
    
###### Object Definitions and Value Descriptions:
- `pin`:
    > The pin code sent to the user/owner/merchant/verifying individual during the verification process

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
        > `FAILED`, `COMPLETED`, `PENDING`, `VERIFICATION_STATE_UNSPECIFIED`

        > Further defined in Accounts.location.verify.md, under *Response Body Content*

 - `createTime`:
    > Timestamp indicating when the verification has been __Requested__
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzY4MDE3NTQ2XX0=
-->
