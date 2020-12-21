## Операции

- [Покупка](#покупкакрипты) 
  - [Формирование токена для покупки](#формирование-токена-для-покупки)
  - [Совершение покупки](#совершение-покупки)
  - [Получение курса для покупки](#получение-курса-для-покупки)
  - [Завершение покупки](#дескриптор-покупка)
- [Продажа](#продажа)
  - [Формирование токена для продажи](#формирование-токена-для-продажи)
  - [Совершение продажи](#совершение-продажи)
  - [Получение курса для продажи](#получение-курса-для-продажи)
- [Перевод на другой кошелек](#перевод-на-другой-кошелек)
  - [`Конвертер`](#конвертер)
  - [`Комиссии за перевод`](#комиссия-за-перевод)
  - [`Совершение перевода`](#совершение-перевода)
  - [`Подтверждение перевода`](#подтверждение-перевода)
  
# Покупка крипты

Для создания покупки необходимо получить объект `Buy`:

```kotlin
val mercuryo: Mercuryo = Mercuryo.create(...)  
val buy: Buy = mercuryo.operations.buy
```

## Формирование токена для покупки

Перед покупкой необходимо получить токен, для этого вы можете воспользоваться методом `.convert`


```kotlin
buy.convert(fromCurrency: String, toCurrency: String, amount: String) : ConverterResult
```

## Совершение покупки

Для совершения покупки необходимо [сформировать токен](#формирование-токена-для-покупки) и вызвать метод

```kotlin
buy.commit(cardId: String, cvv: String, buyToken: String, redirectUrl: String): TransactionStatus
```

| Поле        | Описание                                                                            |
| ----------- | ----------------------------------------------------------------------------------- |
| cardId      | Идентификатор карты в система Меркурио                                              |
| cvv         | Код безопасности карты                                                              |
| buyToken    | Токен сформированный методом [`buy.convert(...)`](#формирование-токена-для-покупки) |
| redirectUrl | Example: http://my.mercuryo.io/orders?invoice={invoice_id}                          |

## Завершение покупки

Для завершения покупки необходимо подвердить дескриптор, который присылает банк.


```kotlin
buy.verifyDescriptor(transactionId: String, code: String): TransactionStatus
```


| Поле          | Описание                                                                            |
| ------------- | ----------------------------------------------------------------------------------- |
| transactionId | Идентификатор транзакции полученый методом [`buy.commit(...)`](#совершение-покупки) |
| code          | Дескриптор                                                                          |

## Получение курса для покупки

Курс включает в себя комиссию для покупки


```kotlin
buy.rate(fromCurrency: String, toCurrency: String): Rate
```

# Продажа крипты 

Для продажи крипты необходимо получить объект `Sell`:

```kotlin
val mercuryo: Mercuryo = Mercuryo.create(...)  
val sell: Sell = mercuryo.operations.sell
```

## Формирование токена для продажи

Перед продажей необходимо получить токен, вызовите метод `.convert`.


```kotlin
sell.convert(fromCurrency: String, toCurrency: String, amount: String) : ConverterResult
```

## Совершение продажи

Для совершения покупки необходимо [сформировать токен](#формирование-токена-для-продажи) и вызвать метод.

```kotlin
sell.commit(cardId: String, sellToken: String): TransactionStatus
```

| Поле      | Описание                                                                             |
| --------- | ------------------------------------------------------------------------------------ |
| cardId    | Идентификатор карты в система Меркурио                                               |
| sellToken | Токен сформированный методом [`sell.convert(...)`](#формирование-токена-для-продажи) |

## Получение курса для продажи

Курс включает в себя комиссию для продажи.

```kotlin
sell.rate(fromCurrency: String, toCurrency: String): Rate
```

# Перевод на другой кошелек

Для создания покупки необходимо получить объект `Withdraw`:

```kotlin
val mercuryo: Mercuryo = Mercuryo.create(...)  
val withdraw: Withdraw = mercuryo.operations.withdraw
```

## Конвертор 

Перед отправкой крипты сервис Меркурио может сконвертировать для вас фиат в крипту или наоборот, для лучшего понимания сделки.


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


