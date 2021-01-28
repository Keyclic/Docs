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
| Création de compte             | L'utilisateur                                           |       |       |   ✓   |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Demande de changement          | L'utilisateur                                           |       |       |   ✓   |
| de mot de passe                |                                                         |       |       |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Commentaire d'une demande      | L'émetteur de la demande                                |   ✓   |   ✓   |       |
|                                |                                                         |       |       |       |
|                                | Les personnes qui ont commenté ou soutenu la demande    |       |       |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Demande créée                  | Les administrateurs                                     |   ✓   |   ✓   |   ✓   |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Demande acceptée               | L'émetteur de la demande                                |   ✓   |   ✓   |       |
|                                |                                                         |       |       |       |
|                                | Les personnes qui ont commenté ou soutenu la demande    |       |       |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Demande clôturée               | L'émetteur de la demande                                |   ✓   |   ✓   |       |
|                                |                                                         |       |       |       |
|                                | Les personnes qui ont commenté ou soutenu la demande    |       |       |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Demande refusée                | L'émetteur de la demande                                |   ✓   |   ✓   |       |
|                                |                                                         |       |       |       |
|                                | Les personnes qui ont commenté ou soutenu la demande    |       |       |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Demande deléguée               | Les administrateurs                                     |   ✓   |   ✓   |   ✓   |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Ajout d'un document            | Les administrateurs                                     |   ✓   |   ✓   |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Intervention assignée          | Le membre assigné à l'intervention                      |   ✓   |   ✓   |   ✓   |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Intervention terminée          | L'administrateur ayant assigné l'intervention           |   ✓   |   ✓   |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Rappel d'intervention          | Les intervenants                                        |   ✓   |   ✓   |       |
|                                |                                                         |       |       |       |
|                                | L'émetteur de la demande                                |       |       |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Commentaire d'une intervention | Le membre assigné à l'intervention                      |   ✓   |   ✓   |       |
|                                | L'administrateur ayant assigné l'intervention           |       |       |       |
|                                |                                                         |       |       |       |
|                                | Les members qui ont commenté l'intervention             |       |       |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+
| Demande à évaluer              | L'évaluateur                                            |   ✓   |   ✓   |       |
+--------------------------------+---------------------------------------------------------+-------+-------+-------+

Lorsqu'une des cibles fait une action déclenchant une notification, il n'est lui-même pas notifié.
Par exemple, si l'émetteur d'une demande commente sa demande, il ne recevra pas de notification lui disant qu'il a commenté sa propre demande.
