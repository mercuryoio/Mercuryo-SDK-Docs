## Cards

- [List of cards](#list-of-cards)
- [Adding card](#adding-card)
- [Removing card](#removing-card)

`CardManager` object needs to be obtained first to start working with cards:

```kotlin
val mercuryo: Mercuryo = Mercuryo.create(...)  
val cardManager: CardManager = mercuryo.card
```

## List of cards

To get a list of linked cards, call the method:

```kotlin
cardManager.getCards(limit: Int, offset: Int): List<Card>
```

![List of cards](img/cards.png "Cards")

## Adding card

```kotlin
cardManager.bindCard(holderName: String, number: String, cvv: String, expirationMonth: String, expirationYear: String, redirectUrl: String): BindCard
```

| Parameter       | Description                                                        |
| --------------- | ------------------------------------------------------------------ |
| holderName      | Cardholder name                                                    |
| number          | Number of card                                                     |
| cvv             | CVV of card                                                        |
| expirationMonth | Expiration month                                                   |
| expirationYear  | Expiration year                                                    |
| redirectUrl     | URL where user will be redirected to after operation. Example: http://my.mercuryo.io/orders?invoice={invoice_id} |

## Removing card

To delete a card call the `deleteCard` method passing the card identifier.

```kotlin
cardManager.deleteCard(cardId: String) 
```