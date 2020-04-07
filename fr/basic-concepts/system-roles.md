---
title: "Les rôles système pour contôler l'accès des utilisateurs"
slug: roles-systeme
---


Les **rôles système** assignés à un utilisateur déterminent les fonctionnalités qui lui seront offertes. Un rôle consiste en un ensemble de permissions parmi celles offertes dans le système. Par exemple, la permission Ajouter utilisateur fait partie du rôle Organization Admin, mais pas du rôle End-User. Conséquemment, seul un utilisateur possédant le rôle Organization Admin est autorisé à ajouter de nouveaux utilisateurs au sein de son organisation.

Pour vérifier votre/vos rôles actuels, procédez comme suit:

1. Dans le menu correspondant à votre nom d’utilisateur (dans la barre de menu), sélectionnez **Préférences**:

![Préférences](/assets/preferences-fr.png)

2. Consultez la valeur de l’item **Rôles système**:

![Page Préférences](/assets/preferences-edit-fr.png)

Par défaut cloud.ca fourni deux rôles de base (Organization Admin et End-user). Si vous avez besoin de davantage de granularité au niveau du modèle de sécurité, vous pouvez créer de nouveaux rôles en utilisant n’importe quelle combinaison de permissions. Vous pouvez ensuite sélectionner les rôles appropriés pour chacun de vos utilisateurs, où le résultat effectif sera l’union des permissions des rôles choisis.

Pour se prémunir contre les élévations de privilèges, un utilisateur possédant la permission Modifier utilisateur n’a que le droit d’assigner à autrui les roles qu’il possède lui-même.
