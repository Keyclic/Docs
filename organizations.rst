.. _organizations:

Organisations
=============

Dans l'application Keyclic, une organisation est une entité telle que corporation, entreprise, département d'entreprise, association, école, institution, etc à laquelle peuvent être rattachées les demandes faites par les utilisateurs.

Un ou plusieurs membres d'une organisation peuvent en être les :ref:`members-organization-admin`. Une organisation possède au minimum un administrateur.

Les :ref:`members-organization-admin` peuvent définir les champs d'intervention de leur organisation en créant des catégories (exemple : voirie, transports, etc) et des zones de responsabilité.
Quand un utilisateur crée une nouvelle demande, les coordonnées géographiques de cette demande sont toujours automatiquement précisées.
Ainsi, l'application est en mesure de lui retourner l'ensemble des organisations qui ont une zone de responsabilité sur cette position.
L'utilisateur a alors accès à des informations lui permettant de l'aiguiller vers l'organisation la plus adéquate.

.. _organizations-creation:

Création d'une organisation
---------------------------

Tout utilisateur peut créer une nouvelle organisation :

.. code-block:: bash

    POST /organizations

.. code-block:: json

    {
        "name":"Nom de l'organisation",
        "billingEmailAddress":"test@test.com",
        "notificationEmailAddress":"test@test.com"
    }

L'utilisateur devient automatiquement membre et administrateur de cette nouvelle organisation.

Pour récupérer toutes les organisations de l'application :

.. code-block:: bash

    GET /organizations

Il est possible de filtrer la requête ci-dessus sur un point géographique (voir ci-dessous : :ref:`organizations-places`) :

.. code-block:: bash

    GET /organizations?geo_coordinates=+44.851404209987386-0.5762618780136108

.. _organizations-members:

Gestion des membres
-------------------

Pour ajouter un nouveau membre à une organisation :

.. code-block:: bash

    POST /organizations/{organization}/members

.. code-block:: json

    {
        "person":"63d07fc5-f4e6-471c-a8cc-3c3f227c8c2d"
    }

Ce endpoint est réservé à un utilisateur possédant le rôle :ref:`members-organization-admin` et membre de l'organisation {organization}.

Pour récupérer les membres d'une organisation :

.. code-block:: bash

    GET /organizations/{organization}/members

Pour retirer un membre d'une organisation, un :ref:`members-organization-admin` de cette organisation exécutera la requête :

.. code-block:: bash

    DELETE /organizations/{organization}/members/{member}

.. _organizations-places:

Gestion des zones de responsabilité
-----------------------------------

Un :ref:`members-organization-admin` peut créer des zones de responsabilité, correspondant aux lieux sur lesquels cette organisation intervient :

.. code-block:: bash

    POST /organizations/{organization}/places

.. code-block:: json

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
            "srid": 4326
        }
    }

Pour récupérer toutes les zones de responsabilité de l'application :

.. code-block:: bash

    GET /places

La requête ci-dessus peut-être filtrée sur une organisation donnée et/ou sur un point géographique donné :

.. code-block:: bash

    GET /places?geo_coordinates=+44.851404209987386-0.5762618780136108&organization={organization}

.. _organizations-categories:

Gestion des catégories
----------------------

Les catégories sont les secteurs d'activité d'une organisation. Un :ref:`members-organization-admin` peut créer une nouvelle catégorie en lui donnant un nom, une couleur et une icône. L'icône sera choisie dans  `le jeu d'icônes de Font Awesome <http://fontawesome.io/icons/>`_.


.. code-block:: bash

    POST /organizations/{organization}/categories

.. code-block:: json

    {
        "name":"Nom de la catégorie",
        "color":"#ff0000",
        "icon":"fa-bug"
    }

Les 3 propriétés name, color et icon peuvent être éditées par une requête PATCH (voir : :ref:`technical-patch`).

Pour récupérer l'ensemble des catégories de l'application :

.. code-block:: bash

    GET /categories

La requête ci-dessus peut-être filtrée sur une organisation donnée et/ou sur un point géographique donné :

.. code-block:: bash

    GET /categories?geo_coordinates=+44.851404209987386-0.5762618780136108&organization={organization}

.. _organizations-relationships:

Gestion des partenariats
------------------------

Une organisation peut avoir des partenaires, c'est-à-dire des organisations qui lui sont rattachées et à qui l':ref:`members-organization-admin` de l'organisation pourra déléguer des demandes. La relation de partenariat est unilatérale : si une organisation A est partenaire d'une organisation B, B n'est pas forcément partenaire de A.

Pour ajouter un nouveau partenaire à l'organisation, un administrateur de l'organisation requêtera sur le endpoint :

.. code-block:: bash

    POST /organizations/{organization}/relationships

.. code-block:: json

    {
        "organization":"84d36093-b8bc-47ad-bc8a-a043b3e301a9"
    }

Pour récupérer les partenaires d'une organisation :

.. code-block:: bash

    GET /organizations/{organization}/relationships

Cette requête ne peut être exécutée que par un administrateur de l'organisation.
