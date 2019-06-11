.. _members:

Membres d'organisation et rôles
===============================

Quand un utilisateur est membre d’une organisation, il peut bénéficier d'aucun, d'un ou plusieurs rôles définissant un ensemble de permissions et de possibilités d’actions. Ces rôles peuvent être cumulés pour un même utilisateur et sont au nombre de cinq :

- Administrateur
- Agent
- Intervenant
- Statistiques
- Export

Un utilisateur pouvant être membre de plusieurs organisations, les rôles qu’il possède sont indépendants et peuvent être différents d’une organisation à une autre.
Tout utilisateur nouvellement attaché à une organisation devient « Membre d’organisation ». Un « Membre d’organisation » possède les mêmes droits qu’un utilisateur de base sans attachement à une organisation.

.. _members-organization-admin:

Administrateur
--------------

Tout utilisateur a la possibilité de créer une nouvelle organisation.

L’utilisateur qui crée une nouvelle organisation en devient automatiquement membre et administrateur, c’est-à-dire qu’il se voit attribuer le rôle « Administrateur ».

Il obtient les permissions et droits suivants :

- Ajouter de nouveaux membres à son organisation
- Modifier les rôles des membres
- Gérer les catégories de son organisation
- Gérer les zones de responsabilité de son organisation
- Gérer les partenaires de son organisation
- Consulter et gérer les rapports reçus et les interventions liées à ces rapports

Voir : :ref:`organizations`

Voir : :ref:`reports`

Note : Un utilisateur peut être « ORGANIZATION:ADMIN » de plusieurs organisations et une organisation peut avoir plusieurs « ORGANIZATION:ADMIN ».

.. _members-agent:

Agent
-----

« Agent » est un rôle particulier adapté aux personnels de terrain qui effectuent des remontées d’observation uniquement dédiées à leur organisation.

Il peut activer le Mode Pro (cf :ref:`feedbacks-organization-member`)

**Note : Un utilisateur ne peut être « ORGANIZATION:AGENT » que d’une seule organisation et une organisation peut avoir plusieurs « ORGANIZATION:AGENT ».**

.. _members-operator:

Intervenant
-----------

Un « Membre d’organisation » possédant ce rôle peut  :

- Être listé par les administrateurs de l’organisation
- Recevoir une assignation à une intervention
- Éditer une intervention (changement des libellés, ajout de photos de constatation, etc)
- Changer le statut d’une intervention

Note : Un utilisateur peut être « ORGANIZATION:OPERATOR » de plusieurs organisations et une organisation peut avoir plusieurs « ORGANIZATION:OPERATOR ».

.. _members-analytics:

Statistiques
------------

Le rôle « Statistiques » permet d’accéder aux statistiques d’une organisation.

Note : Un utilisateur peut avoir le rôle « ORGANIZATION:ANALYTICS » pour plusieurs organisations et une organisation peut avoir plusieurs utilisateurs avec le rôle « ORGANIZATION:ANALYTICS ».

.. _members-export:

Export
------

Le rôle « Export » permet d’accéder aux fonctionnalités d’exportation Excel des rapports qu’a reçu une organisation.

Note : Un utilisateur peut avoir le rôle « ORGANIZATION:EXPORT » pour plusieurs organisations et une organisation peut avoir plusieurs utilisateurs avec le rôle « ORGANIZATION:EXPORT ».

.. _members-retrieving:

Récupération des utilisateurs
-----------------------------

Pour récupérer l'ensemble des utilisateurs de l'application :

.. code-block:: bash

    GET /people

Pour récupérer un utilisateur :

.. code-block:: bash

    GET /people/{user}

Pour rechercher les utilisateurs dont l'adresse email match un mot donné :

.. code-block:: bash

    GET /people?search[email]=martin

.. _members-example:

Exemple de récupération des rôles d'un utilisateur
--------------------------------------------------

La lecture d'une ressource utilisateur permet de découvrir si la personne appartient à une organisation et quel(s) rôle(s) il y tient.

.. code-block:: bash

    GET /people/5020c6ea-ca07-42d1-994f-d90b86703b1a/memberships

.. code-block:: json

    {
        "page": 1,
        "limit": 10,
        "pages": 1,
        "total": 1,
        "_links": {
            "self": {
                "href": "/people/5020c6ea-ca07-42d1-994f-d90b86703b1a/memberships?page=1&limit=10"
            },
            "first": {
                "href": "/people/5020c6ea-ca07-42d1-994f-d90b86703b1a/memberships?page=1&limit=10"
            },
            "last": {
                "href": "/people/5020c6ea-ca07-42d1-994f-d90b86703b1a/memberships?page=1&limit=10"
            }
        },
        "_embedded": {
            "items": [
                {
                    "id": "b0e7e28f-5b91-4c73-875e-8f34aa03553a",
                    "roles": [
                        "ORGANIZATION:ADMIN",
                        "ORGANIZATION:AGENT"
                    ],
                    "createdAt": "2018-02-27T10:00:00+02:00",
                    "_links": {
                        "self": {
                            "href": "/organizations/84d36093-b8bc-47ad-bc8a-a043b3e301a9/members/b0e7e28f-5b91-4c73-875e-8f34aa03553a",
                            "iriTemplate": {
                                "mapping": {
                                    "organization": "84d36093-b8bc-47ad-bc8a-a043b3e301a9",
                                    "member": "b0e7e28f-5b91-4c73-875e-8f34aa03553a"
                                }
                            }
                        },
                        "person": {
                            "href": "/people/5020c6ea-ca07-42d1-994f-d90b86703b1a",
                            "iriTemplate": {
                                "mapping": {
                                    "person": "5020c6ea-ca07-42d1-994f-d90b86703b1a"
                                }
                            }
                        },
                        "organization": {
                            "href": "/organizations/84d36093-b8bc-47ad-bc8a-a043b3e301a9",
                            "iriTemplate": {
                                "mapping": {
                                    "organization": "84d36093-b8bc-47ad-bc8a-a043b3e301a9"
                                }
                            }
                        }
                    },
                    "_embedded": {
                        "availableRoles": [
                            "ORGANIZATION:ADMIN",
                            "ORGANIZATION:ANALYTICS",
                            "ORGANIZATION:EXPORT",
                            "ORGANIZATION:READ_ONLY"
                        ]
                    }
                }
            ]
        }
    }

Ce retour indique que l'utilisateur :

- Est membre de l'organisation 84d36093-b8bc-47ad-bc8a-a043b3e301a9
- Possède le rôle ORGANIZATION:ADMIN, il est donc administrateur de l'organisation 84d36093-b8bc-47ad-bc8a-a043b3e301a9
- Possède le rôle ORGANIZATION:AGENT, il est donc agent de l'organisation 84d36093-b8bc-47ad-bc8a-a043b3e301a9
- Est affilié avec une seule organisation
- A rejoint l'organisation le 27 février 2018.

Aussi, un membre possède deux id différents, un id membre et un id utilisateur.
Ainsi, dans le retour précédent on voit que son id utilisateur (5020c6ea-ca07-42d1-994f-d90b86703b1a) est différent de son id membre (b0e7e28f-5b91-4c73-875e-8f34aa03553a).
L'API distingue les actions effectuées en tant que membre et celles effectuées en tant qu'utilisateur simple.
