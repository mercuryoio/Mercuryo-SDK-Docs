## Авторизация 

Для авторизации SDK получить `SessionManager`


```kotlin
val mercuryo: Mercuryo = Mercuryo.create(...)  
val sessionManager: SessionManager = mercuryo.session
```

## Обновления токена

```kotlin
sessionManager.updateToken(token: String)
```