---
description: Automatische uitrol van Playlistify.
---

# CD workflow

Onderstaande code is de workflow voor het builden van een Docker image en het pushen naar de Docker hub. Op het moment dat er op de main branch iets gepusht wordt, activeert deze workflow. Hij logt in bij docker door middel van een access token, waarna de metadata wordt opgehaald om de image de juiste naam te geven. Daarna wordt de docker image gebouwd aan de hand van de Dockerfile, en wordt deze geupload naar de Docker Hub. Daarna is het mogelijk om deze image op elk apparaat te 'pullen' (downloaden) en te gebruiken als een container. Verdere informatie over de image specifiek vind je onder het kopje [Docker](docker.md).

{% code title="docker-hub.yml" fullWidth="false" %}
```yaml
name: Publish Docker Image

on:
  push:
    branches:
      - main

jobs:
  push_to_registry:
    name: Push images to docker hub
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Log in to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_TOKEN }}
      - name: Docker meta
        id: meta
        uses: docker/metadata-action@v5
        with:
          images: mschreijen/playlistify
      - name: Build and push
        uses: docker/build-push-action@v5
        with:
          context: .
          file: ./Dockerfile
          push: true
          tags: ${{ steps.meta.outputs.tags }}
          labels: ${{ steps.meta.outputs.labels }}
```
{% endcode %}
