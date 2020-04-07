---
title: "Configurer la répartition de charge"
slug: configurer-la-repartition-de-charge
---


La répartition de charge permet de distribuer les requêtes entrantes sur plusieurs ressources de calcul. Ceci permet d'améliorer la performance ainsi que la disponibilité à travers un niveau de redondance. Dans le contexte de cloud.ca, cet objectif est réalisé en associant des règles de répartition de charge à une adresse IP publique d'un VPC.

**Note :**  Il n'est pas possible de configurer des règles de répartition de charge sur une adresse IP publique qui est déjà utilisée à des fins de NAT source, VPN ou redirection de port. De plus, un seul tiers au sein d'un VPC peut avoir des adresses IP pour des fins de répartition de charge.

Dans l'example suivant, nous allons mettre en place un répartition de charge sur le traffic HTTP (port TCP 80), pour les instances *web1* et *web2* en utilisant un algorithme d'ordonnancement en [tourniquet](https://fr.wikipedia.org/wiki/Round-robin_(informatique)).

1. Aller à la page de **Services**
1. Sélectionnez l'environnement approprié dans la barre de navigation de gauche.
1. Choisissez l'onglet de **Réseautage**.
1. A partir du VPC cible, cliquez sur le bouton **IP publiques**.
1. Cliquez sur le bouton **Acquérir une adresse IP**. <br>
![Acquérir une adresse IP](/assets/load-balancing-fr-1.jpeg) <br><br>
![Adresse IP acquise](/assets/load-balancing-fr-2.jpeg)
1. Ajoutez une règle de répartition de charge à l'adresse IP nouvellement acquise :
![Règles de répartition de charge](/assets/load-balancing-fr-3.jpeg)
![Ajouter une règle de répartition de charge](/assets/load-balancing-fr-4.jpeg)
1. Nommez votre règle. spécifiez le port TCP pour la répartition de charge et sélectionnez le tier contenant les instances cibles :
![Ajouter une règle de répartition, information de base](/assets/load-balancing-fr-5.jpeg)
1. Sélectionnez l'algorithme de répartition désiré. Dans cet exemple, nous ne spécifions aucune méthode de persistance et nous ciblons le protocole TCP :
![Ajouter une règle de répartition, règles](/assets/load-balancing-fr-6.jpeg) <br><br>
![Ajouter une règle de répartition, configuration](/assets/load-balancing-fr-7.jpeg)
1. Sélectionnez ensuite les instances sur lesquelles vous voulez répartir le traffic puis cliquez sur **Terminer** : <br>
![Ajouter une règle de répartition, instances](/assets/load-balancing-fr-8.jpeg)
1. Le système confirmera la création de la nouvelle règle:
![Règle de répartition de charge crée](/assets/load-balancing-fr-9.jpeg)
1. Cliquez le lien *Adresses IP Publiques* dans la piste de navigation et validez la bonne création de la règle de répartition de charge:
![Liste des adresses IP publiques](/assets/load-balancing-fr-10.jpeg)
1. Finalement, validez le bon fonctionnement de la règle de répartition en laissant rouler du trafic et en vérifiant que chaque instance sert une part égale des requêtes. Une façon d'effectuer cela est de forcer chaque serveur à retourner un réponse légèrement différente (ex.: le nom de l'hôte) dans sa réponse (ou dans les entêtes de réponse).
