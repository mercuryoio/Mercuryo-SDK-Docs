
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

Модель содержит информацию о проблемах предоставленных документов. 
| Name        | Type                                      | Description                                |
| ----------- | ---------------------------------------- | ------------------------------------------ |
| checkEnable | Boolean                                  | Возможность проходить верификацию          |
| errors      | List\<[`Error`](#documentdetails.error)> | Список ошибок при верификации пользователя |
### `DocumentDetails.Error`

| Name         | Type    | Description        |
| ------------ | ------ | ------------------ |
| documentType | String | Документ с ошибкой |
| message      | String | Descriptionибки    |
 
## `Card`

Модель содержит информацию о карте.

| Name            | Type             | Description                          |
| --------------- | --------------- | ------------------------------------ |
| id              | String          | Уникальный ключ карты                |
| createdAt       | Long            | Время добавления карты               |
| paymentSystem   | String          | Информации о платежной системе карты |
| number          | String          | Последние четыре цифры номера карты  |
| expirationMonth | String          | Месяц окончания действия карты       |
| expirationYear  | String          | Год окончания действия карты         |
| bank            | [`Bank`](#bank) | Информация о банке                   |

## `Bank`

Model containing data about bank.

| Name     | Type                   | Description        |
| -------- | --------------------- | ------------------ |
| title    | String,               | Name of the bank   |
| icon     | String,               | URL of bank logo   |
| color    | [`Color`](#bankcolor) |

### `Bank.Color`

| Name       | Type    | Description                      |
| ---------- | ------ | -------------------------------- |
| background | String | Цвет заднего фона карточки банка |
| foreground | String | Цвет информации о карте          |

## `ConverterResult`

Модель содержит токен для совершение покупки, продажи и дополнительную информацию о состоянии конвертора.

| Name         | Type    | Description                                                                                      |
| ------------ | ------ | ------------------------------------------------------------------------------------------------ |
| token        | String | Ключ для пары значений конвертора, необходимый для совершения транзакции с заданными параметрами |
| currency     | String | Криптовалюта                                                                                     |
| amount       | String | Сумма криптовалюты                                                                               |
| fiatCurrency | String | Фиатная валюта                                                                                   |
| fiatAmount   | String | Сумма для фиатной валюты                                                                         |

## `Rate`

Модель содержит информацию о курсе выбраной валюты.

| Name     | Type    | Description                                      |
| -------- | ------ | ------------------------------------------------ |
| from     | String | Валюта относительно который был сформирован курс |
| to       | String | Валюта в которую был сформирован курс            |
| type     | String | Type операции `buy`, `sell`                       |
| rate     | String | Курс для валюты `to`                             |

## `TransactionStatus`

Модель содержит информацию о транзакции, такие как идентификатор и статус. Возможны промежуточные состояния статуса с одним из опциональных полей, например для покупки может придти [`Redirect`](#redirect) указывающий на необходимость пройти 3ds, или `isVerifyDescription` указывающий о необходимости ввода дескриптора, для завершения транзакции.


| Name                | Type                      | Description                                                              |
| ------------------- | ------------------------ | ------------------------------------------------------------------------ |
| redirect            | [`Redirect?`](#redirect) | Информацию о формирование Url для подтверждения транзакции               |
| id                  | String                   | Идентификатор транзакции в системе Меркурио                              |
| status              | String                   | Статус транзакции                                                        |
| isVerifyDescription | Boolean                  | Флаг указывающий на необходимость подтвердить дескриптор следующим шагом |

## `Redirect`

Модель указывает на необходимость перехода по URL указанном в объекте

| Name        | Type             | Description                                           |
| ----------- | --------------- | ----------------------------------------------------- |
| form        | List\<FormItem> | Список дополнительной информации для формирования URL |
| requestType | String          | Type запроса `GET`, `POST`                             |
| uriTemplate | String          | Адрес                                                 |

### `Redirect.FormItem`

Модель содержит дополнительную информацию для формирования адреса 

| Name     | Type    | Description         |
| -------- | ------ | ------------------- |
| key      | String | Ключ                |
| template | String | Информация по ключу |

## `TransactionType`
 | Type      | Description                                 |
 | -------- | ------------------------------------------- |
 | DEPOSIT  | Транзакции поплнения с другого кошелька     |
 | BUY      | Покупка припты через карту                  |
 | SELL     | Продажа крипты через карту                  |
 | WITHDRAW | Перевод крипты на другой кошелек            |
 | REFERRAL | Пополнение кошелька по реферальной програме |

## `EstimateWithdrawFee`

Модель содержит список доступных комиссий.

| Name           | Type                 | Description               |
| -------------- | ------------------- | ------------------------- |
| cryptoCurrency | String              | Name     криптовалюты     |
| fiatCurrency   | String              | Name     фиатной валюты   |
| fees           | List<[`Fee`](#fee)> | Список доступных комиссий |

## `Fee`

Модель содержит информацию о комиссии.

| Name          | Type           | Description                                                  |
| ------------- | ------------- | ------------------------------------------------------------ |
| id            | String        | Идентификатор комиссии                                       |
| level         | String        | Скорость транзакции, возможные Typeы `slow`, `medium`, `fast` |
| fee           | String        | Комиссия в криптоввалюте                                     |
| fiatAmount    | String        | Комиссия в фиате                                             |
| isPaidByUser  | Boolean       | Указывает будет ли комиссия снята с пользователя             |
| estimatedTime | EstimatedTime | Ориентировачное время выполнения транзакции                  |

## `EstimatedTime`

Модель содержит информацию о времени совершения транзакции.


| Name     | Type  | Description                 |
| -------- | ---- | --------------------------- |
| max      | Int? | Максимальное время перевода |
| min      | Int? | Минимальное время перевода  |

## `Limit`

Model containting info about the user's limits.

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
| cryptoLimit | [`Limit`](#limit) | Limit for crypti         |