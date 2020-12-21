## Authentication 

SDK implies that your company is listed as partner and user already registered in Mercuryo on behalf of your company.

To authenticate user SDK must work with `SessionManager`. Main function is `updateToken` which should get token string as a parameter. It's up to your application to securely obtain token from the backend.


```kotlin
val mercuryo: Mercuryo = Mercuryo.create(...)  
val sessionManager: SessionManager = mercuryo.session
```

## Token update

```kotlin
sessionManager.updateToken(token: String)
```