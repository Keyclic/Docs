.. _notifications:

Notifications
=============

Le service Keyclic peut notifier des utilisateurs après que certaines actions sont réalisées.

.. _notifications-table:

Type des notifications émises suivant les actions
-------------------------------------------------

+------------------------------+------------------------------------------------------------------------+-------------------------+
| Action                       | Destinataire                                                           | Type de notification    |
+==============================+========================================================================+=========================+
| Création de rapport          | Les administrateurs de l'organisation                                  | Email + Push smartphone |
+------------------------------+------------------------------------------------------------------------+-------------------------+
| Clôture du rapport           | L'émetteur de l'observation (dont le rapport est issu)                 | Push smartphone         |
|                              |                                                                        |                         |
|                              | Les personnes qui ont soutenu l'observation (dont le rapport est issu) |                         |
+------------------------------+------------------------------------------------------------------------+-------------------------+
| Assignation d'une opération  | Le membre assigné à l'opération                                        | Push smartphone         |
+------------------------------+------------------------------------------------------------------------+-------------------------+
| Exportation des rapports     | L'administrateur courant de la session                                 | Email                   |
+------------------------------+------------------------------------------------------------------------+-------------------------+
| Modération d'une observation | Les administrateurs de l'application                                   | Push smartphone         |
+------------------------------+------------------------------------------------------------------------+-------------------------+

