# C4 Model

## C1 niveau

Op het C1 niveau kan men de twee systemen zien waar onze gebruiker mee gaat interacteren.  Links staat de software die wij gaan bouwen; Playlistify.me. Rechts staat Spotify, het systeem waar onze software en de gebruiker van onze software veel mee zal interacteren.

<figure><img src=".gitbook/assets/Sioux C4 Project - Main project C1 (Latest).png" alt=""><figcaption></figcaption></figure>



## C2 niveau

Op het C2 niveau zoomen we in op het Playlistify.me systeem. Hierin kan men de verschillende apps waaruit ons systeem bestaat zien: een web interface, een back-end API (gemaakt met spring boot), en een database.

<figure><img src=".gitbook/assets/Sioux C4 Project - Diagram 1 (Latest) (1).png" alt=""><figcaption></figcaption></figure>

## C3 niveau

Op het derde niveau zoomen we nog verder in, deze keer op de back-end API applicatie. Deze app bestaat voornamelijk uit twee grote onderdelen: één component welke gebruikers authenticatie afhandelt, en één component welke het daadwerkelijke mergen van afspeellijsten uitvoert. Beide componenten moeten zwaar met het Spotify systeem interacteren, wat gebeurt doormiddel van API calls over het HTTP protocol.

<figure><img src=".gitbook/assets/Sioux C4 Project - Diagram 1 (Latest).png" alt="" width="563"><figcaption></figcaption></figure>
