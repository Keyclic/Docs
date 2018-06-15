.. _integration:

Intégration
===========

Webhooks
--------

Au contraire d’une API qui requiert que vous l’interrogiez en continu, les Webhooks sont un moyen d’appeler
une application tierce (un service web) lorsqu’un événement défini se produit dans le service Keyclic.

C’est un moyen très efficace de recevoir des notifications en s’affranchissant d’une vérification continuelle.

Les Webhooks peuvent avoir de nombreuses applications, telles que :

    - collecter les rapports créés pour votre data-warehouse
    - synchroniser les rapports et opérations pour votre GMAO
    - envoyer des notifications

Création et configuration de webhooks
-----------------------------------------

Les webhooks peuvent être crée sur demande auprès de notre service. Il est possible de créer autant de
webhooks que nécessaire pour une organisation (un webhook par événement et/ou plusieurs webhooks pour un même événement).

Un webhook est composé de l'événement pour lequel vous souhaitez être notifié et d'une URL à
laquelle sera envoyée la notification.

Types d'événements
------------------

Ceci est une liste de tous les types d'événements pouvant être configuré :

+------------------------------+-----------------------------------------------------------+
| Événement                    | Description                                               |
+==============================+===========================================================+
| **report_created**           | Création d'un nouveau rapport                             |
+------------------------------+-----------------------------------------------------------+
| **report_state_changed**     | Changement de statut d'un rapport                         |
+------------------------------+-----------------------------------------------------------+
| **operation_created**        | Création d'une nouvelle intervention                      |
+------------------------------+-----------------------------------------------------------+
| **operation_state_changed**  | Changement de statut d'une intervention                   |
+------------------------------+-----------------------------------------------------------+
| **operation_removed**        | Suppression d'une intervention                            |
+------------------------------+-----------------------------------------------------------+


Recevoir une notification de webhook
------------------------------------

Une notification de webhook est envoyée en tant que JSON dans le corps d'une requête HTTP POST sur l'url configurée dans le webhook,
elle est composé du nom de l'événement (event) et de l'object concerné par l'événement (payload), l'object pouvant varier en fonction de l'événement.

*Exemple de notification de webhook pouvant être recu lors de la création d'un nouveau rapport (Exemple partiel).*

.. code-block:: json

    {
        "event":"report_created",
        "payload": {
            "type": "Report",
            "id": "b0e7e28f-5b91-4c73-875e-8f34aa03553a",
            "state": "NEW",
            "createdAt": "2018-02-27T10:00:00+02:00",
            "updatedAt": "2018-02-27T10:00:00+02:00",
            _links: {
                feedback: "...",
                operations: "...",
                organization: "...",
                tracking: "...",
            },
            _embedded: {
                stateTransitions: "...",
                tracking: "..",
            }
        }
    }

