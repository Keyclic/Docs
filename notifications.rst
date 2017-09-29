.. _notifications:

Notifications
=============

Le service Keyclic peut notifier des utilisateurs après que certaines actions sont réalisées.

.. _notifications-table:

Type des notifications émises suivant les actions
-------------------------------------------------

+------------------------------+-----------------------------------------------------+-------------------------+
| Action                       | Destinataire                                        | Type de notification    |
+==============================+=====================================================+=========================+
| Création de rapport          | Administrateurs de l'organisation                   | Email + Push smartphone |
+------------------------------+-----------------------------------------------------+-------------------------+
| Clôture du rapport           | Émetteur  du signalement (dont est issu le rapport) | Push smartphone         |
+------------------------------+-----------------------------------------------------+-------------------------+
| Assignation d'une opération  | Membre assigné à l'opération                        | Push smartphone         |
+------------------------------+-----------------------------------------------------+-------------------------+
| Exportation des rapports     | Administrateur courant de la session                | Email                   |
+------------------------------+-----------------------------------------------------+-------------------------+
| Modération d'une observation | Administrateur de l'application                     | Push smartphone         |
+------------------------------+-----------------------------------------------------+-------------------------+
