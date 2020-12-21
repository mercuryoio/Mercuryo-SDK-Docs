## Карты

- [Список карт](#список-карт)
- [Привязка карты](#привязка-карты)
- [Удаление](#удаление)

Для работы с картами необходимо получить `CardManager`

```kotlin
val mercuryo: Mercuryo = Mercuryo.create(...)  
val cardManager: CardManager = mercuryo.card
```

## Список карт

Для получение списка привязанных карт, вызовите метод:

```kotlin
cardManager.getCards(limit: Int, offset: Int): List<Card>
```

## Привязка карты

```kotlin
cardManager.bindCard(holderName: String, number: String, cvv: String, expirationMonth: String, expirationYear: String, redirectUrl: String): BindCard
```

| Поле            | Описание                                                           |
| --------------- | ------------------------------------------------------------------ |
| holderName      | Имя владельца карты                                                |
| number          | Номер карты                                                        |
| cvv             | Код безопасности карты                                             |
| expirationMonth | Месяц окончания действия карты                                     |
| expirationYear  | Год окончания действия карты                                       |
| redirectUrl     | Example: https://my.mercuryo.io/loader.html?cardid3ds={binding_id} |

## Удаление

Чтобы удалить карту, необходимо вызвать метод `deleteCard`, передав идентификатор карты.

```kotlin
cardManager.deleteCard(cardId: String) 
```