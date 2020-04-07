---
title: "Configurer la redirection de ports"
slug: configurer-la-redirection-de-ports
---

La redirection de ports permet d'établir la connectivité en provenance d'internet vers un (ou plusieurs) port d'une instance. Cette configuration est effectuée à partir d'une adresse IP publique d'un VPC dédiée à la redirection de ports.

Note: il est impossible de configurer des règles de redirection de port sur une adresse IP publique qui est déjà allouée à des fins de **Source NAT**, **VPN** ou **Répartition de charge**.

Dans l'exemple qui suit, nous activerons la redirection de port pour le protocole SSH (TCP port 22) sur l'instance *preprod-redis-01* à travers une adresse IP publique via le port 22022.

1. Allez sur la page **Services**.
1. Sélectionnez l'environment désiré dans la barre de gauche.
1. Sélectionnez l'onglet **Réseautage**.
1. Cliquez sur le bouton **IP publiques** du VPC cible dans la liste.
1. Cliquez sur **Acquérir une adresse IP**.

![Acquérir adresse IP](/assets/config-port-fwd-1-fr.jpeg)
![Adresse acquise](/assets/config-port-fwd-2-fr.jpeg)

6. Ajoutez une règle de redirection de port à l'adresse IP publique nouvellement acquise :

![Règles de redirection de port](/assets/config-port-fwd-3-fr.jpeg)
![Ajouter une règle de redirection de port](/assets/config-port-fwd-4-fr.jpeg)

7. Complétez l'étape #1 du formulaire **Ajouter une règle de redirection de port** et cliquez sur **Suivant**:

![Ajouter règle, étape 1](/assets/config-port-fwd-5-fr.jpeg)

8. À l'étape #2, sélectionnez l'instance qui est la cible de la règle de redirection de port et cliquez sur **Terminer**:

![Ajouter règle, étape 2](/assets/config-port-fwd-6-fr.jpeg)
![Règle ajoutée](/assets/config-port-fwd-7-fr.jpeg)

9. Validez le bon fonctionnement de la règle de redirection de port en vous connectant par SSH sur l'instance cible:

![Valider avec SSH](/assets/config-port-fwd-9-fr.jpeg)
