# Guide d'administration :  Contrôle d'accès à base de rôles

Le contrôle d'accès dans CloudMC est atteint par un modèle flexible et multi-titulaire que fournit une manière simple pour diriger les permissions à tous les niveaux d'une hiérarchie d'organisations et d'environnements.  La fonctionnalité du contrôle d'accès à base de rôles que CloudMC vient avec permet un niveaux de contrôle très fine sur les permissions qui sont accordées aux utilisateurs.

## Définitions
- **Permission :** Une autorisation pour exécuter une tâche.  **Les permissions de système** régissent l'accès à la fonctionalité de la console de CloudMC, **les permissions d'environnement** régissent l'accès à les ressources d'un service

- **Rôle système :** Une collection composée de permissions de système dedans une organisation.  CloudMC vient avec cinq **rôles fixes** celles qui ne peuvent être modifiées, et **rôles customisés**, peuvent être crées.  Généralement, les rôles système se réfèrent juste comme "les rôles"

- **Portée :**  L'organisation ou organisations dont s'applique un rôle système

- **Organisation :**  Un groupement de utilisateurs reliés.  Une installation base de CloudMC vient avec l'organisation System

- **Utilisateur :**  Le compte utilisateur est la façon de se connecter un particulière au portal CloudMC.  Un utilisateur est toujours assigné un rôle primaire dans une organisation.  Un utilisateur peut être assigné des rôles additionels, qui peuvent être portés à une ou plusieurs organsiations.

- **Environnemnt :** Une unité logique dedans une organisation, utilisée pour isoler et grouper des ressources sûrement.  L'accès est contrôlé par une combinaison de rôles d'environnement et des contrôles d'accès de l'organisation.

- **Rôle d'environnement :**  Une collection de permissions d'environnement qui s'applique aux membres d'un environnement.

![user access control chart](roles_chart-en.png)

## Les rôles système
La fonctionnalité d'un rôle système est à controller l'accès à la fonctionnalité de CloudMC d'un façon simple et standard.  Un rôle système peut être assigné aux utilisateurs dans une organisation.  Le rôles système sont appliqués dans l'interface Web autant que dans le CloudMC API.  Les rôles customisés peuvent definir des permissions qui sont alignées avec les règles d'affaires, et peuvent aussi permettre la collaboration à travers l'organisation.

Tous les rôles système ont une portée défini, qui peut être un des ceux ci-après :
-

### Les rôles fixes
- Invité
- Utilisateur
- Administrateur
- Revendeur
- Opérateur

### Les rôles customisés

#### Créer un rôle customisé

## Les rôles d'environnement

## Comment assigner le rôles
