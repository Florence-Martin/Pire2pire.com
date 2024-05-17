# Modèle Physique des Données (MPD)

## 1. Introduction

Élaboré à partir du Modèle Logique de Données (MLD), ce MPD est optimisé pour une implémentation dans **PostgreSQL**.  
Le MPD est une représentation détaillée et technique de notre base de données, qui inclut toutes les contraintes d’intégrité nécessaires pour garantir la validité des données.  
Lors de la conception du MPD, nous devons nous assurer que toutes les contraintes sont clairement définies. Cela inclut :

- Contraintes de **Clé Primaire (PRIMARY KEY)** : pour identifier de manière unique chaque enregistrement dans une table.
- Contraintes de **Clé Étrangère (FOREIGN KEY)** : pour maintenir l’intégrité référentielle entre les tables.
- Contraintes **NOT NULL** : pour s’assurer que certaines colonnes ne peuvent pas avoir de valeur NULL
- Contraintes **UNIQUE** : pour garantir l’unicité des valeurs dans une colonne ou un ensemble de colonnes.
- Contraintes **CHECK** : pour imposer des conditions spécifiques sur les valeurs des colonnes.
- Valeurs par **Défaut (DEFAULT)** : pour définir une valeur par défaut si aucune valeur n’est fournie.

## 2. Structure des Tables et Contraintes

### Table `User`

- Description : Stocke les informations personnelles des utilisateurs.
- Contraintes :
  - PRIMARY KEY sur ID_User (UUID, généré automatiquement).
  - NOT NULL sur Firstname, Lastname, Email, Password, User_Type.
  - UNIQUE sur Email.
  - FOREIGN KEY sur ID_Address référencée à Address(ID_Address).
- Index :
  - idx_user_email pour améliorer les performances des requêtes sur l’email des utilisateurs.

### Table `Instructor`

- Description : Stocke les informations spécifiques aux instructeurs.
- Contraintes :
  - PRIMARY KEY sur ID_Instructor (UUID, généré automatiquement).
  - NOT NULL sur Instructor_Code, ID_User.
  - UNIQUE sur Instructor_Code.
  - FOREIGN KEY sur ID_User référencée à User(ID_User).
- Index :
  - idx_instructor_code pour améliorer les performances des requêtes sur le code des instructeurs.

### Table `Address`

- Description : Contient les adresses détaillées des utilisateurs.
- Contraintes :
  - PRIMARY KEY sur ID_Address (SERIAL).

### Table `Role`

- Description : Gère les différents rôles attribuables aux utilisateurs.
- Contraintes :
  - PRIMARY KEY sur ID_Role (SERIAL).
  - NOT NULL sur Name_Role.

### Table `Have`

- Description : La table Have lie les utilisateurs aux rôles dans une relation many-to-many. Chaque entrée indique qu’un utilisateur spécifique possède un rôle particulier.
- Contraintes :
  - PRIMARY KEY composite sur ID_Role et ID_User.
  - FOREIGN KEY sur ID_Role référencée à Role(ID_Role).
  - FOREIGN KEY sur ID_User référencée à User(ID_User).

### Table `Lesson`

- Description : Gère les leçons qui font partie des modules de formation.
- Contraintes :
  - PRIMARY KEY sur ID_Lesson (SERIAL).
  - NOT NULL sur Title_Lesson, Content_Lesson, ID_Module.
  - FOREIGN KEY sur ID_Module référencée à Module(ID_Module).

### Table `Module`

- Description : Contient les modules qui composent les formations.
- Contraintes :
  - PRIMARY KEY sur ID_Module (SERIAL).
  - NOT NULL sur Title_Module, Content_Module, Status_Module, IsValidated.
  - CHECK sur Status_Module pour restreindre les valeurs à Brouillon, Publié, Archivé.
  - DEFAULT sur IsValidated pour définir une valeur par défaut à FALSE.

### Table `Formation`

- Description : Détails des formations disponibles.
- Contraintes :
  - PRIMARY KEY sur ID_Formation (SERIAL).
  - NOT NULL sur Title_Formation, Status_Formation, IsValidated.
  - CHECK sur Status_Formation pour restreindre les valeurs à Brouillon, Publié, Archivé.
  - DEFAULT sur IsValidated pour définir une valeur par défaut à FALSE.
- Index :
  - idx_formation_status pour optimiser les recherches par statut.

### Table `Status`

- Description : La table Status stocke les différents statuts que peuvent prendre les leçons, modules, et formations, tels que “Brouillon”, “Publié”, ou “Archivé”.
- Contraintes :
  - PRIMARY KEY sur ID_Status (SERIAL).
  - NOT NULL sur Status_Type.
  - UNIQUE sur Status_Type.

