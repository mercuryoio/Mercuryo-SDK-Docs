*Предварительно убедитесь, что вы [авторизованы](SignIn)*

# Кошелек

Для работы с кошельком вызовите следущий метод:


```kotlin
val mercuryo = Mercuryo.create(...)
val wallet = mercuryo.wallet
```

## Доступные кошельки

```kotlin
wallet.getWallets(): List<Wallet>
```

## Получение адреса

```kotlin 
wallet.getWalletsAddress(crypto: String): String
```

## Получение транзакций

```kotlin
wallet.getTransactions(type: TransactionType?, limit: Int, offset: Int, currency: String?): List<Transaction> 
```

Метод предоставляет поля для фильтрации:
* `type` - [`TransactionType`](http://gitlab.4taps.me/yablokoff/mercuryo-sdk-common/wikis/%D0%9C%D0%BE%D0%B4%D0%B5%D0%BB%D0%B8#transactiontype), для `type == null`, возвращаются все доступные типы.
* `limit` - максимальное количество запрашиваемых транзакций, дефолтное значение 20.
* `offset` - смещение для начала списка.
* `currency` - фильтрация по криптовалюте, доступные валюты (`BTC`,`ETH`,`BAT`,`USDT`,`ALGO`,`TRX`,`OKB`,`BCH`,`DAI`), для `currency == null`, возвращаются для всех валют.
***
