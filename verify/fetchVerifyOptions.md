# accounts.locations.fetchVerificationOptions

##### Required Oauth scope:
*https://www.googleapis.com/auth/plus.business.manage*

##### *Request:*
_POST https://mybusiness.googleapis.com/v4/{`name`=accounts/`*`/locations/`*`}:fetchVerificationOptions_
    
> Where `*`'s should be replaced with the corresponding id for the preceding field. eg: accounts/{account_id}/locations/{location_id}

> The exact string, accounts/{account_id}/locations/{location_id}, can be found in the name of the returned `googleLocation` object in the response listed in the __googleLocations.search.md__ document

###### Parameters
- name:
    > The string of the format: accounts/{account_id}/locations/{location_id}

    > This is returned in the response from the __googleLocations.search.md__ doc under `name`

### *Request Body Content:*

###### JSON Representation:
```
{
  "languageCode": string
}
```
###### Value Descriptions:
- `languageCode`:
    > The BCP 47 language code that is also sent in in a PostalAddress object (*Listed in the Accounts.Locations.Outline.md doc*)

### *Response Body Content:*
```
{
  "options": [
    {
      object(VerificationOption)
    }
  ]
}
```
*Each VerificationOption Object will take __one__ of the following forms:*
```
{
    "verificationMethod": enum(VerificationMethod), //Defined Below
    "phoneData": {
        object(PhoneVerificationData) //Defined Below
    }
}

{
    "verificationMethod": enum(VerificationMethod), //Defined Below
    "addressData": {
        object(AddressVerificationData)  //Defined Below
    }
}

{
    "verificationMethod": enum(VerificationMethod), //Defined Below
    "emailData": {
        object(EmailVerificationData) //Defined Below
    }
}
```
###### Definitions and Explainations
 - `verificationMethod` 
    > Defines how the location will be verified
    - VerificationMethod enum
       > An enum stating the type of verification process that can be/is being used

        >###### Types
        > - ADDRESS : Send a postcard with a verification PIN to a specific mailing address. The PIN is used to complete verification with Google.
        > - EMAIL : Send an email with a verification PIN to a specific email address. The PIN is used to complete verification with Google.
        > - PHONE_CALL : Make a phone call with a verification PIN to a specific phone number. The PIN is used to complete verification with Google.
        > - SMS : Send an SMS with a verification PIN to a specific phone number. The PIN is used to complete verification with Google.
        > - AUTO : Verify the location without additional user action. This option may not be available for all locations. (Maybe google has a way of just knowing..?)
        > - VERIFICATION_METHOD_UNSPECIFIED : Default value, will result in errors.

- `phoneData`
    > Appears if `verificationMethod` is `SMS` or `PHONE_CALL`

    > __JSON Representation__
    >```
    >{
    >   "phoneNumber": string
    >}
    >```
    >_Definitions_
    > - phoneNumber - The phone number that the verification pin will be sent/relayed to 

- `addressData`
    > Appears if `verificationMethod` is `MAIL`

    > __JSON Representation__
    >```
    >{
    >   "businessName": string,
    >   "address": {
    >       object(PostalAddress)       //Defined in Accounts.Locations.Outline.md doc
    >   }
    >}
    >```
    >_Definitions_
    > - businessName - The name of the business being verified
    > - address - Address that the post card would be sent to 

- `emailData`
    > Appears if `verificationMethod` is `EMAIL`

    > __JSON Representation__
    >```
    >{
    >   "domainName": string,
    >   "userName": string,
    >   "isUserNameEditable": boolean
    >}
    >```
    >_Definitions_
    > - domainName - The domain name of the email address, eg: `gmail.com` or `thrivehive.com`
    > - userName - The user name of the email address, eg: `userperson` from `userperson@gmail.com`
    > - isUserNameEditable - Whether or not the client is allowed to change the username of the email provided
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMTIwMTU5MDhdfQ==
-->