### Table `Give`

- Description : La table Give crée des associations complexes entre les formations, modules, leçons, et leurs statuts respectifs, permettant de gérer les conditions d’accès et de validation des contenus éducatifs.
- Contraintes :
  - PRIMARY KEY composite sur ID_Formation, ID_Module, ID_Lesson, et ID_Status.
  - FOREIGN KEY sur ID_Formation référencée à Formation(ID_Formation).
  - FOREIGN KEY sur ID_Module référencée à Module(ID_Module).
  - FOREIGN KEY sur ID_Lesson référencée à Lesson(ID_Lesson).
  - FOREIGN KEY sur ID_Status référencée à Status(ID_Status).

### Table `Register`

- Description : Stocke les informations d’inscription des utilisateurs aux formations. Inclut les dates de début et de fin d’inscription ainsi que le statut de l’inscription (active ou non).
- Contraintes :
  - PRIMARY KEY sur ID_Register (SERIAL).
  - NOT NULL sur ID_User, ID_Formation, Registration_Date, Is_Active.
  - FOREIGN KEY sur ID_User référencée à User(ID_User).
  - FOREIGN KEY sur ID_Formation référencée à Formation(ID_Formation).

### Table `Validate`

- Description : Gère les validations des leçons des utilisateurs avec la date de validation.
- Contraintes :
  - PRIMARY KEY sur ID_Validate (SERIAL).
  - NOT NULL sur ID_Lesson, ID_User.
  - FOREIGN KEY sur ID_Lesson référencée à Lesson(ID_Lesson).
  - FOREIGN KEY sur ID_User référencée à User(ID_User).

### Table `Compose`

- Description : Assure la relation entre les modules et les formations, indiquant quels modules composent une formation spécifique.
- Contraintes :
  - PRIMARY KEY composite sur ID_Module et ID_Formation.
  - NOT NULL sur ID_Module, ID_Formation.
  - FOREIGN KEY sur ID_Module référencée à Module(ID_Module).
  - FOREIGN KEY sur ID_Formation référencée à Formation(ID_Formation).

## 3. Exemples de Requêtes

### 3.1 Recherche d’un utilisateur par email

```sql
SELECT * FROM User WHERE Email = 'example@email.com';
```

- Explication :
  • Cette requête sélectionne tous les champs de la table User.
  • Elle utilise une clause WHERE pour filtrer les utilisateurs ayant l’adresse email example@email.com.
  • Utile pour vérifier l’existence d’un utilisateur spécifique ou récupérer ses informations complètes.

### 3.2 Liste des formations validées

```sql
SELECT Title_Formation FROM Formation WHERE IsValidated = TRUE;
```

- Explication :
  • Cette requête sélectionne uniquement le champ Title_Formation de la table Formation.
  • Elle utilise une clause WHERE pour filtrer les formations dont le champ IsValidated est TRUE.
  • Utile pour obtenir une liste de toutes les formations qui ont été validées.

### 3.3 Liste des modules qui sont actuellement “Publiés” et disponibles pour les utilisateurs

```sql
SELECT
    m.Title_Module,
    m.Content_Module,
    s.Status_Type
FROM
    public.Module m
JOIN public.Status s ON m.ID_Status = s.ID_Status
WHERE
    s.Status_Type = 'Publié';
```

- Explication :
  • Cette requête sélectionne les champs Title_Module, Content_Module de la table Module et Status_Type de la table Status.
  • Elle utilise une jointure JOIN pour combiner les tables Module et Status en reliant ID_Status.
  • Une clause WHERE est utilisée pour filtrer les résultats où Status_Type est Publié.
  • Utile pour obtenir une liste de modules actuellement publiés et disponibles pour les utilisateurs.

### 3.4 Liste des noms des utilisateurs avec leurs rôles et leurs adresses

```sql
SELECT
    u.Firstname,
    u.Lastname,
    u.Email,
    r.Name_Role,
    a.Address_Street,
    a.Address_City
FROM
    User AS u
JOIN Role AS r ON u.ID_User = r.ID_Role
JOIN Address AS a ON u.ID_Address = a.ID_Address
WHERE
    r.Name_Role = 'Student';
```

- Explication :
  • Cette requête sélectionne les champs Firstname, Lastname, Email de la table User, Name_Role de la table Role, et Address_Street, Address_City de la table Address.
  • Elle utilise des jointures JOIN pour combiner les tables User, Role et Address en reliant ID_User et ID_Address.
  • Une clause WHERE est utilisée pour filtrer les résultats où Name_Role est Student.
  • Utile pour obtenir des informations complètes sur les utilisateurs ayant le rôle de “Student”, incluant leurs noms, rôles et adresses.

