.. _applications:

Applications
============

Une *application* au cœur du service Keyclic permet de cloisonner les demandes suivant des domaines applicatifs.
Cela se traduit par l’utilisation d’applications clientes ou de sites internet spécifiques à certains métiers.

Pour le client éponyme du service, l’*application* déclarée est "com.keyclic.app", toutes les applications clientes ou sites internet utilisant cette clé auront le même cloisonnement. (Ici : l'application iPhone Keyclic, l'application Android Keyclic et le site internet https://app.keyclic.com pour les navigateurs.)

Il existe d’autres *applications* déclarées dans le service Keyclic avec d'autres clés, notamment "Vinci Mon Autoroute" disponible sur iPhone et Android.

Par exemple, depuis "Jaidemaville" (la clé est com.keyclic.city) :

 - il est impossible de lister les demandes dédiées à l’*application* Jaidemaville déclarée avec la clé "com.keyclic.app" et inversement,
 - il est impossible de lister les organisations affiliées à l’*application* Jaidemaville déclarée avec la clé "com.keyclic.app" et inversement.
