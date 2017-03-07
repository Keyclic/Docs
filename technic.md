# Considérations techniques

L'API Keyclic est une **API REST**. Toutes les opérations sont effectuées via le protocole **https** et sécurisées par **JSON Web Token**. Les données sont échangées exclusivement au format **JSON**.

Le nom de domaine de l'API Keyclic est :

```
api.keyclic.com
```

La documentation technique de l'API selon la spécification Swagger peut être téléchargée ici : https://api.keyclic.com/swagger.json

## Domaines applicatifs

Toutes les opérations sont effectuées sur un domaine applicatif particulier. Deux domaines applicatifs sont actuellement reconnus par l'API :

- com.keyclic.app
- com.keyclic.highway.vinci

Tout client de l'API doit donc travailler sur l'un de ces domaines, en le précisant dans les headers de chaque requête (voir ci-desous : [Requêtes](#requêtes)). Si vous souhaitez qu'un nouveau domaine applicatif soit créé, merci d'en faire la demande à la société Keyclic.

## Requêtes

Dans cette documentation, chaque endpoint de l'API sera décrit par le chemin d'accès à la ressource précédé du [verbe HTTP](https://tools.ietf.org/html/rfc7231#section-4.1). Exemple :

```
GET /feedbacks
```

Le endpoint ci-dessus retourne toutes les observations. Son url véritable est https://api.keyclic.com/feedbacks mais pour des raisons de concision, dans cette documentation, nous ne préciserons jamais le protocole ni le nom de domaine.

### Paramètres d'url

Dans cette documentation, les variables d'URI (exemples : identifiant d'une ressource, numéro de page, etc) seront exprimés entre accolades. Par exemple, pour récupérer une observation (feedback) donnée :

```
GET /feedbacks/{feedback}
```

Dans l'API Keyclic, conformément aux principes d'architecture REST, les paramètres de filtrage sont toujours passés en "query string". Exemple :

```
GET /feedbacks?page={page}
```

Par ailleurs, pour une meilleure lisibilité, les paramètres d'uri seront écrits tels quels dans cette documentation, et non sous leur forme url encodée :

```
GET /feedbacks?before=2018-04-22T01:00:00+05:00
```

### Headers

En plus des [headers conventionnels de HTTP/1.1](https://tools.ietf.org/html/rfc7231#section-5), l'API Keyclic accepte, et même exige dans la plupart des cas, le header X-Keyclic-App, correspondant au domaine applicatif (voir ci-dessus : [Domaines applicatifs](#domaines-applicatifs)). Par exemple, pour récupérer toutes les observations sur le domaine applicatif com.keyclic.app, la requête comportera le header :

```
X-Keyclic-App : com.keyclic.app
```

Tous les endpoints exigent que ce header soit fourni, à l'exception des endpoints de login et de changement de mot de passe. (LIEN : authentification)

Toutes les requêtes (à l'exception du login, du register et du changement de mot de passe) doivent aussi comporter le header Authorization afin d'authenfier l'utilisateur. (LIEN : authentification)

## Format des requêtes et réponses

Le seul type de contenu accepté par l'API Keyclic est JSON. Vos requêtes devront donc comporter le header :

```
Content-type: application/json
```

Et les paramètres de requêtes, hors query string, seront toujours envoyés en JSON. Les réponses sont également toujours retournées au format JSON.

## Envoi de fichiers

Tous les fichiers sont envoyés en base 64 à l'API. Voici par exemple l'ajout d'une image représentant un carré rouge d'1 pixel sur 1 sur une observation :

```
POST /feedbacks/{feedback}/images
```

```json
{
    "image":"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAUAAAAFCAIAAAACDbGyAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAB3RJTUUH4QIVDRUfvq7u+AAAABl0RVh0Q29tbWVudABDcmVhdGVkIHdpdGggR0lNUFeBDhcAAAAUSURBVAjXY3wrIcGABJgYUAGpfABZiwEnbOeFrwAAAABJRU5ErkJggg=="
}
```

## Pagination

Tous les endpoints permettant de récupérer une collection de ressources peuvent être paginés avec les filtres **page** et **limit**. Par exemple, pour récupérer la deuxième page des observations à raison de 5 observations par page :

```
POST /feedbacks?page=2&limit=5
```

Par défaut, page a la valeur 1 et limit a la valeur 10. Ainsi le endpoint 

```
POST /feedbacks
```

retourne les 10 premières observations du domaine applicatif.

Le retour d'une collection contient les informations et liens nécessaires pour naviguer entre les pages d'une collection. Exemple de retour de la liste des observations :

```json
{
  "page": 2,
  "limit": 10,
  "pages": 8,
  "total": 72,
  "_links": {
    "self": {
      "href": "/feedbacks?page=2&limit=10"
    },
    "first": {
      "href": "/feedbacks?page=1&limit=10"
    },
    "last": {
      "href": "/feedbacks?page=8&limit=10"
    },
    "next": {
      "href": "/feedbacks?page=3&limit=10"
    },
    "previous": {
      "href": "/feedbacks?page=1&limit=10"
    }
  },
  // ...
}
```

Dans cette documentation, nous ne rappellerons pas systématiquement qu'il est possible de paginer avec les filtres **page** et **limit**, ceux-ci étant communs à tous les endpoints retournant une collection.
























