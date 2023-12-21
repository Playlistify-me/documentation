---
description: Playlistify draaien in een container
---

# Docker

Onderstaand bestand is onze Dockerfile. Deze zorgt er voor dat een image gebouwd kan worden van onze back-end en later gedraaid worden. Hij maakt gebruik van multi-stage builds, wat er voor zorgt dat de uiteindelijke container zo klein mogelijk blijft. Eerst is een stage builder, welke in de Gradle omgeving onze applicatie build. Hij downloadt en installeert alle packages en dependencies, waarna hij de applicatie compiled en build naar een zogenaamde Boot Jar. Dit is een (of soms meerdere) bestand (`.jar`). Daarna starten we een nieuwe omgeving van alleen de Java Runtime, omdat we Gradle niet meer nodig hebben. Hierin kopiëren we, vanaf de eerste stage, alle gemaakte `.jar` bestanden, welke we in `app.jar` bundelen. Ook stellen we poort 8080 (welke wordt gebruikt door onze applicatie) open. Daarna wordt het java commando meegegegeven om de applicatie te kunnen opstarten.

```docker
FROM gradle:jdk17-alpine AS builder
WORKDIR /app
COPY . .
RUN gradle clean bootJar

FROM eclipse-temurin:17-jre-alpine AS runner
WORKDIR /app

COPY --from=builder /app/build/libs/*.jar app.jar
EXPOSE 8080

FROM runner AS runner_actions
CMD ["java", "-jar", "app.jar"]
```
