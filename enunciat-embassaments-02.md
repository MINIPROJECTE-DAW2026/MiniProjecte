# Segona Part

## Migracions

En aquesta part farem servir migracions en comptes de l' `EnsureCreated`. Un cop feta i aplicada la primera migració, caldrà afegir algun camp nou (nullable o amb default value) a alguna de les taules per demostrar que saps fer migracions.

## API per entrar lectures individuals.

Crea dues api per rebre la informació d'una lectura d'una estació i entrar les dades a la base de dades:
* Una API usant el procediment emmagatzemat.
* Una API usant `EF` (amb les mateixes valiadacions que fem al procediment emmagatzemat)

### Proves de rendiment de les APIs.

Usant [Locust](https://locust.io/) o [nbomber](https://nbomber.com/) prepara unes proves de rendiment per veure estadístiques de rendiment de cadascuna de les APIs.

## Formulari entrar dades

Crea un formulari per entrar dades d'una lectura d'una estació i desar-la a la base de dades. Ull, no dupliquis codi, comparteix el codi amb la API feta amb `EF`.

## Desplegament amb Docker

Prepara un desplegament amb Docker de la teva aplicació.

