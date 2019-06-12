.. _notifications:

Notifications
=============

Le service Keyclic peut notifier des utilisateurs après que certaines actions sont réalisées.

.. _notifications-table:

Type des notifications émises suivant les actions
-------------------------------------------------

+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Action                         | Cible                                                   | Push  | Mur   | Email |
+================================+=========================================================+=======+=======+=======+
| Création de compte             | L'utilisateur                                           |   N   |   N   |   O   |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Demande de changement          | L'utilisateur                                           |   N   |   N   |   O   |
| de mot de passe                |                                                         |       |       |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Commentaire d'une observation  | L'émetteur de l'observation                             |   O   |   O   |   N   |
|                                |                                                         |       |       |       |
|                                | Les personnes qui ont commenté ou soutenu l'observation |       |       |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Rapport créé                   | Les administrateurs                                     |   O   |   O   |   O   |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Rapport accepté                | L'émetteur de l'observation                             |   O   |   O   |   N   |
|                                |                                                         |       |       |       |
|                                | Les personnes qui ont commenté ou soutenu l'observation |       |       |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Rapport clôturé                | L'émetteur de l'observation                             |   O   |   O   |   N   |
|                                |                                                         |       |       |       |
|                                | Les personnes qui ont commenté ou soutenu l'observation |       |       |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Rapport refusé                 | L'émetteur de l'observation                             |   O   |   O   |   N   |
|                                |                                                         |       |       |       |
|                                | Les personnes qui ont commenté ou soutenu l'observation |       |       |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Rapport delégué                | Les administrateurs                                     |   O   |   O   |   O   |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Ajout d'un document au rapport | Les administrateurs                                     |   O   |   O   |   N   |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Intervention assignée          | Le membre assigné à l'intervention                      |   O   |   O   |   O   |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Intervention terminée          | L'administrateur ayant assigné l'intervention           |   O   |   O   |   N   |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Rappel d'intervention          | Les administrateurs                                     |   O   |   O   |   N   |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Commentaire d'une intervention | Le membre assigné à l'intervention                      |   O   |   O   |   N   |
|                                | L'administrateur ayant assigné l'intervention           |       |       |       |
|                                |                                                         |       |       |       |
|                                | Les members qui ont commenté l'intervention             |       |       |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Observation à évaluer          | L'évaluateur                                            |   O   |   O   |   N   |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+

Lorsqu'une des cibles fait une action déclenchant une notification, il est n'est pas notifié.
Par exemple, si l'émetteur d'une observation commente son observation, il ne recevra pas de notification lui disant qu'il a commenté l'observation.
