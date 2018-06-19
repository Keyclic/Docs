.. _integration:

Intégration
===========

Webhooks
--------

À la différence d'une API qui requiert des interrogations en continu, le service Keyclic propose des webhooks
lorsque certains événements se produisent (voir la liste plus bas).

C’est un moyen simple et efficace d'appeler un service ou une application tierce afin de recevoir des notifications
et de s’affranchir d’une vérification continuelle.

Les Webhooks peuvent avoir de nombreux usages, tels que :

    - collecter les rapports créés pour votre data-warehouse,
    - synchroniser les rapports et opérations avec votre SI (ex: GMAO, ...),
    - envoyer des notifications.

Création et configuration de webhooks
-----------------------------------------

Les webhooks peuvent être créés sur demande auprès de notre service.

Un webhook est composé de l'évènement pour lequel vous souhaitez être notifié et d'une URL à
laquelle sera envoyée la notification.

Plusieurs webhooks pour chaque type d'évènements peuvent être créés de façon illimitée
(plusieurs webhooks peuvent être créés pour un type d'événement particulier).

Types d'évènements
------------------

+------------------------------+-----------------------------------------------------------+
| Évènement                    | Description                                               |
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

Réception d'une notification de webhook
---------------------------------------

Une notification de webhook est envoyée au format JSON dans le corps d'une requête HTTP POST sur l'url configurée dans le webhook.
Elle est composée du nom de l'évènement (event) et de l'objet concerné par l'évènement (payload), l'objet pouvant varier en fonction de l'évènement.

note : L'objet concerné possède la même sérialisation que ce soit via une requête d'API ou lors d'une notification d'un webhook.

.. code-block:: json

    {
        "event":"report_created",
        "payload": {
            "type": "Report",
            "id": "b0e7e28f-5b91-4c73-875e-8f34aa03553a",
            "state": "NEW",
            "createdAt": "2018-02-27T10:00:00+02:00",
            "updatedAt": "2018-02-27T10:00:00+02:00",
            "_links": {
                "feedback": "...",
                "operations": "...",
                "organization": "...",
                "tracking": "...",
            },
            "_embedded": {
                "stateTransitions": "...",
                "tracking": "..",
            }
        }
    }

*Exemple de notification de webhook pouvant être reçue lors de la création d'un nouveau rapport (Exemple partiel).*
