# Diagramme d'activité - Gestion des formations

Ce diagramme décrit les interactions entre un instructeur potentiel et l’administrateur pour le processus de gestion des formations, depuis la demande pour devenir formateur jusqu’à la validation et la gestion des cours soumis.

![Représentation UML-Diagramme d'activité - gestion des formations](../../Assets/Images/training%20management.png)

<details>
<summary>Version textualisée de ce diagramme</summary>

### Partie “Instructor” (Instructeur)

- 1. Début:
  - • Action: Apply to be a trainer
  - • L’utilisateur fait une demande pour devenir formateur.
- 2. [request]:
  - • Décision prise par l’administrateur: l’utilisateur peut être accepté ou refusé comme formateur.
- 3. [accepted]:
  - • Si accepté, l’instructeur reçoit les droits de formateur.
  - • Action: Have trainers' rights
- 4. Gérer le contenu de formation:
  - • Action: Manage its own learning content
  - • L’instructeur peut créer ou mettre à jour le contenu de formation.
- 5. Créer ou Mettre à jour:
  - • Action: Create/Update
- 6. Attribuer une étiquette et un statut:
  - • Action: Assign a tag et Assign a status
  - • L’instructeur attribue une étiquette et un statut (Brouillon, Publié, Archivé) à son cours.
- 7. Soumettre le cours:
  - • Action: Submit the course
  - • Le cours est soumis pour vérification par l’administrateur.
- 8. Ajouter à ses cours:
  - • Si le cours est validé par l’administrateur, il est ajouté aux cours de l’instructeur.
  - • Action: Add to his courses
- 9. Voir son tableau de bord:
  - • Action: View his Dashboard
  - • L’instructeur peut voir son tableau de bord.

### Partie “Administrator” (Administrateur)

- 1. Prendre une décision:
  - • Action: Take a decision
  - • L’administrateur décide d’accepter ou de refuser la demande de formateur.
  - • [refused]: Si refusé, l’utilisateur reste un simple utilisateur.
  - • [accepted]: Si accepté, l’instructeur peut gérer son contenu de formation.
- 2. Gérer l’ensemble du cours:
  - • Action: Manage overall course
  - • L’administrateur gère l’ensemble du cours, incluant la création, suppression, et gestion des balises de formation.
- 3. Gérer les balises de formation:
  - • Action: Manage training Tags
  - • L’administrateur gère les balises associées aux formations.
- 4. Approuver les changements de statut:
  - • Action: Approve status changes
  - • L’administrateur approuve les changements de statut des cours (Brouillon, Publié, Archivé).
- 5. Vérifier le cours:
  - • Action: Check the course
  - • L’administrateur vérifie le cours soumis par l’instructeur.
  - • [refused]: Si le cours est refusé, l’instructeur est informé et doit revoir son cours.
- 6. Voir son tableau de bord:
  - • Action: View his Dashboard
  - • L’administrateur peut voir son tableau de bord pour suivre l’état des formations et des instructeurs.

</details>
