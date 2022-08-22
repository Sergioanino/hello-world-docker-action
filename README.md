<!-- TUTO : https://github.com/pablokbs/hello-world-docker-action -->

# Docker action 'Hello mundo'

Cette action imprime "Hello mundo" ou "Hello" + le nom de la personne du log.

## Inputs

### `who-to-greet`

**Requerid** Le nom de la personne à qui nous devons saluer. Par défaut, `"Monde"`.

## Outputs

### `time`

La date ou nous nous sommes connu.

## Exemple usage

```
uses: sergioanino/flutter_docker@v1
with:
    who-to-greet: 'sergioanino'
```
