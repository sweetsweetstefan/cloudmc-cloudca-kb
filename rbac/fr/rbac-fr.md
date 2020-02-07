# Guide d'administration :  Contrôle d'accès à base de rôles

Le contrôle d'accès dans CloudMC est obtenu par un modèle flexible et multi-tenancier que fournit une manière simple pour gérer les permissions à tous les niveaux d'une hiérarchie d'organisations et d'environnements.  La fonctionnalité du contrôle d'accès à base de rôles de CloudMC permet un niveaux de contrôle précis sur les permissions qui sont accordées aux utilisateurs.

## Définitions
- **Permission :** Une autorisation pour exécuter une tâche.  **Les permissions de système** régissent l'accès à la fonctionalité de la console de CloudMC, **les permissions d'environnement** régissent l'accès aux ressources d'un service.

- **Rôle système :** Une collection composée de permissions de système à l'intérieur d'une organisation.  CloudMC vient avec des **rôles fixes** qui ne peuvent être modifiés, et permet la création de **rôles personnalisés**.  Généralement, les rôles système sont simplement nommés ≪les rôles≫.

- **Portée :**  L'organisation ou les organisations auxquelles un rôle système s'applique.

- **Organisation :**  Un groupement d'utilisateurs reliés.  Une installation base de CloudMC vient avec l'organisation **System**.

- **Utilisateur :**  Le compte utilisateur est la façon de se connecter au portal CloudMC.  Un utilisateur est toujours assigné un rôle primaire dans l'organisation où son compte est crée.  Un utilisateur peut avoir des rôles additionels assignés, qui peuvent avoir une porté à une ou plusieurs organisation.

- **Environnement :** Une unité logique dedans une organisation, utilisée pour isoler et grouper des ressources sûrement.  L'accès est contrôlé par une combinaison de rôles d'environnement et des contrôles d'accès de l'organisation.

- **Rôle d'environnement :**  Une collection de permissions d'environnement qui s'applique aux membres d'un environnement.

![user access control chart](roles_chart-en.png)

## Les rôles système

La fonctionnalité d'un rôle système permet de controller l'accès à la fonctionnalité de CloudMC d'un façon simple et standard.  Un rôle système peut être assigné aux utilisateurs dans une organisation, et peut aussi permettre la collaboration à travers d'autres organisations.  Le rôles système sont appliqués dans l'interface Web autant que dans l'API CloudMC.  Les rôles personnalisés peuvent être définis avec des permissions qui sont alignées avec les règles d'affaires.

Tous les rôles système ont une portée définie, qui peut être une des celles-ci :
- Toutes les organisations dans CloudMC
- Toutes les organisations de premier niveau
- Une organisation spécifique, sans ses sous-organisations
- Une organisation avec toutes ses sous-organisations
- Seulement les sous-organisations d'une organisation spécifique
- Toutes les organisations avec un étiquette specifique

En utilisant les étiquettes, la portée d'un rôle assigné peut être augmentée automatiquement aux organisations qui reçoivent l'étiquette, et retiré lorsque l'éttiquette est supprimée.  Cette fonctionnalité rend possible les scénarios où la portée d'un rôle se change dynamiquement selon les règles d'affaires.

### Les rôles fixes
Les rôles fixes incorporés dans CloudMC s'appliquent à un vaste gamme de cas d'utilisation.  Ils peut être assignés au rôle primaire d'un utilisateur, ou comme un rôle additionel.

Voici un sommaire de chaque rôle fixe quand il est appliqué au rôle primaire :
- **Invité :**  Un rôle en lecture seule.  Peut voir les ressources dans les environnements auxquels l'utilisateur est membre
- **Utilisateur :**  Peut créer environnements nouveaux avec les connexions de service existantes, et gérer les environnements que possèdes l'utilisateur
- **Administrateur :**  Peut gérer l'organisation.  Peut gérer tous les environnements dans toutes les connexions de service.  Pas capable ni de voir les sous-organisations ni de créer des nouvelles sous-organisiations
- **Revendeur :** Peut gérer l'image de marque et la tarification pour l'organisation et ses sous-organisations, et peut créer des sous-organisations dans l'organisation.  Pas capable de créer des nouvelles organsiations
- **Opérateur :** Peut créer des organisations et des sous-organisations, gérer les connexions de service, les quotas de service, les engagements, et a l'accès complet à toutes autres organisations, ressources et paramètres du système

Chaque rôle fixe a une portée par défaut :
- Invité, Utilisateur, et Administrateur :  Seulement l'organisation dans laquelle l'utilisateur est créé
- Revendeur : L'organisation dans laquelle l'utilisateur est créé et toutes ses sous-organisations
- Opérateur : Toutes les organisations

Comme l'illustre le diagramme ci-dessous, en montant dans le hiérarchie, chaque rôle reçoit toutes les privilèges de ceux qui précèdent :

![permissions chart](permissions-en.png)

### Les rôles personnalisés

CloudMC permet que les utilisateurs avec le rôle *Administrateur* et plus élevé (ou les utilisateaus avec un rôle personnalisé incluyant la permission *Rôles : Gérer*, expliqué dans cette section) à créer des nouveaux rôles avec les permissions qui sont alignées avec les règles d'affiares.  L'administrateur peut sélectionner permissions individuelles et sauvegarder le rôle, et après appliquer ce rôle aux utilisateurs dans l'organisation.  Les permissions effectives d'un utilisateur sont régies par l'union de toutes le permissions et la portée du rôle primarire avec toutes les rôles additionels.  Il faut que le rôle primaire de l'utilisateur soit un des rôles fixes incorporés, jamais un rôle personnalisé.

#### Créer un rôle personnalisé

## Les rôles d'environnement

## Comment assigner le rôles
