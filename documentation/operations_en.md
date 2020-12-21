## Available operations

- [Buying process](#buying-crypto) 
  - [Getting token for buying](#getting-token-for-buying)
  - [Buying](#buying)
  - [Getting rate for buying](#getting-rate-for-buying)
  - [Confirmation of operation](#confirmation-of-operation)
- [Selling process](#selling-process)
  - [Getting token for selling](#getting-token-for-selling)
  - [Selling](#selling)
  - [Getting rate for buying](#getting-rate-for-buying)
- [Withdrawal to another wallet](#withdrawal-to-another-wallet)
  - [`Currency converter`](#currency-converter)
  - [`Комиссии за перевод`](#комиссия-за-перевод)
  - [`Совершение перевода`](#совершение-перевода)
  - [`Подтверждение перевода`](#подтверждение-перевода)
  
# Buying crypto

`Buy` object needs to be obtained first to start the process of buying:

```kotlin
val mercuryo: Mercuryo = Mercuryo.create(...)  
val buy: Buy = mercuryo.operations.buy
```

## Getting token for buying

Before buying, you need to get a unique token designated to this specific operation, for this you can use the `.convert` method:


```kotlin
buy.convert(fromCurrency: String, toCurrency: String, amount: String) : ConverterResult
```

## Buying

After you obtained a [buying token](#getting-token-for-buying) you can call buy method passing parameters of operation.

```kotlin
buy.commit(cardId: String, cvv: String, buyToken: String, redirectUrl: String): TransactionStatus
```

| Parameter   | Description                                                                         |
| ----------- | ----------------------------------------------------------------------------------- |
| cardId      | ID of card in Mercuryo                                                              |
| cvv         | CVV code of card                                                                    |
| buyToken    | Buying token [`buy.convert(...)`](#getting-token-for-buying)                        |
| redirectUrl | URL where user will be redirected after operation. Example: http://my.mercuryo.io/orders?invoice={invoice_id}                          |

## Confirmation of operation

To finalize an operation user may need to confirm ownership of bank account by providing a descriptor sent as a part of transaction. 


```kotlin
buy.verifyDescriptor(transactionId: String, code: String): TransactionStatus
```


| Parameter     | Description                                                                         |
| ------------- | ----------------------------------------------------------------------------------- |
| transactionId | ID of transaction obtained after [`buy.commit(...)`](#buying)                       |
| code          | Descriptor code                                                                     |

## Getting rate for buying

User may want to know the rate of fiat-crypto conversion which may be obtained using the following method:


```kotlin
buy.rate(fromCurrency: String, toCurrency: String): Rate
```

# Selling process

`Sell` object needs to be obtained first to start the process of buying:

```kotlin
val mercuryo: Mercuryo = Mercuryo.create(...)  
val sell: Sell = mercuryo.operations.sell
```

## Getting token for selling

Before selling, you need to get a unique token designated to this specific operation, for this you can use the `.convert` method:


```kotlin
sell.convert(fromCurrency: String, toCurrency: String, amount: String) : ConverterResult
```

## Selling

Для совершения покупки необходимо [сформировать токен](#формирование-токена-для-продажи) и вызвать метод.

```kotlin
sell.commit(cardId: String, sellToken: String): TransactionStatus
```

| Parameter | Description                                                                          |
| --------- | ------------------------------------------------------------------------------------ |
| cardId    | ID of card in Mercuryo                                                               |
| sellToken | Токен сформированный методом [`sell.convert(...)`](#формирование-токена-для-продажи) |

## Получение курса для продажи

Курс включает в себя комиссию для продажи.

```kotlin
sell.rate(fromCurrency: String, toCurrency: String): Rate
```

# Withdrawal to another wallet

`Withdraw` object needs to be obtained first to start the process of buying:

```kotlin
val mercuryo: Mercuryo = Mercuryo.create(...)  
val withdraw: Withdraw = mercuryo.operations.withdraw
```

## Currency converter 

Before sending crypto it may be beneficial for user to know how amount converts to fiat or vice versa. Mercuryo SDK provides a method for that allowing to understand transaction better.


```kotlin
withdraw.convert(fromCurrency: String, toCurrency: String, amount: String) : ConverterResult
```

## Комиссия за перевод

Перед совершением превода необходимо получить комиссию для перевода. При отсутвии комиссии метод выбросит ошибку `CurrencyNotSupportFeeException`.

```kotlin
withdraw.getEstimateFee(currency: String, fiatCurrency: String, address: String, amount: String): EstimateWithdrawFee
```


## Совершение перевода

```kotlin
withdraw.commit(currency: String, address: String, amount: String, estimateId: String?): VerifyMetaData
```

| Поле       | Описание                                                                                                              |
| ---------- | --------------------------------------------------------------------------------------------------------------------- |
| currency   | Криптовалюта                                                                                                          |
| address    | Адресс кошелька для перевода                                                                                          |
| amount     | Сумма для перевода в крипте                                                                                           |
| estimateId | Идентификатор комиссии выбранной пользователем, смотреть метод      [`withdraw.getEstimateFee`](#комиссия-за-перевод) |

## Подтверждени перевода

Для завершения необходимо подтвердить перевод.


```kotlin
withdraw.verify(next: VerifyMetaData.NextStep, key: String, code: String): TransactionStatus
```


