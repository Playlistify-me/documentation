---
description: De puzzelstukjes waar Het Leffe Circuit uit bestaat
---

# Gebruikte technologieën

## Front-end

[Next.js](https://nextjs.org/) (en daarmee ook [React](https://react.dev/)) is het framework voor onze front-end. Met dit framework kan een website met modules en componenten makkelijk worden opgezet. Ook is het makkelijk om verschillende routes aan te geven voor je website, dit gaat geheel via de map structuur van je project.

## Back-end

Voor het opbouwen van een back-end met API gebruiken wij [NestJS](https://nestjs.com/). Dit is net als de front-end gebaseerd op Node. Het opbouwen van router kan doormiddel van modules welke een controller en service class kunnen hebben. Daarnaast maken wij verbinding met onze database via de [Prisma](https://www.prisma.io/) ORM.

## Database

Wij hebben een gehoste [MySQL](https://www.mysql.com/) database welke er voor zorgt dat onze data gepersisteerd wordt. Ook kunnen wij hierin wanneer wij dit willen onze foutmeldingen opslaan, en als wij dit willen, de gebruikersinformatie van een op maat gemaakt authenticatie systeem opslaan.

## Overig

### Versiebeheer

Wij hebben gekozen voor [Github](https://github.com/) voor ons versiebeheer. Github is gratis, en de features die wij nodig hebben zijn accessible zonder een paywall. Ook kunnen wij hiermee gebruik maken van Github Actions, waardoor wij CI en CD workflows kunnen implementeren.

