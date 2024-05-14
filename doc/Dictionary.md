![Dictionnaire de données](../doc/Assets/Images/datas-dictionary.jpeg)

# Dictionnaire de données

Un dictionnaire de données est un outil crucial pour la gestion des données qui décrit minutieusement la structure des bases de données. Il fournit des détails précis sur les tables, colonnes, types de données et contraintes, garantissant ainsi une standardisation et une cohérence des données dans l'application.

Il sert de référence essentielle pour les développeurs, les administrateurs de bases de données et les analystes, aidant à préserver l'intégrité des données, à faciliter les modifications structurelles et à assurer la conformité réglementaire.

### Dictionnaire de Données Complet

| Entité     | Attribut         | Type de Données | Longueur | Contraintes                           | Description                                            | Exemple                                      |
| ---------- | ---------------- | --------------- | -------- | ------------------------------------- | ------------------------------------------------------ | -------------------------------------------- |
| User       | ID_User          | UUID            |          | PRIMARY KEY, NOT NULL                 | Identifiant unique pour chaque utilisateur             | "a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11"       |
|            | Firstname        | VARCHAR         | 50       | NOT NULL                              | Prénom de l'utilisateur                                | "Emmy"                                       |
|            | Lastname         | VARCHAR         | 50       | NOT NULL                              | Nom de famille de l'utilisateur                        | "Durand"                                     |
|            | Birthdate        | DATE            |          | NOT NULL                              | Date de naissance de l'utilisateur                     | "1990-05-15"                                 |
|            | Email            | VARCHAR         | 50       | NOT NULL                              | Adresse email de l'utilisateur                         | "emmy.durand@example.com"                    |
|            | Password         | VARCHAR         | 50       | NOT NULL                              | Mot de passe de l'utilisateur                          | "s3cureP@ss!"                                |
|            | User_Type        | VARCHAR         | 50       | NOT NULL                              | Type de l'utilisateur                                  | "Instructor"                                 |
|            | ID_Address       | INT             | 11       | NOT NULL, FOREIGN KEY                 | Clé étrangère référençant l'adresse de l'utilisateur   | 102                                          |
| Address    | ID_Address       | INT             | 11       | AUTO-INCREMENT, PRIMARY KEY, NOT NULL | Identifiant unique pour chaque adresse                 | 102                                          |
|            | Address_Number   | VARCHAR         | 50       | NOT NULL                              | Numéro de bâtiment ou de maison                        | "42"                                         |
|            | Address_Street   | VARCHAR         | 100      | NOT NULL                              | Nom de la rue                                          | "rue Belfort"                                |
|            | Address_Postcode | VARCHAR         | 20       | NOT NULL                              | Code postal de l'adresse                               | "69004"                                      |
|            | Address_City     | VARCHAR         | 50       | NOT NULL                              | Ville de l'adresse                                     | "Lyon"                                       |
| Role       | ID_Role          | INT             | 11       | AUTO-INCREMENT, PRIMARY KEY, NOT NULL | Identifiant unique pour chaque rôle                    | 1                                            |
|            | Name_Role        | VARCHAR         | 50       | NOT NULL                              | Nom du rôle                                            | "Administrator"                              |
| Instructor | ID_Instructor    | UUID            |          | PRIMARY KEY, NOT NULL                 | Identifiant unique pour chaque instructeur             | "c0eebc99-9c0b-4ef8-bb6d-6bb9bd380a12"       |
|            | Instructor_Code  | VARCHAR         | 50       | NOT NULL                              | Code unique de l'instructeur                           | "INST001"                                    |
|            | ID_User          | UUID            |          | NOT NULL, FOREIGN KEY                 | Clé étrangère référençant l'utilisateur                | "a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11"       |
| Formation  | ID_Formation     | INT             | 11       | AUTO-INCREMENT, PRIMARY KEY, NOT NULL | Identifiant unique pour chaque formation               | 10                                           |
|            | Title_Formation  | VARCHAR         | 50       | NOT NULL                              | Titre de la formation                                  | "Introduction to SQL"                        |
|            | Description      | TEXT            |          | NOT NULL                              | Description détaillée de la formation                  | "Covers basic SQL commands and operations."  |
|            | Status_Formation | VARCHAR         | 50       | NOT NULL                              | Statut actuel de la formation                          | "Publié"                                     |
|            | IsValidate       | BOOL            |          |                                       | Indique si la formation a été validée                  | true                                         |
| Module     | ID_Module        | INT             | 11       | AUTO-INCREMENT, PRIMARY KEY, NOT NULL | Identifiant unique pour chaque module                  | 5                                            |
|            | Title_Module     | VARCHAR         | 50       | NOT NULL                              | Titre du module                                        | "Database Basics"                            |
|            | Content_Module   | TEXT            |          | NOT NULL                              | Contenu du module                                      | "Fundamentals of database structures."       |
|            | Version          | VARCHAR         | 50       |                                       | Version du module                                      | "1.0"                                        |
|            | Objectif         | TEXT            |          | NOT NULL                              | Objectifs pédagogiques du module                       | "Understand core database concepts."         |
|            | Status_Module    | VARCHAR         | 50       | NOT NULL                              | Statut actuel du module                                | "Publié"                                     |
|            | IsValidate       | BOOL            |          |                                       | Indique si le module a été validé                      | true                                         |
| Lesson     | ID_Lesson        | INT             | 11       | AUTO-INCREMENT, PRIMARY KEY, NOT NULL | Identifiant unique pour chaque leçon                   | 30                                           |
|            | Title_Lesson     | VARCHAR         | 50       | NOT NULL                              | Titre de la leçon                                      | "SQL Joins"                                  |
|            | Content_Lesson   | TEXT            |          | NOT NULL                              | Contenu textuel de la leçon                            | "Explains how to use SQL joins effectively." |
|            | Video            | TEXT            |          | NOT NULL                              | URL de la vidéo associée                               | "http://example.com/sql-joins-video"         |
|            | Image            | TEXT            |          | NOT NULL                              | URL de l'image associée                                | "http://example.com/sql-joins-image"         |
|            | Tag              | VARCHAR         | 50       | NOT NULL                              | Tag pour catégoriser la leçon                          | "#TypeScript"                                |
|            | Status_Lesson    | VARCHAR         | 50       | NOT NULL                              | Statut actuel de la leçon                              | "Brouillon"                                  |
|            | ID_Module        | INT             | 11       | NOT NULL, FOREIGN KEY                 | Clé étrangère référençant le module                    | 5                                            |
|            | ID_Instructor    | UUID            |          | NOT NULL, FOREIGN KEY                 | Clé étrangère référençant l'instructeur                | "c0eebc99-9c0b-4ef8-bb6d-6bb9bd380a12"       |
| Status     | ID_Status        | INT             | 11       | AUTO-INCREMENT, PRIMARY KEY, NOT NULL | Identifiant unique pour chaque statut                  | 2                                            |
|            | Type_Status      | VARCHAR         | 50       | NOT NULL                              | Description du statut (brouillon, publié, archivé)     | "Publié"                                     |
| Have       | ID_Role          | INT             | 11       | PRIMARY KEY, FOREIGN KEY              | Clé étrangère vers la table Rôle                       | 1                                            |
|            | ID_User          | UUID            |          | PRIMARY KEY, FOREIGN KEY              | Clé étrangère vers la table User                       | "a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11"       |
| Validate   | ID_Lesson        | INT             | 11       | PRIMARY KEY, FOREIGN KEY              | Clé étrangère vers la table Lesson                     | 30                                           |
|            | ID_User          | UUID            |          | PRIMARY KEY, FOREIGN KEY              | Clé étrangère vers la table User                       | "a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11"       |
|            | Validate_Date    | DATE            |          | NOT NULL                              | Date de validation de la leçon                         | "2024-05-14"                                 |
|            | IsCompleted      | BOOL            |          | NOT NULL                              | Indique si la leçon a été complétée                    | true                                         |
| Register   | ID_Formation     | INT             | 11       | PRIMARY KEY, FOREIGN KEY              | Clé étrangère vers la table Formation                  | 10                                           |
|            | ID_User          | UUID            |          | PRIMARY KEY, FOREIGN KEY              | Clé étrangère vers la table User                       | "a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11"       |
|            | Inscription_Date | DATE            |          | NOT NULL                              | Date à laquelle l'utilisateur s'inscrit à la formation | "2024-05-01"                                 |
|            | Is_Active        | BOOL            |          | NOT NULL                              | Indique si l'inscription est active                    | true                                         |
|            | End_Date         | DATE            |          | NOT NULL                              | Date de fin de l'inscription                           | "2025-05-01"                                 |
| Give       | ID_Formation     | INT             | 11       | PRIMARY KEY, FOREIGN KEY              | Clé étrangère vers la table Formation                  | 10                                           |
|            | ID_Module        | INT             | 11       | PRIMARY KEY, FOREIGN KEY              | Clé étrangère vers la table Module                     | 5                                            |
|            | ID_Lesson        | INT             | 11       | PRIMARY KEY, FOREIGN KEY              | Clé étrangère vers la table Lesson                     | 30                                           |
|            | ID_Status        | INT             | 11       | PRIMARY KEY, FOREIGN KEY              | Clé étrangère vers la table Status                     | 2                                            |
| Compose    | ID_Module        | INT             | 11       | PRIMARY KEY, FOREIGN KEY              | Clé étrangère vers la table Module                     | 5                                            |
|            | ID_Formation     | INT             | 11       | PRIMARY KEY, FOREIGN KEY              | Clé étrangère vers la table Formation                  | 10                                           |

[🔝 Retour à la Table des matières](../README.md#table-des-matieres)
