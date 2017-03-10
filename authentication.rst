.. _authentication:

Authentification et connexion
=============================

L'API Keyclic se base sur le standard JSON Web Token pour la sécurisation de l'échange des données. Toute requête à l'API est nécessairement effectuée en fournissant un jeton d'accès (accessToken) permettant au serveur de vérifier l'identité de l'utilisateur. Un endpoint permet à l'utilisateur d'obtenir ce jeton d'accès en fournissant son login et son mot de passe. Cette section détaille la création d'un compte, l'obtention et l'utilisation d'un accessToken, et la modification d'un compte utilisateur.

Pour plus d'informations sur le standard JWT, voir : `le site officiel de JSON Web Tokens <https://jwt.io/>`_.

.. _authentication-account-creation:

Création d'un compte utilisateur
--------------------------------

Un nouveau compte utilisateur est créé avec la requête :

.. code-block:: bash

    POST /security/register

Exemple :

.. code-block:: json

    {
        "email":"test@test.com",
        "password":"test"
    }

Le nouvel utilisateur se voit attribuer un identifiant unique et le rôle ROLE_USER, lui permettant d'utiliser les fonctionnalités de base de l'API.

.. _authentication-login:

Connexion
---------

La connexion consiste à envoyer ses credentials au serveur afin d'obtenir en retour un accessToken qui sera utilisé pour les requêtes ultérieures.

La connexion s'effectue avec la requête :

.. code-block:: bash

    POST /security/login

Exemple :

.. code-block:: json

    {
        "login":"test@test.com",
        "password":"test"
    }

Si les credentials sont reconnus par le serveur, celui-ci retourne un accessToken qui sera utilisé par l'utilisateur pour ses futures requêtes.

.. _authentication-using-token:

Utilisation du token
--------------------

La quasi-totalité des requêtes à l'API nécessitent que l'utilisateur soit authentifié, c'est-à-dire qu'il fournisse son accessToken. Le token est envoyé dans l'en-tête Authorization de la requête, préfixé par Bearer.

Par exemple, pour récupérer la liste des feedbacks de l'application com.keyclic.app, un utilisateur utilise le endpoint :

.. code-block:: bash

    GET /feedbacks

.. code-block:: bash

    Request headers :
        X-Keyclic-App : com.keyclic.app
        Authorization : Bearer eyJhbGciOiJSUzI1N0wAwe5O4CQhebI

(Pour une meilleure lisibilité, nous avons réduit la chaîne de caractères de l'accessToken dans l'exemple ci-dessus).

Toutes les requêtes à l'API Keyclic nécessitent l'envoi d'un accessToken dans les headers, à l'exception évidente des endpoints suivants :

- création d'un compte (POST /security/register)
- login (POST /security/login)
- demande de changement de mot de passe
- changement de mot de passe (POST /security/password/change/{changePasswordToken})

.. _authentication-password-change:

Modification du mot de passe
----------------------------

Un utilisateur qui souhaite modifier son mot de passe procède en deux étapes.

Il effectue d'abord une demande de changement de mot passe :

.. code-block:: bash

    POST /security/password/change-request

Exemple :

.. code-block:: json

    {
        "email":"test@test.com"
    }

Cette requête envoie un email à l'utilisateur contenant un lien se terminant par un token de vérification. Exemple de lien :

.. code-block:: bash

    https://domain.com/#/password-reset/jrtVqBLxxoSA0c2hpsOBN-JQGQHGN3YXsKPMG1PWWWA

Dans le lien ci-dessus, le nom de domaine dépend de la configuration de l'application et jrtVqBLxxoSA0c2hpsOBN-JQGQHGN3YXsKPMG1PWWWA est le jeton de changement de mot de passe.

L'utilisateur peut ensuite changer son mot de passe avec :

.. code-block:: bash

    POST /security/password/change/-VtYMG0VnU8vHJdKUC_AqA_XpypI9kd8OmOvWj4NYMw

Exemple :

.. code-block:: json

    {
        "password":"password"
    }

.. _authentication-user-edition:

Modification des données utilisateur
------------------------------------

Pour les données autres que le mot de passe, l'utilisateur requêtera sur le endpoint :

.. code-block:: bash

    PATCH /people/8fa7a1aa-dc61-42df-9233-b103fc34771d

Par exemple, pour modifier son nom :

.. code-block:: json

    [
	    {
		    "op":"replace",
		    "path":"/familyName",
		    "value":"Nom de famille"
	    }
    ]

Les champs qu'un utilisateur peut modifier sont : son nom (familyName), son prénom (givenName), sa photo (image), son travail (job), son adresse email (email).


