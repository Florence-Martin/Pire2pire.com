# Modèle Physique des Données (MPD)

## 1. Introduction

Ce document détaille le Modèle Physique des Données pour notre système de gestion d'apprentissage. Élaboré à partir du Modèle Logique de Données (MLD), ce MPD est optimisé pour une implémentation dans **PostgreSQL**. Il tire parti des fonctionnalités avancées de ce SGBD pour optimiser la performance, la sécurité, et l'intégrité des données.

## 2. Structure des Tables

### Table `User`

```sql
CREATE TABLE public.User(
    ID_User      SERIAL PRIMARY KEY,
    Firstname    VARCHAR(60) NOT NULL,
    Lastname     VARCHAR(60) NOT NULL,
    Birthdate    DATE,
    Email        VARCHAR(60) UNIQUE NOT NULL,
    Password     VARCHAR(60) NOT NULL,
    User_Type    VARCHAR(60) NOT NULL,
    ID_Address   INT REFERENCES Address(ID_Address)
);
```

- Description : Stocke les informations personnelles des utilisateurs.
- Indices : Un index est créé sur Email pour accélérer les requêtes de connexion.

### Table `Role`

```sql
CREATE TABLE public.Role(
    ID_Role     SERIAL PRIMARY KEY,
    Name_Role   VARCHAR(50) NOT NULL
);
```

- Description : Gère les différents rôles attribuables aux utilisateurs.

### Table `Have`

```sql
CREATE TABLE public.Have(
    ID_Role   INT NOT NULL,
    ID_User   INT NOT NULL,
    CONSTRAINT Have_PK PRIMARY KEY (ID_Role, ID_User),
    CONSTRAINT Have_Role_FK FOREIGN KEY (ID_Role) REFERENCES public.Role(ID_Role),
    CONSTRAINT Have_User_FK FOREIGN KEY (ID_User) REFERENCES public.User(ID_User)
);
```

- Objectif : La table Have lie les utilisateurs aux rôles dans une relation many-to-many. Chaque entrée indique qu’un utilisateur spécifique possède un rôle particulier.
- Contraintes de clé étrangère : Les contraintes garantissent que les identifiants des rôles et des utilisateurs référencés existent réellement dans les tables Role et User, respectivement, ce qui renforce l’intégrité des données.

### Table `Address`

```sql
CREATE TABLE public.Address(
    ID_Address      SERIAL PRIMARY KEY,
    Address_Number  VARCHAR(50),
    Address_Street  VARCHAR(100),
    Address_Postcode VARCHAR(20),
    Address_City    VARCHAR(50)
);
```

- Description : Contient les adresses détaillées des utilisateurs.

### Table `Instructor`

```sql
CREATE TABLE public.Instructor(
    ID_Instructor   SERIAL PRIMARY KEY,
    Instructor_Code VARCHAR(50) UNIQUE NOT NULL,
    ID_User         INT NOT NULL REFERENCES User(ID_User)
);
```

- Description : Stocke les informations spécifiques aux instructeurs.
- Indices : Un index sur Instructor_Code pour faciliter la recherche d’instructeurs.

### Table `Formation`

```sql
CREATE TABLE public.Formation(
    ID_Formation       SERIAL PRIMARY KEY,
    Title_Formation    VARCHAR(50) NOT NULL,
    Description        VARCHAR(2000),
    Status_Formation   VARCHAR(50) NOT NULL,
    IsValidated        BOOL NOT NULL
);
```

- Description : Détails des formations disponibles.
- Indices : Index sur Status_Formation pour optimiser les recherches par statut.

### Table `Lesson`

```sql
CREATE TABLE public.Lesson(
    ID_Lesson     SERIAL PRIMARY KEY,
    Title_Lesson  VARCHAR(50) NOT NULL,
    Content_Lesson TEXT NOT NULL,
    ID_Module     INT NOT NULL REFERENCES Module(ID_Module)
);
```

- Description : Gère les leçons qui font partie des modules de formation.

### Table `Module`

```sql
CREATE TABLE public.Module(
    ID_Module        SERIAL PRIMARY KEY,
    Title_Module     VARCHAR(50) NOT NULL,
    Content_Module   TEXT NOT NULL,
    Status_Module    VARCHAR(50) NOT NULL,
    IsValidated      BOOL NOT NULL
);
```

- Description : Contient les modules qui composent les formations.

### Table `Status`

```sql
CREATE TABLE public.Status(
    ID_Status     SERIAL NOT NULL,
    Status_Type   VARCHAR(50) NOT NULL,
    Description   TEXT,
    CONSTRAINT Status_PK PRIMARY KEY (ID_Status)
);
```

- Objectif : La table Status stocke les différents statuts que peuvent prendre les leçons, modules, et formations, tels que “Brouillon”, “Publié”, ou “Archivé”. Cela permet de gérer les états de publication et d’accès des contenus.
- Usage : Cette table est essentielle pour s’assurer que les interactions avec les contenus sont appropriées. Par exemple, elle peut être utilisée pour empêcher l’accès ou la validation de contenus qui ne sont pas encore en état de “Publié”.

### Table `Give`

```sql
CREATE TABLE public.Give(
    ID_Formation   INT NOT NULL,
    ID_Module      INT NOT NULL,
    ID_Lesson      INT NOT NULL,
    ID_Status      INT NOT NULL,
    CONSTRAINT Give_PK PRIMARY KEY (ID_Formation, ID_Module, ID_Lesson, ID_Status),
    CONSTRAINT Give_Formation_FK FOREIGN KEY (ID_Formation) REFERENCES public.Formation(ID_Formation),
    CONSTRAINT Give_Module_FK FOREIGN KEY (ID_Module) REFERENCES public.Module(ID_Module),
    CONSTRAINT Give_Lesson_FK FOREIGN KEY (ID_Lesson) REFERENCES public.Lesson(ID_Lesson),
    CONSTRAINT Give_Status_FK FOREIGN KEY (ID_Status) REFERENCES public.Status(ID_Status)
);
```

