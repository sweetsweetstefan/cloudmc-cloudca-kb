# Guide d'administration :  Contrôle d'accès à base de rôles

Le contrôle d'accès dans CloudMC est atteint par un modèle flexible et multi-titulaire que fournit une manière simple pour diriger les permissions à tous les niveaux d'une hiérarchie d'organisations et d'environnements.  La fonctionnalité du contrôle d'accès à base de rôles que CloudMC vient avec permet un niveaux de contrôle très fine sur les permissions qui sont accordées aux utilisateurs.

## Définitions
- **Permission :** Une autorisation pour exécuter une tâche.  **Les permissions de système** régissent l'accès à la fonctionalité de la console de CloudMC, **les permissions d'environnement** régissent l'accès à les ressources d'un service

- **Rôle système :** Une collection composée de permissions de système dedans une organisation.  CloudMC vient avec **rôles fixes** celles qui ne peuvent être modifiées, et **rôles personnalisés**, peuvent être crées.  Généralement, les rôles système se réfèrent juste comme "les rôles"

- **Portée :**  L'organisation ou organisations dont s'applique un rôle système

- **Organisation :**  Un groupement de utilisateurs reliés.  Une installation base de CloudMC vient avec l'organisation System

- **Utilisateur :**  Le compte utilisateur est la façon de se connecter un particulière au portal CloudMC.  Un utilisateur est toujours assigné un rôle primaire dans l'organisation où le compte est crée.  Un utilisateur peut être assigné des rôles additionels, qui peuvent être portés à une ou plusieurs organsiations.

- **Environnemnt :** Une unité logique dedans une organisation, utilisée pour isoler et grouper des ressources sûrement.  L'accès est contrôlé par une combinaison de rôles d'environnement et des contrôles d'accès de l'organisation.

- **Rôle d'environnement :**  Une collection de permissions d'environnement qui s'applique aux membres d'un environnement.

![user access control chart](roles_chart-en.png)

## Les rôles système
La fonctionnalité d'un rôle système est à controller l'accès à la fonctionnalité de CloudMC d'un façon simple et standard.  Un rôle système peut être assigné aux utilisateurs dans une organisation, et peut aussi permettre la collaboration à travers l'organisation.  Le rôles système sont appliqués dans l'interface Web autant que dans le CloudMC API.  Les rôles personnalisés peuvent être crées avec des permissions qui sont alignées avec les règles d'affaires.

Tous les rôles système ont une portée défini, qui peut être un des ceux ci-après :
- Toutes les organisations dans CloudMC
- Toutes les organisations de premier niveau
- Une organisation spécifique, pas ses sous-organisations
- Une organisation et toutes ses sous-organisations
- Seulement les sous-organisations d'une organisation spécifique
- Toutes les organisations avec un étiquette specifique

En utilisant les étiquettes, la portée d'un rôle assigné peut être augmentée automatiquement aux organisations qui reçois l'étiquette, et retiré lorsque l'ettiquette est supprimée.  Cette fonctionnalité rendre possible les scénarios où la portée d'un role se change dynamiquement selon les règles d'affaires.

### Les rôles fixes
Les rôles fixes incorporés dans CloudMC s'appliquent à un vaste gamme de cases d'utilisation.  Ils peut être assignés au rôle primary d'un utilisateur, aussi bien qu'un rôle additionel.

Un sommaire de chaque rôle fixe quand il est appliqué au rôle primaire :
- **Invité :**  Un rôle lecture seule.  Peut voir les ressources dans les environnements duquels l'utilisateur est membre
- **Utilisateur :**  Peut créer environnements nouveaux avec les connexions de service existant, et gérer ceux environnements possédés par l'utilisateur
- **Administrateur :**  Peut gérer l'organisation.  Peut gérer tous les environnements dans toutes les connexions de service.  Pas capable ni de voir les sous-organisations ni de créer des nouvelles sous-organsiations
- **Revendeur :** Peut gérer l'image de marque et la tarification pour l'organisation et ses sous-organisations, et peut créer des sous-organisations dans l'organisation.  Pas capable de créer des nouvelles organsiations
- **Opérateur :** Peut créer des organisations et des sous-organisations, gérer les connexions de service, les quotas de service, les engagements, et a le plein accès aux toutes autres organisations, ressources et paramètres du système

Chaque rôle fixe a un défaut portée :
- Invité, Utilisateur, et Administrateur :  Seulement l'organisation dedans est crée l'utilisateur
- Revendeur : L'organisation dedans es crée l'utilisateur et toutes ses sous-organisations
- Opérateur : Toutes les organisations

Comme l'illustre le diagramme ci-dessous, en monter dans le hiérarchie chaque rôle reçoit toutes les privilèges de ceux qui prècedent :

![permissions chart](permissions-en.png)

### Les rôles personnalisés
Le rôle primaire de l'utilisateur doit être un des rôles fixes incorporés, jamais un rôle personnalisé.

#### Créer un rôle personnalisé

## Les rôles d'environnement

## Comment assigner le rôles
