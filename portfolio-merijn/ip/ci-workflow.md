---
description: De waarborging van kwaliteit van de Playlistify software.
---

# CI workflow

Hieronder staat de workflow van onze SonarQube scan. Deze workflow zorgt er voor dat, op het moment dat er naar de main branch wordt gepusht, en op elke pull request die er wordt gemaakt, een sonarqube scan wordt uitgevoerd. SonarQube is een tool voor statische code analyze, welke aan de hand van bepaalde regels de gemaakte code beoordeeld. Zo wordt er gekeken naar veiligheids risico's, hoe onderhoudbaar de code is, en hoeveel de code wordt getest, en of dit allemaal voldoet aan de eisen die je zelf opzet.

{% code title="sonar.yml" %}
```yaml
name: SonarCloud
on:
  push:
    branches:
      - main
      - feature/cicd
  pull_request:
    types: [opened, synchronize, reopened]
jobs:
  build:
    name: Build
    runs-on: ubuntu-latest
    env:
      SPOTIFY_CLIENT_ID: ${{ secrets.SPOTIFY_CLIENT_ID }}
      SPOTIFY_CLIENT_SECRET: ${{ secrets.SPOTIFY_CLIENT_SECRET }}
      SPOTIFY_REDIRECT_URL: ${{ secrets.SPOTIFY_REDIRECT_URL }}
      SPRING_DATASOURCE_URL: ${{ secrets.SPRING_DATASOURCE_URL }}
      SPRING_DATASOURCE_USERNAME: ${{ secrets.SPRING_DATASOURCE_USERNAME }}
      SPRING_DATASOURCE_PASSWORD: ${{ secrets.SPRING_DATASOURCE_PASSWORD }}
    steps:
      - uses: actions/checkout@v3
        with:
          fetch-depth: 0
      - name: Set up JDK 17
        uses: actions/setup-java@v3
        with:
          java-version: 17
          distribution: "temurin"
      - name: Cache SonarCloud packages
        uses: actions/cache@v2
        with:
          path: ~/.sonar/cache
          key: ${{ runner.os }}-sonar
          restore-keys: ${{ runner.os }}-sonar
      - name: Cache Gradle packages
        uses: actions/cache@v2
        with:
          path: ~/.gradle/caches
          key: ${{ runner.os }}-gradle-${{ hashFiles('**/*.gradle') }}
          restore-keys: ${{ runner.os }}-gradle
      - name: Build and analyze
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
        run: ./gradlew build sonarqube --info
```
{% endcode %}
