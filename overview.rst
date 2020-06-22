.. _overview:

Aperçu
======

Fonctionnement général
----------------------

L'application Keyclic est librement ouverte aux inscriptions. Une fois inscrit, tout utilisateur peut créer des demandes. Une demande est toujours liée à une zone de responsabilité et comporte éventuellement une position géographiqe et des données complémentaires photos, description, métadonnées, etc.

Certains utilisateurs peuvent également être regroupés au sein d'organisations. Une organisation est donc un groupe d'utilisateurs membres de la même entreprise, association, corporation, école, etc. Tout utilisateur est libre de créer sa propre organisation et d'inviter d'autres utilisateurs à en devenir membres.

Les administrateurs définissent des zones de responsabilité sur lesquelles leur organisation peut intervenir, des catégories d'intervention (exemple : plomberie, peinture, climatisation), un cycle de vie de la demande (exemple : Nouveau, En cours, Terminé) et un ensemble de paramètres concernant la confidentialité des demandes reçues.

Ainsi, quand un utilisateur crée une demande, la zone de responsabilité de cette demande permet de lui proposer les catégories et de le laisser choisir celle qui lui semble la plus adaptée.
Aussi, quand un utilisateur crée une demande, suivant les paramètres de confidentialité de l'organisation, celui-ci peut avoir le choix de la rendre publique ou privée. Si publique, la demande est visible par la communauté : ainsi, les autres utilisateurs peuvent la commenter et/ou la soutenir (Voir la page :ref:`privacy`).

La demande envoyée, elle est transmise à l'organisation concernée.

Un administrateur a donc accès à l'ensemble des demandes concernant son organisation. Pour chaque demande, il peut créer une ou plusieurs interventions, et affecter ces interventions aux membres de son organisation. Une autre possibilité est de déléguer cette demande à une organisation partenaire, le partenaire aura alors la charge de créer des interventions. Une fois que toutes les interventions ont été accomplies, il pourra considérer que le traitement est terminé et clôturer la demande.

Liens utiles
------------

- `Spécification Swagger de l'API <https://api.keyclic.com/swagger.json>`_
- `Documentation technique de l'API <https://app.swaggerhub.com/apis/Keyclic/keyclic/>`_
- `Code source du SDK client javascript <https://github.com/Keyclic/app-sdk>`_

Vocabulaire
-----------

Demande
~~~~~~~~~~~

Remarque effectuée sur le terrain par un utilisateur, pouvant porter sur un dysfonctionnement, un problème technique, une nuisance, etc. Toute demande est forcément faite en une position géographique donnée. Elle peut éventuellement comporter des photos, et être commentée et/ou soutenue par les autres utilisateurs.

Terme technique : feedback.

Voir la page :ref:`feedbacks`.

Demande (organisation)
~~~~~~~

Toute demande peut entraîner la génération d'une demande à une organisation. Une demande reprend donc toutes les informations de la demande dont elle est issu, et n'est visible et manipulable que par l'organisation concernée. C'est sur cette demande que l'organisation travaille : création d'interventions, suivi, délégation, etc.

Terme technique : report.

Voir la page :ref:`reports`

Organisation
~~~~~~~~~~~~

Groupe d'utilisateurs pouvant être une entreprise, une école, une association, un groupe de personnel d'un site, d'un chantier, etc.

Terme technique : organization.

Voir la page :ref:`organizations`.

Zone de responsabilité
~~~~~~~~~~~~~~~~~~~~~~

Aire géographique sur laquelle une organisation peut intervenir.

Terme technique : place.

Voir la section :ref:`organizations-places`.

Catégorie
~~~~~~~~~

Secteur d'activité d'une organisation.

Terme technique : category.

Voir la section :ref:`organizations-categories`.


Soutien
~~~~~~~

Une demande peut être soutenue par les utilisateurs de la communauté, afin de leur donner plus de poids.

Terme technique : contribution.

Voir la section :ref:`feedbacks-contributions`.

Intervention
~~~~~~~~~

Une intervention est une tâche créée par un administrateur sur une demande donnée. Cette tâche est assignée à un membre de l'organisation. Un rapport ne peut être clôturé que si toutes les interventions qui lui sont liées ont été accomplies (ou refusées).

Terme technique : operation.

Voir la section :ref:`reports-operations`.

Partenaires
~~~~~~~~~~~

Un administrateur peut définir des organisations partenaires, qui sont d'autres organisations auxquelles il pourra déléguer des demandes.

Terme technique : relationship.

Voir la section :ref:`organizations-relationships`.
