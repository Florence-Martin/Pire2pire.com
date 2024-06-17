# Diagramme de classe -

Ce diagramme décrire le système de gestion de formations en ligne, où les utilisateurs peuvent s’inscrire, suivre des cours, et où les instructeurs peuvent créer et gérer le contenu des formations.

![Représentation UML-Diagramme de classe](../../Assets/Images/diagramme-de-classe.png)

<details>
<summary>Version textualisée de ce diagramme</summary>

### Classes Principales et Héritage

- User
  - • Attributs : prénom, nom, email, mot de passe, adresse complète (rue, code postal, ville, pays), date de naissance.
  - • Méthodes : Réinitialisation de mot de passe.
- Student (hérite de User)
  - • Attributs : Liste d’inscriptions, progression de visionnage.
  - • Méthodes : Inscription à une formation, validation d’un module, désinscription, demande de suppression de compte.
- Instructor (hérite de User)
  - • Attributs : Code instructeur, liste de leçons créées, liste de modules créés.
  - • Méthodes : Ajout/suppression de leçon, ajout/suppression de module, mise à jour de formation, gestion des statuts de contenu, demande de suppression de compte.
- Administrator
  - • Méthodes : Enregistrement de formateur, ajout/suppression de l’utilisateur, restauration de contenu.
- SuperAdministrator (hérite de Administrator)
  - • Méthodes : Ajout/suppression d’administrateur, mise à jour des informations d’administrateur.

### Gestion de Formations et Modules

- Formation
  - • Attributs : Titre de la formation, description, tags, liste de modules, statut, dates de début et de fin.
  - • Méthodes : Ajout/suppression de tag, ajout/suppression de module, mise à jour de statut, activation/désactivation de la formation, validation de la formation.
- Module
  - • Attributs : Titre, contenu, tags, statut, liste de leçons.
  - • Méthodes : Ajout/suppression de leçon, validation du module, activation/désactivation du module.
- Lesson
  - • Attributs : Titre, texte, URL de l’image, URL des vidéos.
  - • Méthodes : Validation de la leçon.

### Évaluation et Inscription

- RegisterFormation
  - • Attributs : Étudiant, formation, date d’inscription, date de fin, statut du cours.
- FormationEvaluate
  - • Attributs : Booléen de validation.

### Recherche

- Interface Search
  - • Méthodes : Recherche par mots-clés, exécution de recherche, filtrage des résultats.

### Autres Composants

- Dashboard
  - • Attributs : Items, notifications, mise à jour de la vue, accès à l’item.
- Tag
  - • Méthodes : Création/suppression de tag.

### Enumérations

- CourseStatus : Statuts de cours (En cours, Terminé).
- ContentStatus : Statuts de contenu (Publié, Brouillon, Archivé).

  </details>
