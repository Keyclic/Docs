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
| Création de compte             | L'utilisateur                                           |   ⨯   |   ⨯   |   ✓   |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Demande de changement          | L'utilisateur                                           |   ⨯   |   ⨯   |   ✓   |
| de mot de passe                |                                                         |       |       |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Commentaire d'une observation  | L'émetteur de l'observation                             |   ✓   |   ✓   |   ⨯   |
|                                |                                                         |       |       |       |
|                                | Les personnes qui ont commenté ou soutenu l'observation |       |       |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Rapport créé                   | Les administrateurs                                     |   ✓   |   ✓   |   ✓   |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Rapport accepté                | L'émetteur de l'observation                             |   ✓   |   ✓   |   ⨯   |
|                                |                                                         |       |       |       |
|                                | Les personnes qui ont commenté ou soutenu l'observation |       |       |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Rapport clôturé                | L'émetteur de l'observation                             |   ✓   |   ✓   |   ⨯   |
|                                |                                                         |       |       |       |
|                                | Les personnes qui ont commenté ou soutenu l'observation |       |       |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Rapport refusé                 | L'émetteur de l'observation                             |   ✓   |   ✓   |   ⨯   |
|                                |                                                         |       |       |       |
|                                | Les personnes qui ont commenté ou soutenu l'observation |       |       |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Rapport delégué                | Les administrateurs                                     |   ✓   |   ✓   |   ✓   |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Ajout d'un document au rapport | Les administrateurs                                     |   ✓   |   ✓   |   ⨯   |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Intervention assignée          | Le membre assigné à l'intervention                      |   ✓   |   ✓   |   ✓   |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Intervention terminée          | L'administrateur ayant assigné l'intervention           |   ✓   |   ✓   |   ⨯   |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Rappel d'intervention          | Les intervenants                                        |   ✓   |   ✓   |   ⨯   |
|                                |                                                         |       |       |       |
|                                | L'émetteur de l'observation                             |       |       |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Commentaire d'une intervention | Le membre assigné à l'intervention                      |   ✓   |   ✓   |   ⨯   |
|                                | L'administrateur ayant assigné l'intervention           |       |       |       |
|                                |                                                         |       |       |       |
|                                | Les members qui ont commenté l'intervention             |       |       |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Observation à évaluer          | L'évaluateur                                            |   ✓   |   ✓   |   ⨯   |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+

Lorsqu'une des cibles fait une action déclenchant une notification, il est n'est pas notifié.
Par exemple, si l'émetteur d'une observation commente son observation, il ne recevra pas de notification lui disant qu'il a commenté l'observation.
