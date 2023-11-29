---
description: Onze verbinding met de database
---

# Spring JPA + Hibernate & Flyway

Voor de persistentie van data maken wij gebruik van een MySQL database. Om verbinding te maken met de database maken wij gebruik van Spring JPA. Hiervoor configureren wij een database url, login gegevens voor een gebruiker, en een aantal configuratie opties voor Hibernate (de onderliggende ORM van Spring JPA).

{% code title="application.properties" %}
```properties
spring.datasource.url=${SPRING_DATASOURCE_URL}
spring.datasource.username=${SPRING_DATASOURCE_USERNAME}
spring.datasource.password=${SPRING_DATASOURCE_PASSWORD}
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.hibernate.naming.physical-strategy=org.hibernate.boot.model.naming.PhysicalNamingStrategyStandardImpl
spring.jpa.generate-ddl=true
spring.jpa.hibernate.ddl-auto=update
```
{% endcode %}

Daarna kunnen wij Entity classes gaan aanmaken en annoteren. De annotaties in deze classes laten Spring JPA weten hoe de relaties tussen bepaalde entiteiten is, en welke data structuur er precies nodig is bij bepaalde velden.

{% code title="Playlist.java" %}
```java
@Entity
@Data
public class Playlist {
    @Id
    @GeneratedValue(strategy = GenerationType.UUID)
    public String id;

    @Column(unique = true)
    public String spotify_uri;

    @ManyToMany()
    @JoinTable(
            name = "TrackInPlaylist",
            joinColumns = @JoinColumn(name = "Playlist_id"),
            inverseJoinColumns = @JoinColumn(name = "Track_id")
    )
    public Set<Track> tracks;
}
```
{% endcode %}

Nu is het nog belangrijk dat wij Spring JPA laten weten dat wij deze entiteit willen bijhouden in onze database. Hiervoor maken wij een interface aan welke zal acteren als onze 'repository' voor een bepaalde entiteit. Deze interface zal een JpaRepository extenden, en geannoteerd worden met een @Repository. Hierdoor weet Spring JPA dat het een repository is van een bepaalde entiteit en zal de verbinding leggen met de database.\
In deze repository is het niet nodig om de standaard CRUD functies te implementeren, want dat gebeurt al in de JpaRepository interface.&#x20;

{% code title="UserRepository.java" %}
```java
@Repository
public interface UserRepository extends JpaRepository<User, UUID> {
}
```
{% endcode %}

