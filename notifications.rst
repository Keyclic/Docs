.. _notifications:

Notifications
=============

Le service Keyclic peut notifier des utilisateurs après que certaines actions sont réalisées.

.. _notifications-table:

Type des notifications émises suivant les actions
-------------------------------------------------

+--------------------------------+-------------------------+------------------------------------------------------------------------+
| Action                         | Notification Type       | Target                                                                 |
+================================+=========================+========================================================================+
| Observation à modérer          | Push smartphone         | Les modérateurs                                                        |
+--------------------------------+-------------------------+------------------------------------------------------------------------+
| Commentaire d'une observation  | Push smartphone         | L'émetteur de l'observation                                            |
|                                |                         |                                                                        |
|                                |                         | Les personnes qui ont commenté ou soutenu l'observation                |
+--------------------------------+-------------------------+------------------------------------------------------------------------+
| Rapport créé                   | Email + Push smartphone | Les administrateurs                                                    |
+--------------------------------+-------------------------+------------------------------------------------------------------------+
| Rapport accepté                | Push smartphone         | L'émetteur de l'observation                                            |
|                                |                         |                                                                        |
|                                |                         | Les personnes qui ont commenté ou soutenu l'observation                |
+--------------------------------+-------------------------+------------------------------------------------------------------------+
| Rapport fermé                  | Push smartphone         | L'émetteur de l'observation                                            |
|                                |                         |                                                                        |
|                                |                         | Les personnes qui ont commenté ou soutenu l'observation                |
+--------------------------------+-------------------------+------------------------------------------------------------------------+
| Rapport refusé                 | Push smartphone         | L'émetteur de l'observation                                            |
|                                |                         |                                                                        |
|                                |                         | Les personnes qui ont commenté ou soutenu l'observation                |
+--------------------------------+-------------------------+------------------------------------------------------------------------+
| Rapport delégué accepté        | Push smartphone         | Les administrateurs du rapport parent                                  |
+--------------------------------+-------------------------+------------------------------------------------------------------------+
| Rapport delégué fermé          | Push smartphone         | Les administrateurs du rapport parent                                  |
+--------------------------------+-------------------------+------------------------------------------------------------------------+
| Rapport delégué refusé         | Push smartphone         | Les administrateurs du rapport parent                                  |
+--------------------------------+-------------------------+------------------------------------------------------------------------+
| Intervention assignée          | Push smartphone         | Le membre assigné à l'intervention                                     |
+--------------------------------+-------------------------+------------------------------------------------------------------------+
| Intervention résolue           | Push smartphone         | Les administrateurs                                                    |
+--------------------------------+-------------------------+------------------------------------------------------------------------+
| Commentaire d'une intervention | Push smartphone         | Le membre assigné à l'intervention                                     |
|                                |                         |                                                                        |
|                                |                         | Les members qui ont commenté l'intervention                            |
+--------------------------------+-------------------------+------------------------------------------------------------------------+
| Observation à évaluer          | Push smartphone         | L'évaluateur                                                           |
+--------------------------------+-------------------------+------------------------------------------------------------------------+
| Export de rapport(s)           | Email                   | L'administrateur qui a fait la demande d'export                        |
+--------------------------------+-------------------------+------------------------------------------------------------------------+
