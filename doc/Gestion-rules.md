# Règles de gestion

### Application

- **Accessibilité**
  - L'application doit être conforme aux normes d'accessibilité WCAG pour garantir l'accessibilité à tous les utilisateurs.

### Gestion des utilisateurs

- **Visiteurs**
  - un visiteur peut voir les formations disponibles
  - un visiteur ne peut pas accéder aux fonctionnalités réservées aux utilisateurs connectés (inscription à une formation, la visualisation du contenu des leçons ou des modules, etc.)
  - un visiteur peut s’enregistrer pour devenir apprenant avec un nom, un prénom, une adresse physique, une date de naissance, un email et un mot de passe
- **Apprenant**
  - un apprenant peut exercer son droit à l'effacement conformément au RGPD, demandant la suppression de son compte et des données personnelles associées, mais il ne pourra plus avoir accès aux formations auxquelles il s’est inscrit
  - un apprenant peut s’inscrire à 0 ou plusieurs formations
  - un apprenant a un dashboard où il visualise ses formations ("En cours", "Terminée")
  - un apprenant peut visualiser sa progression globale dans une formation à l'aide d'un pourcentage de leçons et modules validés
  - un apprenant peut valider une leçon en cliquant sur un bouton dédié, indiquant ainsi qu'il la maîtrise
  - un apprenant peut valider un module si toutes les leçons associées sont validées
  - un apprenant peut valider une formation si tous les modules associés sont validés
  - un apprenant peut désactiver une formation qu’il ne veut plus suivre de son dashboard
- **Formateur**
  - un formateur s’inscrit sur la plateforme par le biais d’une candidature auprès de l’administrateur
  - un formateur possède les même attributs d’enregistrement qu’un apprenant, plus un code spécifique (pas de nomenclature particulière demandée par le client)
  - un formateur peut exercer son droit à l'effacement conformément au RGPD, demandant la suppression de son compte et des données personnelles associées
  - les leçons, modules et formations dont le formateur est l'auteur restent sur la plateforme, même après son effacement, pour des raisons de continuité pédagogique.
  - un formateur peut ajouter, modifier, et gérer le statut de ses leçons, ses modules et ses formations (de "brouillon" à "publiée" ou à "archivée").
  - un formateur ne peut pas désactiver une leçon, un module ou une formation
  - un formateur peut visualiser, mais pas modifier ou désactiver les leçons, modules et formations d'autres formateurs
  - un formateur peut ajouter ou modifier les tags associés à ses propres formations.
  - un formateur a un dashboard où il visualise ses leçons, ses modules et ses formations (brouillon, publiée, archivée)
- **Administrateur**
  - un administrateur peut inscrire un candidat en tant que formateur (code, nom, prénom, adresse physique, date de naissance, adresse email et mot de passe)
  - un administrateur peut ajouter, modifier et désactiver un compte utilisateur
  - un administrateur peut restaurer un compte ou un contenu archivé si nécessaire
  - un administrateur peut ajouter, modifier et désactiver une formation
  - un administrateur est responsable de l'approbation des changements de statut d'une formation de "brouillon" à "publiée" ou "archivée"
  - un administrateur peut ajouter, modifier et désactiver un module
  - un administrateur est responsable de l'approbation des changements de statut d'un module de "brouillon" à "publié" ou "archivé"
  - un administrateur peut ajouter, modifier et désactiver une leçon
  - un administrateur peut ajouter, modifier ou supprimer un ou plusieurs tags d'une formation
- **Super-administrateur**
  - un super-administrateur peut ajouter, modifier et désactiver un compte administrateur

### Droit commun à tous les utilisateurs

- un utilisateur doit avoir le statut d’apprenant, formateur, administrateur ou super-administrateur
- un utilisateur peut se connecter avec son email et son mot de passe
- un utilisateur peut réinitialiser son mot de passe si il l’a oublié via un email ou une question de sécurité.

### Gestion des inscriptions aux formations

- une inscription relie un apprenant à une formation
- une inscription est enregistrée avec une Date d'inscription et une Date de fin
- une inscription peut être créée mais ne pas encore avoir de date de début assignée
- une inscription peut ne pas avoir de date de fin prévue
- une inscription a un statut ("En cours", "Terminée")

### Gestion des Formations

- une formation a un titre, un descriptif, un statut
- une formation possède 1 à plusieurs tags (# Merise, #UML, #Conception d’application…)
- une formation possède 0 à plusieurs modules
- une formation peut être ajoutée, modifiée
- une formation ne peut pas être supprimée
- une formation a un statut (brouillon, publiée, archivée)
- une formation peut être créée à l'état de "brouillon"
- une formation peut être désactivée
- une formation peut être validée ou non validée
- une formation est activée dès l'inscription
- une formation a une date de début et de fin
- un module peut être désactivé d’une formation

### Gestion des Modules

- un module a un titre, un contenu, une version, un objectif
- un module appartient à 0 ou plusieurs formations
- un module possède 0 à plusieurs leçons
- un module peut être ajouté, modifié
- un module ne peut pas être supprimé
- un module a un statut (brouillon, publié, archivé)
- un module peut être créé à l'état de "brouillon"
- une leçon peut être désactivée d’un module
- un module peut être désactivé
- un module orphelin (associé à aucune formation) peut être ajouté à une ou plusieurs formations
- un module peut être validé ou non validé

### Gestion des Leçons

- une leçon a un titre, un contenu, une image, un texte, une vidéo
- une leçon peut être ajoutée à un ou plusieurs modules
- une leçon peut être modifiée
- une leçon ne peut pas être supprimée
- une leçon peut être validée ou non validée par l'apprenant ou par la leçon terminée
- une leçon peut être désactivée d’un ou plusieurs modules
- une leçon appartient à 0 ou plusieurs modules
- une leçon peut avoir un statut (brouillon, publiée, archivée)
- une leçon peut être créée à l'état de "brouillon"
- une leçon contient 1 texte
- une leçon contient 1 vidéo
- une leçon contient 1 à plusieurs image
- une leçon orpheline (associée à aucun module) peut être ajouté à un ou plusieurs modules
- une leçon doit contenir au moins un élément de contenu (texte, image ou vidéo) pour être publiée

### **Gestion de l'Archivage et de la Sécurité**

- La gestion des comptes et des contenus archivés ou désactivés est couverte par la **Stratégie de Sécurisation**, qui détaille les procédures d'archivage, de sauvegarde et de restauration des données.
- Cette stratégie comprend également des politiques de sécurité pour garantir la préservation des informations personnelles (RGPD) et pédagogiques.

[🔝 Retour à la Table des matières](../README.md#table-des-matieres)
