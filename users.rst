.. _users:

Utilisateurs et rôles
=====================

Les utilisateurs de l'application Keyclic possèdent un ou plusieurs rôles, définissant un ensemble de permissions et de possibilités d'action. Ces rôles, qui peuvent être cumulés pour un même utilisateur, sont au nombre de trois :

- ROLE_USER : utilisateur de base
- ORGANIZATION:ADMIN : administrateur d'une organisation
- APPLICATION:ADMIN : administrateur d'application

.. _users-basic-user:

Utilisateur de base (rôle ROLE_USER)
------------------------------------

Tout utilisateur nouvellement inscrit possède automatiquement le rôle ROLE_USER. Ce rôle lui permet de :

- consulter et modifier son profil
- consulter les observations faites par les autres utilisateurs
- soutenir une observation
- commenter une observation
- créer une nouvelle observation

Voir : :ref:`feedbacks`

.. _users-organization-admin:

Administrateur d'organisation (rôle ORGANIZATION:ADMIN)
-------------------------------------------------------

Tout utilisateur a la possibilité de créer une nouvelle organisation.

L'utilisateur qui crée une nouvelle organisation en devient automatiquement membre et administrateur, c'est-à-dire qu'il se voit attribuer le rôle ORGANIZATION:ADMIN. Une organisation peut posséder plusieurs administrateurs, mais un utilisateur ne peut être membre, et par conséquent administrateur, que d'une seule organisation.

**Attention** : si un utilisateur est déjà membre d'une organisation et qu'il en crée une nouvelle, étant donné qu'il sera automatiquement rattaché à cette nouvelle organisation, il sera, de fait, retiré de la liste des membres de l'organisation à laquelle il appartenait auparavant.

L'administrateur d'une organisation peut :

- Ajouter de nouveaux membres à son organisation
- Gérer les catégories de cette organisation
- Gérer les aires géographiques de cette organisation
- Gérer les partenaires de cette organisation
- Consulter et gérer les rapports reçus par cette organisation et les opérations liées à ces rapports

Voir : :ref:`organizations`

.. _users-application-admin:

Administrateur d'application (rôle APPLICATION:ADMIN)
-----------------------------------------------------

L'administrateur d'une application a la possibilité de modérer les observations avant que celles-ci soient transmises, sous forme de rapports, aux organisations concernées.

Voir : :ref:`feedbacks-lifecyle`

.. _users-organization-member:

Membres d'organisation
----------------------

Quand un utilisateur est membre d'une organisation, cela ne lui confère par un rôle particulier, mais cette appartenance à l'organisation lui donne la possibilité de créer une nouvelle observation de façon à ce que celle-ci soit aussitôt visible par la communauté, sans passer par l'étape de modération (voir : :ref:`feedbacks-lifecyle`).

De plus, les membres d'une organisation peuvent se voir assigner des opérations par les administrateurs de cette organisation (voir : :ref:`reports-operations`).



Note : dans l'application cliente Keyclic, ce fonctionnement est obtenu par l'activation du mode Pro.

.. _users-example:

Exemple de ressource utilisateur
--------------------------------

La lecture d'une ressource Utilisateur permet de découvrir les rôles de cet utilisateur, et éventuellement l'organisation dont il est administrateur et/ou l'application dont il est administrateur.

.. code-block:: bash

    GET /people/{user}

.. code-block:: json

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

Ce retour indique que :

1. Cet utilisateur possède le rôle ROLE_USER, comme tous les utilisateurs.
2. Il est membre de l'organisation 84d36093-b8bc-47ad-bc8a-a043b3e301a9
3. Il possède le rôle ORGANIZATION:ADMIN, il est donc administrateur de l'organisation 84d36093-b8bc-47ad-bc8a-a043b3e301a9
4. Il possède le rôle APPLICATION:ADMIN, il est donc administrateur de l'application à laquelle est rattachée l'organisation 84d36093-b8bc-47ad-bc8a-a043b3e301a9

.. _users-retrieving:

Récupération des utilisateurs
------------------------

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

