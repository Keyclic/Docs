# Utilisateurs et rôles

Les utilisateurs de l'application Keyclic possèdent un ou plusieurs rôles, définissant un ensemble de permissions et de possibilités d'action. Ces rôles, qui peuvent être cumulés pour un même utilisateur, sont au nombre de trois :

- ROLE_USER : utilisateur de base
- ORGANIZATION:ADMIN : administrateur d'une organisation
- APPLICATION:ADMIN : administrateur d'un domaine applicatif

## Utilisateur de base (rôle ROLE_USER)

Tout utilisateur nouvellement inscrit possède automatiquement le rôle ROLE_USER. Ce rôle lui permet de :
- consulter et modifier son profil
- consulter les observations faites par les autres utilisateurs
- soutenir une observation
- commenter une observeration
- créer une nouvelle observation

LIEN : rubrique observations

## Administrateur d'organisation (rôle ORGANIZATION:ADMIN)

Tout utilisateur a la possibilité de créer une nouvelle organisation.

L'utilisateur qui crée une nouvelle organisation en devient automatiquement membre et administrateur, c'est à dire qu'il se voit attribuer le rôle ORGANIZATION:ADMIN. Une organisation peut posséder plusieurs administrateurs, mais un utilisateur ne peut être membre, et par conséquent administrateur, que d'une seule organisation.

**Attention** : Si un utilisateur est déjà membre d'une organisation et qu'il en crée une nouvelle, étant donné qu'il sera automatiquement rattaché à cette nouvelle organisation, il sera de fait retiré de la liste des membres de l'organisation à laquelle il appartenait auparavant.

L'administrateur d'une organisation peut :
- Ajouter de nouveaux membres à son organisation
- Gérer les catégories de cette organisation
- Gérer les aires géographiques de cette organisation
- Gérer les partenaires de cette organisation
- Consulter et gérer les rapports reçus par cette organisation et les opérations liées à ces rapports

LIEN : rubrique organisation

## Administrateur de domaine applicatif (rôle APPLICATION:ADMIN)

L'administrateur d'un domaine applicatif a la possibilité de modérer les observations.

LIEN : Feedbacks / modération

## Membres d'organisation

Quand un utilisateur est membre d'une organisation, celui ne lui confère par un rôle particulier, mais cette appartenance à l'organisation lui donne la possibilité de créer une nouvelle observation de façon à ce que celle-ci soit aussitôt visible par la communauté, sans passer par l'étape de modération.

LIEN : Observations / Création d'une observation sans modération

Note : dans l'appli cliente Keyclic, ce fonctionnement est obtenu par l'activation du mode Pro.

## Exemple de ressource utilisateur

La lecture d'une ressource Utilisateur permet de découvrir les rôles de cet utilisateur, et éventuellement l'organisation dont il est administrateur et/ou le domaine applicatif dont il est administrateur.

```
GET /people/5020c6ea-ca07-42d1-994f-d90b86703b1a
```

```json
{
  "username": "test@gmail.com",
  "email": "test@gmail.com",
  "type": "Person",
  "roles": [
    "APPLICATION:ADMIN",
    "ORGANIZATION:ADMIN",
    "ROLE_USER"
  ],
  "id": "5020c6ea-ca07-42d1-994f-d90b86703b1a",
  "createdAt": "2017-02-20T17:52:39+01:00",
  "updatedAt": "2017-02-27T14:48:39+01:00",
  "_links": {
    "self": {
      "href": "/people/5020c6ea-ca07-42d1-994f-d90b86703b1a",
      "iriTemplate": {
        "mapping": {
          "person": "5020c6ea-ca07-42d1-994f-d90b86703b1a"
        }
      }
    },
    "memberOf": {
      "href": "https://api.sandbox.keyclic.com/organizations/84d36093-b8bc-47ad-bc8a-a043b3e301a9",
      "iriTemplate": {
        "mapping": {
          "organization": "84d36093-b8bc-47ad-bc8a-a043b3e301a9"
        }
      }
    }
  }
}
```

Ce retour indique que :

1. Cet utilisateur possède le rôle ROLE_USER, comme tous les utilisateurs.
2. Il est membre de l'organisation 84d36093-b8bc-47ad-bc8a-a043b3e301a9
3. Il possède le rôle ORGANIZATION:ADMIN, il est donc administrateur de l'organisation 84d36093-b8bc-47ad-bc8a-a043b3e301a9
4. Il possède le rôle APPLICATION:ADMIN, il est donc administrateur du domaine applicatif auquel est rattachée l'organisation 84d36093-b8bc-47ad-bc8a-a043b3e301a9

## Récupération des membres

Pour récupérer l'ensemble des utilisateurs de l'application :

```
GET /people
```

Pour récupérer un utilisateur :
```
GET /people/{person}
```

Pour rechercher les membres dont l'adresse email match un mot donné :

```
GET /people?search[email]=marti
```

Pour filtrer les membres d'une organisation :

```
GET /people?organization={organization}
```

















