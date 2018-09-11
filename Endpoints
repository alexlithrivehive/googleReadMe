### Google.Locations.Endpoints.Flow.md
#### *A general outline for interacting with these endpoints*

#### Business Search Flow
1. Use googleLocations.search to see if the business is already on Google
    > Details found in *googleLocations.search.md*
    1. Obtain the following information (or as much as possible) from the merchant
        - locationName
        - primaryPhone
        - additionalPhones
        - address
        - primaryCategory
        - additionalCategories 
        - websiteUrl
        - regularHours 
        - serviceArea (Optional)
        - latlng (Optional)
    2. Parsing the given data into a the __*Location*__ structure (*found in Accounts.Locations.Outline.md*), and filling in the request structure listed in the *googleLocations.search.md* Doc, make a request to googleLocations.search
    3. The returned request, if successful, will have a list of *GoogleLocation* Objects
        - The list will be sorted so that the top-most object is the most likely business to match the search criteria, with decreasing accuracy as the list is descended
        - __IF the list is empty or the merchant's business is not included in the list__ the business has likely not yet been recorded/tracked by google, and will need to be created.
            - To create a new business location, follow the *Create New Business Flow* (Recommended that the `Location` object passed in during this search flow is used for the creation flow as well)
        - __OTHERWISE__ the business has been recorded by google. The business may or may not be claimed or verified.
            - To determine if the business has been claimed/is being claimed, follow the *List Current Verifications Flow* (Not generated yet)
            - To move forward with a new verification process for the selected location, follow the *Fetch Verifcation Options Flow*

2. Check the status of the location
    - 2a. Location is already on Google and claimed by a different user (outside of this SPIKE)
    - 2b. Location is on Google, but is not yet claimed (move to 3)
    - 2c. Location is not on Google (move to 3)
3. Use create endpoint to add a new listing (if 2b then the create should include the placeId of the existing location)
4. Use locations.fetchVerificationOptions endpoint to see all possible verification methods
5. Use locations.verify to specify the method selected by user
6. Use verifications.complete to submit the pin sent to user by Google


#### Create New Business Flow
*Use Accounts.Locations.Create endpoint to generate a new business*
 > *Complete documentation regarding this endpoint can be found in Accounts.Locations.Create.md Docs*

 1. Obtain the following information (As much as possible) from the merchant
    - Location Name
    - Primary Phone
    - Additional Phones
    - Address
    - Primary Business Category
    - Additional Categories
    - Website URL
    - Regular Hours
    - Service Area (Optional)
    - Latitude and Longitude (Optional)
2. Parse the given data into a `Location` Object, as described in the `Accounts.Locations.Outline.md` Docs (This data will be further referred to as `location`)
3. Ensure that the following data is available:
    - User's GMB Account Name (This will further be referred to as `accountID`
    - Generate a Unique UUID for the request that will be made (Must be 50 characters or fewer in length) (This will further be referred to as `requestID`)
4. `POST` the following statement with the data included
    > *https://mybusiness.googleapis.com/v4/{parent=accounts/{accountID}/locations?validateOnly=false&requestId={requestID}
    - The body of the POST should contain the `location` Object created earlier
5. The response, if successful, will contain an identical `Location` object to what was sent in, though this one *should* (assumption) contain data in the `name` component that contains a location ID.
6. With the new business created, and a location ID obtained, move on to the *Fetch Verification Options Flow*


#### Fetch Verification Options Flow
 > *Continues from the Create New Business Flow*

*Use Accounts.Locations.FetchVerificationOptions endpoint to determine what steps should be taken to verify a business location*
 > *Complete documentation regarding this endpoint can be found in Accounts.Locations.FetchVerificationOptions.md*

1. Ensure that the `name` object for a location has been obtained. (This object will be further referred to as `nameIdentifier`)
    > This can be obtained from a successful completion of either of the following flows, unless it has been obtained by some previous means (User sign in and location selection)
    >   - *Create New Business Flow*
    >   - *Business Search Flow*
2. Send a `POST` request to the following request, with the following parameters
    > *POST https://mybusiness.googleapis.com/v4/{name={`nameIdentifier`}}:fetchVerificationOptions*
    - The body of the post can contain a `languageCode` parameter. In most cases, we will use the English language code `en`. The body will look like so:
        ```
        {
            "languageCode":"en"
        }
        ```
3. If the request is successful, the response will contain a list of verification options for the business. The `options` object will contain a list of  some, if not all of the following verification objects.
    ```
    {
        "verificationMethod": SMS, // This could also be PHONE_CALL
        "phoneData": {
            "phoneNumber":"SomePhoneNumberProvidedInTheOriginalLocationSent"
        }
    }

    {
        "verificationMethod": ADDRESS,
        "addressData": {
            "businessName": string,
            "address": {
                object(PostalAddress)       //Defined in Accounts.Locations.Outline.md doc
            }  
        }
    }

    {
        "verificationMethod": EMAIL,
        "emailData": {
            "domainName": string,
            "userName": string,
            "isUserNameEditable": boolean   // Further explained in Accounts.locations.fetchVerificationOptions.md Doc
        }
    }

    {
        "verificationMethod": AUTO         
    }
    ```
