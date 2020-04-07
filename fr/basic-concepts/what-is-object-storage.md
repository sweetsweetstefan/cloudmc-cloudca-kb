---
title: "Qu'est-ce que le stockage objet?"
slug: qu-est-ce-que-le-stockage-objet
---


Selon Wikipedia, le Object Storage (ou stockage objet) est décrit comme "une architecture de stockage qui gère les données comme des objets, ce qui le différencie des autres architectures de stockage comme les systèmes de fichiers qui gèrent les données sous forme de hiérarchie et le stockage par bloc qui gèrent les données sous forme de blocs à l'intérieur de secteurs et des pistes".

Toujours nébuleux n'est-ce pas ? Ajoutons quelques détails !

**L'Object Storage (ou stockage objet)** est essentiellement une façon différente de stocker, organiser et accéder les données. Ce type de plateforme fournit une infrastructure de stockage pour sauvegarder des fichiers avec beaucoup de métadonnées ajoutées à ceux-ci, donc ce qu'on appelle des objets. Avec le stockage objet, il n'y a pas de hiérarchie ou système de fichiers. Les utilisateurs vont typiquement accéder leurs données à travers une application qui utilise un API de type REST (un protocole Internet optimisé pour les applications en-ligne). Cette approche fait du stockage objet un engin idéal pour tout ce qui est en-ligne, surtout dans une environnement infonuagique. Lorsque les objets sont stockés, un identifiant est alors créé pour localiser l'objet dans la grappe. Les applications peuvent donc, grâce à cet identifiant ou encore les métadonnées, retrouver les bonnes données et ce très rapidement. Cette approche va donc significativement augmenter la vitesse d'accès aux données en évitant ainsi la surcharge en temps système comme dans un système de fichier traditionnel.

## Capacités générales
- Fournit un environnement de stockage redondant et évolutif composé de grappes de serveurs capable de stocker des pétaoctets de données.
- Système de stockage distribué pour des données statiques comme des images de machine virtuelle, des photos, des courriels, ainsi que des fichiers de sauvegarde. Avec un concept sans "tête dirigeante" ou de serveur maître, cela amène une meilleure durabilité et redondance des données.
- Les objets et les fichier sont répliqués sur plusieurs disques répartis dans plusieurs serveurs dans le centre de données pour assurer une réplication et intégrité optimale des données dans la grappe.
- La grappe de stockage évolue de manière horizontale. Si un serveur ou un disque ne fonctionne plus, le système va automatiquement répliquer le contenu dans un nouvel emplacement dans la grappe.

## Cas d'utilisation
Le stockage objet à énormément de cas d'utilisation potentiels, nous ne les listerons pas tous ici. Cependant, voici une courte liste pour vous aider:

- Archivage et Sauvegarde (i.e.: journaux, copie de base de données, etc.)
- Fichier statiques/Web (i.e.: images, vidéos, contenu statique, etc.)
- Partage de documents
- Métriques de surveillance
- etc.