- Objectif: La table Give sert à créer des associations complexes entre les formations, modules, leçons, et leurs statuts respectifs, ce qui permet de gérer les conditions d’accès et de validation des contenus éducatifs.
- Utilité: Cette structure est essentielle pour s’assurer que les actions telles que l’inscription à une formation ou la validation d’une leçon sont conditionnées par le statut approprié (par exemple, un module ne peut pas être validé s’il est en statut “Brouillon”).

### Table `Register`

```sql
CREATE TABLE public.Register(
    ID_Register      SERIAL PRIMARY KEY,
    ID_User          INT NOT NULL REFERENCES User(ID_User),
    ID_Formation     INT NOT NULL REFERENCES Formation(ID_Formation),
    Registration_Date DATE NOT NULL,
    Is_Active        BOOL NOT NULL,
    End_Date         DATE
);
```

- Description : Stocke les informations d’inscription des utilisateurs aux formations. Inclut les dates de début et de fin d’inscription ainsi que le statut de l’inscription (active ou non).

### Table `Validate`

```sql
CREATE TABLE public.Validate(
    ID_Validate  SERIAL PRIMARY KEY,
    ID_Lesson    INT NOT NULL REFERENCES Lesson(ID_Lesson),
    ID_User      INT NOT NULL REFERENCES User(ID_User),
    Validate_Date DATE,
    Is_Completed BOOL
);
```

- Description : Gère les validations des leçons des utilisateurs avec la date de validation.

### Table `Compose`

```sql
CREATE TABLE public.Compose(
    ID_Compose   SERIAL PRIMARY KEY,
    ID_Module    INT NOT NULL REFERENCES Module(ID_Module),
    ID_Formation INT NOT NULL REFERENCES Formation(ID_Formation)
);
```

- Description : Assure la relation entre les modules et les formations, indiquant quels modules composent une formation spécifique.

## 3. Exemples de Requêtes

### 3.1 Recherche d’un utilisateur par email

```sql
SELECT * FROM User WHERE Email = 'example@email.com';
```

### 3.2 Liste des formations validées

```sql
SELECT Title_Formation FROM Formation WHERE IsValidated = TRUE;
```

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

#### Explication de la Requête

- Jointures : Cette requête connecte les tables User, Role, et Address pour rassembler les informations pertinentes sur les utilisateurs.
- Filtre : Elle filtre spécifiquement les utilisateurs qui ont le rôle de ‘Student’.

#### Optimisation par les Indices

- Indices sur les clés étrangères : Avoir des indices sur u.ID_Role et u.ID_Address assure que les jointures entre les tables User, Role, et Address soient efficaces.
- Indice sur la condition de filtre : Un indice sur r.Name_Role aide à accélérer la requête lorsque nous recherchons par rôle.

## 4. Indexation pour Optimisation des Performances

Les indices sont utilisés pour accélérer la récupération des données sur les colonnes fréquemment utilisées dans les requêtes, en particulier dans les clauses `JOIN`, `WHERE` et pour le tri des résultats. Voici quelques exemples d'indices mis en place :

```sql
CREATE INDEX idx_user_email ON public.User(Email);
CREATE INDEX idx_instructor_code ON public.Instructor(Instructor_Code);
CREATE INDEX idx_formation_status ON public.Formation(Status_Formation);
```

## 5. Sécurité

La sécurité des données est une priorité absolue dans notre système. Voici les mesures clés que nous avons prises :

- **Cryptage des Données Sensibles** : Les mots de passe des utilisateurs sont sécurisés en utilisant BCrypt, un algorithme de hachage robuste et fiable. Ce choix garantit que même en cas d'accès non autorisé à notre base de données, les mots de passe restent protégés.

- **Contraintes de Base de Données** : L’intégrité des données est maintenue grâce à des contraintes strictes de clés étrangères, qui assurent des références fiables entre les tables. Ces contraintes préviennent les erreurs de données et garantissent que les relations entre les données restent cohérentes.

- **Gestion des Valeurs NULL** : Nous définissons soigneusement les colonnes qui ne doivent pas accepter les valeurs NULL pour éviter les données incomplètes, ce qui est crucial pour les colonnes qui sont essentielles à la logique de notre application.

- **Rôles d'Accès** : Des rôles d'accès spécifiques sont définis pour contrôler qui peut lire, écrire, ou administrer les différentes parties de la base de données. Ces rôles aident à minimiser les risques d'accès non autorisé ou de modification malveillante des données.

- **Audits et Logs** : Des systèmes de logs détaillés et des audits réguliers sont en place pour suivre l'accès et les modifications apportées à la base de données, permettant une réponse rapide en cas d'activités suspectes.

Ces mesures renforcent la sécurité de notre base de données et assurent la protection de l'information contre les accès et modifications non autorisés.

## 6. Conclusion

Ce MPD est conçu pour fournir une base solide pour notre système de gestion d’apprentissage, garantissant performance, sécurité et intégrité des données, même sous une charge élevée.
En suivant les directives détaillées dans ce document, les développeurs et administrateurs de base de données pourront efficacement mettre en œuvre, maintenir, et utiliser la base de données.
[🔝 Retour à la Table des matières](../../README.md#table-des-matieres)