4. If none of the verification options have the `verificationMethod` type of `VERIFICATION_METHOD_UNSPECIFIED`, then the option request was a success. Continuing with the received data and the `nameIdentifier` used in this flow, begin following the *Start Business Verification Flow*


#### Start Business Verification Flow
*Notify Google that the user is ready to begin a verification process*
 > *Complete documentation can be found in the Accounts.Location.Verify.md doc*

> *Continues from the __Fetch Verification Options Flow__*

- Revisiting the data recieved from the in the `options` object. There are 5 successful types of verification, with 3 possible sets of data.
    - AUTO
        > Automatically verifies the location once the verification request is sent during this flow. There will be no need for the user to verify a pin.
    - SMS, PHONE_CALL
        > Uses the user's phone number (provided when the location was created, and returned in the `phoneData` object) to contact the user and relay a pin number to be used for verification
    - EMAIL
        > Uses data from the user's email to relay a pin to the user. 
        - If the `isUserNameEditable` object (from the returned `emailData` object) is set to __false__, then the specific email provided in the data is the only one that can have the pin relayed to it. The email must be: {userName}@{domainName}.
        - If the `isUserNameEditable` object is set to __true__, then anyone with an email using the returned `domainName` can have the pin relayed to it. The email can be {anyPerson}@{domainName}
    - ADDRESS
        > Uses data from the Business' address to relay a pin to the user.
        - This sends a physical post card to the address provided in the `addressData` Object. The post card will have the verification pin written on it.

1. Using the information provided, and the data sent in the the previous flow, select a form of verification to use to have a pin conveyed to the user (for `AUTO`, no pin is used). Multiple verification types can be used, though only one request can be sent at a time.
2. Send a `POST` request to the following address using the `nameIdentifier` used previously:
    > *POST https://mybusiness.googleapis.com/v4/{name={nameIdentifier}:verify*
    - The request body should contain one of the following objects:
        - For AUTO:
            ```
            {
                "method": "AUTO",
                "languageCode": "en",
            }
            ```
        - For SMS, PHONE_CALL:
            ```
            {
                "method": "SMS",            // Could also be PHONE_CALL
                "languageCode": "en",
                "phoneInput": {
                    "phoneNumber":"{PhoneNumberSentFromGoogle}"
                }
            }
            ```
        - For EMAIL:
            ```
            {
                "method": "EMAIL",
                "languageCode": "en",
                "emailInput": {
                    "emailAddress": "{userName}@{domain}
                }
            }
            ```
        - For ADDRESS:
            ```
            {
                "method": "ADDRESS",
                "languageCode": "en",
                "addressInput": {
                    "mailerContactName": "{Person who should receive the postcard's name}"
                }
            }
            ```
3. The response from this request will take the following form:
    ```
    {
        "verification": {
            "name": "Accounts/{accountId}/Locations/{locationId}/Verifications/{verificationId}",
            "method": "AUTO",   //Or SMS, PHONE_CALL, EMAIL, ADDRESS
            "state": "PENDING",     //Or COMPLETED, FAILED
            "createTime": TimeOfVerificationRequest
        }
    }
    ```
    - In the case of a method of AUTO, state should be COMPLETED without any additional action. No further action will be needed once this has occurred.
    - For all other methods, state should return as PENDING for the initial request, and further action will be needed from the user.
    - From the `name` object, we receive a string that points directly to the specific request that has just been created. This will further be referred to as the `verificationName`. Using this information, move to the *Complete Verification Flow*


#### Complete Verification Flow
*Continued from Start Business Verification Flow*
 > *Complete documentation is available from Accounts.Locations.Verifications.Complete docs*

*__NOTE:__ This step can only be completed once the user has received a pin from Google to be used for verification*

1. Once the user has received a verification pin from Google, the following endpoint can have a `POST` request sent to it:
    > *POST https://mybusiness.googleapis.com/v4/{name={verificationName}:complete*
    > - Note that verificationName must match the verification request that is tied to the recieved pin. An EMAIL pin cannot complete an ADDRESS verification
    - The request body contains only the following object:
        ```
        {
            "pin":"123456"
        }
        ```

2. The response from the request, when successful, will contain the following `Verification` object:
    ```
    {
        "verification": {
            "name": "{verificationName}",
            "method": "SMS",   //Or PHONE_CALL, EMAIL, ADDRESS
            "state": "COMPLETED",
            "createTime": TimeOfVerificationRequest  //Not time of verification completion           
        }
    }
    ```

3. From here, the business location has been verified with the owner/manager/admin being the user






<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkxMjk3MTE0OV19
-->
