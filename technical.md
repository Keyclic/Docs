# Considérations techniques

L'API Keyclic est une **API REST**. Toutes les opérations sont effectuées via le protocole **https** et sécurisées par **JSON Web Token**. Les données sont échangées exclusivement au format **JSON**.

Le nom de domaine de l'API Keyclic est :

```
api.keyclic.com
```

La documentation technique Swagger de l'API peut être téléchargée ici : https://api.keyclic.com/swagger.json

## Applications et clés d'applications

Tout client de l'API doit transmettre dans les headers de chaque requête une clé définissant l'application sur laquelle il travaille.

Si vous développez un client pour travailler sur une application existante de Keyclic, vous devez connaître la clé de cette application. Si au contraire vous développez un client pour une nouvelle application, merci de vous adresser à la société Keyclic pour que celle-ci crée l'application et sa configuration et vous fournisse la clé correspondante.

Deux clés d'application sont actuellement disponibles :

- com.keyclic.app
- com.keyclic.highway.vinci

Chaque requête doit donc préciser, dans ses headers, la valeur du paramètre X-Keyclic-App. Voir ci-dessous le paragraphe [Requêtes](#requêtes) pour la mise en œuvre.

Notez cependant que la base utilisateurs est commune à toutes les applications Keyclic. De fait, les endpoints d'inscription et de connexion (LIEN : authentification) font exception à la règle ci-dessus : ces deux endpoints n'exigent pas qu'une clé d'application leur soit fournie.

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

En plus des [headers conventionnels de HTTP/1.1](https://tools.ietf.org/html/rfc7231#section-5), l'API Keyclic accepte, et même exige dans la plupart des cas, le header X-Keyclic-App, correspondant à l'application utilisée (voir ci-dessus : [Domaines applicatifs](#domaines-applicatifs)). Par exemple, pour récupérer toutes les observations sur l'application com.keyclic.app, la requête comportera le header :

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

Par défaut, *page* a la valeur 1 et *limit* a la valeur 10. Ainsi le endpoint 

```
POST /feedbacks
```

retourne les 10 premières observations.

Le retour d'une collection contient les informations et liens nécessaires pour naviguer entre les pages de cette collection. Exemple de retour de la liste des observations :

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

Dans cette documentation, nous ne rappellerons pas systématiquement qu'il est possible de paginer avec les filtres *page* et *limit*, ceux-ci étant communs à tous les endpoints retournant une collection.

## Modification de ressources avec la méthode PATCH

Dans l'API Keyclic, la modification des ressources s'effectue avec la méthode [PATCH](https://tools.ietf.org/html/rfc5789). Contrairement à la méthode [PUT](https://tools.ietf.org/html/rfc7231#section-4.3.4), la méthode [PATCH](https://tools.ietf.org/html/rfc5789) permet de modifier une seule propriété, ou une partie seulement des propriétés, d'une ressource, sans qu'il soit nécessaire d'en envoyer une représentation complète. Le format utilisé pour la description du patch est [JSON Patch](https://tools.ietf.org/html/rfc6902). La seule opération acceptée par l'API lors d'un PATCH est l'opération *replace*. 

À titre d'exemple, voici la modification de la popriété *billingEmailAddress* d'une organisation :

```
PATCH /organizations/{organization}
```

```json
[
	{
		"op":"replace",
		"path":"/billingEmailAddress",
		"value":"test@test.com"
	}
]
```

## Retours d'erreurs

Toute erreur entraîne une réponse de code [4xx](https://tools.ietf.org/html/rfc7231#section-6.5) reflétant le type d'erreur.

Quand il s'agit d'une erreur de type [400](https://tools.ietf.org/html/rfc7231#section-6.5.1) (Bad Request), les raisons de l'erreur sont retournées.

## Changements de statut

Plusieurs ressources manipulées par l'API ont un cycle de vie et possèdent un certain statut à un instant donné. C'est le cas des observations, des rapports et des opérations.

Pour ces ressources, l'état est toujours indiqué dans la réponse avec le paramètre *state*, et les actions possibles pour faire évoluer ce statut sont toujours indiqués sous le paramètre *stateTransitions*. Exemple :

```
GET reports/{report}
```

Réponse :
```json
{
  "type": "Report",
  "id": "cb7118b5-a821-4cf2-9475-0c0d0efdb8d0",
  "state": "NEW",
  "_embedded": {
    "stateTransitions": [
      "accept",
      "refuse"
    ]
  },
  // ...
}
```

Dans l'exemple ci-dessus, le rapport est en statut NEW et les actions possibles sur son statut sont *accept* et *refuse*.

Tout changement de statut est effectué avec la méthode PATCH et l'opération *replace*, en précisant *transition* pour le path, et l'action à effectuer pour la valeur.

Par exemple, pour accepter le rapport ci-dessus :

```
PATCH /reports/{report}/state
```

```json
[
	{
		"op":"replace",
		"path":"transition",
		"value":"accept"
		
	}
]
```

La réponse nous informe que le rapport possède désormais le statut ACCEPTED, et que les actions possibes sont désormais *refuse*, *hold* et *progress* :

```json
{
  "type": "Report",
  "id": "32219286-528a-4f97-b81e-fe7a8cb85707",
  "state": "ACCEPTED",
  "_embedded": {
    "stateTransitions": [
      "refuse",
      "hold",
      "progress"
    ]
  },
  // ...
}
```

Les actions et status possibles pour chaque type de ressources sont décrits dans les sections idoines de cette documentation.

