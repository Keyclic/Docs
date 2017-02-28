# Organisations

Dans l'application Keyclic, une organisation est une entité telle que club, entreprise, association, corporation, etc, à laquelle peuvent être rattachées les observations faites par les utilisateurs.

Les membres d'une organisation sont des utilisateurs de l'application Keyclic rattachés à cette organisation. Un ou plusieurs membres d'une organisation peuvent en être les administrateurs. Une organisation possède au minimum un membre, et un utilisateur ne peut être membre que d'une seule organisation.

Les administrateurs d'une organisation peuvent définir les champs d'intervention de leur organisation en créant des catégories (exemple : voirie, transports, etc) et des zones géographiques. Quand un utilisateur crée une nouvelle observation, il précise toujours les coordonnées géographiques de cette observation. Ainsi, l'application est en mesure de lui retourner l'ensemble des organisations et de leurs catégories, ce qui lui permet de choisir la catégorie la plus adéquate à son observation.

## Création d'une organisation

Tout utilisateur peut créer une nouvelle organisation :

```
POST /organizations
```

```
body :
    name => Nom de l'association
    billingEmailAddress => Adresse email de facturation
    notificationEmailAddress => Adresse email de notification
```

L'utilisateur devient automatiquement membre et administrateur de cette nouvelle organisation.

Pour récupérer toutes les organisations du domaine applicatif :

```
GET /organizations
```

Il est possible de filtrer la requête ci-dessus sur un point géographique (voir ci-dessous : zones géographiques) :

```
GET /organizations?geo_coordinates=+44.851404209987386-0.5762618780136108
```

## Gestion des membres

Pour ajouter un nouvel utilisateur à une organisation :

```
POST /organizations/{organization}/members
```

```
body : 
    person => c7469b6b-e531-400b-8cb6-e8f9560cba7d
```

Ce endpoint est réservé à un utilisateur possédant le rôle ORGANIZATION:ADMIN et membre de l'organisation {organization}, et l'utilisateur ajouté ne doit être membre d'aucune organisation.

Pour récupérer les membres d'une organisation :

```
GET /people?organization={organization}
```

LIEN : Pour plus d'informations sur le rôle ORGANIZATION:ADMIN et ses privilèges, voir .

# Gestion des zones géographiques

Un administrateur d'organisation peut créer des zones géographiques, correspondant aux lieux sur lesquels cette organisation intervient :

```
POST /organizations/{organization}/places
```

```json
body :
{
    "name": "Test",
    "polygon":
    {
        "rings":
        [
            {
                "points":
                [
                    {
                        "longitude": 2.373991012573242,
                        "latitude": 48.84088179130599
                    },
                    {
                        "longitude": 2.3763084411621094,
                        "latitude": 48.84205393836751
                    },
                    {
                        "longitude": 2.376694679260254,
                        "latitude": 48.84189859515306
                    },
                    {
                        "longitude": 2.3787975311279297,
                        "latitude": 48.84041574931067
                    },
                    {
                        "longitude": 2.376115322113037,
                        "latitude": 48.839031720249054
                    },
                    {
                        "longitude": 2.373991012573242,
                        "latitude": 48.84088179130599
                    }
                ]
            }
        ],
        "srid": 5555
    },
    "elevation": 1
}
```

Pour récupérer toutes les zones géographiques du domaine applicatif :

```
GET /places
```

La requête ci-dessus peut-être filtrée sur une organisation donnée et/ou sur un point géographique donné :

```
GET /places?geo_coordinates=+44.851404209987386-0.5762618780136108&organization={organization}
```

## Gestion des catégories

Les catégories sont les secteurs d'activité d'une organisation. Un administrateur d'organisation peut créer une nouvelle catégorie en lui donnant un nom, une couleur et une icône. L'icône sera choisie dans le jeu d'icônes de Font Awesome : http://fontawesome.io/icons/

Exemple :

```
POST /organizations/{organization}/categories
```

```
body :
    name : "Nouvelle catégorie"
    color : "#00ff00"
    icon : fa-bug
```

Les 3 propriétés name, color et icon peuvent être éditées par une requête PATCH (LIEN).

Pour récupérer l'ensemble des catégories du domaine applicatif :

```
GET /categories
```

La requête ci-dessus peut-être filtrée sur une organisation donnée et/ou sur un point géographique donné :

```
GET /categories?geo_coordinates=+44.851404209987386-0.5762618780136108&organization={organization}
```

## Gestion des partenariats

Une organisation peut avoir des partenaires, c'est à dire des organisations qui lui sont rattachées et à qui l'administrateur de l'organisation pourra déléguer des rapports. La relation de partenariat est unilatérale : si une organisation A est partenaire d'une organisation B, B n'est pas forcément partenaire de A.

Pour ajouter un nouveau partenaire à l'organisation, un administrateur de l'organisation exécutera le endpoint :

```
POST /organizations/{orga}/relationships
```

```
body :
    organization : uuid de l'organisation partenaire
```

Pour récupérer les partenaires d'une organisation :

```
GET /organizations/{{orga}}/relationships
```

Cette requête ne peut être exécutée que par un administrateur de l'organisation.






















