---
title: "Gérer mes objets avec l'outil de ligne de commande Swift"
slug: gerer-mes-objets-avec-outil-de-ligne-de-commande-swift
---

L'outil de ligne de command fourni par Swift est une façon pratique pour interagir avec vos environnements de stockage objet. Grâce à de simple commandes, vous pouvez gérer vos **récipients** et **objets** à partir de scripts, permettant ainsi d'automatiser des tâches répétitives. D'autres alternatives valides sont l'utilisation de l'[interface web du portail](manage-my-objects-using-the-self-service-portal.md) et l'utilisation de l'API du service de stockage objet.

### Configurer votre environnement

Premièrement, vous allez devoir installer le [CLI OpenStack](https://docs.openstack.org/newton/user-guide/common/cli-install-openstack-command-line-clients.html) générique ou le [CLI de Swift](https://www.swiftstack.com/docs/integration/python-swiftclient.html).


Pour installer le CLI OpenStack générique, vous allez devoir installer le paquet **python-openstackclient**. Pour installer le CLI de Swift, vous devrez installer les paquets **python-keystoneclient** et **python-swiftclient**.

Ensuite, il va vous falloir configurer les variables d'environnement pour permettre la connection vers vos environnements de stockage objet. Vous pouvez récupérer vos identifiants en suivant les instructions sur cette page : [Comment obtenir les informations pour l'API de stockage objet?](how-to-obtain-object-storage-api-credentials.md) Utilisez la section **Identifants pour le service de stockage objet avec Keystone v3 (défaut)**.

Si vous voulez gérer plusieurs environnements Swift avec le CLI, vous pouvez créer un script shell pour chaque environnement, contenant les variables d'environnement appropriées, et utiliser la [commande source (en)](http://bash.cyberciti.biz/guide/Source_command).

### Gestion des récipients et objets

#### Les exemples suivants utilisent tous le CLI de Swift.

Pour énumérer les récipients dans l'environnement actif, exécutez la commande suivante :

```
swift list
```

Pour énumérer les objets dans un récipient :

```
swift list <nom_du_récipient>
```

Pour avoir un résultat détaillé (incluant la taille des objets et leur date de dernière modification) :

```
swift list -l <nom_du_récipient>
```

Pour créer un nouveau récipient :

```
swift post <nom_du_récipient>
```

Pour créer un nouveau récipient avec une stratégie de stockage spécifique :

```
swift post -H 'X-Storage-Policy: <policy_name>' <bucket_name>
```

Pour télé-transférer un fichier dans un récipient (les jokers sont permis pour si vous désirez télé-transférer plusieurs fichiers à la fois) :

```
swift upload <nom_du_récipient> <fichier_local>
```

Pour télécharger un objet à partir d'un récipient :

```
swift download <nom_du_récipient> <nom_de_l'objet>
```

Pour effacer un objet d'un récipient :

```
swift delete <nom_du_récipient> <nom_de_l'objet>
```

Pour effacer un récipient :

```
swift delete <nom_du_récipient>
```

Pour obtenir les statistiques d'un récipient :

```
swift stat <nom_du_récipient>
```

Pour obtenir les statistiques de tous les récipients :

```
swift stat
```

Pour une liste exhaustive de toutes les options de la commande Swift, veuillez vous référer à son [manuel d'utilisation](https://docs.openstack.org/ocata/cli-reference/swift.html).
