# Java + Spring Boot

De back-end wordt ontwikkeld in Java en maakt gebruik van Spring Boot. Met Spring is het erg makkelijk om een REST API op te zetten en alle routing automatisch af te laten handelen. Op het moment dat de applicatie wordt uitgevoerd roepen wij de methode SpringApplication.run aan. Daarna handelt Spring Boot de rest af, zoals het wachten op http requests, deze doorvoeren naar de juiste locaties, en ook de responses op deze requests juist terug sturen.

Wij configureren zelf een zogenaamde 'Controller' class. Deze class geven wij een bepaalde route mee, waardoor de controller op deze URI bereikbaar is. In de controller kunnen wij dan functies definiëren die reageren op bepaalde http requests.

Hieronder een voorbeeld van één van onze controllers:

```java
package io.playlistify.api.Controllers;

import io.playlistify.api.Authorization.AuthCodeRequestDto;
import io.playlistify.api.Authorization.SpotifyApiAuthenticator;
import io.playlistify.api.Authorization.TokenDto;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import java.net.URI;

@RestController
@RequestMapping("/auth")
public class AuthController {

    @GetMapping("urigenerator")
    public ResponseEntity<URI> GetSpotifyAuthCodeURI() {
        URI authCodeURI = SpotifyApiAuthenticator.generateAuthCodeUri();
        return ResponseEntity.ok(authCodeURI);
    }

    @PostMapping("authcodegrant")
    public ResponseEntity<?> AuthCodeRequest(@RequestBody() AuthCodeRequestDto authCodeRequestDto) {
        TokenDto tokens = SpotifyApiAuthenticator.getAccessSetRefreshToken(authCodeRequestDto.getAuthCode());

        return ResponseEntity.ok(tokens);


    }
}

```

Deze controller wordt gedraaid op de uri '/auth'. Hier zijn dan twee andere routes op te vinden:&#x20;

* '/urigenerator' kan een GET request op uitgevoerd worden.
* '/authcodegrant' kan een POST request op uitgevoerd worden.

De gedefinieërde routes zijn dus als volgt

* GET /auth/urigenerator
* POST /auth/authcodegrant

Het is mogelijk om een GET en POST op de zelfde URI te definiëren. Duplicate methoden gaat niet.
