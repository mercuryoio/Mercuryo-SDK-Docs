
- [Models](#models)
  - [`VerifyMetaData`](#verifymetadata)
  - [`VerifyMetaData.NextStep`](#verifymetadatanextstep)
  - [`Wallet`](#wallet)
  - [`MercuryoUser`](#mercuryouser)
  - [`SanctionStatusType`](#sanctionstatustype)
  - [`VerificationStatusType`](#verificationstatustype)
  - [`DocumentDetails`](#documentdetails)
    - [`DocumentDetails.Error`](#documentdetailserror)
  - [`Card`](#card)
  - [`Bank`](#bank)
    - [`Bank.Color`](#bankcolor)
  - [`ConverterResult`](#converterresult)
  - [`Rate`](#rate)
  - [`TransactionStatus`](#transactionstatus)
  - [`Redirect`](#redirect)
    - [`Redirect.FormItem`](#redirectformitem)
  - [`TransactionType`](#transactiontype)
  - [`EstimateWithdrawFee`](#estimatewithdrawfee)
  - [`Fee`](#fee)
  - [`EstimatedTime`](#estimatedtime)
  - [`Limit`](#limit)
  - [`LimitPair`](#limitpair)

# Models

## `VerifyMetaData`

The model containing information about the next step to confirm actions.


| Name       | Type                    | Description                                             |
| ---------- | ----------------------- | ------------------------------------------------------- |
| key        | String                  | Public key for verification                             |
| codeLength | Int                     | Number of characters in the code                        |
| step       | [`NextStep`](#nextstep) | Model indicating the Type of verification               |
| timeout    | Int                     | The period between requesting a new confirmation code   |
| recipient  | String?                 | Recipient of confirmation code                          |


## `VerifyMetaData.NextStep` 

Model pointing to the next step of the flow.


| Type              | Description                           |
| ----------------- | ------------------------------------- |
| PHONE             | Code sent via text message            |
| EMAIL             | Code sent via email                   |
| SET_PASSWORD      | Need to set password                  |
| SET_EMAIL         | Need to set email                     |
| SET_PERSONAL_DATA | Need to add personal data             |


## `Wallet`

Model containing data about the wallet balance.

| Name         | Type   | Description                    |
| ------------ | ------ | ------------------------------ |
| currency     | String | Name of cryptocurrency         | 
| balance      | Double | Balance in crypto              |
| fiatCurrency | String | Name of fiat currency          |
| fiatBalance  | Double | Balance in fiat                |

## `MercuryoUser`

Model containing info about the user.

| Name               | Type                                                 | Description                                                           |
| ------------------ | --------------------------------------------------- | --------------------------------------------------------------------- |
| uuid               | String                                              | Unique identifier of the user                                           |
| firstName          | String                                              | First name of the user                                                       |
| lastName           | String                                              | Last name of the user                                                  |
| fullName           | String                                              | Full name of the user                                               |
| birthday           | String                                              | Date of birth, format is  dd-MM-yyyy                         |
| email              | String                                              | Email of the user                                        |
| referral           | String                                              | Referral code of the user                                           |
| countryCode        | String                                              | Country code of the user                                               |
| phone              | String                                              | Phone of the user                                           |
| sendPromo          | Boolean                                             | Consent to receive information about promotions                            |
| fiatCurrency       | String                                              | Saved fiat currency of the user                                                   |
| sanctionStatus     | [`SanctionStatusType`](#sanctionstatustype)         | Sanctions status of the user                                         |
| verificationStatus | [`VerificationStatusType`](#verificationstatustype) | Identification status of the user                                     |
| documentDetails    | [`DocumentDetails`](#documentdetails)               | Information about provided documents for user identification |

## `SanctionStatusType`

Sanctions status of the user. Choices are `INCOMPLETE`, `UNDER_REVIEW`, `COMPLETED`, `FAILED`.

## `VerificationStatusType`

Identification status of the user. Choices are `INCOMPLETE`, `UNDER_REVIEW`, `COMPLETED`, `FAILED`.

## `DocumentDetails`

Model containing data regarding possible errors in submitted verification documents.

| Name        | Type                                      | Description                               |
| ----------- | ---------------------------------------- | ------------------------------------------ |
| checkEnable | Boolean                                  | Ability to pass verification again         |
| errors      | List\<[`Error`](#documentdetails.error)> | List of verification errors                |
### `DocumentDetails.Error`

| Name         | Typ    | Description                 |
| ------------ | ------ | -------------------------   |
| documentType | String | Document caused the failure |
| message      | String | Description of the error    |
 
## `Card`

Model containing data about card.

| Name            | Type            | Description                   |
| --------------- | --------------- | ----------------------------- |
| id              | String          | Card ID                       |
| createdAt       | Long            | Timestamp of creation         |
| paymentSystem   | String          | Payment system                |
| number          | String          | Last 4 digits of card number  |
| expirationMonth | String          | Month of expiration date      |
| expirationYear  | String          | Year of expiration date       |
| bank            | [`Bank`](#bank) | Bank info                     |

## `Bank`

Model containing data about bank.

| Name     | Type                   | Description        |
| -------- | --------------------- | ------------------ |
| title    | String,               | Name of the bank   |
| icon     | String,               | URL of bank logo   |
| color    | [`Color`](#bankcolor) |

### `Bank.Color`

| Name       | Type    | Description                          |
| ---------- | ------ | ------------------------------------- |
| background | String | Background color of bank card         |
| foreground | String | Color of text and info of bank card   |

## `ConverterResult`

Model containing buying token, selling token and additional info about the state of converter.

| Name         | Type    | Description                                                                                      |
| ------------ | ------ | ------------------------------------------------------------------------------------------------ |
| token        | String | Buying or selling token |
| currency     | String | Crypto currency                                                                                     |
| amount       | String | Amount of crypto                                                                               |
| fiatCurrency | String | Fiat currency                                                                                    |
| fiatAmount   | String | Amount of fiat                                                      |

## `Rate`

Model containing data about exchange rates.

| Name     | Type    | Description                    |
| -------- | ------ | ------------------------------- |
| from     | String | Source currency                 |
| to       | String | Destination currency            |
| type     | String | Type of operation `buy`, `sell` |
| rate     | String | Exchange rate `to`/`from`       |

## `TransactionStatus`

Model containing data about the transaction such as ID and status. Intermediate status states with one of the optional fields are possible, for example, [`Redirect`](#redirect) may come for a purchase indicating the need to go through 3ds, or` isVerifyDescription` indicating the need to enter a descriptor to complete the transaction.


| Name                | Type                      | Description                                                              |
| ------------------- | ------------------------ | ------------------------------------------------------------------------ |
| redirect            | [`Redirect?`](#redirect) | URL info for transaction confirmation                |
| id                  | String                   | Mercuryo ID of transction                            |
| status              | String                   | Status of transaction                                                        |
| isVerifyDescription | Boolean                  | Flag showing whether user needs to enter descriptor on the next step |

## `Redirect`

Model containing data about the need to be redirected to the specified URL.

| Name        | Type             | Description                                       |
| ----------- | --------------- | -------------------------------------------------- |
| form        | List\<FormItem> | List of additional data items for URL composing    |
| requestType | String          | Type of request `GET` or `POST`                    |
| uriTemplate | String          | Address                                            |

### `Redirect.FormItem`

Model containing data about additional parameters for URL.

| Name     | Type    | Description        |
| -------- | ------ | ------------------- |
| key      | String | Key                 |
| template | String | Info about the key  |

## `TransactionType`

 | Type     | Description                                 |
 | -------- | ------------------------------------------- |
 | DEPOSIT  | Deposit of crypto from another wallet       |
 | BUY      | Buying crypto with card                     |
 | SELL     | Selling crypto to card                      |
 | WITHDRAW | Withdrawal of crypto to another wallet      |
 | REFERRAL | Top-up of crypto using referral program     |

## `EstimateWithdrawFee`

Model containing the list of available transaction Fees.

| Name           | Type                 | Description              |
| -------------- | ------------------- | ------------------------- |
| cryptoCurrency | String              | Crypto currency           |
| fiatCurrency   | String              | Fiat currency             |
| fees           | List<[`Fee`](#fee)> | List of available fees    |

## `Fee`

Model containing data about fees.

| Name          | Type          | Description                                                  |
| ------------- | ------------- | ------------------------------------------------------------ |
| id            | String        | ID of the fee                                                |
| level         | String        | Possible types of transaction, choices are `slow`, `medium`, `fast` |
| fee           | String        | Fee in crypto                                                |
| fiatAmount    | String        | Fee in fiat                                                  |
| isPaidByUser  | Boolean       | Shows whether fee is deducted from user's balance            |
| estimatedTime | EstimatedTime | Expected time of transaction                                 |

## `EstimatedTime`

Model containing data about estimated time of transaction.

| Name     | Type | Description                 |
| -------- | ---- | --------------------------- |
| max      | Int? | Max transaction time        |
| min      | Int? | Min transaction time        |

## `Limit`

Model containting data about the user's limits.

| Name           | Type   | Description                                                  |
| -------------- | ------ | ------------------------------------------------------------ |
| initDay        | Double | Daily limit of the user                                      | 
| day            | Double | Balance of daily limit                                       |
| initWeek       | Double | Weekly limit of the user                                     |
| week           | Double | Balance of weekly limit                                      |
| initMonth      | Double | Monthly limit of the user                                    |
| month          | Double | Balance of monthly limit                                     |
| operationMin   | Double | System-wide minimum transaction amount for any user          |
| operationMax   | Double | System-wide maximum transaction amount for any user          |

## `LimitPair`

Pair of limits for fiat and crypto currencies.


| Name        | Type              | Description              |
| ----------- | ----------------- | ------------------------ |
| fiatLimit   | [`Limit`](#limit) | Limit for fiat           |
| cryptoLimit | [`Limit`](#limit) | Limit for crypto         |