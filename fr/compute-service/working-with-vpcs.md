---
title: "Gestion des VPCs"
slug: gestion-des-vpcs
---


Pour une entrée en matière à propos des VPCs, veuillez vous référer à l'[article suivant](what-is-a-vpc.md).

### Création d'un VPC

**Note :** Cette opération est uniquement disponible si votre compte utilisateur possède le rôle **Environment Admin** sur l'environnement cible.

1. Allez sur la page **Services**.
1. Sélectionnez l'environnement désiré dans la barre de gauche.
1. Sélectionnez l'onglet **Réseautage**.
1. Cliquez sur **Ajouter un VPC**.
1. Complétez le formulaire d'ajout de VPC :
   1. **Nom :** Nom du VPC (ex. prod-vpc1)
   1. **Description :** Description du VPC (ex. Production site A)
   1. **Zone :** le nom de la zone dans cloud.ca où vous voulez déployer votre VPC (ex. QC-1)
   1. **CIDR :** Sous-réseau assigné à votre VPC. Présentement non-éditable.
   1. **Domaine Réseau :** Nom de domaine pour vos instances.
   1. **L’offre de VPC :** Choisissez le niveau de service pour ce VPC:
      - **Default VPC Offering :**  VPC de base qui fournit jusqu'à 4 sous-réseaux (tiers), un access VPN, NAT public, la translation de ports et la répartition de charge.
1. Cliquez sur **Terminer**.

### Ajout d'un tiers à l'intérieur d'un VPC

**Note :** Cette opération est uniquement disponible si votre compte utilisateur possède le rôle **Environment Admin** sur l'environnement cible.

1. Allez sur la page **Services**.
1. Sélectionnez l'environnement désiré dans la barre de gauche.
1. Sélectionnez l'onglet **Réseautage**.
1. Cliquez sur le bouton **Tiers** du VPC cible dans la liste.
1. Cliquez sur **Ajouter un tiers**.
1. Complétez le formulaire d'ajout d'un tiers :
   1. **Nom :** Nom du tiers (ex. net-web1)
   1. **Description :** Une courte description de contenu du tiers (ex. Serveurs Web)
   1. **Sélectionnez une offre réseau :** Choisissez le niveau de service pour ce tiers
      - **Standard Tier :**  Réseau régulier qui supporte le NAT et la translation de port. Idéal pour les applications internes comme les serveurs de base de données.
      - **Load Balanced Tier :**  Similar au "Standard Tier" mais offre en plus la possibilité de faire de la répartition de charge entre plusieurs instances déployées sur ce ties, via des règles de répartition de charge appliquées sur des adresse IP publiques. A noter que cette offre réseau ne peut s'appliquer qu'à un seul Tiers à l'intérieur d'un VPC.
   1. **ACL :** Liste d’accès pour gérer les communications entre les tiers du VPC.
      - **default_allow :**  Permet tout le traffic de/vers un autre tier du VPC.
      - **default_deny  :**  Empêche tout traffic de/vers un autre tier du VPC.
1. Cliquez sur **Terminer**.

### VPN site-à-site

Un VPN site-à-site permet l’interconnection:

   - De plusieurs VPCs
   - De votre bureau vers le VPC
   - D’un autre fournisseur vers votre VPC

La configuration d’un VPN site-à-site est présentement indisponible sur le portail d’administration de cloud.ca. Si vous avez besoin d’une telle configuration, contactez l'équipe de support de cloud.ca, qui sera en mesure de vous aider.

##### Considérations :

- Un sous-réseau du VPC ne doit pas interférer avec les adresses du site distant
- Le VPN utilise le protocole IPsec
- La sécurité du VPN est géré via des listes d’accès (ACL)
