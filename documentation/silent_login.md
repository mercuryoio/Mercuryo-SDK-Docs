## Server-to-server communication

Below you can find URLs and endpoints for server-to-server silent login and silent sign up operations.

## Silent login

```
POST /sdk-partner/login

Headers:
Sdk-Partner-Token (String)
```

Parameters:

| Field        | Type           | Description  |
| ------------- |:-------------:| -----:|
| phone      | String | User phone number |


## Silent sign up with full flow

```
POST /sdk-partner/sign-up

Headers:
Sdk-Partner-Token (String)
```

Parameters:

| Field        | Type           | Description  |
| ------------- |:-------------:| :-----|
| phone      | String | User phone number |
| accept      | Boolean | Whether user has accepted terms and conditions |
| country_code      | String | User's 2-letter country code (e.g. 'US') |
| first_name      | String | User's first name |
| last_name      | String | User's last name |
| birthday      | String | User's birthday, format '2000-01-01' |
| email      | String | User's email |
| share_token      | String | SumSub's share token |
| document      | Array | User's documents |
|     type      | String | User's document type (eq passport, id_card, driver_license) |
|     files      | String | User's document files. document.files must contain an array with filename as key and file content as value. For current document type requirements for list of files differs. id_card. Count of files must be 3. File names must be 'face.', 'side-1.', 'side-2.'; passport. Count of files must be 2. File names must be 'face.', 'side-1.'; driver_license. Count of files must be 3. File names must be 'face.', 'side-1.', 'side-2.'. Extensions in file names must correspond .jpg, .png. |