---
description: De puzzelstukjes waar Playlistify uit bestaat
---

# Gebruikte technologieën

Playlistify is opgezet met een database, een API die hiermee interfaced, en een front-end voor de gebruikers interactie. De front-end wordt gemaakt met Next.js, de back-end met Spring Boot, en de database is een MySQL database.

## Front-end

[Next.js](https://nextjs.org/) (en daarmee ook [React](https://react.dev/)) is het framework voor onze front-end. Met dit framework kan een website met modules en componenten makkelijk worden opgezet. Ook is het makkelijk om verschillende routes aan te geven voor je website, dit gaat geheel via de map structuur van je project. De authenticatie wordt afgehandeld door [NextAuth.js](https://next-auth.js.org/), een framework voor Next.js welke implementaties heeft voor verschillende providers (Google, Microsoft, Spotify, Github, etc).

## Back-end

De back-end API is een Java project met [Spring Boot](https://spring.io/projects/spring-boot). Hierdoor kunnen wij makkelijk nieuwe routes definieren en services voor dataverwerking aanmaken en implementeren. De database connectie wordt afgehandeld door [Spring Data JPA](https://spring.io/projects/spring-data-jpa), welke in combinatie met de [Hibernate ORM](https://hibernate.org/orm/) en [Flyway Migrations](https://flywaydb.org/) de behoefte voor een DBMS verwijdert. Entiteiten worden geannoteerd met bepaalde eigenschappen, en zodra de applicatie wordt opgestart zorgt Spring JPA er voor dat de database schemas up-to-date zijn met de entiteiten zoals ze beschreven staan in de code.

## Database

Wij hebben een gehoste [MySQL](https://www.mysql.com/) database welke er voor zorgt dat onze data gepersisteerd wordt. Ook kunnen wij hierin wanneer wij dit willen onze foutmeldingen opslaan, en als wij dit willen, de gebruikersinformatie van een op maat gemaakt authenticatie systeem opslaan.

## Overig

### Versiebeheer

Wij hebben gekozen voor [Github](https://github.com/) voor ons versiebeheer. Github is gratis, en de features die wij nodig hebben zijn accessible zonder een paywall. Ook kunnen wij hiermee gebruik maken van Github Actions, waardoor wij CI en CD workflows kunnen implementeren.

### Deployment

Voor het uitrollen van onze applicatie en het deployen maken wij gebruik van [Docker](https://www.docker.com/). Dit geeft ons de mogelijkheid om van onze applicatie een 'container' te maken welke alleen de stukjes software heeft die nodig zijn voor het draaien van Playlistify. Deze container is daarna op elke computer te draaien, en met een beetje configuratie is Playlistify dan ook te bereiken via het netwerk op die computer.