### 3.5 Lister les modules et leçons associés à une formation spécifique, mais uniquement ceux qui sont dans un état “Publié”

```sql
SELECT
    f.Title_Formation,
    m.Title_Module,
    l.Title_Lesson,
    s.Status_Type
FROM
    public.Give g
JOIN public.Formation f ON g.ID_Formation = f.ID_Formation
JOIN public.Module m ON g.ID_Module = m.ID_Module
JOIN public.Lesson l ON g.ID_Lesson = l.ID_Lesson
JOIN public.Status s ON g.ID_Status = s.ID_Status
WHERE
    s.Status_Type = 'Publié' AND
    f.ID_Formation = 101;  -- Assumant 101 est l'ID d'une formation spécifique
```

- Explication :
  • Cette requête sélectionne les champs Title_Formation de la table Formation, Title_Module de la table Module, Title_Lesson de la table Lesson, et Status_Type de la table Status.
  • Elle utilise des jointures JOIN pour combiner les tables Give, Formation, Module, Lesson et Status en reliant les identifiants appropriés (ID_Formation, ID_Module, ID_Lesson, ID_Status).
  • Une clause WHERE est utilisée pour filtrer les résultats où Status_Type est Publié et ID_Formation est 101.
  • Utile pour obtenir une liste détaillée des modules et leçons d’une formation spécifique qui sont publiés.

## 4. Indexation pour Optimisation des Performances

Les indices sont utilisés pour accélérer la récupération des données sur les colonnes fréquemment utilisées dans les requêtes, en particulier dans les clauses `JOIN`, `WHERE` et pour le tri des résultats. Voici les index mis en place :

```sql
CREATE INDEX idx_user_email ON public.User(Email);
CREATE INDEX idx_instructor_code ON public.Instructor(Instructor_Code);
CREATE INDEX idx_formation_status ON public.Formation(Status_Formation);
```

## 5. Gestion Automatisée des Validations

### 5.1 Objectif

Implémenter des procédures stockées pour gérer automatiquement la validation des leçons et assurer la propagation de la validation aux niveaux supérieurs, soit les modules puis les formations. Cette automatisation garantit que :

- La validation de toutes les leçons d’un module entraîne la validation du module.
- La validation de tous les modules d’une formation entraîne la validation de la formation.

### 5.2 Procédure de Validation de Leçon

Cette procédure est déclenchée lorsqu’une leçon est validée par un apprenant. Elle vérifie si toutes les leçons associées à un module donné sont validées et, le cas échéant, marque le module comme validé. Ensuite, elle vérifie si tous les modules associés à une formation sont validés et, si c’est le cas, marque la formation comme validée.

## 6. Sécurité

La sécurité des données est une priorité absolue dans notre système. Voici les mesures clés que nous avons prises :

- **Cryptage des Données Sensibles** : Les mots de passe des utilisateurs sont sécurisés en utilisant BCrypt, un algorithme de hachage robuste et fiable. Ce choix garantit que même en cas d'accès non autorisé à notre base de données, les mots de passe restent protégés.

- **Contraintes de Base de Données** : L’intégrité des données est maintenue grâce à des contraintes strictes de clés étrangères, qui assurent des références fiables entre les tables. Ces contraintes préviennent les erreurs de données et garantissent que les relations entre les données restent cohérentes.

- **Gestion des Valeurs NULL** : Nous définissons soigneusement les colonnes qui ne doivent pas accepter les valeurs NULL pour éviter les données incomplètes, ce qui est crucial pour les colonnes qui sont essentielles à la logique de notre application.

- **Rôles d'Accès** : Des rôles d'accès spécifiques sont définis pour contrôler qui peut lire, écrire, ou administrer les différentes parties de la base de données. Ces rôles aident à minimiser les risques d'accès non autorisé ou de modification malveillante des données.

- **Audits et Logs** : Des systèmes de logs détaillés et des audits réguliers sont en place pour suivre l'accès et les modifications apportées à la base de données, permettant une réponse rapide en cas d'activités suspectes.

Ces mesures renforcent la sécurité de notre base de données et assurent la protection de l'information contre les accès et modifications non autorisés.

## 7. Conclusion

Ce MPD est conçu pour fournir une base solide pour notre système de gestion d’apprentissage, garantissant performance, sécurité et intégrité des données, même sous une charge élevée.
En suivant les directives détaillées dans ce document, les développeurs et administrateurs de base de données pourront efficacement mettre en œuvre, maintenir, et utiliser la base de données.

[🔝 Retour à la Table des matières](../../README.md#table-des-matieres)
