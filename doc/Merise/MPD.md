# MPD (Modèle Physique des Données)

# Introduction

Ce document présente le Modèle Physique de Données pour notre système de gestion d'apprentissage, élaboré à partir du Modèle Logique de Données.  
Ce MPD a été spécifiquement conçu pour une implémentation dans **PostgreSQL**, tirant profit des fonctionnalités avancées de ce SGBD pour optimiser la performance, la sécurité et l'intégrité des données. En respectant scrupuleusement les spécifications du MLD, le MPD intègre des types de données spécifiques et des mécanismes d'indexation, garantissant une gestion efficace et une performance optimisée de la base de données.

## Structure des Tables

Le MPD inclut des tables qui stockent les informations des utilisateurs, des rôles, des formations, et plus. Chaque table est décrite ci-dessous avec ses clés primaires, ses relations, et d'autres contraintes.

### Table `Role`

```sql
CREATE TABLE public.Role(
    ID_Role     SERIAL NOT NULL,
    Name_Role   VARCHAR(50) NOT NULL,
    CONSTRAINT Role_PK PRIMARY KEY (ID_Role)
);
```

- Description : Stocke les différents rôles attribuables aux utilisateurs.

### Table `Formation`

```sql
CREATE TABLE public.Formation(
    ID_Formation       SERIAL NOT NULL,
    Title_Formation    VARCHAR(50) NOT NULL,
    Description        VARCHAR(2000) NOT NULL,
    Status_Formation   VARCHAR(50) NOT NULL,
    IsValidated        BOOL NOT NULL,
    CONSTRAINT Formation_PK PRIMARY KEY (ID_Formation)
);
```

- Description : Contient les informations sur les formations proposées.

### Table `Module`

```sql
CREATE TABLE public.Module(
    ID_Module        SERIAL NOT NULL,
    Title_Module     VARCHAR(50) NOT NULL,
    Content_Module   VARCHAR(2000) NOT NULL,
    Version          VARCHAR(50) NOT NULL,
    Objectif         VARCHAR(2000) NOT NULL,
    Status_Module    VARCHAR(50) NOT NULL,
    IsValidated      BOOL NOT NULL,
    CONSTRAINT Module_PK PRIMARY KEY (ID_Module)
);
```

- Description : Détaille les modules qui composent les formations.

### Table `Status`

```sql
CREATE TABLE public.Status(
    ID_Status     SERIAL NOT NULL,
    Type_Status   VARCHAR(50) NOT NULL,
    CONSTRAINT Status_PK PRIMARY KEY (ID_Status)
);
```

- Description : Gère les différents statuts que peuvent prendre les leçons, modules, et formations.

### Autres tables

Les tables **User** et **Instructor** utilisent des UUID pour une identification unique et robuste, garantissant l'intégrité globale et la facilité de gestion des données à travers divers systèmes.  
Les tables **Address**, **Lesson**, **Register**, **Compose**, **Have**, et **Validate** sont configurées de façon similaire, chacune ayant ses propres clés primaires et étrangères, types de données adaptés, et contraintes nécessaires pour assurer la cohérence et la sécurité des opérations.

## Indexation pour Optimisation des Performances

Pour améliorer les performances de la base de données, des index ont été créés sur des colonnes fréquemment utilisées dans les requêtes. Voici quelques exemples :

### Index sur `User.Email`

```sql
CREATE INDEX idx_user_email ON public.User(Email);
```

- But : Accélérer les requêtes de recherche et de connexion des utilisateurs par leur email.

### Index sur `Formation.Status_Formation`

```sql
CREATE INDEX idx_formation_status ON public.Formation(Status_Formation);
```

- But : Optimiser les requêtes filtrant les formations par leur statut.

### Index sur `Instructor.Instructor_Code`

```sql
CREATE INDEX idx_instructor_code ON public.Instructor(Instructor_Code);
```

- But : Faciliter la recherche rapide d'instructeurs par leur code unique.

[🔝 Retour à la Table des matières](../../README.md#table-des-matieres)
