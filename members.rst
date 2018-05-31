.. _members:

Membres d'organisation et rôles
===============================

Quand un utilisateur est membre d’une organisation, il peut bénéficier d'aucun, d'un ou plusieurs rôles définissant un ensemble de permissions et de possibilités d’actions. Ces rôles peuvent être cumulés pour un même utilisateur et sont au nombre de cinq :

- Aucun rôle - Membre d’organisation
- Administrateur
- Agent
- Statistiques
- Export

Un utilisateur pouvant être membre de plusieurs organisations, les rôles qu’il possède sont indépendants et peuvent être différent d’une organisation à une autre.

.. _members-no-roles:

Aucun rôle - Membre d’organisation
----------------------------------

Tout utilisateur nouvellement attaché à une organisation devient « Membre d’organisation ». Un « Membre d’organisation » possède les mêmes droits qu’un utilisateur de base sans attachement à une organisation.

Ce rôle permet en plus de pouvoir :

- Être listé par les administrateurs de l’organisation
- Recevoir une assignation à une intervention
- Éditer une intervention (changement des libellés, ajout de photos de constatation, etc)
- Changer le statut d’une intervention

Note : Un utilisateur peut être membre d’organisation de plusieurs organisations et une organisation peut avoir plusieurs membres d’organisation.

.. _members-organization-admin:

Administrateur
--------------

Tout utilisateur a la possibilité de créer une nouvelle organisation.

L’utilisateur qui crée une nouvelle organisation en devient automatiquement membre et administrateur, c’est-à-dire qu’il se voit attribuer le rôle « Administrateur ».

Aux permissions et aux droits des « Membres d’organisation » s’ajoute les suivants :

- Ajouter de nouveaux membres à une organisation
- Modifier les roles des membres
- Gérer les catégories d’une organisation
- Gérer les zones de responsabilité d’une organisation
- Gérer les partenaires d’une organisation
- Consulter et gérer les rapports reçus et les opérations liées à ces rapports

Voir : :ref:`organizations`

Voir : :ref:`reports`

Note : Un utilisateur peut être « Administrateur » de plusieurs organisations et une organisation peut avoir plusieurs « Administrateurs ».

.. _members-agent:

Agent
-----

« Agent » est un rôle particulier adapté aux personnels de terrain qui effectuent des remontées d’observation uniquement dédiées à leur organisation.

Aux permissions et aux droits des « Membres d’organisation » s’ajoute les suivants :

- Activer le Mode Pro (cf infra: Observation postée en Mode Pro)

**Note : Un utilisateur ne peut être « Agent » que d’une seule organisation et une organisation peut avoir plusieurs « Agents ».**

.. _members-stat:

Statistiques
------------

Le rôle « Statistique » permet d’accéder aux statistiques d’une organisation.

Note : Un utilisateur peut avoir le rôle « Statistique » pour plusieurs organisations et une organisation peut avoir plusieurs utilisateurs avec le rôle « Statistique ».

.. _members-export:

Export
------

Le rôle « Export » permet d’accéder aux fonctionnalités d’exportation Excel des rapports qu’a reçu une organisation.

Note : Un utilisateur peut avoir le rôle « Export » pour plusieurs organisations et une organisation peut avoir plusieurs utilisateurs avec le rôle « Export ».

.. _members-retrieving:

Récupération des utilisateurs
-----------------------------

Pour récupérer l'ensemble des utilisateurs de l'application :

.. code-block:: bash

    GET /people

Pour récupérer un utilisateur :

.. code-block:: bash

    GET /people/{user}

Pour rechercher les membres dont l'adresse email match un mot donné :

.. code-block:: bash

    GET /people?search[email]=martin

Pour filtrer les membres d'une organisation :

.. code-block:: bash

    GET /people?organization={organization}

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

Ce retour indique que :

1. Il est membre de l'organisation 84d36093-b8bc-47ad-bc8a-a043b3e301a9
2. Il possède le rôle ORGANIZATION:ADMIN, il est donc administrateur de l'organisation 84d36093-b8bc-47ad-bc8a-a043b3e301a9
3. Il possède le rôle ORGANIZATION:AGENT, il est donc agent de l'organisation 84d36093-b8bc-47ad-bc8a-a043b3e301a9
4. L'id d'utilisateur (5020c6ea-ca07-42d1-994f-d90b86703b1a) est différent de l'id de membre (b0e7e28f-5b91-4c73-875e-8f34aa03553a)
5. Il est affilié avec une seule organisation
6. Il a rejoint l'organisation le 27 février 2018.
